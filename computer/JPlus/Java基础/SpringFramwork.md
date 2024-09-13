# Spring框架



## 简介

```
Spring框架的核心就是   XML文件 or 注解 来驱动底层以反射执行Java代码    XML配置（注解） <--反射--> Java
我需要重点掌握的是  理解IOC容器  与   如何使用AOP
```





## 一. IOC







## 二. AOP





















# Spring MVC



```
@Pathvariable :   是获取请求路径中的变量作为参数,需要和 @RequestMapping(“item/{itemId}”) 配合使用
@Requestparam :   注解接收的参数是来自于 requestHeader 中，即请求头。都是用来获取请求路径 url 中的动态参数。
				  也就是在 url 中，格式为 xxx?username=123&password=456
				  总之，除了Json格式外好像都用这个
@RequestBody :    注解接收的参数则是来自于 requestBody 中，即请求体中
				  Get 方式无请求体，所以使用 @RequestBody 接收数据时，前端不能使用 Get 方式提交数据;
@ResponseBody :   javaBean -> json字符串   ，直接RestController即可 
```













# Mybatis



### 1.引用

```
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.2.0</version>
</dependency>
```



```
mybatis:
  #mapper配置文件
  mapper-locations: classpath:mapper/*.xml
  type-aliases-package: com.zlc.entity
  configuration:
    # 开启驼峰命名
    map-underscore-to-camel-case: true
```



### 2.动态SQL

**<font color='orange'>动态SQL中 使用 #{}取值</font>**

- \#{}是预编译处理，mybatis在处理#{}时，会将其替换成"?"，再调用PreparedStatement的set方法来赋值。
- ${}是拼接字符串，将接收到的参数的内容不加任何修饰的拼接在SQL语句中，会引发SQL注入问题。

**<font color='orange'>动态SQL常用的标签</font>**

```
1.if[判断]

2.where【拼接where语句】

3.choose/when/otherwise【类比swich case default】

4.foreach【类似in】

5.trim【替换关键字/定制元素的的功能】

6.set【在update的set元素中，可以保证进入set标签的属性被修改，而没有进入set的，保持原来的值]
```



**演示if  where :**

- 注意:mybatis底层会自动地去掉多余的and，所以在where标签里面大胆地用and，最好在每一个句子前面都加上一个and

```
    <!--动态查询user -->
    <select id="querySingleUser" resultType="com.zlc.sykks.entity.User">
        select id,name,password,age,sex,address,phone from user
        <where>
            <if test="name != null">and name = #{name}</if>
            <if test="id != null">and id = #{id}</if>
            <if test="password != null">and password = #{password}</if>
        </where>
    </select>
```

**演示foreach:**

- 常见使用场景是对集合进行遍历（尤其是在构建 IN 条件语句的时候
- 属性描述:
  - collection	指定要遍历的集合。表示传入过来的参数的数据类型。该属性是必须指定的，要做 foreach 的对象。
  - index	索引，index 指定一个名字，用于表示在迭代过程中，每次迭代到的位置。遍历 list 的时候 index 就是索引，遍历 map 的时候 index 表示的就是 map 的 key，item 就是 map 的值。
  - item	表示本次迭代获取的元素，若collection为List、Set或者数组，则表示其中的元素；若collection为map，则代表key-value的value，该参数为必选
  - open	表示该语句以什么开始，最常用的是左括弧’(’，注意:mybatis会将该字符拼接到整体的sql语句之前，并且只拼接一次，该参数为可选项
  - separator	表示在每次进行迭代之间以什么符号作为分隔符。select * from tab where id in(1,2,3)相当于1,2,3之间的","
  - close	表示该语句以什么结束，最常用的是右括弧’)’，注意:mybatis会将该字符拼接到整体的sql语句之后，该参数为可选项

```
<!--查询id属于目标范围的user>
<select id="xxx" parameterType="map" resultType="User">
	select * from `user`
	<where>
		`id` IN
		<foreach collection="ids" item="id" open="(" seperator="," close=")">
			#{id}
		</foreach>
	</where>
</select>
```



**演示set:**

- **<font color='red'>注意：别忘了加逗号，这个还挺容易错的</font>**

