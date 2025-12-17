

# NEED



## 1、生产任务

```
生产任务：利用c++实现的算法去自动扫描board，生成缺陷图
1、createTask
   校验数据：对板子进行检查、判断是否存在相同机台的自动任务
   存储任务->存一份记录到数据库，主要是用来记录任务数据
   旧数据清理->如果是指定任务且开启了回写功能，需要清理旧历史数据
   任务执行->创建一个任务放到本地缓存，这样就算是创建任务->BoardQueueMonitor就是一个线程，监控调度一个板子任务队列（里面都是板子），该线程不停取板子将其均衡地分配、暂停、恢复和删除。
   负载均衡如何实现：就是找到最棒的AI节点(匹配度高、且空闲的节点)，以最快的速度跑完检测任务。
   暂停与恢复：无非就是一个字段去控制
   分配任务：就是远程调用AI节点
   暂停：在最后再次检测任务队列的status，决定是否暂停，一般情况肯定是直接就run了 
   etc： 除了create,suspend、start 其实就很简单了

处理ai推理后给出的缺陷图片组的加工处理逻辑
```



## 2、ai推理

```
2、dowork 
	-> prepare data and put log 
	-> verify valid work and release the memory
	-> prepare supplementary data sucn as WhiteLableList(白名单：检测到这些标签可以省略)、高危NG规则、判废规则
	-> 新老算法分支
	-> 推理结束

  新算法：
		初始化(准备数据)、图像分组：分成固定大小的组可能是为了降低单次推理的内存占用，提高效率
		-> 外层遍历图像分组，内层遍历组中每张图片，finish 标记是否是该组最后一张图，在处理完后做特定操作（如导出 ROI 信息）。
		    ① 校验模板图与缺陷图大小是否一致，不一致就打印记录+跳过；若图像已经标记为“不良 pic”，也跳过
		    ② 无缺陷ROI：默认有一个defectRegion,调用一次AI推理；postProcess后，对AI推理结果进行后置处理，更新缺陷区域列							表；调用AI决策，
		      有缺陷ROI：有多个defectRegion，循环每个缺陷区域，调用AI推理；根据模型类型，解析AI输出，判断是否NG，调用AI决策
		      AI推理：初始化 ->计算和设置切割区域(有个专门的图像处理类，可以多了解一下o机，就是基于 OpenCV提供API组合逻辑)
		      			   ->处理切割后的每个图像区域
		      			   ->图像切割与模板匹配，其他图像数据处理
		      			   ->推理请求构造，远程调用AI推理
		      			   ->处理响应
		      AI决策：AI推理之后，负责根据规则将模型的输出结果转化为最终的业务判定结果
		      		 规则比如：阈值判断（如置信度 > 0.8 才算 NG）；又比如一些特殊缺陷即使模型判定OK，也要强制NG
			③ 特殊机台处理：调用定制的接口去服务
			④ 结果回写 + 异常处理  
```



## 3、缺失字段告警

