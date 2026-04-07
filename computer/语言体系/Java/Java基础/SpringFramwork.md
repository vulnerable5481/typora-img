# Spring框架



## 简介

```
Spring框架的核心就是   XML文件 or 注解 来驱动底层以反射执行Java代码    XML配置（注解） <--反射--> Java
我需要重点掌握的是  理解IOC容器  与   如何使用AOP
```





## 一. IOC

// 手写一个简单的IOC容器





## 二. AOP

// 手写一个简单的AOP + AOP相关内容整理



















# Spring MVC



## 1. 参数注解

```
@PathVariable  —— URL 路径的一部分
@RequestParam —— 请求参数（query / form）
@RequestBody  —— 请求体（JSON）

URL路径的一部分很好理解
请求参数也是URL后面的一些数据 /xx?a=1&b=2&c=3
请求体就是HTTP请求的单独一个属性Body用来携带请求数据的   
```



- **@Pathvariable**

  - 接收URL中 /exit/{token} 占位参数

  - ```
    // 前端请求                                   
    export function exit(token) {
      return httpRequest
        .post(`/user/exit/${token}`)
        .then((response) => {
          return response;
        })
        .catch((error) => {
          throw error;
        });
    }
    // 后端请求
    @RequestMapping("/exit/{token}")
    (@Pathvariable String token)
    ```

- **@RequestParam**

  - 接收URL中 url?key=value

  - ```
    // 前端请求
    export function exit(token) {
      return httpRequest
        .post(`/user/exit?token=${token}`)   // 注意key=${value}中的key一定要和@RequestParam("key")保持一致
        .then((response) => {
          return response;
        })
        .catch((error) => {
          throw error;
        });
    }
    // 后端
    (@RequestParam("token") String token)
    ```

- **@RequestBody**

  - 如果是对象还用说吗，但是前端如果就偏要单独传一个属性，还偏偏指定使用@RequestBody怎么办？
    很简单：后端我们造一个只有一个属性的对象不就完事了

  - ```
    // 前段请求
    export function exit(params) {
      return httpRequest
        .post('/user/exit', params)
        .then((response) => {
          return response;
        })
        .catch((error) => {
          throw error;
        });
    }
    // 后端不能直接接收此处的token，需要使用
    ```

- **@ResonseBody 与 @RestController**
  - easy





# Mybatis

## 0.简介

- Mybatis是一款优秀的持久层框架，真正强大在于它的**语句映射**，这是它的魔力所在。由于它的异常强大，映射器的 XML 文件就显得相对简单。如果拿它跟具有相同功能的 JDBC 代码进行对比，你会立即发现省掉了将近 95% 的代码。致力于减少使用成本，让用户能更**专注于 SQL 代码**。

- 什么是jdbc？

  - 谈起jdbc，不得不回忆一下我刚开始学习的那段光辉岁月

  - ```
    jdbc是java提供的一种api，允许java程序与关系型数据库比如mysql进行通信。
    通过jdbc，我们可以在Java中，连接数据库、执行sql语句操作数据库等等
    jdbc的基本工作流程：
    	1.加载数据库驱动
    	2.建立数据库连接
    	3.创建Statement对象，执行sql语句
    	4.如果是查询语句，需要处理结果集，可以通过ResultSet对象处理
    	5.关闭连接
    ```

- Mybatis可以帮助我们免除上述一系列jdbc代码和获取结果集的工作，极大地提高了我们的开发速度！

## 1.引用

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

## 2.动态SQL

**<font color='orange'>动态SQL中 使用 #{}取值</font>**

- \#{}是预编译处理，相当于占位符，mybatis在处理#{}时，会将其替换成"?"，再调用PreparedStatement的set方法来赋值。
- ${}是拼接字符串，将接收到的参数的内容不加任何修饰的拼接在SQL语句中，会引发SQL注入问题。

**<font color='orange'>动态SQL常用的标签</font>**