```
<update id="xxx" parameterType="map" >
	UPDATE `user`
	<set>
		<if test="name != null and name != '' ">
			`name` = #{name},
		</if>
		<if test="age != null and age != '' ">
			`age` = #{age}
		</if>
	</set>
	<where>
		and `id` = #{id}
	</where>
</update>
```





### 3.模糊查询

<font color='orange'>在xml配置文件中添加"%"通配符，借助mysql函数</font>

```
<select id="fuzzyQuery" resultType="com.bin.pojo.Book">
    select * from mybatis.book where bookName like 
    concat('%',#{info},'%');
</select>
```



### 4.获取子增值

**<font color='orange'>1.@Option useGeneratedKeys、keyProperty、keyColumn    //效率高，推荐使用这个</font>**

- userGeneratedKeys="true"  允许获取自增值

  keyColumn   对应数据库表自增主键列名字

  keyProperty   对应实体类要填充的属性， keyColumn取出的值将赋给这个  （如果没有指定KeyColumn，自动将自增值给这个）

- **经常只需要这样写 userGeneratedKeys=ture , keyProperty = id ,   因为如果没有指定KeyColumn，自动将自增值给这个属性**

注解版本

```
@Insert("        INSERT INTO `user` (`age`,`name`,`gender`,`salary`)" +
        "        VALUES(#{age},#{name},#{gender},#{salary})")
@Options(useGeneratedKeys = true,keyProperty = "id",keyColumn = "id")
public boolean addUser(User user);
```

配置文件版本

```
<insert id="insertBook" parameterType="com.learn.entity.Book" useGeneratedKeys="true" keyColumn="id" keyProperty="id">
        INSERT INTO BOOK(NAME) VALUES(#{name})
</insert>
```



### 5.PageHelper



### 6.XML映射器

**SQL映射文件常用的几个顶级元素（按照定义列出）**

- cache ---该命名空间的缓存配置
- cache-ref --引用其他命名空间的缓存配置
- resultMap--描述如何从数据库结果集中加载对象，是最复杂也是最强大的元素
- parameterType--将会传入这条语句的参数的类全限定名或别名



### 7.映射关系







### 8. 缓存





































# MybatisPlus



## 1. 命名约定

**<font color='orange'>约定是什么？</font>**

```
如果实体类叫UserInfo,数据库应该叫user_info
如果属性名username,对应数据库 username
如果属性名createTime,对应数据库 create_time
```

**<font color='orange'>不符合约定怎么办？三个注解来帮忙 ! </font>**

- @TableName : 表名
- @TableId ： 主键
- @TableField ： 属性名

**<font color='orange'>几种情况如下：</font>**

- 常规情况：表名，属性名不一致
- 特殊情况：
  - 1.默认id为主键，若**没有id**需要 tableld标明哪一个是主键，其中属性type可以实现数据库自增，程序员指定，雪花生成ID共三种
  - 2.<font color='red'>**如果属性是boolean(包装类Boolean好像就没事)且名字为 isXxxxx,mybatisplus底层反射时， 会自动去除is比如此处就会映射成错误的名字:married,需要注解来标明**</font>有时间你自己测试一下Boolean会不会出错吧
  - 3.<font color='red'>**最好别冲突**</font>如果属性名与数据库关键字冲突，比如此处order 与 order by中的order冲突 需要@TableField("`order`")处理
  - 4.如果属性在数据库中没有出现，你也得标明，@TableField(exist = false)

![image-20240913132355531](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913132355531.png)



## 2.常用配置

**//大部分都是默认值，基本就配个别名**

![image-20240913133207964](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913133207964.png)





## 3.条件构造器

**<font color='orange'>专门解决where条件语句</font>**

### 3.1 Wrapper

![image-20240913141024187](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913141024187.png)

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913141143895.png" alt="image-20240913141143895" style="zoom:50%;" />

### 3.2 快速入门

- 查询名字中带o ，存款大于1000元的人的id,username,info,balance

```
1.构建查询条件
QueryWrapper<User> wrapper = new QueryWrapper<>()
								.select("id","username","info","balance")
								.like("username","o")
								.ge("balance",1000);    //大于
2.查询
List<User> users = userMapper.selectList(wrapper);
users.forEach(System.out::println);
```