```
数据库缺少字段，提醒操作人员捞出对应SQL执行
	原设计方案：在全局异常那里去匹配，如果匹配到对应的SQL异常，获取sql异常中的errorMsg，解析出来unknow column，也就是缺失字				段，将添加到告警信息
	问题：	@ExceptionHandler，只有当异常一直被抛到Controller层，还是没人处理，那就走这里的处理逻辑，但问题是业务逻辑大概率会           catch捕获异常，这样就无法触发这里的逻辑，无法添加告警信息
@ExceptionHandler(value = {BadSqlGrammarException.class, SQLSyntaxErrorException.class, MyBatisSystemException.class})
    @ResponseBody
    public ApiResponse sqlErrorException(Exception e) 
	新设计方案：配置一个Mybatis拦截器，如果捕获到目标SQL异常，就触发我们的逻辑：解析errorMsg，添加告警信息
	遇到的问题：循环依赖是如何解决的？@Transaction注解中scope的妙用，不设置的话，即使逻辑没有问题也无法正确添加告警信息
	代码：
/**
 * MyBatis SQL 异常拦截器
 */
@Slf4j
@Component
@Intercepts({
        @Signature(type = Executor.class, method = "update", args = {MappedStatement.class, Object.class}),
        @Signature(type = Executor.class, method = "query", args = {MappedStatement.class, Object.class, RowBounds.class, ResultHandler.class})
})
public class SqlErrorInterceptor implements Interceptor {

    private WarnLogService warnLogService;

    private WarnLogService getWarnLogService() {
        if (warnLogService == null) {
            warnLogService = SpringUtil.getBean(WarnLogService.class);
        }
        return warnLogService;
    }

    private static final String MYSQL_UNKNOWN_COLUMN_ERROR = "Unknown column";

    @Override
    public Object intercept(Invocation invocation) throws Throwable {
        try {
            return invocation.proceed();
        } catch (Exception e) {
            // 拦截SQL异常
            log.error("拦截SQL异常: {}", e.getMessage(), e);
            Throwable sqlException = findSqlException(e);
            if(sqlException != null){
                handleSqlError(sqlException);
            }
            // 继续抛,让业务逻辑感知
            throw e;
        }
    }

    /**
     * 向下查找异常链中的 SQL 异常
     */
    private Throwable findSqlException(Throwable e) {
        while (e != null) {
            if (e instanceof BadSqlGrammarException ||
                    e instanceof SQLSyntaxErrorException ||
                    e instanceof MyBatisSystemException) {
                return e;
            }
            e = e.getCause();
        }
        return null;
    }

    private void handleSqlError(Throwable e) {
        try {
            String errorMsg = e.getMessage();
            if (StringUtils.isNotBlank(errorMsg) && errorMsg.contains(MYSQL_UNKNOWN_COLUMN_ERROR)) {
                String errorSegment;
                int start = errorMsg.indexOf("Unknown column");
                int end = errorMsg.indexOf("### The error may");
                if (start != -1 && end != -1 && end > start) {
                    errorSegment = errorMsg.substring(start, end);
                } else {
                    errorSegment = errorMsg;
                }

                int firstQuote = errorSegment.indexOf("'");
                int secondQuote = errorSegment.indexOf("'", firstQuote + 1);
                String missingField = (firstQuote != -1 && secondQuote != -1)
                        ? errorSegment.substring(firstQuote + 1, secondQuote)
                        : "未知字段";

                String warnInfo = "更新软件包时，数据库更新失败，缺少字段：" + missingField +
                        "，请通过缺失字段关键字在SQL文件中找到对应的sql内容，捞出来重新执行";

                WarnLog warnLog = WarnLog.builder()
                        .warnType(WarnConstants.WarnTypeEnum.DATA_EXCEPTION.name())
                        .warnIp(IpUtils.getLocalIpFromWindows())
                        .warnInfo(warnInfo)
                        .warnLevel(WarnConstants.WarnLevelEnum.ERROR.name())
                        .build();
                getWarnLogService().saveLogScoped(warnLog);
            }
        } catch (Exception inner) {
            log.error("存储SQL异常告警信息失败: {}", inner.getMessage());
        }
    }

    @Override
    public Object plugin(Object target) {
        return Plugin.wrap(target, this);
    }

    @Override
    public void setProperties(Properties properties) {
    }
}


@Configuration
public class MybatisConfig {

//    @Bean
//    public Interceptor sqlErrorInterceptor(WarnLogService warnLogService) {
//        return new SqlErrorInterceptor(warnLogService);
//    }
}


    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void saveLogScoped(WarnLog warnLog) {
        warnLogMapper.insert(warnLog);
    }

```



## 4、接入机台



### 1、标准机台