```
1.if[判断]

2.where【拼接where语句】

3.choose/when/otherwise【类比swich case default】

4.foreach【类似in】

5.trim【自定义sql语句】

6.set【在update的set元素中，可以保证进入set标签的属性被修改，而没有进入set的，保持原来的值]
```

**演示if  where :**

- 注意:mybatis底层会自动地去掉多余的and，所以在where标签里面大胆地用and，最好在每一个句子前面都加上一个and

```
    <!--动态查询user -->
    <select id="querySingleUser" resultType="com.zlc.sykks.entity.User">
        select id,name,password,age,sex,address,phone from user
        <where>
            <if test="name != null">name = #{name}</if>
            <if test="id != null">and id = #{id}</if>
            <if test="gender != null">and gender = #{gender}</if>
            <if test="password != null">and password = #{password}</if>
        </where>
    </select>
```

**演示foreach:**

- 常见使用场景是对集合进行遍历（尤其是在构建 IN 条件语句的时候
- 属性描述:
  - collection	指定要遍历的集合。表示传入过来的参数的数据类型。**该属性是必须指定的**，要做 foreach 的对象。
  - index	索引，index 指定一个名字，用于表示在迭代过程中，每次迭代到的位置。遍历 list 的时候 index 就是索引，遍历 map 的时候 index 表示的就是 map 的 key，item 就是 map 的值。
  - item	表示本次迭代获取的元素，若collection为List、Set或者数组，则表示其中的元素；若collection为map，则代表key-value的value，**该参数为必选**
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

## 3.模糊查询

- <font color='orange'>在xml配置文件中添加"%"通配符，借助mysql函数</font>

```
<select id="fuzzyQuery" resultType="com.bin.pojo.Book">
    select * from mybatis.book where bookName like 
    concat('%',#{info},'%');
</select>
```

## 4.获取子增值

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

## 5.PageHelper

## 6.resultMap

### ① 简介

- resultMap是何许人也？

  - ```
    `resultMap`元素是 `MyBatis` 中最重要最强大的元素。它可以让你从 90% 的 `JDBC ResultSets` 数据提取代码中解放出来，并在一些情形下允许你进行一些 JDBC 不支持的操作。实际上，在为一些比如连接的复杂语句编写映射代码的时候，一份 `resultMap` 能够代替实现同等功能的长达数千行的代码。`ResultMap` 的设计思想是：对于简单的语句根本不需要配置显式的结果映射，而对于复杂一点的语句只需要描述它们的关系就行了>
    ```

- **<font color='blue'>联表查询，resultMap就非常关键！</font>**

### ② 字段映射

- 最简单最基础的应用场景，字段映射，专门解决字段名字不匹配的问题

- 比如说，数据库中表的字段与`User`类的属性名称一致，我们就可以使用`resultType`来返回；
    但是，假如数据库是name字段，但是User类是username字段，字段不一样怎么办？

- ```
  1.定义resultMap
  <resultMap id="getUserByIdMap" type="User">
  	<result property="id" column="uid"></result>
  </resultMap>
  
  2.修改select语句
  <select id="getUsers" resultMap="getUserByIdMap">
  ```

### ③ 一对一级联

- **级联查询**：在数据库中包含着一对多、一对一的关系。比如说一个人和他的身份证就是一对一的关系，但是他和他的银行卡就是一对多的关系。我们的生活中存在着很多这样的场景。我们也希望在获取这个人的信息的同时也可以把他的身份证信息一同查出，这样的情况我们就要使用级联。在级联中存在三种对应关系，一对一，一对多，多对多。

- 实际的业务中，我们的用户一般都有一个角色，用户与角色就是一对一的关系，可以用级联查询！

- **如何解决一对一的级联？**

  - ```
    @Data
    public class User {
        //省略用户属性...
    	
        //角色信息
        private Role role;
    }
    ```

