

# ARS

## 1、节点负载均衡



## 2、dump分析



## 3、机台接口

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



# ATS

## 1、训练子进程

## 2、oAuth2	

## 3、分片上传 + MD5

## 4、wbs消息通道

```
1、抽象wbs能力：与我个人项目中实现不同，此处的web除了有一个websocket类，还单独抽出来一个controller/Feign调用wbs里面的方法，这样设计将wbs的能力封装到了HHTP/Feign中，提高了灵活性；
2、消息中心落库：系统消息不是只推一下，它会保存到数据库让前端消息中心可以看到未读消息
3、多渠道通知，除了 WebSocket，还支持邮件、钉钉工作通知、钉钉待办、钉钉机器人
```









# 问题集合

```
1、Java中的实体类为什么要 implements Serializable?
2、java ->  c++  = Native.load()....
3、assert device != null;  	Java 的断言语法，用来在开发/测试阶段检查某些条件是否成立。
						     默认情况下，Java 不会执行 assert，除非启动 JVM 时加了 -ea（enable assertions）参数：
4、AiRunCache是本地缓存，封装了系统中所有运行时的缓存结构，比如任务缓存、AI节点缓存、板号缓存、模型缓存等等。
	它的底层是通过 @CreateAqCache 注解和 AqCache 框架（一个自研或内部封装的缓存框架）自动生成的。
```



# 项目集合

## 1、ARS

```
项目介绍：PCB厂商在采购外观检测设备后，设备拍照会存在大量假点，设备本身没有AI能力，导致PCB厂商需要大量的人力来进行缺陷复判。集成ARS产品后，可以帮助设备提高检测能力，降低60-80%的假点，帮助工厂降低人力成本，提高出货效率。
```



## 2、ATS

```消息通知
基于 Spring Cloud 2021 、Spring Boot 2.6、 OAuth2 的 RBAC 权限管理系统，核心功能：文件存储、消息通知、模型/工程训练测试
```



# 信息集合

```
-----系统账号--------
1、aqworking： zlc 123456
2、gitlab: 邮箱 无字母base版
3、禅道地址：https://chan.aqrose.com/
        用户名：liancheng.zhao
        密码：Aqrose123  
4、ATS默认账户密码 atsyh 123456


-----加密狗---------
1、绿色加密狗：101215126 version:2.4
2、蓝色加密狗：772100003830 version:3.3.0

-----共享文件-------
共享文件
访问方式：远程网络路径
IP：192.168.2.218
账号/密码：zxx/1
位置：\\192.168.2.218
```



















































