| 需要实现函数接口        | 函数功能说明                                                 | 是否必须                                                     |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 继承AbstractDevice      | 继承抽象机台                                                 | 是                                                           |
| deviceType              | 标记这个机台接口属于AVI或者AOI                               | 是，这个会决定放到AVI复判页面或者AOI群组复检页面             |
| getProductList          | 获取料号列表                                                 | 是                                                           |
| getBatchList            | 获取批次列表                                                 | 是                                                           |
| getBoardList            | 获取板号列表                                                 | 是                                                           |
| getTimeList             | 获取时间列表                                                 | 取决于文件夹目录是否包含时间                                 |
| getMergeLayerListByFile | 获取层别列表                                                 | 取决于文件夹目录是否包含层别                                 |
| getBoardDefect          | 获取板的信息                                                 | 是                                                           |
| parseDir                | 用于解析自动任务目录                                         | 是                                                           |
| getExportList           | AI回写策略                                                   | 非必须，看机台接口是否支持AI回写                             |
| groupReCheck            | 单板复判结束复写AI结果                                       | 否，1.看机台接口是否支持AI回写 2.看是否需要支持这个场景      |
| matchMode               | 料号匹配查询方式： SELECT_BY_TIME：根据时间查逻辑； ALL_SELECT：全查逻辑； SELECT_BY_CACHE：查询缓存逻辑（牧德AOI特殊）； NO_SELECT：不需要查询料号 | 是                                                           |
| cutOkImageStrategy      | 切OK图策略                                                   | 非必须，如果机台接口直接提供了双图，则不需要实现切图策略。覆盖成：CutOkImageStrategyEnum.NOT_CUT |
| setGerberImg            | 加载复判页面的左下角大图                                     | 非必须，看机台接口是否提供了大图                             |
| setTemplateImg          | 加载用于推理的大图，先加载大图，再根据切OK图策略，得到OK图   | 非必须，看机台接口是否提供了大图                             |
| isNonDefectRoi          | 机台图片是否有缺陷roi输入（如果没有roi输入跑完算法之后可能有多个缺陷roi，需要走特定的算法结果判定构造正确的imageDefect.defectRegions） | 否，目前悉智项目定制                                         |
| postProcess             | 新算法AI后置额外处理                                         | 否，目前悉智项目定制                                         |
| getIndexOrder           | 自定义前端展示列表                                           | 否                                                           |
| aiRunListLayerUseByFile | 层别获取方式                                                 | 否，AOI机台选择                                              |
| reLoadProduct           | 从板号重新获取料号或获取第一个料号                           | 否                                                           |
| storeDefectImage        | 保存缺陷图片到本地                                           | 否                                                           |
| readBoardImages         | 根据getBoardDefect中存储的图片地址获取对应的缺陷，模板，Gerber图片 | 否                                                           |



| 关键字段                                         | 说明                  | 是否必须                                  |
| ------------------------------------------------ | --------------------- | ----------------------------------------- |
| com.aqrose.core.device.ImageDefect#defectImage   | 缺陷图像              | 是                                        |
| com.aqrose.core.device.ImageDefect#templateImage | OK图像->模板图        | PCB场景是必须，半导体非必须               |
| com.aqrose.core.device.ImageDefect#gerberImage   | OK图像->CAM图/Gerbe图 | PCB场景是必须，半导体非必须               |
| com.aqrose.core.device.ImageDefect#expandImage   | 复判页面的局部放大图  | 非必须，看机台接口是否提供了大图          |
| com.aqrose.core.device.ImageInfo#boardName       | 板号                  | 是                                        |
| com.aqrose.core.device.ImageInfo#shotName        | 相机号                | 是，为空会丢失AI结果。如果没有值默认SHOT0 |
| com.aqrose.core.device.ImageInfo#defectName      | 缺陷名                | 是，图像名的唯一标记，同一板不能重复      |



### 2、AI回写

```
就是一个Factory->export
```



### 3、watcher

```
package com.aqrose.airun.design.watcher.device;
监听机台（AVI 设备）的文件夹变化，当机台产出新的板（Board）相关文件时，自动触发 AI 的“板运行任务
文件系统监听器 + AI自动运行触发器
```



### 4、枚举兼容

```
1、FactoryTypeEnum
2、MachineTypeEnum
3、DeviceFactory
4、FactoryProducer
5、AutoTaskFactory
```



### 5、前端兼容

```
由很多地方可能需要添加，因为不同的机台可能要展示的是什么字段可能不同
```











# Question

```
1、Java中的实体类为什么要 implements Serializable?
2、java ->  c++  = Native.load()....
3、assert device != null;  	Java 的断言语法，用来在开发/测试阶段检查某些条件是否成立。
						     默认情况下，Java 不会执行 assert，除非启动 JVM 时加了 -ea（enable assertions）参数：
```