- 假如我们查询的时候也希望联表得到该数据，我们会这样来写查询语句：

  - **关于方法一和二哪个好？**实际上就是比较 多表连查VS 多次单表查询 ，数据量比较大的情况下，使用多次单表查询，但是数据量不怎么大的时候，可以用联表查询。【实际上很多公司都不让用联表查询，怕以后数据量大了性能下降】【单表几百万就不适合联表查询了】【阿里规约中，禁止使用三表以上的join】
    							

  - ```
    方法一：  【联表查询】
    <resultMap id="userMap" type="User">
    	<id property="id column="id></id>
    	<result property="username" column="username"></result>
    	<result property="password" column="password"></result>
    	<result property="address" column="address"></result>
    	<result property="email" column="email"></result>
    	
    	<association property="role" javaType="Role">
    		<id property="id" column="id"></id>
    		<result property="name" columen="name"></result>
    	</association>
    </resultMap>
    
    <select id="getUsers" resultMap="userMap">
    	SELECT
    		u.id,u.username,u.password,u.address,u.email,r.id,r.name
    	FROM USER u
    			LEFT JOIN user_roles ur ON u.id = ur.user_id
    			LEFT JOIN role r ON r.id = ur.role_id
    	where u.id=#{id}
    </select>
    方法二：   【分治思想：多表联查拆分成多个单表查询】❤推荐！
    	 		我们有userMapper也有roleMapper！
    //////////////【UserMapper】:	
    <resultMap id="userMap" type="User">
    	<id property="id column="id></id>
    	<result property="username" column="username"></result>
    	<result property="password" column="password"></result>
    	<result property="address" column="address"></result>
    	<result property="email" column="email"></result>
    	// 注意此处的column就是getRoleByUserId的一个参数，简单理解为getRoleByUserId(column),此处就是userId为参数
    	<association property="role" column="id" select="com.zlc.mapper.RoleMapper.getRoleByUserId">
    	</association>
    </resultMap>
    
    <select id="getUsers" resultMap="userMap">
    	SELECT
    		u.id,u.username,u.password,u.address
    	FROM USER u
    	where u.id=#{id}
    </select>
    /////////////【roleMapper】:
    <select id="getRoleByUserId" resultType="Role">
    	select xxx
    	from role
    	where user_id = #{id}
    </select>
    方法三：  自动填充 【看完下面第六小节，你就明白了】
    <select id="getUsers" resultMap="userMap">
    	SELECT
    		u.id,u.username,u.password,u.address,u.email,r.id AS role.id,r.name AS role.name
    	FROM USER u
    			LEFT JOIN user_roles ur ON u.id = ur.user_id
    			LEFT JOIN role r ON r.id = ur.role_id
    	where u.id=#{id}
    </select>
    ```


### ④ 一对多级联

- 前面说到一个用户有一个角色，实际上一个用户可能有多个角色信息，需要User类，Role就需要修改为List

- **如何解决多个类型的关联？**

- ```
  <resultMap id="userMap" type="User">
  	<id property="id column="id></id>
  	<result property="username" column="username"></result>
  	<result property="password" column="password"></result>
  	<result property="address" column="address"></result>
  	<result property="email" column="email"></result>
  	
  	<collection property="roles" column="id" ofType="Role" select="xxx.xxx">
  	</collection>
  </resultMap>
  
  <select id="getUsers" resultMap="userMap">
      SELECT	
          u.id AS 'user_id', 
          u.username, 
          u.password, 
          u.address, 
          u.email,
      FROM USER u
      WHERE u.id = #{id}
  </select>
  
  ```

- 这样即使有多个角色也会被显示出来

- ```
  {
      "id": "1003",
      "username": "貂蝉",
      "password": "123456",
      "address": "北京市东城区",
      "email": "510273027@qq.com",
      "roles": [
          {
              "id": "1",
              "name": "中单"
          },
          {
              "id": "2",
              "name": "打野"
          }
      ]
  }
  ```


### ⑤ 集合的嵌套Select查询

- 比如说我们有菜单实体类，实际上可以分为一级，二级，多级菜单

- ```
  @Data
  public class Menu {
      private String id;
      private String name;
      private String url;
      private String parent_id;
      private List<Menu> childMenu;
  }
  ```

- **思考一下，我们如何在只调用一次Mapper层的方法就返回我们想要的多级菜单？**  修改对应resultmap即可