**<font color='orange'>上面都是硬编码，不太推荐，下面使用lambda</font>**

```
1.构建查询条件
LamdaQueryWrapper<User> wrapper = new LamdaQueryWrapper<>()
								.select(User::getId,Use1r::getUsername,User::getInfo,User::getBalance)
								.like(User::getUsername,"o")
								.ge(User:getBalance,1000);    //大于
2.查询
List<User> users = userMapper.selectList(wrapper);
users.forEach(System.out::println);
```















## 4.继承BaseMapper

- 内部有单表的crud
- 继承BaseMapper,指定范型即可调用



## 5.Iservice



### 5.1 升级

**<font color='orange'>BaseMapper的升级版，新增批处理和一些细节的改动</font>**

![image-20240913135919156](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913135919156.png)





### 5.2 继承与实现

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913140251468.png" alt="image-20240913140251468" style="zoom: 50%;" />

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913140933145.png" alt="image-20240913140933145" style="zoom:50%;" />





### 5.3 lambda使用

**<font color='orange'>基础的crud直接使用方法，稍微麻烦点的就用lambda，很麻烦的就老老实实自己去写sql</font>**

- 复杂条件查询

```
public List<User> queryUsers(String name,Integer status,Integer minBalance,Integer maxBalance){
	return lamdaQuery()
				.like(name != null ,User::getUsername,name)
				.eq(status != null,User::getStatus,status)
				.ge(minBalance != null,User::getMinBalance,minBalance)
				.le(maxBalance != null,User::getMaxBalace,maxBalamce)
				.list();	
}
```

- 复杂条件修改

![image-20240913150429733](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913150429733.png)





### 5.4 MybatisX

**<font color='orange'>代码生成器</font>**



### 5.5 逻辑删除

**原理类似redis学的逻辑过期**

**比如淘宝订单这种数据，用户即使删除了数据库层面不会真的删除，会有一个属性比如deleted 记录，以后增删改查都需要一个条件：where deleted = 0,很冗余麻烦，mybatisplus就可以使用配置文件实现全局的逻辑删除**

![image-20240913153014950](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913153014950.png)

### 5.6 分页插件

#### ① 注意

**PageHelper是Mybatis的分页插件，在MP是没有的，如果你想要使用得引入pagehelper的依赖。但<font color='orange'>mp实际上有属于自己的分页插件</font>何必多此一举，而且pagehelper的依赖还有可能导致mp版本冲突，慎用！**



#### ② 注册分页插件

![image-20240913154029949](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240913154029949.png)

#### ③ 简单使用

```java
						 //第几页           每页数据量
public R testPage(Integer pageNo,Integer pageSize){
		//1.1 通过Page.of来创建一个page
		Page<User> page = Page.of(pageNo,pageSize);
		//1.2 排序参数,通过OrderItem来制定    true升序，false降序
		page.addOrder(new OrderItem("balance",true));
    	page.addOrder(new OrderItem("id",true));
		//1.3 分页查询
        Page<User> p = userService.page(page);
   		这里的p实际上就是上面的page，你可以不用返回，继续使用上面的page
        
        //2.总条数
        long total = p.getTotal();
        //3.总页数
        long pages = p.getPages();
        
        //4.分页数据
    	List<User> users = p.getRecords();
	
	}
```

#### ④ 真实开发







# Spring Boot



## 一.基础





### 1.@Configuration

```
配置类   注入Bean
@Configuration : 向spring boot 声明这是一个配置类
@Bean :  注入到容器
@Scope : 单例 or 多例
```