# Result

```
1、AiRunCache是本地缓存，封装了系统中所有运行时的缓存结构，比如任务缓存、AI节点缓存、板号缓存、模型缓存等等。
	它的底层是通过 @CreateAqCache 注解和 AqCache 框架（一个自研或内部封装的缓存框架）自动生成的。
2、ThreadFactory统一线程
3、git commit假如出现了冲突，
```



<<<<<<< HEAD
# TASK

```
本周任务：
	1、复习学习笔记，快速之前的内容
	2、结束ospf协议
今日任务：
	1、完成部分ospf协议
	
公司任务：
	1、需要把自己没有接触过的智能工业 -> 文档
	2、想办法知道算法都是怎么做的，如果让我去实现，我能做到吗?
	3、想办法知道运维的工作内容，如果让我去做，我能做到吗？
	4、从项目中整理need  (1/4)
学校任务：
能力提升：
	1、深挖GIT
	2、NIO可以利用空闲时间深入学习一下
	3、算法可以凑空接着训练
	4、continue to learn OS、 review Network、 
	5、深入实践AOP
	6、通过Mybatis拦截器认识到自己的不足之处：① 拦截器、监听器、配置类的原理、应用场景 ② Mybatis的执行原理
										③ @Transaction注解scope的应用 ④ 循环依赖的解决

cons:
	1、英语的持续输入输出：每天的空余时间可以去学习单词、利用追剧+游戏+novle保持活跃度、大量输出=找真实外国人对话
	2、哲学的持续学习：利用在出租屋的时间，时不时就去看看哲学书籍
	3、身为作家：经常去把一些有趣的事情记录下来
	4、体能，嗯，可以去研究一下健身房？或者找个不错的跑道？
```



# Thesis

```
中英文摘要 ………………………………………… （I）  
1 OSPF协议概述        ……………………………………… （1）
1 .1 OSPF协议简介                    ……………………………………   （1.1）
1 .2 OSPF协议的基本特点              ……………………………………   （1.2）
2 OSPF报文类型      ……………………………………… （2）
2 .1 OSPF首部                        ……………………………………   （2.1）
2 .2 HELLO报文                       ……………………………………   （2.2）
2 .3 DD报文                          ……………………………………   （2.3）
2 .4 LSR报文                         ……………………………………   （2.4）
2 .5 LSU报文                         ……………………………………   （2.5）
2 .6 LSAck报文                       ……………………………………   （2.6）
3 OSPF工作机制     ………………………………………（3）
3 .1 邻居状态机及状态变迁            ……………………………………   （3.1）
3 .2 邻居关系建立与维护              ……………………………………   （3.2）
3 .3 链路状态数据库同步机制          ……………………………………   （3.3）
4 不同区域下的测试与分析   ………………………………………（4）
4 .1 多区域                          ……………………………………   （4.1）
    4.1.1 网络测试环境及配置命令
    4.1.2 一类与三类LSA扩散特性
    4.1.3 状态信息与结果分析
4 .2 广播网络                        ……………………………………   （4.2）
4 .3 Stub区域                       ……………………………………   （4.3）
4 .4 Totally Stub区域               ……………………………………   （4.4）
4 .5 NSSA区域                       ……………………………………   （4.5）
4 .6 Totally NSSA区域               ……………………………………   （4.6）
5 虚链路的测试与分析      ………………………………………（5）
5 .1 虚链路产生的背景与设计目的      ……………………………………   （5.1）
5 .2 虚链路的测试与分析              ……………………………………   （5.2）
参考文献 ……………………………………………（II）
附录     …………………………………………………（III）
致谢     …………………………………………………（IV）
```



# OSPF