- ```
  <resultMap id="menuMap" type="Menu">
  	 <id property="id" column="id"></id>
  	 <result property="name" column="name"></result>
  	 <result property="url" column="url"></result>
  	 <result property="parent_id" column="parent_id"></result>
  	 
  	 <collection property="childMenu" ofType="Menu" select="getMenus" column="{parent_id=id}">  
  	 </collection>
  </result>
  
  <select id="getMenus" resultMap="menusMap">
  	SELECT
  		m.id,
  		m.name,
  		m.url,
  		m.parent_id
  	FROM menus m
  	<choose>
  		<when test="parent_id != 0">
  			amd m.parent_id = #{parent_id}
  		</when>
  		<otherwise>
  			and m.parent_id = '0'
  		</otherwise>
  	</choose>
  ```


### ⑥自动填充关联对象

- 上面我提到了一个用户对应一个角色的例子，实际上我们也可以利用mybatis的自动填充的一个特性

- ```
  自动填充特性：
  			我们知道，在Mybatis解析返回值的时候。
              第一步是获取返回值类型，拿到Class对象，然后获取构造器，设置可访问并返回实例，然后又把它包装成MetaObject对象。
              从数据库rs中拿到结果之后，会调用MetaObject.setValue(String name, Object value) 来填充对象。
              在这过程中，有趣的是，它会以.符号来分隔这个name属性。
              如果name属性中包含.符号，就找到.符号之前的属性名称，把它当做一个实体对象来处理。
  比如说：  mybatis解析到 r.id AS role.id 通过.符号分割之后，发现role别名对应Role对象，
  		则会先初始化Role对象，并将对应的值赋给id，这样即使我们不使用resultMap也能做到联表查询的效果
  ```

### ⑦discriminator

## 7. 缓存





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
- @TableField ： 属性名   **一般情况只有这个常用**

**<font color='orange'>几种情况如下：</font>**

- 常规情况：表名，属性名不一致
- 特殊情况：
  - 1.默认id为主键，若**没有id**需要 tableld标明哪一个是主键，其中属性type可以实现数据库自增，程序员指定，雪花生成ID共三种
  - 2.<font color='red'>**如果属性是boolean(包装类Boolean好像就没事)且名字为 isXxxxx,mybatisplus底层反射时， 会自动去除is比如此处就会映射成错误的名字:married,需要注解来标明**</font>有时间你自己测试一下Boolean会不会出错吧
  - 3.<font color='red'>**最好别冲突**</font>如果属性名与数据库关键字冲突，比如此处order 与 order by中的order冲突 需要@TableField("`order`")处理
  - **4.如果属性在数据库中没有出现，你也得标明，@TableField(exist = false)**

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





### 5.4 MybatisX

**<font color='orange'>代码生成器</font>**



### 5.5 逻辑删除

**原理类似redis学的逻辑过期**

**比如淘宝订单这种数据，用户即使删除了数据库层面不会真的删除，会有一个属性比如deleted 记录，以后增删改查都需要一个条件：where deleted = 0,很冗余麻烦，mybatisplus就可以使用配置文件实现全局的逻辑删除**

<font color='orange'>使用步骤1： 配置全局的逻辑删除规则(可省略,默认1代表逻辑删除和0逻辑未删除)
</font>
<font color='orange'>使用步骤2：配置逻辑删除的组件Bean(3.1版本以后不需要加)</font>

<font color='orange'>使用步骤3：给逻辑删除字段 添加注解@Tablelogic</font>

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

- @Slk4j注解 :   就可以使用log.info("xxxx:{}", zlc)  打印日志。【slk4j是一种快速打印日志框架，比如日志框架可能是log4j，slk4j封装																										 API就可以快速调用log4j的接口】



### 4.静态资源

// 前后端分离之后，应该用处不大了吧，一般都是存储到别的地方

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

【前后端分离项目，基本都是restcontroller+json，springMVC的传统视图处理作用几乎很少，所以posthandler也几乎没用，但是其他两个方法还是很有用的！】
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











































































































































































































































































