```
/*
* 创建线程池，注入到Bean中
* */
@Configuration
public class ConstanceConfig implements WebMvcConfigurer {

    //规定线程池核心线程数：5
    private static final int CORE_POLL_SIZE = 5;
    //规定线程池最大线程数： 10
    private static final int MAX_POOL_SIZE = 10;
    //规定线程池持有的队列容量：100
    private static final int QUEUE_CAPACITY = 100;
    //规定线程池 线程等待时间：1L
    private static final Long KEEP_ALIVE_TIME = 1L;

    /*
    * 创建一个线程池
    * */
    @Bean
    public ThreadPoolExecutor threadPoolExecutor(){
        return  new ThreadPoolExecutor(
                CORE_POLL_SIZE,      //设置线程池核心线程数
                MAX_POOL_SIZE,       //设置线程池最大线程数量
                KEEP_ALIVE_TIME,     //设置线程等待时间
                TimeUnit.SECONDS,    //设置线程等待时间单位
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),//设置线程池使用ArrayBlockingQueue队列
                //设置线程池饱和政策:CallerRunsPolicy(),"该策略既不会抛弃任务，也不会抛出异常，而是将任务回推到调用者
                new ThreadPoolExecutor.CallerRunsPolicy()
        );
    }
}

```



### 2.MultipartFile

```
    @PostMapping("/uploadFile")
    public Result uploadFile(@RequestParam("files") MultipartFile files[]){
        log.info("服务器接收文件:{}",files);
        //1. 若文件为空，则报错
        if(files.length <= 0){
            return Result.error(FileConstance.FILE_IS_NOT_NULL);
        }

        for(MultipartFile file : files){
            //2.创建并调用线程
            FileRunnable fileRunnable = new FileRunnable();
            fileRunnable.setFile(file);
            threadPoolExecutor.execute(fileRunnable);
        }

        //3.上传文件成功，返回
        return Result.success(FileConstance.FILE_UPLOAD_SUCCESS);
    }
```



### 3.Lombok

**需要引入依赖**

- @Data 等价于 @Getter @Setter @ToString @RequiredConstructor @EqualsAndHashCode
- @ToString     
- @NoArgsConstructor:虽然默认情况下会生成无参构造器，但是会被全参构造器覆盖(比如只用了@Data注解，就会把无参构造器覆盖)，所以有时候需要这个注解

在idea 安装lombok插件就可以使用一些扩展注解，比如日志的输出

- @Slk4j注解 :   就可以使用log.info("xxxx:{}", zlc)  打印日志。



### 4.静态资源

```
SpringBoot 默认配置就可以直接URL访问类路径下的静态资源

1. classpath:/META-INF/resources/
2. classpath:/resources/
3. classpath:/static/
4. classpath:/public/
```



### 5.拦截器

- **三个方法**

```
preHandler:   当前请求处理完成之前，也就是Controller 方法调用之前执行



postHandler:  当前请求处理完成之后，也就是 Controller 方法调用之后执行，但是它会在 DispatcherServlet 进行视图返回渲				  染之前被调用，所以我们可以在这个方法中对 Controller 处理之后的 ModelAndView 对象进行操作


afterHandler: 该方法将在整个请求结束之后，也就是在 DispatcherServlet 渲染了对应的视图之后执行。此方法主要用来进行资源清理。
```



- **创建xxxxxinterceptor**

```
/*
*  登录拦截器
* */
@Slf4j
public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //1.判断是否需要拦截
        UserDTO userDTO = UserHodler.getUser();
        //2.拦截
        if(userDTO == null){
            //没有，需要拦截，设置状态码     //401表示没有权限!!!
            response.setStatus(401);
            //拦截
            return false;
        }
        //3.放行
        return true;
    }
}
```

- **注册拦截器**

```
@Slf4j
@Configuration
public class WebMvcConfig implements WebMvcConfigurer {

    @Resource
    StringRedisTemplate stringRedisTemplate;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        log.info("开始注册自定义拦截器...");
        //token刷新的拦截器
        registry.addInterceptor(new RefreshTokenInterceptor(stringRedisTemplate))
                .addPathPatterns("/**");
        //登录拦截器
        registry.addInterceptor(new LoginInterceptor())
                .excludePathPatterns("/user/login");

    }
}
```

- **每个拦截器默认优先级为0，如果没有设置优先级，那么就按照注册顺序依次执行；如果设置优先级则按照优先级执行.**

```
    //登录拦截器
    registry.addInterceptor(new LoginInterceptor())
            .excludePathPatterns(
                    "/shop/**",
                    "/voucher/**",
                    "/shop-type/**",
                    "/upload/**",
                    "/blog/hot",
                    "/user/code",
                    "/user/login"
            )
            .order(1);  //值越小 优先级越高！
```



### 6.异常处理











































































































































































































































































