```
1、ospf的报文类型
	① Hello报文：主要就是用于建立和维持邻居关系
	② DD报文   ：描述数据库摘要，携带LSA摘要，告诉对方我的数据库大概有什么东西
	③ LSR报文  ：向对方请求自己缺失或版本落后的LSA
	④ LSU报文  ：携带实际的LSA数据
	⑤ LSAck报文：对收到的LSU(或者说对收到的LSA数据进行确认)，保证可靠传输

2、描述一下ospf协议的基础工作原理
	路由器之间通过发送hello报文发现并创建邻居关系，此后通过发送hello报文维持邻居关系。
	建立完全邻居关系后，路由器之间会交换LSA用来同步各自的链路状态数据库。
	同步之后，每台路由器都会提供Dijkstra算法计算到达网络中其他节点的最短路径，进而形成自己的路由表。
	当网络拓扑发生变化，受影响的路由器会重新发送LSA，触发整个网络中数据库与路由的更新。

3、邻居关系建立过程、LSDB数据同步过程
	down：最开始的阶段，表示路由器没有被发现
	Init：表示路由器已经收到了对方的Hello数据包但是自己还不是对方的邻居，不再对方的邻居表中
	2-way：收到了对方的hello报文，且已经是对方的邻居
	ExStart：表示路由器与邻居协商DD报文的初始序列号
	Exchange：表示路由器开始交换DD报文，同步LSDB的主要信息
	Loading:表示路由器请求并接收到了需要的LSA，已经完成了同步
	Full：两个路由器都已经完成了同步，建立了完全的邻居关系
	
建立邻居关系：
	最开始R1、R2都处于down状态，当R1先给R2发送hello包，R2接收到发现对方不在自己的邻居表，此时R1进入Init状态；
	R2发送Hello包之后，发现R2的邻居表已经有了自己，所以R1直接进入2-way状态，当R2再次收到之后也进入2-way状态；
协商主从：
	当R1和R2已经建立了邻居关系之后，R1和R2会进入Exstart状态，开始交换DD报文，协商主从.
	最开始双方发送的DD报文，I均为1，表示初次交换，MS均为1，第一次都认为自己是master，第一次交互后，R2的router id更大，
	R2被选为master主导DD报文的交互，此后R2的DD报文MS=1，R1的MS=0.
	协商完主从，进入Exchange状态
交换信息：
	协商出R2是master，R1发出的DD报文中的序列号就使用R2的，并携带上R1的LSA摘要信息，R2的DD报文也携带自己的LSA摘要信息；
	通过DD报文交互，双方就知道自己缺失/版本落后的LSA，进入Loading状态
数据交换：
	R2收到DD报文后，向R1发送LSR报文，请求获取需要的LSA链路信息
	R1接收到后，将R2需要的LSA链路信息封装到LSU报文，通过LSU发送给R2，R2收到后，会回复LSAck报文，其中的序列号与之前LSU中的序	列号匹配，此时R2进入Full状态；
	R1收到DD报文后，向R2发送LSR报文,请求获取需要的LSA链路信息
	R2接收到后，将R1需要的LSA链路信息封装到LSU报文，通过LSU发送给R1，R1收到后，会回复LSAck报文，其中的序列号与之前LSU中的序	列号匹配，此时R1进入Full状态；
	
4、对LSA的分析
	① 单、多区域一、三类LSA
		一类LSA：每一个路由器都会产生；只会在本区域内传播，默认不会出现跨区域传递，也就是无法穿透ABR；描述自己和邻居的链路状态
		三类LSA：由ABR产生；通过ABR进行区域间扩散，实现将区域的汇总路由信息传递给其他区域，不泄露内部拓扑；
	② 广播网络二类LSA
			  ：由DR产生；在本区域内传播；描述广播网络上的所有路由器（包括 DR、BDR 和其他路由器 ID）
	③ 虚连接一、三类LSA
		// todo
	④ 特殊区域各类LSA
		// todo
	
5、虚链路：
	 ospf采用了区域化的设计，正常情况下所有常规区域都要和骨干区域直接连接，通过骨干区域交换LSA，常规区域即使直接相连也无法交换LSA，在某些情况下，有的常规区域不能与骨干区域直连而只能与其它常规区域直连，为了让这些常规区域也能交换LSA，虚链路诞生了。
	 虚连接（Virtual link）是指在两台ABR之间通过一个非骨干区域建立的一条逻辑上的连接通道。说白了就是拓展骨干区域的范围
	 
6、特殊区域
	Stub区域、Totally Stub区域、NSSA区域和Totally NSSA区域
	// todo
	
7、ospf协议与isis协议的区别，后续答辩可能会询问
```

































































































