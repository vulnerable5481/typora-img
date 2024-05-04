## 目录

[TOC]

# SSM框架

## Spring框架

### 一.导入

#### 1.什么是Spring?

spring是一个开源的轻量级框架，Spring为了简化企业级的开发而生，它完成了大量开发中通用的步骤，使用者只需使用特定部分，大大提高了开发效率。

#### 2.Spring框架的优点

(1IOC容器降低了业务对象替换的复杂性，提高了组件之间的解耦。将对象之间的依赖关系交给Spring，让我们更专注于应用逻辑。

(2)AOP支持允许将一些通用任务如安全、事务、日志等进行集中式管理，从而提供了更好的复用。

#### 3.Spring的七大模块

​		1.**核心容器**(已掌握)：核心容器提供 Spring 框架的基本功能。核心容器的主要组件是 BeanFactory，它是工厂模式的实现。BeanFactory 使用控制反转 （IOC） 模式将应用程序的配置和依赖性规范与实际的应用程序代码分开。

​		2.**Spring 上下文（已掌握）**：Spring 上下文是一个配置文件，向 Spring 框架提供上下文信息。Spring 上下文包括企业服务，例如 JNDI、EJB、电子邮件、国际化、校验和调度功能。

​		3.**Spring AOP**(已掌握)：通过配置管理特性，Spring AOP 模块直接将面向切面的编程功能 , 集成到了 Spring 框架中。所以，可以很容易地使 Spring 框架管理任何支持 AOP的对象。Spring AOP 模块为基于 Spring 的应用程序中的对象提供了事务管理服务。通过使用 Spring AOP，不用依赖组件，就可以将声明性事务管理集成到应用程序中。

​		4.**Spring DAO**：JDBC DAO 抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理和不同数据库供应商抛出的错误消息。异常层次结构简化了错误处理，并且极大地降低了需要编写的异常代码数量（例如打开和关闭连接）。Spring DAO 的面向 JDBC 的异常遵从通用的 DAO 异常层次结构。

​		5.**Spring ORM**：Spring 框架插入了若干个 ORM 框架，从而提供了 ORM 的对象关系工具，其中包括 JDO、Hibernate 和 iBatis SQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结构。

​		6.**Spring Web 模块**：Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提供了上下文。所以，Spring 框架支持与 Jakarta Struts 的集成。Web 模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。

​		7.**Spring MVC 框架**(已掌握)：MVC 框架是一个全功能的构建 Web 应用程序的 MVC 实现。通过策略接口，MVC 框架变成为高度可配置的，MVC 容纳了大量视图技术，其中包括 JSP、Velocity、Tiles、iText 和 POI。

### 二.Spring环境搭配

1.<!-- Spring的依赖，引入context之后，会根据依赖的传递性，自动引入spring的其他几个核心jar包 -->

```
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.3.8</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-beans</artifactId>
            <version>5.3.8</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.8</version>
        </dependency>
        //////////////////////// Junit
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        ////////////////AOP
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>5.3.8</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>5.3.8</version>
        </dependency>
```

2.引入Junit

```
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```

3.XML配置文件

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

### 三.SringIOC容器解析

```
ApplicationContext ioc = new ClassPathXmlApplicationContext("你所选择的xml文件");
```

### 四.Bean的XMl配置和管理

##### 1.XML配置

###### (1)一个基本的XML配置

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean class="com.zlc.spring.bean.Monster"  id="monster02">
        <property name="monsterId" value="2"/>
        <property name="name" value="孙悟空"/>
        <property name="skill" value="七十二变"/>
    </bean>
</beans>
```

解析：1.class : 是 用来 指定 全路径，作用是为了底层的反射创建

​			2.id :属性表示 该对象 在Spring容器的id ，将来可以通过Id获得这个对象，id唯一

​			3.property :是赋给对象属性  name,value是赋给对象各个属性的val , 如果不给 会有一个默认值 如null

​			4.ref 依赖引入其他的bean

###### (2)配置XML文件的各种操作

//////暂时跳过,用到自己去查

###### (3)详解bean

a.<bean id="monster02" class="com.zlc.spring.entity.Monster" parent="monster01">

parent="monster01"：就是montser02 完成复制monster01

b.<bean id ="monster01" class="com.zlc.spring.entity.Monster" scope="propotype">

scope="propotype:就是指多例; scope = "singleton"（默认就是单例）

c.bean的后置处理器

首先去实现BeanPostProcessor,然后去XML文件配置

```
public class MyBeanPostProcess implements BeanPostProcessor {
//	初始化之前完成一些定制的业务逻辑
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("postProcessBeforeInitialization被调用");
        return BeanPostProcessor.super.postProcessBeforeInitialization(bean, beanName);
    }
//	初始化之后完成一些定制的业务逻辑
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("postProcessAfterInitialization被调用");
        return BeanPostProcessor.super.postProcessAfterInitialization(bean, beanName);
    }
}
```

```
<bean class="com.zlc.spring.bean.MyBeanPostProcess" id="myBeanPostProcess"></bean>
```

作用：**bean后处理器**主要应用于bean的创建过程中的一些操作，如检测下是否实现了指定接口，或用一个代理包装下bean实例，把代理返回等等。

d.bean的生命周期

bean的创建是由JVM完成的，然后执行以下方法

1.构造器

2.执行set相关方法

3.调用Bean初始化的方法（需要配置）

4.使用Bean

5.当容器关闭时，调用Bean的销毁方法（需要配置）

##### 2.注解配置Bean

四个最常见的:@Component,@Controller,@Service,@Repository(没什么可说的).

扫描包也没啥可以说的<context:component-scan base-package="要扫描的包名".

下面重点说一下，自动装配

(1) @Resource (最常用):

@Resource有两个重要的属性：name type ，spring容器会解析@Resource注解的name属性为bean的名字，type属性为bean的类型，使用@Resource注解的name属性表示按照byName进行解析，使用type属性表示按照byType类型进行解析;不指定的时候默认使用name,默认为类的首字母小写.默认按名称装配,当找不到名称匹配的bean再按类型装配.可以写在成员属性上,或写在setter方法上(//注意使用@Resource需要加入依赖//)

(2)@Autowired

默认按类型匹配,自动装配(Srping提供的),如果由多个该类型的bean,就按照首字母小写去查找，找不到就报错.可以写在成员属性上,或写在setter方法上;

###  五.AOP

#### 1.前置条件:熟悉动态代理,基于动态代理,通过aspect框架来实现的

#### 2.易错点：要去在xml文件中启动aop注解,不然aop注解就失效了

```
<aop:aspectj-autoproxy/>
```

#### 3.五种通知

(1)@Before--前置通知

 (2)@AfterReturning--返回通知

(3)@AfterThrowing--异常通知

(4)@After--后置通知

(5)@Around--环绕通知 (用的少，知道就好)

具体使用:

1.需要开启aop   : <aop:aspects-atuxxxx>

2.配置一个aspect类，在此类里面去进行切入

```
@Aspect
@Component
public class SmartPhoneAbspect {
    @Before(value = "execution(public void com.zlc.spring.entity.SmartPhone.ring())")
    public static void beforeWay(JoinPoint joinPoint){
        Signature signature = joinPoint.getSignature();
        System.out.println("方法名"+signature.getName());
    }
    @AfterReturning(value ="execution(public int com.zlc.spring.entity.SmartPhone.getSum(int,int))")
    public void afterWay(){
        System.out.println("你好");
    }
}
```

3.以@Before为例: @Before(value = "execution(权限修饰符 返回值类型 全类名.方法（只写int 这种）)")

4.  当你开启了AOP，就要用接口来接收，因为你已经是代理类型了.

   ```
   public static void main(String[] args) {
       ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
       SmartPhone redmi12 = ioc.getBean("redmi12", SmartPhone.class);
       redmi12.ring();
       redmi12.getSum(1,1);
   }
   ```

#### 4.细节

1.模糊配置//需要自己去查

2.JoinPoint :

常用方法 需要自己去查

3.如果需要返回值，可以在@AfterReturning中用 returning = "xxx"获取.

```
@AfterReturning(value = "execution(public int com.zlc.spring.entity.SmartPhone.getSum(int,int))",returning = "res")
public void afterGetSum(Object res){
    System.out.println(res);
}
```

4.如果需要获取异常和第三条同理，不过是在@AfterThrowing,用throwing = "xxx"

5.切入点的优先级

如果同一个方法有多个切面同时切入，那么执行的优先级如何控制？
基本语法：@order(value = n) n越小优先级越高   一般作用在切面类上面，也可以作用在切面方法上

#### 5.切面类表达式的重用（常用）

```
@Pointcut(value = "execution(public void com.zlc.spring.entity.SmartPhone.ring())")
public void ring(){
}

@Before(value = "ring()")
public static void beforeWay(JoinPoint joinPoint){
    Signature signature = joinPoint.getSignature();
    System.out.println("方法名"+signature.getName()+"开始前");
}
@AfterReturning(value = "ring()")
public void afterWayRunning(){
    System.out.println("方法开始后");
}
```



### 六.JDBCTemplate

#### 1.环境搭配

(1)需要的依赖d

    <!-- Spring-jdbc的依赖，JdbcTemplate依赖的jar包 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>${spring.version}</version>
    </dependency>
```
//Mysql驱动
<dependency>
  <groupId>com.mysql</groupId>
  <artifactId>mysql-connector-j</artifactId>
  <version>8.0.33</version>
</dependency>
```

```
//durid 德鲁伊连接池   
<dependency>
  <groupId>com.alibaba</groupId>
  <artifactId>druid</artifactId>
  <version>1.0.9</version>
</dependency>
//c3p0 连接池
    <dependency>
      <groupId>com.mchange</groupId>
      <artifactId>c3p0</artifactId>
      <version>0.9.5</version>
    </dependency>
```

(2)需要的配置文件

a.c3p0版的配置文件

![image-20231122180344614](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231122180344614.png)

b.德鲁伊连接池版的配置文件





（3）在xml文件中  1.引入外部jdbc.properties配置文件  2. 配置数据源对象  3.配置jdbcTemplate对象

a.c3p0版的

```
<!--       引入外部的jdbc.properties-->
        <context:property-placeholder location="classpath:jdbc.properties"/>
<!--       配置数据源对象                                                 -->
    <bean class="com.mchange.v2.c3p0.ComboPooledDataSource" id="dataSource">
        <property name="user" value="${jdbc.user}"/>
        <property name="password" value="${jdbc.password}"/>
        <property name="driverClass" value="${jdbc.driver}"/>
        <property name="jdbcUrl" value="${jdbc.url}"/>
    </bean>
<!--    配置jdbcTemplate对象-->
    <bean class="org.springframework.jdbc.core.JdbcTemplate" id="jdbcTemplate">
        <property name="dataSource" ref="dataSource"/>
    </bean>
```

b.德鲁伊版的

#### 2.添加与修改

a.add:

```
ApplicationContext ioc =
        new ClassPathXmlApplicationContext("beans1.xml");
JdbcTemplate jdbcTemplate = ioc.getBean(JdbcTemplate.class);
String sql = "insert into admin(name,password) values(?,?)";
int tom = jdbcTemplate.update(sql, "tom", "8888");
System.out.println(tom);
if(tom > 0) System.out.println("数据添加成功");
```

b.update:

```
ApplicationContext ioc =
        new ClassPathXmlApplicationContext("beans1.xml");
JdbcTemplate jdbcTemplate = ioc.getBean(JdbcTemplate.class);
String sql = "update admin set password = ? where id = ?";
jdbcTemplate.update(sql,"011111",2);
```

#### 3.查询单个后封装成对象

```
        ApplicationContext ioc =
                new ClassPathXmlApplicationContext("beans1.xml");
        JdbcTemplate jdbcTemplate = ioc.getBean(JdbcTemplate.class);
        String sql = "select name,password from admin where id = ?";
        //查询是不是需要返回一个javaBean   这里使用实现RowMapper的BeanPropertyRowMapper
//        BeanPropertyRowMapper可以将数据库查询结果转换为Java类对象。
        //使用RowMapper接口返回的数据进行一个封装,底层是反射,所以传入一个JavaBean.class也很正常喽~~~
        //queryForObject(String sql, RowMapper<T> var2,args...)
        BeanPropertyRowMapper<User> userBeanPropertyRowMapper = new BeanPropertyRowMapper<>(User.class);
        User user = jdbcTemplate.queryForObject(sql, userBeanPropertyRowMapper, 1);
        System.out.println(user);
```

#### 4.查询后返回对象集合

```
ApplicationContext ioc =
        new ClassPathXmlApplicationContext("beans1.xml");
JdbcTemplate jdbcTemplate = ioc.getBean(JdbcTemplate.class);
String sql = "select id,name,password from admin";
List<Book> books = jdbcTemplate.query(sql, new BeanPropertyRowMapper<Book>(Book.class) {
});
for(Book book:books){
    System.out.println(book);
}
```

#### 5.查询返回单行数据

```
ApplicationContext ioc =
        new ClassPathXmlApplicationContext("beans1.xml");
JdbcTemplate jdbcTemplate = ioc.getBean(JdbcTemplate.class);
String sql = "select name from admin where id = ? ";
String s = jdbcTemplate.queryForObject(sql, String.class,1);
System.out.println(s);
```

#### 6.具名参数











### 七.声明式事务

1.快速演示

(1)在需要的service层方法上加上@Trnsactionl 

(2)在启动类上























## SpringMVC框架

### 一.简介：

是Spirng关于WEB的一个组件，因为比较重要所以就单独拿出来作为一个知识点

SpringMVC的执行框架图⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐

![在这里插入图片描述](https://img-blog.csdnimg.cn/31e0fb3fad6841049234733ea5bcc1da.png)

































### 二.SpringMVC环境搭配

(1)需要的依赖

```
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.3.8</version>
    </dependency>
<!--    springMVC2-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.3.8</version>
    </dependency>
```

(2)需要在WEB-INF下面的web.xml文件中配置中央处理器

```
<!--  中央处理器-->
  <servlet>
    <servlet-name>springDispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    //下面是配置中央处理器
    //<init-param>
    //<param-name>contextConfigLocation</param-name>
    //springDispatcherServlet-servlet.xml文件是配置的一个文件用来写扫描包之类的东西的
    //<param-value>classpath:springDispatcherServlet-servlet.xml></aram-value>
    //<init-param>
    //设置web项目启动时就自动加载
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>springDispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
```

（3）然而我们更常用的是在WEB-INF下面写一个springDispatcherServlet-servlet.xml（注意springDispatcherServlet是由你自己决定的，这个名字必须保持和你在web.xml配置的中央处理器的名字一样）底层源码里会默认去WEB-INF下面寻找配置的中央处理器的名字拼接-servlet拼接.xml，如果找到了就读取这个配置文件.

(4)配置视图处理器

```
<!--        配置视图解析器-->
        <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
            <property name="prefix" value="/WEB-INF/pages/"/>
            <property name="suffix" value=".jsp"/>
        </bean>
```

### 三.SpringMVC的基础知识

#### 1.@RequestMapping

```
@RequestMapping(value = "/vote")
@Controller
public class VoteHandler {
    @RequestMapping(value = "/getparam")
    public String getParam(@RequestParam(value = "name",required = false)String votename){
        System.out.println(votename);
        return "work_over";
    }
}
```

（1）@RequestMapping 注解可以在控制器类上和控制器类中的方法上使用。修饰类的时候 ，比如本次例子: /vote/getparam

（2）return 返回的是jsp html这种

（3）method = Reuqestmappring.POST/DELETE/GET/PUT  默认是可以接受post和get

​			也可以这样表达 @PostMappring @DeleteMapping  @PutMapping @GetMapping

​				//温馨提示：这种表达方式是Rest风格

​				//不过得先去配置Rest

```
<!--  配置Rest需要的HiddenHttpMethodFilter-->
  <filter>
    <filter-name>hiddenHttpMethordFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>hiddenHttpMethordFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
```

（4）测试 @RequestMapping 的 params 属性，该属性表示请求参数，也就是追加在URL上的键值对，多个请求参数以&隔开，例如：

```text
http://localhost/SpringMVC/user/login?username=kolbe&password=123456
```

```text
@Controller
@RequestMapping(path = "/user")
public class UserController {
        
        // 该方法将接收 /user/login 发来的请求，且请求参数有 username=kolbe&password=123456
        //如果是params={"username=A","password=B,那么请求参数则必须是username=A&password=B,否则浏览器错误
	@RequestMapping(path = "/login", params={"username","password"})
	public String login() {
		return "success";
	}
}
```

（5）注意如果你使用了Rest风格 ， 那你在return时，则必须要使用redirect:,相当于是搞了一个方法用来当跳板

```
    @PutMapping(value = "/book/{id}")
    public String updataBook(@PathVariable("id")String id){
        System.out.println("updata = "+id);
        return "redirect:/user/success";
        //解析成/网络工程名/user/success
    }
    @RequestMapping(value ="/success")
    public String successGenecal(){
        return "work_over";
    }
```

#### 2.获取数据之两个注解

(1）@RequestParam  输入的是参数

​		@RequestParam(value = "bookname")String bookName

​			value 必须要和你在页面中输入的相同 ,比如   <input type = "text" name = "bookname">

```
@RequestMapping(value = "/appendBook")
public String appendBook(@RequestParam(value = "bookname")String bookName){
    System.out.println("添加书籍" + bookName);
    return "work_over";
}
```

(2)   @PathVariable   输入的是URL中的占位符对应的数据 比如     /user/book/100

​		细节：required = false   默认是true  ，意思是该数据你必须给我，不然就报错

```
@PutMapping(value = "/book/{id}")
public String updataBook(@PathVariable("id",required = false)String id){
    System.out.println("updata = "+id);
    return "redirect:/user/success";
}
```

（3）两者的异同:

​				都是用来接受数据的，但是@RequestParam是用来接收参数的，@PathVariable是用来接收URL里的数据

#### 3.获取数据之javabean and 原生servlet

（1）javabean 是自动封装的

Book book  这个是从前台获取的数据自动封装成一个javabean

```
@RequestMapping(value = "/appendBook")
public String appendBook(Book book){
    System.out.println("要添加的书籍是" + book);
    return "work_over";
}
```

(2) 获取原生Servlet 

同理HttpServletRequest，HttpServletReponse,HttpSession,HttpCookie都是这样可以直接获得的

```
@RequestMapping(value ="/success")
public String successGenecal(HttpServlet servlet){
    return "work_over";
}
```

#### 4.获取数据之模型数据

(1)将数据放入 request域(放入request域之后就可以在前端去调用了)

a.使用map

```
@RequestMapping(value ="/success")
public String successGenecal(Book book,Map<String,Object> map){
	map.put("name",book.getName());
	map.put("price",book.getPrice());
    return "work_over";
}
```

b.使用HttpServletRequest

```
@RequestMapping(value = "/getparam")
public String test(Book book,HttpServletRequest){
    request.setAtribute("bookname",book.getName());
    return "work_over";
}
```

c.使用ModelAndView

不是很熟悉，以后用到的时候再去查吧

d.javaBean 自动封装

#### 5.@ModelAttrbute

有点类似于我们前面学的前置通知

如果你在一个方法上面加了这个标签，当调用该Controller/Handler其他方法时都会先调用这个方法.

#### 6.重定向和请求转发

刚刚我们在学习如何解决Restful风格导致的浏览器405错误时，用到了重定向redirect，那么这里将会重点讲解一下

(1)redirect

reurn "redirect:/user/success"  : 会解析成  /web工程名/user/success

(2) return "forward:/user/success"  

(3)注意事项:

经过在idea中的实测，以下四种写法都是ok的

redirect：
return “redirect:/register”;------------ ok
return “redirect:/register.html”; ------------ ok
以上这两种写法都是ok的 加不加html 对于redirect是一样的

forward：
return “forward:/activationemail”; ------------ ok
return “forward:/activationemail.html”; ------------ ok
同样的, 上面的写法对于forward也成立. 但是有一个大坑, forward不能forward到自己的@RequestMapping("")里面去

重定向不可以访问WEB-INF下面的资源但是访问外面的web资源:0

请求转发可以访问WEB-INF下的资源，那可以访问外面的web资源？应该不可以吧，我也不确定.??????????

redirect方式相当于”response.sendRedirect()”. 这种方式浏览器地址栏最后显示的路径是转发后的新的路径。最后返回到浏览器后,因为地址栏显示的是转发后的url,所以刷新页面时只会执行后面的url映射的控制器.

forward方式相当于request.getRequestDispatcher().forward(request,response)，最后返回到浏览器后,因为地址栏显示的是转发前的url,所以刷新页面时会依次执行前后两个控制器.

#### 7.视图解析器

##### (1) 默认视图解析器

InternalResourceViewResolver是默认视图解析器,我们写的这个算是修改了默认视图解析器，如果我们在最开始没有写这个,那么底层也是有默认视图解析器的,只不过我们在return 的时候需要使用 forward 和direct  不然就报错.

```
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/pages/"/>
    <property name="suffix" value=".jsp"/>
</bean>
```

##### (2)自定义视图解析器(有时候可能会用到,先做了解好吧)

a.自定义视图解析器需要我们配置一个 BeanNameViewResolver来解析我们自定义的视图解析器

```
<!--    配置自定义视图解析器
        1.BeanNameViewResolver可以解析我们自定义的视图解析器
        2.属性 Order 是  决定执行顺序,值越小优先级越高;默认视图解析器的order默认值为Integer.MAX_VALUE；
        自定义视图解析器的order默认值为LOWST_PRECDENCE = 2147483647
        所以说，你随便给自定义视图解析器Order一个数就Ok ，这样自定义视图解析器优先级就比默认视图解析器高.
-->
        <bean class="org.springframework.web.servlet.view.BeanNameViewResolver" id="myView">
            <property name="order" value="99"/>
        </bean>
```

b.需要一个类去继承AbstractView 实现render（）方法

```
@Component(value = "MyView")
public class MyView extends AbstractView {
    @Override
    protected void renderMergedOutputModel(Map<String, Object> map, HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        //完成视图渲染
        //并且完成跳转
        ///WEB-INF/pages/my_view.jsp 会被springMVC 解析成/工程路径/WEB-INF/pages/my_view.jsp
        System.out.println("进入到自己的试图...");
        httpServletRequest.getRequestDispatcher("/WEB-INF/pages/my_view.jsp")
                .forward(httpServletRequest,httpServletResponse);
    }
}
```

#### 8.注解驱动

```
<!--        加入两个常规配置-->
<!--        支持SpringMVC的高级功能，比如JSR303校验，映射动态等等-->
        <mvc:annotation-driven></mvc:annotation-driven>
<!--        将spinrgMVC不能处理的请求，交给tomcat处理，比如css,js-->
        <mvc:default-servlet-handler></mvc:default-servlet-handler>
```

#### 9.数据格式化和数据检验

##### （1）为什么需要数据格式化和数据检验?

​			你想一下，如果你在前端输入一个生日，但是却恶意输入一堆字符串这时候浏览器就会报错，尽管前端可以做到数据检验，但是我们后端也必须再进行一次校验.!!!(SpringMVC可以将根据需要转换的类型进行自动转换，但当转换失败的时候（例如：非数字无法转换成数数字），会返回`400错误`)

##### ![在这里插入图片描述](https://img-blog.csdnimg.cn/e2ec98a76b584fb7b685b04b429b4646.png)(2)数据转换(一般的不需要担心)

特殊的类型转换

 除了字符串转换为数字之外，我们在使用中也会遇到很多其他特殊类型的数据格式需要进行转换。
 下边我们演示两种特使格式的转化（格式化）：

前端页面:

<h3>添加妖怪</h3>
<form action="save1">
    妖怪名字：<input type="text" name="name"/><br/>
    妖怪年龄：<input type="text" name="age"/><br/>
    妖怪邮箱：<input type="text" name="email"/><br/>
    生日：<input type="text" name="birthday"/>格式："2000-11-11"<br/>
    薪水：<input type="text" name="salary"/>格式："666,666.66"<br/>
    <input type="submit" value="添加妖怪">
</form>
```
//后端的一个JavaBean
public class Monster {
    private String name;
    private Integer age;
    private String email;
    //用这两个注解
    @DateTimeFormat(pattern = "yyyy-MM-dd")
    private Date birthday;
    @NumberFormat(pattern = "###,###.##")
    private Float salary;
    //构造器 什么get set toString都省略了
```

 从上边这些我们都可以看出，当我们的数据转换出现问题的时候，都会返回`400错误`，而这种回显方式显然是很不合理的，下边我们会给出解决方案。

需要的Jar包

![img](https://img-blog.csdnimg.cn/f7ddf0ea094e4d8488fdcf98efa5b4ec.png)

##### (3)<<from:from>>标签:和实际运用

介绍： 在这个表单中，我们使用了<form:form>这个标签，这是SpringMVC提供的一个标签。它的使用主要注意以下几点：

SpringMVC 表单标签在显示之前必须在request中有一个 bean, 该 bean 的属性和表单标签的字段要对应。
request 中的 key 为: form 标签的modelAttrite属性值， 比如这里的 monsters。

//例子

<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>添加妖怪页面</title>
</head>
<body>

<form:form action="save" modelAttribute="monster">
    妖怪名字：<from:input path="name"/><form:errors path="name"/><br/>
    妖怪年龄：<from:input path="age"/><form:errors path="age"/><br/>
    妖怪邮箱：<from:input path="email"/><form:errors path="email"/><br/>
    生日：<form:input path="birthday"/><form:errors path="birthday"/><br/>
    薪水：<form:input path="salary"/><form:errors path="salary"/><br/>
    <input type="submit" value="添加妖怪">
</form:form>
</body>
</html>

在上边的前端代码中，我们使用了SpringMVC提供的标签，这是为了方便于回显我们的数据。也就是当出现数据转换错误，或者数据验证错误的时候，不会回显我们的`400错误`，而是回显`提示信息`。

//javabean类

public class Monster {
    private Integer id;
    // 不能为空（null），也不能为empty
    // Asserts that the annotated string, collection, map or array is not {@code null} or empty.
    @NotEmpty
    private String name;

    // 我们的注解可以配合使用。但需要注意的是：NotNull和NotEmpty是有所区别的，NotNull支持所有的类型
    @NotNull(message = "age不能为空")
    // 指定数值的范围，默认最小值是0，最大值是Long的最大值（Long.MAX_VALUE）
    @Range(min = 1,max=100)
    private Integer age;
    @NotEmpty(message = "邮箱不能为空")
    private String email;
    @NotNull(message = "生日不能为空")
    @DateTimeFormat(pattern = "yyyy-MM-dd")
    private Date birthday;
    @NotNull(message = "薪水不能为空")
    @NumberFormat(pattern = "###,###.##")
    private Float salary;
@Controller
@Scope(value = "prototype")
public class MonsterHandler {
    /**
     * 当我们在map存放数据的时候，他会存放到request
          * @param map
          * @return
               */
            // 显示添加monster的页面
            @RequestMapping(value = "/addMonsterUI")
            public String addMonster(Map<String,Object> map){
            // 如果使用了SpringMVC的表单，那么就得在request中放入一个bean对象
            // 这个对象的属性名要对应 表单标签的 modelAttribute 属性值。
            map.put("monster",new Monster());
            return "datavaild/monster_addUI";
            }

    /**
     * SpringMVC可以将提交的数据，按参数名和对象的属性匹配，封装成一个对象。
     * @Valid Monster monster表示对monster进行校验
     * Errors errors，如果校验的过程中出现错误，会将其保存到 errors 对象中
     * Map<String,Object> map，如果校验出现错误，讲错误信息保存到map中去，同时报错monster对象
     *
     * 校验发生的时机：在SpringMVC底层反射调用目标方法时，会接收到http请求，然后根据注解来进行校验
     *      在校验过程中，如果出现了错误，就把错误信息填充到errors和 map 中
     * @param monster
     * @return
     */
    // 编写方法，处理添加bean
    @RequestMapping(value = "/save")
    public String save(@Valid Monster monster, Errors errors, Map<String,Object> map){
        System.out.println("----monster----" + monster);
        System.out.println("====map=====");
        for (Map.Entry<String, Object> entry : map.entrySet()) {
            System.out.println("key= " + entry.getKey() + " " + "value= " +entry.getValue());
        }
        System.out.println("====errors=====");
                if (errors.hasErrors()){
                List<ObjectError> allErrors = errors.getAllErrors();
                for (ObjectError allError : allErrors) {
                    System.out.println("error=" + allError);
                }
                return "datavaild/monster_addUI";
            }
            return "datavaild/success";
        }

注意：我们想要使用数据验证，还得再验证的数据(对象)之前，加上`@Vaild`注解才能生效。

#### 10.乱码问题

(1)解决方式1 使用一个自定义的过滤器，将所有的请求都设置编码utf-8,但这样就写死了,只能是utf-8.

```
public class MyCharacterFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        //加入对编码的处理
        servletRequest.setCharacterEncoding("utf-8");
        //放行请求
        filterChain.doFilter(servletRequest,servletResponse);
    }

    @Override
    public void destroy() {

    }
}
```

```
<filter>
  <filter-name>MyCharacterFilter</filter-name>
  <filter-class>com.zlc.filter.MyCharacterFilter</filter-class>
</filter>
<filter-mapping>
  <filter-name>MyCharacterFilter</filter-name>
  <url-pattern>/*</url-pattern>
```

(2)创建Spring过滤器（更加方便更加强大）

```
<filter>
  <filter-name>CharacterEncodingFilter</filter-name>
  <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
</filter>
<filter-mapping>
  <filter-name>CharacterEncodingFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

使用Spring提供的CharacterEncodingFilter,并且设置utf-8

#### 11.SpringMVC实现json数据交互(@ResponseBody)

##### 1.环境搭配

(1)引入依赖

<!-- jackson依赖 -->
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-core</artifactId>
  <version>2.9.9</version>
</dependency>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>2.9.9</version>
</dependency>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-annotations</artifactId>
  <version>2.9.9</version>
</dependency>

（2）配置类型转换器

引入相关的依赖jar包后，需要在SpringMVC核心配置文件springmvc.xml中，为处理器适配器（HandlerAdapter）配置类型转换器列表MessageConverter，并在其中添加需要的类型转换器。这样当请求到达处理器适配器层时，配置的@RequestBody注解与@ResponseBody注解就会利用具体的类型转换器MessageConverter将请求信息转换为指定的格式。具体配置如下：
<!-- 注解适配器 -->
<!-- 注意：如果配置了<mvc:annotation-driven/>自动注解标签，那么这种情况就不需要配置类型转换器了.因为SpringMVC已经默认初始化了7种转换器。 -->
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter">
    <property name="messageConverters">
        <list>
            <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"></bean>
        </list>
    </property>
</bean>

#### 12.处理JSON

##### 1.@ResponseBody

(1)  作用 ：  

```
  将Controller方法上的返回值
   使用特定的格式写入到response的body处
   然后再返回给客户端 
```

```
注意事项:
   1.如果一个方法上没有加入ResponseBody注解,则Spring会将方法的返回值封装为一个ModelAndView对象返回
   2.如果一个方法上加入了ResponseBody注解时,当返回值是字符串时，则返回字符串至客户端
      如果返回值是一个对象时,则将对象转换为json串,返回到客户端
   3.注意：在使用此注解之后不会再走视图处理器，而是直接将数据写入到输入流中，他的效果等同于通过response对象输出指定格式的数据。
```

(2)详细知识:

a. 使用场景：@ResponseBody是作用在方法上的，@ResponseBody 表示该方法的返回结果直接写入 HTTP response body 中，一般在异步获取数据时使用【也就是AJAX】。

b.ResponseBody注解实现原理

```
通过HttpMessageConverter中的方法进行转换
   HttpMessageConverter是一个接口
   在其实现类完成转换
 如果是bean对象,会调用对象的getXXX()方法获取属性值并且以键值对的形式进行封装,转化为json串
 如果是map集合,采用get(key)方式获取value值,然后进行封装
```

(3)拓展知识@RestController

在类上用@RestController，其内的所有方法都会默认加上@ResponseBody，也就是默认返回JSON格式。如果某些方法不是返回JSON的，就只能用@Controller了吧，这也是它们俩的区别。

(4) 例子

```
@Controller
@RequestMapping(value = "/testResponseBody")
public class TestResponseBody {
    @RequestMapping(value = "/getJson")
    @ResponseBody
    public User test(){
        User user = new User(1, "zlc", "000000", "88@qq.com");
        return user;
    }
}
```



```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        window.onload = function (){
            var getJson = document.getElementById("getJson");
            getJson.onclick = function (){
                //发送ajax请求
                //大概就是先到TestResponseBody里面执行方法，然后就经过一系列操作比如将信息回显，最后发送ajxa请求
                //这里视频用的jquer 我不会，后面学了vue 再说吧
            }
        }
    </script>
</head>
<body>
<input type="button" id="getJson" value="获取JSON数据">
</body>
</html>
```

##### 2.@RsquestBody

（1）导言：上面学了将 JavaBean  —> Json串(我们给前端的数据)  ，那么我们经常也会用到  将 Json串  —> javaBean（前端给我们的数据）

（2）基础知识讲解 :   

a.  @RequestBody主要用来接收前端传递给后端的json字符串中的数据的(请求体中的数据的)；而最常用的使用请求体传参的无疑是POST请求了，所以使用@RequestBody接收数据时，一般都用POST方式进行提交。在后端的同一个接收方法里，@RequestBody与@RequestParam()可以同时使用，@RequestBody最多只能有一个，而@RequestParam()可以有多个。

（3）例子

```
@RequestMapping(value = "/getData")
public User test2(@RequestBody User user){
    System.out.println(user);
    return user;
}
```



##### 3.HttpMessageConverter机制介绍



#### 13.SpringMVC文件上传和文件下载

##### 1.文件上传

（1）导言 ：

Servlet3.0规范已经提供方法来处理文件上传，但这种上传需要在Servlet中完成。而Spring MVC则提供了更简单的封装。
Spring MVC为文件上传提供了直接的支持，这种支持是用即插即用的MultipartResolver实现的。
Spring MVC使用Apache Commons FileUpload技术实现了一个MultipartResolver实现类：CommonsMultipartResolver。因此，SpringMVC的文件上传还需要依赖Apache Commons FileUpload的组件。

文件上传是项目开发中最常见的功能之一 ，SpringMVC 可以很好的支持文件上传，但是SpringMVC上下文中默认没有装配MultipartResolver，因此默认情况下其不能处理文件上传工作。如果想使用Spring的文件上传功能，则需要在上下文中配置MultipartResolver。

（2）前端要求:

前端表单要求：为了能上传文件，必须将表单的`method`设置为`POST`，并将`enctype`设置为`multipart/form-data`。只有在这样的情况下，浏览器才会把用户选择的文件以二进制数据发送给服务器。

![image-20231128115412638](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231128115412638.png)

表单中enctype属性的详细说明：

application/x-www=form-urlencoded：默认方式，只处理表单域中的 value 属性值，采用这种编码方式的表单会将表单域中的值处理成 URL 编码方式。
multipart/form-data：这种编码方式会以二进制流的方式来处理表单数据，这种编码方式会把文件域指定文件的内容也封装到请求参数中，不会对字符编码。
text/plain：除了把空格转换为 “+” 号外，其他字符都不做编码处理，这种方式适用直接通过表单发送邮件。

（3）需要的搭配:

导入这个依赖组件，Maven会自动帮我们导入它的依赖包【commons-io】

<!--文件上传-->
<dependency>
   <groupId>commons-fileupload</groupId>
   <artifactId>commons-fileupload</artifactId>
   <version>1.3.3</version>
</dependency>

配置bean：multipartResolver

**注意：** 这个bena的id必须为：multipartResolver ， 否则上传文件会报400的错误！

![image-20231128120048828](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231128120048828.png)

CommonsMultipartFile 的常用方法：

String getOriginalFilename()：获取上传文件的原名
InputStream getInputStream()：获取文件流
void transferTo(File dest)：将上传文件保存到一个目录文件中



随便举一个例子

```
@Controller
@RequestMapping(value = "/file")
public class TransmitFile {
    @RequestMapping(value = "/transmitFile")
    public String fileup(@RequestParam(value = "file") MultipartFile file, HttpServletRequest request) throws IOException {
        //获取文件名
        String upFileName= file.getOriginalFilename();
        //如果文件为空则直接返回首页
        if("".equals(upFileName)){
            return "index";
        }
        System.out.println("上传文件名:" + upFileName);
        //设置保存路径,上传的文件保存在哪里
        String filepath = request.getServletContext().getRealPath("/img/" + upFileName);
        //创建文件
        File saveFile = new File(filepath);
        //将上传的文件，转存到savaToFile
        file.transferTo(saveFile);
        return "my_view";
    }
}
```

疑惑： 为什么我的Controller方法一直接受不到 file???????????

解惑：：我他妈的把multipartResolver 配置到web.xml里面去了，应该配置到springDispatcherServlet-servlet.xml，巨大失误，浪费了我他妈的一个小时的时间.



##### 2.文件下载

- 第一种可以直接向response的输出流中写入对应的文件流
- 第二种可以使用 ResponseEntity<byte[]>来向前端返回文件

1️⃣传统方式

**文件下载步骤：**

- （1）设置 response 响应头
- （2）读取文件 — InputStream
- （3）写出文件 — OutputStream
- （4）执行操作
- （5）关闭流 （先开后关）

@GetMapping("/download1")
@ResponseBody
public R download1(HttpServletResponse response){
    FileInputStream fileInputStream = null;
    ServletOutputStream outputStream = null;
    try {
        // 这个文件名是前端传给你的要下载的图片的id
        // 然后根据id去数据库查询出对应的文件的相关信息，包括url，文件名等
        String  fileName = "wang.jpg";

        //1、设置response 响应头，处理中文名字乱码问题
        response.reset(); //设置页面不缓存,清空buffer
        response.setCharacterEncoding("UTF-8"); //字符编码
        response.setContentType("multipart/form-data"); //二进制传输数据
        //设置响应头，就是当用户想把请求所得的内容存为一个文件的时候提供一个默认的文件名。
        //Content-Disposition属性有两种类型：inline 和 attachment 
        //inline ：将文件内容直接显示在页面 
        //attachment：弹出对话框让用户下载具体例子：
        response.setHeader("Content-Disposition",
                           "attachment;fileName="+ URLEncoder.encode(fileName, "UTF-8"));
    
    	// 通过url获取文件
        File file = new File("D:/upload/"+fileName);
        //2、 读取文件--输入流
        fileInputStream = new FileInputStream(file);
        //3、 写出文件--输出流
        outputStream = response.getOutputStream();
    
        byte[] buffer = new byte[1024];
        int len;
        //4、执行写出操作
        while ((len = fileInputStream.read(buffer)) != -1){
            outputStream.write(buffer,0,len);
            outputStream.flush();
        }
        return R.success();
    } catch (IOException e) {
        e.printStackTrace();
        return R.fail();
    }finally {
        if( fileInputStream != null ){
            try {
                // 5、关闭输入流
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        if( outputStream != null ){
            try {
                // 5、关闭输出流
                outputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
2️⃣使用ResponseEntity方式

@GetMapping("/download2")
public ResponseEntity<byte[]> download2(){
    try {
        String fileName = "wang.jpg";
        byte[] bytes = FileUtils.readFileToByteArray(new File("D:/upload/"+fileName));
        HttpHeaders headers=new HttpHeaders();
        // Content-Disposition就是当用户想把请求所得的内容存为一个文件的时候提供一个默认的文件名。
        headers.set("Content-Disposition","attachment;filename="+ URLEncoder.encode(fileName, "UTF-8"));
        headers.set("charsetEncoding","utf-8");
        headers.set("content-type","multipart/form-data");
        ResponseEntity<byte[]> entity=new ResponseEntity<>(bytes,headers, HttpStatus.OK);
        return entity;
    } catch (IOException e) {
        e.printStackTrace();
        return null;
    }
}	





#### 15.异常处理







## MyBatis

### 一.一图胜千言

**传统的jdbc**

![image-20231130183610400](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231130183610400.png)

**使用MyBatis框架**

​	![image-20231130182657193](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231130182657193.png)



![image-20231130184008360](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231130184008360.png)



### 二.MyBatis基础知识



##### (1) 新知识点 父项目管理子项目

删除父项目的src ， 然后给父项目增加子项目

![image-20231130191122996](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231130191122996.png)

##### (2)配置Mybatis-config.xml 文件

**注意：模板自己去文档里copy**

//这里我直接在xml文件就指定了一些属性，实际上一般都是用properties文件来配置

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
//只需要在这里引入 配置文件   然后后面什么driver url username password的value 都这样写value = "${driver}".....
	//<properties ref = "src\main\resource\xxxx.properties"/>
    <environments default="development">
        <environment id="development">  
<!--            配置事务管理器-->
            <transactionManager type="JDBC"/>
<!--            配置数据源-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://127.0.0.1:3306/jdbctemplate?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                <property name="username" value="root"/>
                <property name="password" value="1674472827zlC"/>
            </dataSource>
        </environment>
    </environments>
<!--    这里我们设置需要关联的mapper.xml文件
        tip : 这里我们可以点击菜单中的copy中的Path from source root，这样比较快.
-->
    <mappers>
        <mapper resource="com/zlcstu/mapper/MonsterMapper.xml"/>
    </mappers>
</configuration>
```







##### (3)#{},${}

**#{}本质是占位符**，比如select * from student where id = #{}   => select * from student where id = ? 

​																											=>select * from student where id = '1'(假设id = 1)

**${}本质是字符拼接**，比如select * from student where id = #{}   => select * from student where id = 

​																											=>select * from student where id = 1(假设id = 1)

**简单理解:  #{}会自带单引号，而#{}不会带单引号**



案例：select * from 表名 

解答 select * from ${}   ,因为sql中表名是不能带单引号的.









##### (4)@Param



**建议只要是参数都加上这个注解**，不过如果只有一个参数其实不用加，好像是maven 从3.xx版本就可以实现多个参数不加@Param也不会报错



##### (5)模糊查询

"%#{id}%" => "%?%"  这个问号会被识别成 模糊查询的条件而不当成占位符



1. select * from table where id = '%${id}%'
2. select * from table where id = concat('%',#{id},'%')  （我个人偏向于使用第二个）
3. select * from tablke where id = "%"#{id}"%" （推荐使用第三个）





##### (6)解决字段名和属性名不一致

1. select的时候起别名

2. 配置文件设置，将_自动映射为驼峰

3. 使用映射(不过映射一般都用在 一对多，多对多)  工作中，**一般都是起别名，但是也要手动映射一下**

   ```/java
   （1）级联查询
   <resultMap id="empResultMap" type="Employee">
   	<id property="empId" column="emp_id"></id>
   	<result property="empName" column="emp_name"></result>
   	<result property="age" column="age"></result>
   	<result property="salary" column="salary"></result>
   	<result property="phone" column="phone"></result>
   	//相同的可以省略
   	//如果employee类里面有个department类型的属性，想要获取dept_id和dept_name
   	<association property="dept" javaType="Department"
   		<id property="id" column="id">
   		<result property="name" column="name">
   		<result property="phone" column="phone">
   	</association>
   </resultMap>
   
   
   <select id="xx" resultMap="empResultMap">
   xxxxxxxxxxxxxxxxx
   </select>
   
   (2)分布查询
   在empMapper中
   <resultMap id="empResultMap" type="Employee">
   	<id property="empId" column="emp_id"></id>
   	<result property="empName" column="emp_name"></result>
   	<result property="age" column="age"></result>
   	<result property="salary" column="salary"></result>
   	<result property="phone" column="phone"></result>
   	//相同的可以省略
   	//如果employee类里面有个department类型的属性，想要获取dept_id和dept_name
   	<association property="dept"
       	select="xxx.xx.deptMapper.xxxx(一个方法Id/resultMap名字)"
   		column="demp_id"   //查询条件
    	</association>
   </resultMap>
   在dempMapper中确实有一个通过id查询信息的select
   <select id=xxxx type="emo">
   	xxxxxxxxx
   </select>
   
   
   
   ```

4. 







##### (5)PageHelper



pageNum:当前页数 ，  pageSize:每页共有多少数据

​	PageHelper.startPage(pageNum,pageSize);

​	

例子:

```
//设置分页
PageHelper.startPage(ordersPageQueryDTO.getPage(),ordersPageQueryDTO.getPageSize());

//查询
Page<Orders> page = orderMapper.pageQuery(ordersPageQueryDTO);
//page中 有很多 数据，比如 page.getResult()返回的是当前页的所有数据
```



















##### (8)遇见常时，比如xxxxx文件找不到

**起因：不同版本的idea和maven之间互相起冲突**

比如这次测试中，你就会发现会报错,你的MonsterMapper.xml会显示找不到,你去target一看果然没有，那该怎么办呢？？

**解决方案一**： 在build中配置resources,来防止我们资源导出失败

​					解读：

​					1.不同的idea/maven 可能提示的错误不一样

​					2.不变应万变，少什么文件，就增加响应的配置即可

​					3.含义是将 src/main/java目录和 src/main/resource 目录和子目录的资源文件xml 和properties

​						在build项目时的，导出到对应的target目录下.

**将下面的粘贴到 父项目 的 pom.xml文件里加入build即可**

<build>
<resources>
      <resource>
        <!--表示需要编译的源文件路径-->
        <directory>src/main/java</directory>
        <includes>
          <!--表示以.properties和*.xml结尾的文件将进行编译-->
          <include>**/*.properties</include>
          <include>**/*.xml</include>
        </includes>
        <filtering>false</filtering>
      </resource>

             <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.*</include>
                </includes>
            </resource>
    </resources>
</build> 

**解决方案二（百分百解决，最终大招）**

设置一下目录

![image-20231130210016602](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231130210016602.png)

clean一下maven

![image-20231130210144128](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231130210144128.png)

然后你也可以切换回你自己的Maven（我好像使用的是Idea自带的maven????）





##### (9)配置日志输出

日志在多表查询  以及后面追究错误原因很有用

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<!--    配置日志输出-->
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
```



**输出信息案例：**

```
Logging initialized using 'class org.apache.ibatis.logging.stdout.StdOutImpl' adapter.
PooledDataSource forcefully closed/removed all connections.
PooledDataSource forcefully closed/removed all connections.
PooledDataSource forcefully closed/removed all connections.
PooledDataSource forcefully closed/removed all connections.
class com.sun.proxy.$Proxy9
Opening JDBC Connection
Created connection 192428201.
Setting autocommit to false on JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@b7838a9]
==>  Preparing: SELECT `name`,`age`,`salary` FROM `user`
==> Parameters: 
<==    Columns: name, age, salary
<==        Row: Goto Sakura, 196, 726.69
<==        Row: Sylvia Ramirez, 233, 375.58
<==        Row: Wong Wai Man, 533, 822.59
<==        Row: Ng Yu Ling, 444, 704.67
<==        Row: Jerry Ellis, 197, 884.17
<==        Row: Maeda Kasumi, 1, 1192.55
<==        Row: Rebecca Kennedy, 189, 43.36
<==        Row: Yue Chung Yin, 663, 298.21
<==        Row: Dai Kwok Kuen, 559, 72.15
<==        Row: Dong Jiehong, 199, 534.58
<==        Row: Lo Tin Wing, 1, 1476.22
<==        Row: Kaneko Minato, 533, 98.25
<==        Row: Heung Ling Ling, 831, 760.34
<==      Total: 13
User{id=null, age=196, name='Goto Sakura', gender=null, salary=726.69}
User{id=null, age=233, name='Sylvia Ramirez', gender=null, salary=375.58}
User{id=null, age=533, name='Wong Wai Man', gender=null, salary=822.59}
User{id=null, age=444, name='Ng Yu Ling', gender=null, salary=704.67}
User{id=null, age=197, name='Jerry Ellis', gender=null, salary=884.17}
User{id=null, age=1, name='Maeda Kasumi', gender=null, salary=1192.55}
User{id=null, age=189, name='Rebecca Kennedy', gender=null, salary=43.36}
User{id=null, age=663, name='Yue Chung Yin', gender=null, salary=298.21}
User{id=null, age=559, name='Dai Kwok Kuen', gender=null, salary=72.15}
User{id=null, age=199, name='Dong Jiehong', gender=null, salary=534.58}
User{id=null, age=1, name='Lo Tin Wing', gender=null, salary=1476.22}
User{id=null, age=533, name='Kaneko Minato', gender=null, salary=98.25}
User{id=null, age=831, name='Heung Ling Ling', gender=null, salary=760.34}
Resetting autocommit to true on JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@b7838a9]
Closing JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@b7838a9]
Returned connection 192428201 to pool.

```





##### (11)获取子增值

1. **在insert标签/options注解中使用 useGeneratedKeys、keyProperty、keyColumn 属性获取；**//效率高，推荐使用这个

   userGeneratedKeys="true"  允许获取自增值

   keyColumn   对应数据库表自增主键列名字

   keyProperty   对应实体类要填充的属性， keyColumn取出的值将赋给这个  （如果没有指定KeyColumn，自动将自增值给这个）
   
2. 经常只需要这样写 userGeneratedKeys=ture , keyProperty = id ,   因为如果没有指定KeyColumn，自动将自增值给这个属性



**配置文件版本**

<insert id="insertBook" parameterType="com.learn.entity.Book" useGeneratedKeys="true" keyColumn="id" keyProperty="id">
        INSERT INTO BOOK(NAME) VALUES(#{name})
    </insert>

**注解版本**

```
@Insert("        INSERT INTO `user` (`age`,`name`,`gender`,`salary`)" +
        "        VALUES(#{age},#{name},#{gender},#{salary})")
@Options(useGeneratedKeys = true,keyProperty = "id",keyColumn = "id")
public boolean addUser(User user);
```















### 三.手写MyBatis

#### 1.MyBatis核心框架图

![image-20231202103234204](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231202103234204.png)



### 四.Mybatis-config.xml配置文件详解



#### 1.properties属性

**前面已经讲过了**

#### 2.settings 全局参数定义

**这里的参数都是直接影响mybatis的行为，自己去查看文档去**

#### 3.typeAliases( 别名处理器)

1.你在xxmapper.xml文件中配置方法的时候常常需要指定类的全类名,为了降低全类名的代码冗余，你可以在mybatis-config.xml

文件中去统一配置

java 自带的java.lang.Integer 什么的不用写，可以直接写简称 Integer,因为**typeHanddler**已经帮我们搞完了



```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<!--    配置日志输出-->
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
<!--    配置全类名的简称-->
    <typeAliases>
        <typeAlias type="com.zlcstu.entity.User" alias="User"/>
        <typeAlias type="com.zlcstu.entity.Monster" alias="Monster"/>
        <typeAlias type="com.zlcstu.entity.Customer" alias="Customer"/>
    </typeAliases>
    //后面的略
```

上面的还是不够简洁，可以直接整合一个包，**id就是类名**

```
<!--    配置全类名的简称-->
    <typeAliases>
        <package name="com.zlcstu.entity"/>
    </typeAliases>
```

#### 4.typeHandlers(类型处理器)

**强调：这个一般都是使用默认的，你不需要操作**

**作用：将Mysql中的类型 --> Java类型**

**tip:如果你不知道Mysql类型对应的Java类型，自己去查，一定要注意别类型转换出错喽！！！**

比如：我以前还以为char 对应Java的Character,那以后我的JavaBean是用Character还是String???s![image-20231205172008740](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231205172008740.png)

#### 5.environments(环境)

1.resource 注册Mapper文件：xxxMapper.xml文件 （常用）

2.class：接口注解实现（也常用）

3.url：外部路径（使用很少，不推荐）  **<mapper uel = "file://D:\yy\kk\MonsterMapper.xml".**

4.package 方式注册

<mapper name = "com.zlc.mapper"/>



### 五.XML映射器

#### 1.简介

**导言：mybatis真正强大在于它的语句映射（在xxxMapper.xml配置），由于它的异常强大，当你拿它和具有相同功能的jdbc代码对比，会发现将近省略了百分之九十万的代码.//mybatis 致力于减少使用成本，让用户能更专注于SQL语句.**



**SQL映射文件常用的几个顶级元素（按照定义列出）**

- **cache ---该命名空间的缓存配置**
- **cache-ref --引用其他命名空间的缓存配置**
- **resultMap--描述如何从数据库结果集中加载对象，是最复杂也是最强大的元素**
- **parameterType--将会传入这条语句的参数的类全限定名或别名**





#### 2.XML映射器--parameterType

##### 问题1：

如果你想要查询 id = 76  or name = jdk100 的User，你该如何操作呢？



注意点(1)： 此时传入的不再是 一个 int id or String name 而是直接传入一个对象

![image-20231206163444057](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206163444057.png)





注意(2)：直接去填充 属性  - - - > new User

![image-20231206163614630](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206163614630.png)



##### 问题2:

如果你想要模糊查询  name含有 jack 的所有User，你该如何操作？

**//注意       模糊查询的一个坑！！！！！必须使用${}!!!!!!!**

![image-20231206164531371](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206164531371.png)

![image-20231206164749769](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206164749769.png)

![image-20231206164557926](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206164557926.png)

#### 3.XML映射器--Map入参类型

##### 问题1（Map入参）：

要求：id > 70 and salary > 100.00  , 并且要求传入参数为Map

//实际上以 Map 的形式来入参  更加灵活多变，因为不受javaBean/Pojo/entity的限制!!!!

![image-20231206171232975](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206171232975.png)



![image-20231206171426549](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206171426549.png)



![image-20231206171319920](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206171319920.png)

##### 问题2(map返回类型):

要求：id > 70 and salary > 100.00  , 并且要求传入参数为Map，返回类型也得是Map

//其实和Map入参一个道理，用键值对的形式给你把信息存起来了，而非之前用javaBean去存信息



![image-20231206172420329](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206172420329.png)



![image-20231206172541316](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206172541316.png)



![image-20231206172559146](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206172559146.png)



#### 4.XML映射器--ResultMap

**“resultMap 元素是Mybatis中最重要最强大的元素......ResultMap 的设计思想是，对简单的语句做到零配置，对于复杂一点的语句，只需要描述语句之间的关系就行了”**

**基本介绍：当实体类的属性和表单字段名字不一致时，我们可以通过resultMap进行映射，从而屏蔽实体类属性名和表的字段名的不同**

**//其实这个resultMap 还可以解决 多表查询  的一些东西，在映射那边**

##### 问题：

如果实体类的属性和表单字段名字不一样时，那么按照传统的方法查询，得到的结果只有名字一样的才能查到.不一样的是默认值（null）



![image-20231206190757571](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206190757571.png)



![image-20231206190952540](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206190952540.png)





![image-20231206191002312](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206191002312.png)



##### **问题的解决:**

##### **1.使用resultMap**:

![image-20231206192253036](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231206192253036.png)



**其实还可以使用表字段别名来解决，可以用，但是我们更推荐使用resultMap来解决这个question.后面学了mybatis-plus ，你就可以直接用一个注解@TableFiled来解决实体字段名和表字段名不一致的问题，@TableFiled甚至可以解决类名和表中的table名字不一致！！！！！太便捷了！！！！**

##### 2.ResultMap

**这个很重要自己去学习一下**

https://blog.csdn.net/krismile__qh/article/details/90644058

    <resultMap id="唯一标识" type="映射的entity对象的绝对路径">
        <id column="表主键字段" jdbcType="字段类型" property="映射entity对象的主键属性" />
    <result column="表某个字段" jdbcType="字段类型" property="映射entity对象的某个属性"/>
     
    <!-- 指的是entity对象中的对象属性 -->
    <association property="entity中某个对象属性" javaType="这个对象的绝对路径">
        <id column="这个对象属性对应的表的主键字段" jdbcType="字段类型" property="这个对象属性内的主键属性"/>
        <result column="表某个字段" jdbcType="字段类型" property="这个对象属性内的某个属性"/>
    </association>
     
    <!-- 指的是entity对象中的集合属性 -->
    <collection property="entity中的某个集合属性" ofType="这个集合泛型所存实体类的绝对路径">
        <id column="这个集合属性中泛型所存实体类对象对应表的主键字段" jdbcType="字段类型"
            property="这个集合属性中泛型所存实体类对象的主键属性"
        />
        <result column="表某个字段" jdbcType="字段类型" 
                property="这个集合属性泛型所存实体类对象的属性"
        />  
    </collection>
     
    <!-- 引用另一个resultMap (套娃) -->
    <collection property="entity中的某个集合属性" 
                resultMap="这个引用的resultMap的type,就是这个集合属性泛型所存实体类的绝对路径"
    />
    </resultMap>


### 六.动态SQL

##### 1.导言



- **为什么需要动态SQL：**

1.动态sql是mybatis最强大的特性之一

2.使用jdbc或者其他类似框架，根据不同条件拼接sql语句非常麻烦，例如拼接式要确保不能忘记添加必要的空格，还要注意去掉列表最后一个列名的逗号等等

3.sql映射语句中的强大动态sql语言，可以很好的解决这个问题

- **基本介绍**

1.在一个实际项目里面，sql语句往往很复杂

2.为了满足更复杂的业务需求，Mybatis的设计者提供了动态SQL的功能

- **动态SQL的必要性**

1.比如我们查询user，如果程序员输入的age<=0 ，我们的sql语句就不带age,如果>0，我们的sql语句就带上age（传统方法无法实现）

2.更新User对象时，没有设置新的属性值，就保持原来的只，设置了新的值，才更新

- **问题的解决**

1.使用mybatis提供的动态SQL

- **动态SQL常用的标签**

1.if[判断]

2.where【拼接where语句】

3.choose/when/otherwise【类似Java的switch语句，注意是单分支】

4.foreach【类似in】

5.trim【替换关键字/定制元素的的功能】

6.set【在update的set元素中，可以保证进入set标签的属性被修改，而没有进入set的，保持原来的值]



##### 2.if标签

**还是比较好理解的，如果age<=0那么就输出全部，如果age>0那么就执行If里面的语句**

![image-20231207124646673](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231207124646673.png)



##### 3.where标签

**注意：where标签，会在组织动态SQL中，加上where**

**注意:mybatis底层会自动地去掉多余的and，所以在where标签里面大胆地用and，在每一个句子前面都加上一个and**

**注意：当你在编写方法，传入的是一个对象比如这里的是User,那么在标签里面可以直接使用属性名，不需要@Param之类的东西,用map入参也是一个道理**

**一个很有趣的点：第一次我不小心把ParameterType=“map”写成ParameterType="User"，结果两者居然没有区别！！估计是底层的一些操作使得两者没区别，以后技术厉害了可以去看看源码研究一下为什么会没有区别**

<img src="https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231207131349339.png" alt="image-20231207131349339"  />



![image-20231207134225035](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231207134225035.png)



##### 4.choose/when/otherwise

**//类比swich case default**

![image-20231207133002160](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231207133002160.png)



##### 5.foreach标签

**介绍**

动态 SQL 的另一个常见使用场景是对集合进行遍历（尤其是在构建 IN 条件语句的时候

**参数解释：**
foreach 的主要作用在构建 in 条件中，它可以在 sql 语句中进行迭代一个集合(可以是list,set,数组,map等等)。foreach 元素的属性主要有 collection，item，separator，index，open，close。

**属性	描述**

- collection	指定要遍历的集合。表示传入过来的参数的数据类型。该属性是必须指定的，要做 foreach 的对象。
- index	索引，index 指定一个名字，用于表示在迭代过程中，每次迭代到的位置。遍历 list 的时候 index 就是索引，遍历 map 的时候 index 表示的就是 map 的 key，item 就是 map 的值。
- item	表示本次迭代获取的元素，若collection为List、Set或者数组，则表示其中的元素；若collection为map，则代表key-value的value，该参数为必选
- open	表示该语句以什么开始，最常用的是左括弧’(’，注意:mybatis会将该字符拼接到整体的sql语句之前，并且只拼接一次，该参数为可选项
- separator	表示在每次进行迭代之间以什么符号作为分隔符。select * from tab where id in(1,2,3)相当于1,2,3之间的","
- close	表示该语句以什么结束，最常用的是右括弧’)’，注意:mybatis会将该字符拼接到整体的sql语句之后，该参数为可选项



![image-20231207140451850](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231207140451850.png)

![image-20231207140502901](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231207140502901.png)



##### 6.trim标签(用的比较少)



##### 7.set标签

**注意：别忘了加逗号，这个还挺容易错的**

![image-20231207151555565](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231207151555565.png)



##### 8.一个注意事项

![image-20231207124535333](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231207124535333.png)



### 七.映射关系

#### 1.为什么需要映射？

**如果是多表查询，比如一个Person中的`card_id`关联一个idencard，（一个人对应一个身份证），那你如何在Java程序里面将idencard类与person类连在一起？**



#### 2.映射的演示(方式一多表联查)

//建表

![image-20231210181627989](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231210181627989.png)

//建类

![image-20231210182015653](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231210182015653.png)



//借助mybatis的resultMap来实现

![image-20231210184933085](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231210184933085.png)



#### 3.一个改进，提高一点性能，使用id

![image-20231210185114465](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231210185114465.png)

比如: 就是将primary key的那个属性单独搞出来.
	![image-20231210185256413](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231210185256413.png)

#### 4.第二种方式(推荐！！)

**有时候用第一种方式多表查询会很麻烦,第二种方式就会更加清爽!!!!!~~~**

**此方法的核心思想就是将多表查询分割成单表查询，简洁且更利于维护,而且可以复用已经写好的方法,其实就是组合使用，这种思想很厉害！要学习**

![image-20231210191058900](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231210191058900.png)

**一个小细节:  **  

![image-20231210191739202](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231210191739202.png)

**重点:**

```
<association property="card" column="card_id" select="com.zlc.mapper.IdenCardMapper.getIdenCardByID"/>
```

**association的property对应类的属性，column对应后面select方法的入参参数,select方法需要什么参数你就把要传给他的参数对应的表的属性名字写在这里**





#### 5.映射关系多对一

**一对多很简单，所以我们直接来写双向的一对多，比如Master和pet,一个master可以有多个pet，通过master可以查到pets,通过Pet又可以查到master**

//准备表     (有坑)

![image-20231217130035660](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217130035660.png)

//准备poji类

![image-20231217130104967](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217130104967.png)

![image-20231217130116527](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217130116527.png)

//准备mapper接口

![image-20231217130136536](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217130136536.png)

![image-20231217130153711](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217130153711.png)

//mapper.xml文件

![image-20231217130331202](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217130331202.png)

![image-20231217130340647](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217130340647.png)

//注意  必要使用toString 去输出 不然master 里面会输出pet   , pet里面会输出master，死循环就 爆stackover的错误

**//输出结果可证：master里面的Pets确实封装了pet的所有信息,而且Pet也确实封装了所有master的信息**

![image-20231217130951222](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217130951222.png)









































### 八.缓存-检索的利器

#### 1.介绍

![image-20231217132739382](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217132739382.png)



#### 2.一级缓存

**(1)默认情况下，mybatis自动启用一级缓存/本地缓存/Local Cache,它是sqlsession级别的**

**(2)同一个SqlSession接口对象调用了相同的select语句，会直接从缓存里面获取，而不是再去查询数据库** 

![image-20231217133750393](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217133750393.png)

**(3)一级缓存失效分析**

a.sqlSession会话关闭后，一级缓存会失效

b.执行sqlSession.clearCache()方法后，一级缓存会失效

c.当你对同一个User对象进行修改时，该对象在一级缓存会失效（因为修改对象就会修改数据库，所以缓存里的数据就过时了事务机制会使一级缓存失效）



#### 3.二级缓存

##### **(1)为什么需要二级缓存和两级别缓存的最大区别？**

- **区别**一级缓存的作用域是sqlSession会话级别，在一次会话有效，而二级缓存的作用域是全局范围，针对不同会话都有效.

![image-20231217144529789](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217144529789.png)

- **什么时候开启二级缓存**一级缓存默认是打开的，二级缓存需要配置才可以开启。那么我们必须思考一个问题，在什么情况下才有必要去开启二级缓存？

1、因为所有的增删改都会刷新二级缓存，导致二级缓存失效，所以适合在查询为主的应用中使用，比如历史交易、历史订单的查询。否则缓存就失去了意义。

2、如果多个namespace 中有针对于同一个表的操作，比如Blog 表，如果在一个namespace 中刷新了缓存，另一个namespace 中没有刷新，就会出现读到脏数据的情况。所以，推荐在一个Mapper 里面只操作单表的情况使用。

思考：如果要让多个namespace 共享一个二级缓存，应该怎么做？

跨namespace 的缓存共享的问题，可以使用<cache-ref>来解决：

<cache-ref namespace="com.leon.crud.dao.DepartmentMapper" />
cache-ref 代表引用别的命名空间的Cache 配置，两个命名空间的操作使用的是同一个Cache。在关联的表比较少，或者按照业务可以对表进行分组的时候可以使用。

注意：在这种情况下，多个Mapper 的操作都会引起缓存刷新，缓存的意义已经不大了。


##### **(2)快速入门**

**a**//默认就是true  ,如果你要开启就不需要做如何动作，如果要关闭需要改成false;

![image-20231217144703806](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217144703806.png)

**b**//使用二级缓存时，entity类实现序列化接口（Serializable），因为二级缓存可能使用到序列化技术(cache会持久化在内存或者磁盘，如果是磁盘那就需要序列化)

//不过就算你不实现，在大部分情况下也是没事的；根据实际情况来选择，你也可以等他报错了再去配也行

![image-20231217145145658](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217145145658.png)

**c**//要启用二级缓存其实只需要在你的SQL映射文件加上一行 <cache/>

//这个是一个最简单的配置

这个简单语句的效果如下:

- 映射语句文件中的所有 select 语句的结果将会被缓存。
- 映射语句文件中的所有 insert、update 和 delete 语句会刷新缓存。
- 缓存会使用最近最少使用算法（LRU, Least Recently Used）算法来清除不需要的缓存。
- 缓存不会定时进行刷新（也就是说，没有刷新间隔）。
- 缓存会保存列表或对象（无论查询方法返回哪种）的 1024 个引用。
- 缓存会被视为读/写缓存，这意味着获取到的对象并不是共享的，可以安全地被调用者修改，而不干扰其他调用者或线程所做的潜在修改。

**提示** 缓存只作用于 cache 标签所在的映射文件中的语句。如果你混合使用 Java API 和 XML 映射文件，在共用接口中的语句将不会被默认缓存。你需要使用 @CacheNamespaceRef 注解指定缓存作用域。

//

这些属性可以通过 cache 元素的属性来修改。比如：

```
<cache
  eviction="FIFO"
  flushInterval="60000"
  size="512"
  readOnly="true"/>
```

这个更高级的配置创建了一个 FIFO 缓存，每隔 60 秒刷新，最多可以存储结果对象或列表的 512 个引用，而且返回的对象被认为是只读的，因此对它们进行修改可能会在不同线程中的调用者产生冲突。

可用的清除策略有：

- `LRU` – 最近最少使用：移除最长时间不被使用的对象。
- `FIFO` – 先进先出：按对象进入缓存的顺序来移除它们。
- `SOFT` – 软引用：基于垃圾回收器状态和软引用规则移除对象。
- `WEAK` – 弱引用：更积极地基于垃圾收集器状态和弱引用规则移除对象。

默认的清除策略是 LRU。

**d**//位置

![image-20231217150423607](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217150423607.png)



##### (3)禁用二级缓存的三种方式

1.在mybatis-config.xml的settings中配置成false(这相当于总开关，全局地开启关闭二级缓存)

![image-20231217151103909](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217151103909.png)

2.你在对应的Mapper.xml文件不去配置对应的<cache/>，这样就算总开关是开的，也不会生效

3.更加颗粒化的方式：在指定方法上禁用二级缓存

![image-20231217151428833](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217151428833.png)



#### 4.EHCache

##### (1)基本介绍

- **是一个优质的纯java的第三方缓存框架，具有快速，精干的特点 **
- **虽然MyBtis有自己默认的二级缓存，但在实际项目中我们往往使用更加专业的第三方缓存产品，作为Mymatis的二级缓存**

##### (2)EHCache配置与使用

1.引入poml依赖 







# SpringBoot



## 一.机制

### （1）版本仲裁

在引入的父项目中，所有需要的东西都给你配置完了，版本是默认的，如果你需要更改就自己去dependencies指定，遵循就近原则就会使用你指定的版本,或者在properties里面设置这样的标签 <mysql-version>5.1.49</mysql-version>

### （2）场景启动器

**就是梦寐以求的一键配置Jar包！！！！**

比如：![image-20231224110641850](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224110641850.png)

比如我们做web开发，该starter就会导入与web相关的所有jar包

//以下是依赖树

![image-20231224111158115](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224111158115.png)

所有场景启动器最基本的依赖就是spring-boot-starter，这个依赖也就是springbot自动配置的核心依赖



有的时候可能需要使用第三方场景启动器,  xxx-spring-boot-starter(xx是第三方启动程序的项目名)，是第三方为我们提供的简化开发的场景启动器

//通过名称要一眼看出是第三方还是官方的



### **（3）自动配置**

**a.spring自动配置了什么**

- tomcat
- springmvc
- web常用功能：如字符过滤器
- 默认扫描包:默认扫描主程序及下面的包(怪不得)



**b.如何修改默认配置**
//一句话 搞定 ：  所有默认配置 都可以在  yaml 文件中修改

- 修改默认扫描包结构
  注解方法(建议使用文件修改)：在主程序的@SpringBootApplication中指定属性 可以是一个包(一个包可以省略{}) 也可以是多个包

```
@SpringBootApplication(scanBasePackages = {"com.zlc","xxx.xxx"})
```

- 修改默认配置（配置大全！！！）
  //所有的默认配置都可以在这里配置	
  //必须 在resoures下面写一个名字必须为application.properties/yaml文件，用来管理默认属性

```
# 希望修改监听端口
server.port=8080
#修改上传文件的大小
#解读：
#multipart.max-file-size 属性可以指定springboot上传文件的大小
#默认配置最终都是映射到某个类上,比如multipart.max-file-size会映射到MultipartProperties类
#ctrl+b即可找到它，这样的类，我们叫做是属性类
spring.servlet.multipart.max-file-size=10MB
```

- 常用的配置
- 自定义配置
  还可以在properties文件中自定义配置属性
  //比如:![image-20231224122645305](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224122645305.png)

![image-20231224122659581](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224122659581.png)



**c.按需加载**













## 二.基础常用内容



### （1）容器

##### 1.传统Spring注解和xml配置文件依然有效

//@Component @Service @Repository @ Controller  依然使用!

//传统spring 注入一个Bean ，就是在bean.xml里面<bean class= id=>,然后ioc.getBean(.class),从下面可见依然有用

![image-20231224130818176](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224130818176.png)





##### 2.@Configuration + @Bean

//springBoot 提供了新的方式来  注入bean   (感觉springboot的更好用一点)

解释：1.@Configuration  标识这是一个配置类，等价于配置文件

​			//有一个小细节，被@Configuration标识后，这个配置类本身也会注入到容器

​			2.程序员可以通过@Bean  注解注入Bean对象到容器

​			@Bean:  添加主件到容器，

​			monster01()  默认你的方法名就是Bean的名字/id

​			Monster：注入类型

​			new Monster(xxx) 注入到容器的信息

​			@Bean(name = "")  / Bean(value = "")    指定名字id 为多少

​			@Scope("prototype")  多例   ，默认为单例

![image-20231224134852570](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224134852570.png)

```
@Configuration    
public class BeanConfig {


    @Bean
//    @Scope("prototype")   这个注解就是多例
    public Monster monster01(){
        return new Monster("李寒山","岁梦长枪",28);
    }
}
```



















**proxyBeanMethods:代理Bean的方法**

1. Full模式（@Configuration(proxyBeanMethods=true)【保证每个@Bean方法被调用都返回单例，代理模式】/默认是true

2. Lite模式（@Configuration(proxyBeanMethods=false) 【保证每个@bean方法被调用都返回多例， 非代理模式】

3. 特别说明：proxyBeanMethods是在 调用@Bean方法后生效，因此需要先获取BeanConfig组件，再调用,而不是直接要通过springboot主程序来获取Bean
   比如：Lite模式  就必须要用组件获取才行，如果还是springboot主程序获取那就相当于话是Full模式了

4. ```
   Monster monster01 = beanconfig.monster01();
   Monster monster02 = beanconfig.monster01();
   System.out.println(monster01 + ",hashcode:" + monster01.hashCode());  hashcode 不同,lite模式成功
   System.out.println(monster02 + ",hashcode:" + monster02.hashCode());
   
   ```

```
Monster monster01 = beanconfig.monster01();
Monster monster02 = beanconfig.monster01();
System.out.println(monster01 + ",hashcode:" + monster01.hashCode());  hashcode  same，lite模式失败
System.out.println(monster02 + ",hashcode:" + monster02.hashCode());
```

5. 模式的选用：组件依赖必须使用Full模式（默认），如果不需要组件依赖就可以使用Lite模式
   lite模式 也被称为轻量级模式，因为不检擦依赖关系，运行速度快.
   当你不知道用什么模式的时候就使用默认的就ok,需要用到多例就用@Scope("propotype")就可以



**配置类可以有多个，就和Spring xml配置文件可以有多个是一个道理**





##### 3.@Import 

//作用也是将类 注入容器

//区别： **@Import 注解主要用于导入其他模块或第三方库的类或配置类，而 @EnableConfigurationProperties 注解主要用来声明配置类**。

//  名字/id  默认是类的全类名



![image-20231224143016636](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224143016636.png)



![image-20231224143024496](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224143024496.png)



##### 4.@Conditional

//约束注解:就是用来添加约束的，这里只是举了一个ConditionalOnBean的例子还有onClass 之类的

//如果是在方法上面就是对方法进行约束，放在类上面就是对整个类进行约束 

```
@Bean
//只有当 容器中有 一个id = monster01的Monster对象 才会创建 monster02
@ConditionalOnBean(name = "monster01")
public Monster monster02(){
    return new Monster("盗版李寒山","山寨岁梦长枪",28);
}
```



#####  5.@ImportResource

//正常情况是springBoot主程序的ioc是拿不到beans.xml文件中的信息，但是通过这个注解就可以拿到了

//  "classpath:xxx"    

//可以导入多个xml文件@ImportResource("classpath:xxx"  ,  "classpath:xxx"    )

![image-20231224145948907](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224145948907.png)



##### 6.配置绑定

**@ConfigurationProperties :用于获取配置文件中的属性定义并绑定到Java Bean或属性中**

//如何将 applicaton中的k-v数据 导入到furn01呢，然后配给HelloController中的private Furn furn属性呢？？

1.首先在entity中的该类 使用@Conponent/@Configuration标识为注解,然后使用@ConfigurationProperties(prefix = "xxx"),xxx为容器中的对象id/名字

![image-20231224160311717](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224160311717.png)



2.在  application文件中 写好属性,如果是中文需要使用unicode编码形式（随便去网上整个转换器就Ok了）

![image-20231224160514441](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224160514441.png)

3.关于这个小案例我当时由于对@Resource和@ConfigurationProperties的prefix不是很通透，所以犯错(以为prefix中的furn01早就创建了)



![image-20231224161151453](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231224161151453.png)





//实际应用:

在sky-take-out项目中，我们提前注入这么个东西，就可以直接在后面使用

![image-20240228125052863](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228125052863.png)

![image-20240228125156137](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228125156137.png)







### （2）lombok

**作用：项目中有很多没有技术含量又必须存在的代码，比如get set方法，I/O流的关闭等等,Lombok应运而生**



- @Data 等价于 @Getter @Setter @ToString @RequiredConstructor @EqualsAndHashCode
- @ToString     
- @NoArgsConstructor:虽然默认情况下会生成无参构造器，但是会被全参构造器覆盖(比如只用了@Data注解，就会把无参构造器覆盖)，所以有时候需要这个注解

在idea 安装lombok插件就可以使用一些扩展注解，比如日志的输出

- @Slk4j  





### （4）YAML

**YAML是一个以数据做为中心的标记语言，类似于XML，JSON。和传统的标记语言不同，YAML是注重于数据，非常适合用来做以数据为中心的配置文件，比如我们的Springboot 中的 application.yml**



##### a.基本语法

**语法注意事项**

- 大小写敏感
- 使用缩进表示层级关系
- 缩进时不允许使用Tab键，只允许使用空格。
- 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可
- \#表示注释，从这个字符一直到行尾，都会被解析器忽略。
- 字符串无需加引号

**语法**

对象:   不仅仅是object,map,set等集合也可以,比如第二个例子中wife就是一个map集合的形式

- 行内写法：  address:{province:山东，city:枣庄} /     monster{name:牛魔王,wife:{name:铁扇公主,skill:xxx}}
- 换行写法:   
  address:
      province:山东
      city:枣庄

数组:不仅仅是 数组还有array list queue

- 行内写法: hobbyList[游泳，跑步]
- 换行写法:
  hobbyList:
     - 游泳
     - 跑步

纯量:

- 字符串 默认不用加引号，包含空格或特殊字符必须加引号，单引号或双引号都可以

```yml
userId: S123
username: "lisi"
password: '123456'
province: 山东
city: "济南 : ss"
```

- 布尔值

```yml
success: true
```

- 整数

```yml
age: 13
```

- 浮点数

```yml
weight: 75.5
```

- Null

```yml
gender: ~
```

- 时间
  时间使用ISO8601标准 [ISO8601](https://baike.baidu.com/item/ISO 8601/3910715?fr=aladdin)

```yml
createDate: 2001-12-14T21:59:43.10+05     
```



##### b.具体实例

```
person:
  name: 赵联城
  isMarried: true
  birth: 2003/12/26
  bestcar: {name: 宝马,price: 100}
#  skills: [1,2,吃人,外地户籍]
  skills:
    - 封魔拳
    - 安雨樱流沙
```





##### c.注意事项

- @ConfigurationProperties的prefix就是这个，也就是属性前缀

![image-20231225123045287](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231225123045287.png)

- 注意.properties的优先级大于.yaml

- 解决yaml文件中没有提示信息的问题：引入依赖

- ```
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-configuration-processor</artifactId>
      <optional>true</optional>
      //这个ture是防止本次依赖扩散到其他子项目中
  </dependency>
  ```

### （5）静态资源直接访问

一般现在都是前后端分离方式，SpringBoot主要提供接口服务，但有时候有一些小项目就希望一个jar前后端都搞定，因此一些页面等静态资源都放入SpringBoot中。 这里记录一下静态资源访问方式和引入shiro后的修改。

**SpringBoot 默认配置就可以直接URL访问类路径下的静态资源**

1. **classpath:/META-INF/resources/**
2. **classpath:/resources/**
3. **classpath:/static/**
4. **classpath:/public/**



**常见的静态资源：html,js,css,图片，字体文件**



**访问方式:默认：项目根路径/静态资源名,比如https://localhost:8080/hi.jsp**



**注意事项与细节**

- 直接把静态资源放在resources下面 是无法访问的
- localhost:8080/1.jpg  ,  访问顺序是 先看Controller能不能处理，没有这样的controller就给静态资源处理器，如果静态资源处理器找不到就响应404页面
- 放在templates下面的html也是无法直接访问的，可以通过 controller层来访问
- 如果出现了上面的冲突，我们就需要改变静态资源的访问前缀来解决冲突

![image-20231225134833936](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231225134833936.png)

- 注意  yaml文件缩进会影响层级关系，所以我们最好顶格去写，这样代码提示才会更全.
- spring.mvc.static-path-pattern：根据官网的描述和实际效果，可以理解为静态文件URL匹配头，也就是静态文件的URL地址开头。Springboot默认为：/**。
  spring.web.resources.static-locations：根据官网的描述和实际效果，可以理解为实际静态文件地址，也就是静态文件URL后，匹配的实际静态文件。Springboot默认为：classpath:/META-INF/resources/,classpath:/resources/,classpath:/static/,classpath:/public/
- 如果修改了就会破坏默认的url,最好加上默认的

![image-20231225142037936](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231225142037936.png)





### （5）Rest风格

**在Springboot中的rest风格的使用**

![image-20231225143208510](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231225143208510.png)



**注意事项和细节**

-  如果是用表单提交的话，表单提交只支持get 和 post ， 如果是delete 和 put 就不行
  解决方法：使用filter开启 + 隐藏域传递 _method 参数定值
  ![image-20231225145907030](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231225145907030.png)

```
<form action="/monster" method="post">
    <input type="text" name="name"><br>
    <input type="hidden" name="_method" value="delete">！！！！！！！！！！！！！！！！！！
    <input type="submit" value="点击提交">
</form>
```



深入理解：比如：return "hello";  顺序1 先看有没有可以匹配的Controller 顺序2 如果没有找到视图解析器，就在类路径下面找有没有名字为  "hello.jsp/html"  的资源

**如果你配置了视图解析器，那么就只会找有没有 这个视图资源**

//**此时如果你想要从一个controller去另外一个controller ， 需要使用return "forward:/xxx" or return "redirect:/xxx"**

**那如何配置视图解析器呢？**

![image-20231225152238898](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231225152238898.png)

**此外，还有别的方式也会启动视图解析器，比如引入 thymeleaf-start的依赖,也会开启视图解析器**







### （6）接收参数相关注解

##### 1.@PathVariable

@GetMapping("/monster/{id}/{name}")

public String test(**@PathVariable("id")Integer id,@PathVariable("name") String name**){

xxxxxxx

}

还记得吗？  {id}{name}是占位符,用@PathVariable可以接收在url上的数据

其实还有一种方法当时没讲：  @PathVariable Map<String,Object> map  **可以直接一口获取所有数据,有的时候比如需要遍历数据的时候会用到**

public String test(**@PathVariable Map<String,Object> map**){

xxxxxxx

}



##### **2.@**RequestParam

接受 从表单 或者 href = "/monster?name=king&id=10"等  这种参数数据

也可以使用map  取一口气梭哈，有个小细节就是 href = "/monster?name=king&name=zlc，这样用map只能获取一个前一个会被顶替



##### 3.@RequestHeander(暂时没有遇见过)

用来获取请求头的信息,和@PathVariable差不多也可以用map一口气梭哈

@ReuqestMapping(xxx)

public String test(@RequestHeader("Host")){

xxxxxxx;   				//**表示只获取一个Host,用到什么就取什么 ，也可以一口气梭哈**

}





##### 4.@RequestBody



//获取从前端发出的数据，以Json形式



##### 5.@CookieValue



//用来获取Cookie

String 是cookie 中单个数据，Cookie 就是 整个 Cookie的信息

@CoolieValue(value = "xxx") String  cookie/ Cookie cookie



**//也可以直接用原生的HttpServletRequest request的request.getCookies()去接收**





##### 6.@RequestAttribute

//获取request域中的数据

//也可以使用原生的HttpServletRequest 去获取



##### 7.@SessionAttribute

//懒得说了，easy



##### 8.复杂参数

比如Map , Model ,   Errors/BindingResult,RedirectAttributes,ServletResponse,SessionStatus,等等

这里重点介绍Map ,Modle ,RedirectAttribute.



@GetRequestMapping("/register")

public String test(Map<String,String> map,Model model){

map.put("xx","xx");

map.put("xx","xx);

modle.addAttribute("xx","xx");

**//上述数据都会放入到request域中，这样就可以在别的方法里面取出使用**

return "forward:/registerOk";

}

-

##### 9.自定义对象参数

//底层可以自动完成   自动封装 - - 级联封装

//后面会讲 一点相关的 底层-- 转换器







### （7）转换器

**介绍：比如转换器会将网页上填写 name birth age  skill中的birth会将 string -> Date ,age 会将 string -> Integer**

**以我们的2.5.3的springboot 内置了 100多个转换器，同时也允许我们使用自定义转换器**



**自定义转换器:**

 用到的时候再去学吧



### （8）JSON



@ResponseBody  返回xml/json数据

类上面就用 @RestController

**//如果使用了 @ResponseBody或者 @RestController ， 就不会走 视图解析器那一套，会直接返回内容协商的指定格式**





**误区！！！！： 我一直以为这个注解让服务器返回给客户端的数据改为json形式，其实不对，实际上是按照内容协商来指定格式的!!!!!!!!!!!!!!!**



//**那么底层是如何返回json格式的数据呢 ?**

自己去追一下源码  或者  看以下 之前的视频解析



### (9)内容协商

**介绍：客户端和服务器端就响应的资源内容进行协商交涉，然后提供给客户端最为合适的资源。内容协商是以响应资源的语言、字符集、编码方式等作为判断的基准。**



//比如:正常情况下  下面的案例  服务器会返回给客户端一个 json数据



@PostMapping("/test")

@ResponseBody

public Monster monster11(){

return new Monster(xxxx);

}



**知识回顾 :  请求头**

- Accept：告诉服务端，客户端这边需要的MIME类型(一般是多个，比如text/plain，application/json等，*/*表示可以是任何MIME类型的资源);
- Accept-Language：告诉服务端，客户端这边需要的语言;
- Accept-Charset：告诉服务端，客户端这边需要的字符集;
- Accept-Encoding：告诉服务端，客户端需要的压缩方式(gzip,deflate,br)。

//大致上就是  底层会 获取 请求头的 Accept   ，然后  通过一些类和方法 判断需要使用哪种Jsongenerator(该接口可以返回json,xml等格式)来返回数据。

比如此处的案例，就是会返回Json  , 

因为此处请求头的Accept 为text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/ *;q=0.8

-  q = 0.9是权重
- application/xml 是格式
- */ * 表示 其他所有的格式（这里面又以json优先）

意思是  text/html,application/xhtml+xml,application/xml;q=0.9 中的**q=0.9**是权重，权重大的优先使用这个格式,但是为什么json的去在权重=0.8 < xml的0.9,可是我们平时都是返回的json呢？

因为：处理xml格式的数据需要依赖的支撑！！！，你有默认又处理Json却没有处理xml需要的依赖所以自然就优先使用json了，所以当你启用了处理xml的依赖那就默认返回的是xml的格式,因为他权重高

```
<!--        处理xml格式的依赖-->
        <dependency>
            <groupId>com.fasterxml.jackson.dataformat</groupId>
            <artifactId>jackson-dataformat-xml</artifactId>
        </dependency>
```

引入这个之后，那就默认按照权重优先返回xml格式的数据

![image-20231226140111497](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231226140111497.png)

**实际上，你也可以自定义accept= xx ，需要开启请求参数的内容协商功能，?format=xx**



### （10）Thymeleaf

**介绍：是一种服务器渲染技术(数据渲染还是在服务器端进行的)的模板引擎，通常和SprnigBoot一块使用**

**使用了thymeleaf,不是前后端分离**

Thymeleaf是一款用于渲染XML/XHTML/HTML5内容的模板引擎。类似JSP，Velocity，FreeMaker等， 它也可以轻易的与Spring MVC等Web框架进行集成作为Web应用的模板引擎。与其它模板引擎相比， Thymeleaf**最大的特点**是能够直接在浏览器中打开并正确显示模板页面，而不需要启动整个Web应用。

##### a.表达式

| ${…} | Variable Expressions           | 变量表达式     | 取出上下文变量的值     |
| ---- | ------------------------------ | -------------- | ---------------------- |
| *{…} | Selection Variable Expressions | 选择变量表达式 | 取出选择的对象的属性值 |
| #{…} | Message Expressions            | 消息表达式     | 使文字消息国际化，I18N |
| @{…} | Link URL Expressions           | 链接表达式     | 用于表示各种超链接地址 |
| ~{…} | Fragment Expressions           | 片段表达式     | 引用一段公共的代码片段 |



//自己去看文档 







##### b.在Springboot中的应用

- **需要引用themeleadf-starter**

```
<!--        引入thymeleaf - start-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
                <!--        yaml文件提示功能-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>
```

**//注意:!!!!!!引用了thymeleaf-start的依赖会自动开启视图解析器,而且这个视图解析器默认属性是这样的：**

默认前缀：DEFAULT_PREFIX = "classpath:/templates/"

默认后缀：DEFAULT_SUFFIX = ".html"

所以我们需要 在 类路径下面创建一个templates 将 html资源存放到这里,在这之外的html资源是无法访问到的



**//引入这个依赖后，为什么要在类路径下面搞一个/templates的包？**

上面的注意已经回答了这个问题



自己去看文档吧，懒得记了

**//注意使用thmeleaf之后，不能直接访问静态资源,必须使用controller才能跳转至静态页面，因为底层css的渲染需要用controller跳转才行**

**好像默认的${}是从request域中取数据**





### （11）拦截器



#### 1.基本逻辑介绍

**//拦截器的三个方法**

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //1.该方法在目标方法执行前被执行
        //2.如果这个方法返回false，那么不再执行目标方法，相当于拦截了目标方法
        //3.该方法可以获取到request,response,handler（目标处理器）
        //4.这里根据业务逻辑可以进行拦截，并指定跳转到哪个页面
        System.out.println("prehandle");
        return true;
    }
    
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        //1.执行完目标方法，该方法被执行
        //2.这个方法可以获取request,response,handler,modelAndView
        //3.可以二次处理你的业务逻辑
        System.out.println("posthandle");
    }
    
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        //1.在视图渲染后被执行，这里可以进行资源清理工作
        //2.可以获取到request,response,handler,ex(异常)
        System.out.println("afterCompletion");
    }

![image-20231228181623222](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231228181623222.png)

 自定义拦截器执行流程说明
\1. 如果 preHandle 方法 返回 false, 则不再执行目标方法, 可以在此指定返回页面
\2. postHandle 在 目 标 方 法 被 执 行 后 执 行 . 可 以 在 方 法 中 访 问 到 目 标 方 法 返 回 的
ModelAndView 对象
\3. 若 preHandle 返回 true, 则 afterCompletion 方法 在渲染视图之后被执行.

\4. 若 preHandle 返回 false, 则 afterCompletion 方法不会被调用
\5. 在配置拦截器时，可以指定该拦截器对哪些请求生效，哪些请求不生效



![image-20231228182021202](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231228182021202.png)



#### 2.注册拦截器





**//通过@Bean的方式**

![image-20231231160143165](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231231160143165.png)

**//通过实现 WebMvcConfigurer**

 

```java
public class WebMvcConfiguration implements WebMvcConfigurer {
    /*
    * 注册自定义拦截器
    * */
    @Autowired
    private StringRedisTemplate stringRedisTemplate;


    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        log.info("开始注册自定义拦截器...");
        //token刷新的拦截器
        registry.addInterceptor(new RefreshTokenInterceptor(stringRedisTemplate))
                .addPathPatterns("/**");
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
                );
    }
}
```



#### 3.优先级



每个拦截器默认优先级为0，如果没有设置优先级，那么就按照注册顺序依次执行；如果设置优先级则按照优先级执行.

        registry.addInterceptor(new RefreshTokenInterceptor(stringRedisTemplate))
                .addPathPatterns("/**")
                .order(0);
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
                .order(1);







### (12)文件上传



#### 1.本地文件上传

​		**a.前端三要素 ： method = post , enctype=multipart/form-data,  type=file**

![image-20240103194351052](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240103194351052.png)

**b.后端服务器:**

**使用  MultipartFile filename接收  注意 filename必须和前端name保持一致**

核心方法  就是  filename.transferTo();

还有  什么的getOriginalFilename(),   getSize之类的方法

**c.yaml配置文件:**

```
#配置单个文件上传大小限制
  servlet:
    multipart:
      max-file-size: 10MB
#配置单个请求最大大小的限制
      max-request-size: 100MB
```



#### 2.阿里云OSS

//OSS     (Object Storage Service)

//使用阿里云OSS 可以通过网络随时存储和调用包括文本，图片，音频等在内的各种文件。

//需要的知识：sdk: Software Development Kit的缩写，软件开发工具包，包括辅助软件开发的依赖(jar包)、示例代码等等，都叫SDK.

​							bucket: 存储空间是用户用于存储对象(Object，就是文件)的容器，所有的对象都必须隶属于某个存储空间.







**a.前言:由于本地存储存在 磁盘满了，上传下载不方便，容易被攻击 等等问题，实际开发基本不会使用本地存储,经常使用第三方存储 **





在Maven工程中使用OSS Java SDK，只需在pom.xml中加入相应依赖即可。在<dependencies>中加入如下内容：

**说明**

优先使用最新版本的依赖项，此处以3.15.1版本为例。

 

**需要的依赖：**

```plaintext
<dependency>
    <groupId>com.aliyun.oss</groupId>
    <artifactId>aliyun-sdk-oss</artifactId>
    <version>3.15.1</version>
</dependency>
```

如果使用的是Java 9及以上的版本，则需要添加JAXB相关依赖。添加JAXB相关依赖示例代码如下：

```plaintext
<dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
    <version>2.3.1</version>
</dependency>
<dependency>
    <groupId>javax.activation</groupId>
    <artifactId>activation</artifactId>
    <version>1.1.1</version>
</dependency>
<!-- no more than 2.3.3-->
<dependency>
    <groupId>org.glassfish.jaxb</groupId>
    <artifactId>jaxb-runtime</artifactId>
    <version>2.3.3</version>
</dependency>
```

//有关于阿里云那边的操作就懒得说了，直接看在Java中如何操作的

**这个是用官方文档中的Demo来讲解**

```
public class Demo {

    public static void main(String[] args) throws Exception {
        // Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "myfirstbucket123";
        // 填写Object完整路径，例如exampledir/exampleobject.txt。Object完整路径中不能包含Bucket名称。
        String objectName = "firstdir/test1.txt";
        //  填写本地文件地址
        String filePath = "E:\\MyVideo\\test.jpg";

        // 创建OSSClient实例。
        OSS ossClient = new OSSClientBuilder().build(endpoint, credentialsProvider);

        try {
            FileInputStream inputStream = new FileInputStream(filePath);
            //创建PutObject请求
            ossClient.putObject(bucketName,objectName,inputStream);
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message:" + oe.getErrorMessage());
            System.out.println("Error Code:" + oe.getErrorCode());
            System.out.println("Request ID:" + oe.getRequestId());
            System.out.println("Host ID:" + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message:" + ce.getMessage());
        } finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
        }
    }
}
```

**//这个用自己写的Util直接来讲解**

```
@Component
public class AliOSSUtils {
    private String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
    private EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
    private String bucketName = "myfirstbucket123";

    public AliOSSUtils() throws ClientException {
    }

    /*
    * 实现上传图片到OSS
    * */
    public String upload(MultipartFile file) throws IOException {
        //获取上传文件的输入流
        InputStream inputStream = file.getInputStream();

        // 避免文件覆盖
        String originalFilename = file.getOriginalFilename();
        String fileName = "firstdir/"+UUID.randomUUID() + originalFilename.substring(originalFilename.lastIndexOf("."));

        //上传文件到 OSS
        OSS ossClient = new OSSClientBuilder().build(endpoint,credentialsProvider);
        ossClient.putObject(bucketName, fileName,inputStream);

        //文件访问路径
        String url = endpoint.split("//")[0]+"//" + bucketName+"."+endpoint.split("//")[1]+"/"+fileName;

        //关闭ossClient
       if(ossClient != null){
           ossClient.shutdown();
       }

        return url;
    }
}
```

























### (13)异常处理



##### 0.SpringBoot异常处理机制：

- 默认情况，SpringBoot提供/error处理所有错误的映射，也就是说一旦程序中出现了异常, SpringBoot 会向/error 的 url 发送请求。在 SpringBoot 中提供了一个名为 **BasicErrorController** 来处理/error 请求，然后跳转到默认显示异常的页面来展示异常信息。SpringBoot底层会自动请求转发到/error 这个映射
- 具体的debug追源码： 大概过程就是去遍历  staticLocation(也就是类路径下面的staitc,public,resources,META-INF/resources)寻找有没有 /error/404.html,没有的话就再去遍历寻找 这四个路径下面有没有 /error/4xx.html,如果还是没有就返回 默认的那个404错误
  
- 比如   使用浏览器访问不存在的接口

 



##### 1.自定义异常页面

**//存放到   templates/error(这是在启动thymeleaf的存放位置)**

![image-20240104182613460](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240104182613460.png)

**//可以取出timestamp,error,status,path一些错误信息,这个报错好像不用管**

![image-20240104183133187](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240104183133187.png)

![image-20240104183147235](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240104183147235.png)





##### 2.局部异常

//使用@ExceptionHandler 注解

**//使用：value   ->  捕获异常类型**

    @RequestMapping("/byZero")
        public String byZero(){
            int i=10/0;
            return "ok";
        }
    @ExceptionHandler(value = {java.lang.NullPointerException.class,java.lang.ArithmeticException.class})
    public ModelAndView handlerNullException(Exception e){
        ModelAndView view = new ModelAndView();
        view.setViewName("smallError");//在 templates/error/下面有一个smallError的回显页面
        view.addObject("smallError",e.toString());
        return view;
    
    }





##### 3.全局异常

//使用@ExceptionHandler 加@ControllerAdvice 注解

**//自定义异常是用状态码来选择显示错误页面**

**//全局，局部异常是通过Java的异常类 来 选择显示错误页面**

**//全局异常的 优先级 >   默认优先级(先找404，再找4xx)**  

**//全局异常类  里面就包含  许多处理局部异常的方法 **

![image-20240104190045229](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240104190045229.png)



 

##### 4.自定义处理

//用到再学















### (14)注入Servlet,Filter,Listener

##### 1.基本介绍

**考虑到业务的复杂性，SpringBoot支持将Servlet,Listener,Filter注入到Spring容器中，成为Spring bean**
			**也就是说，SpringBoot放开了和原生WEB组件（Servlet,Filter,Listener）的兼容**



##### 2.例子1-使用注解注入

- servlet
- 步骤1.配置原生servlet，继承httpServlet，使用注解@WebServlet完成映射,完成业务逻辑
- 步骤2.在Springboot启动对象中加入注解@ServletComponentScan（basePackages = "xxxx"）;javaweb三大组件都可以自动注册了!!!

![image-20240104195114286](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240104195114286.png)

![ ](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240104195124682.png)

- **Filter**
- 步骤和上面的Servlet差不多
- ![image-20240104203049908](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240104203049908.png)



- **Listener**

**//和上面的一摸一样 ，懒得写了**

**//Listener干什么用的，我都给忘了**





##### 3.例子2-使用RegjistrationBean方式注入

//此处以之前的拦截器为例子,好像还可以使用注解实现?



1.实现拦截器 - ------实现HandlerInterceptor接口/继承一个抽象类

![image-20240105182158576](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240105182158576.png)

2.创建一个配置类，继承WebMvcConfigurer，并重写addInterceptors()方法来注册拦截器

![image-20240105182150132](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240105182150132.png)



//使用注册类 去注册servlet,listener,filter，统一使用注册类servletRegistrationBean

​			Servlet/Listener/Filter   xxx = new XXXX;

​			return ServletRegistrationBean(xx);

//除了拦截器之类 必须使用 注册类注册，建议还是使用接口去注册.



##### 4.注意事项和细节

- **SpringBootApplication 上使用@ServletComponentScan 注解后
  Servlet可以直接通过@WebServlet注解自动注册
  Filter可以直接通过**@WebFilter**注解自动注册**
  **Listener可以直接通过@WebListener 注解自动注册**
- 疑惑：为什么url请求   servlet  不会执行拦截器？
            这是因为  tomcat的精确匹配的问题，tomcat会优先匹配名字一致的servlet，最后如果没有匹配的好像是去匹配"/"，   
            在springboot中，"/"对应的servlet就是前端处理器/中央处理器  





- **5.一个重要的知识点**

- 2.过滤器与拦截器的区别

  **//概念上的区别**

  - 过滤器实现的是java.servlet.Filter 接口，而这个接口是在Servlet规范中定义的，也就说过滤器filter的使用要依赖tomcat等容器，
    ,Filter只能在web程序中使用. 

  - 拦截器是SpringBoot的一个组件，由Springboot容器管理，并不依赖tomcat之类的容器，是可以单独使用的，不仅能使用在web程序，也可以使用在application等程序中.

  

  **//触发时机的区别**

  - filter是在请求进入容器后，但进入servlet之前进行预处理，**请求结束是在servlet处理完之后**.
  - interceptor是在请求进入servlet后，在进入Controller之前进行预处理**,Controller中渲染了对应的视图之后请求结束.**
  - 过滤器不会处理请求转发，拦截器会处理请求转发 （好像是内部的请求转发）

  ![image-20240103203259754](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240103203259754.png)

   



#### (20)内置webServer

**1.Springboot支持的webServlet：tomcat，jetty，Undertow**

//默认是使用内置的tomcat





**2.tomcat的配置**



**//可以通过yaml文件去配置   ，  也可以使用类来配置(不建议，知道就可以)**

![image-20240105203247469](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240105203247469.png)





**3.放弃tomcat，切换undertow**



**//1.首先要排除内置的tomcat**

![image-20240105203749683](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240105203749683.png)





**2.引入你要用的WebServer**

![image-20240105203945014](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240105203945014.png)







#### 	(21) 数据库操作



##### 1.springboot默认数据库操作

**//默认是JDBC + HikariDataSource()**



**(1)首先要引入数据库开发需要的依赖**

```
<!--        引入数据库开发需要的依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jdbc</artifactId>
        </dependency>
```

**//为什么引入这个就可以进行数据库开发呢？那肯定是因为引入了Jdbc和Hikari连接池相关的依赖喽**



**(2)指定使用的数据库和版本**

//springboot不知道你使用的是什么数据库和版本，所以需要你去指定使用的数据库和版本

```
<!--        引入mysql的驱动-->
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>8.0.33</version>
        </dependency>
```



**(3)配置数据库信息**

![image-20240105211209240](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240105211209240.png)

























##### 2.

































































# JSON +  Ajax + ThreadLocal

### 一 Json

#### 1 . 基础变量

var 变量名 = {

​		"k1"value,  //number类型

​		"k2":"你好",    //字符串类型

​		"k3":{}//json类型                          such as        "k3":{"age":12,"name":"jack"}

​		"k4":[{},{}]//json数组 		 such as        "k3":[{"age":12,"name":"jack"},{"age":13,"name":"jddddack"}]

​	};

#### 2.JSON转字符串，字符串转JSON

JSON.stringify(JSON对象)  ： 

​			var person = JSON.stringofy("username":username,"age":age);

JSON.parse(字符串):

```
window.onload = function (){
    var person = {
        "name":"jack",
        "age":100
    };
    var s = JSON.stringify(person);
    var parse = JSON.parse(s);
    console.log(parse);
}
```

细节：   (1)这两种方法都不会影响之前的数据

​			（2）推荐字符串都使用 ""  

​			（3）字符串转JSON , var str = "{\\"name\\":\\"jack\\", \\"age\\":100}"  注意在""内部的""要加上转义字符\不然就转换失败

#### 3.JSON在Java中的使用（在以后的开发中会经常使用到）

##### （1）环境搭配：在JAVA中使用需要先去引入一个依赖

```
<dependency>
  <groupId>com.google.code.gson</groupId>
  <artifactId>gson</artifactId>
  <version>2.2.4</version>
</dependency>
```

##### （2）GSON

Gson是Google提供的一个Java 类库，旨在将Java对象转换为JSON字符串，以及将JSON字符串转换为Java对象。它提供了简单易用的API，可以轻松地进行序列化和反序列化操作。

（3）演示

a. 从javaBean到json版字符串

```
Gson gson = new Gson();
Book book = new Book("百年孤独", 100.0, "jack");
String strBook = gson.toJson(book);
System.out.println(strBook);
```

b.从json字符串到JavaBean

```
Gson gson = new Gson();
Book book = new Book("百年孤独", 100.0, "jack");
String strBook = gson.toJson(book);
Object o = gson.fromJson(strBook,Book.class);
System.out.println(o);
```

c.从List到json字符串(有一点复杂)

```
Gson gson = new Gson();
Book book1 = new Book("百年孤独", 100.0, "jack");
Book book2 = new Book("百年孤独2", 200.0, "tom");
List<Book> bookList = new ArrayList<>();
bookList.add(book1);
bookList.add(book2);
//解读：1.返回类型的完整路径java.util.List<com.plus.Book>
//     2.gson的设计者，需要得到完整的路径来进行底层反射
//     3.所以gson设计者就提供TypeToken，来搞定.简单来说，这个TypeToken<>(){}.getType()就是用来获取list,map的类全路径
//     4. new TypeToken<List<Book>>(){}.getType();    详解{}
//      (1)如果我们直接new TypeToken<List<Book>>().getType()实际上是调用的无参构造器
//      (2)但是TypeToken的无参构造器是 protected,不同包不能访问,所以我们直接这样用是会报错的
//      (3)当我们加入{}，此时类型不再是TypeToken 而是匿名内部类class:com.google.gson.internal.$Gson$Types$ParameterizedTypeImpl
//      (4)你可以简单理解为此时的类型是TypeToken的一个子类，当子类使用自己的无参构造器时，就会默认super();也就是默认调用父类的无参构造器.
//      全是Java基础
Type type = new TypeToken<List<Book>>(){}.getType();
System.out.println(type.getClass());
String s = gson.toJson(bookList, type);
System.out.println(s);
```

d.从map到json字符串

```
HashMap<Integer, Book> bookMap = new HashMap<>();
bookMap.put(1,book1);
bookMap.put(2,book2);
String s = gson.toJson(bookMap);
System.out.println(s);
```

e.从json字符串转成Map，list

```
Gson gson = new Gson();
Book book1 = new Book("百年孤独", 100.0, "jack");
Book book2 = new Book("百年孤独2", 200.0, "tom");
HashMap<Integer, Book> bookMap = new HashMap<>();
bookMap.put(1,book1);
bookMap.put(2,book2);
String s = gson.toJson(bookMap);
Map<Integer,Book> o = gson.fromJson(s, new TypeToken<Map<Integer, Book>>() {
}.getType());
System.out.println(o);
```

list同理

### 二.Ajax

#### 1.Ajax是什么？

Ajax即是”Asynchronous Javascript And XML“(异步javaScript 和xml)

Ajax是一种浏览器异步发起请求，局部更新页面的技术

#### 2.Ajax的应用场景

- 搜索引擎根据用户输入关键字，自动提示检索关键字
- 动态加载数据，按需取得数据【树形菜单，联动菜单】
- 改善用户体验[【输入内容前提示，带进度条文件上传】
- 电子商务应用【购物车，邮件订阅...】
- 访问第三服务。【访问搜索服务，rss阅读器】
- 页面局部刷新

#### 3.两个重要的流程图

(1).传统的web应用获取数据

![image-20231122162528623](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231122162528623.png)



(2).Ajax获取数据

![image-20231122164106611](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231122164106611.png)

#### 4.XMLHttpReuqest

##### 1.快速入门

//需求：就是写一个页面，提交后判断username是否和"king"重名,如果重名就返回一个“用户不可用”else return "用户名可以"

//前端页面:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        window.onload = function (){
            var checkButton = document.getElementById("checkButton");
            checkButton.onclick = function (){
                //1.创建XMLHTTPREQUEST对象
                var xhr = new XMLHttpRequest();
                var username = document.getElementById("username").value;
                //2.准备发送数据
                //xhr.open("method","url",true/false)  : method就是POST/GET  ，
                //url就是要去的servlet的url，一般情况都是true，就是决定是不是异步
                //xhr.send()是真正的发送
                xhr.open("GET","ajax/CheckUserServlet?username=" + username,true);
					
                //3.在send()函数方法前，可以给XmlHttpReuqest对象绑定一个事件onreadystatechange
                //该事件表示，可以指定一个函数，当函数变化时，会触发onreadystatechange
                xhr.onreadystatechange = function (){
                    if(xhr.readyState == 4 && xhr.status == 200){
                        var responseText = xhr.responseText;
                        if(responseText != "111"){
                            document.getElementById("error").value = "用户名不可用";
                        }else{
                            document.getElementById("error").value = "用户名可用";
                        }
                    }
                }



                //4s.真正发送ajax请求（其实ajax请求底层还是Http请求）
                xhr.send();
            }
        }
    </script>
</head>
<body>
<form action="ajax/CheckUserServlet" method="post">
    u:<input type="text" name="name" id="username"/>
    <input style="border-width: 0;color: red" type="text" id="error"><br>
    <input type="button" id="checkButton" value="验证用户名是否合法"><br>
    p:<input type="password" name="pwd" id="userpassword"/><br>
    e:<input type="text" name="email" id="useremail"/><br>
    <input type="submit" value="提交">
</form>
</body>
</html>
```

//用来检查是否重名的servlet:

```
@WebServlet(name = "CheckUserServlet", value = "/ajax/CheckUserServlet")
public class CheckUserServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String username = request.getParameter("username");
        response.setContentType("text/html;charset=utf-8");
        if("king".equals(username)){
            //从DB获取
            User king = new User(100, "King", "666", "8841@qq.com");
            //转成Json字符串
            String strKing = new Gson().toJson(king);
            //返回
            response.getWriter().write(strKing);
        }else{
                //随便返回个
            response.getWriter().write("111");
        }
    }
}
```

##### 2.关于快速入门的一些细节

（1）就和流程图一样分为四个步骤

![image-20231123145400243](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231123145400243.png)

（2）       准备发送数据
                //xhr.open("method","url",true/false)  : method就是POST/GET  ，
                //url就是要去的servlet的url，一般情况都是true，就是决定是不是异步
                //xhr.send()是真正的发送

（3）		send()函数方法前，可以给XmlHttpReuqest对象绑定一个事件onreadystatechange
                //该事件表示，可以指定一个函数，当函数变化时，会触发onreadystatechange
                xhr.onreadystatechange = function (){
                    if(xhr.readyState == 4 && xhr.status == 200){
                        var responseText = xhr.responseText;
                        if(responseText != "111"){
                            document.getElementById("error").value = "用户名不可用";
                        }else{
                            document.getElementById("error").value = "用户名可用";
                        }
                    }
                }

（4）method == "GET"  就直接在url带上数据

​		 method =="POST" 可以在send（）中带上数据

 such as :

xhr.send("username=jack&password=123456");

![image-20231123145728118](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231123145728118.png)



3.XMLHttpRequest的一些属性

(1)readystate

![image-20231123150255108](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231123150255108.png)

(2)status  200 404 那些

(3)requestTEXT这个存放数据的



### 三.ThreadLocal



# JavaSe-Review

### 一.IO流

#### 1.文件的操作

(1)File类

注意：File类可以表示一个文件，还可以表示一个目录（Directory），所以我们可以在程序中用File 类的对象可以表示一个文件 或者 目录
当创建了 File 对象之后，我们可以利用该对象来对文件或者目录进行书属性修改：例如：文件的名称，修改日期的日期等等
File 类的对象 还不能直接对文件进行读写操作，只能修改文件的属性等静态操作

File类的一些基本操作：

- `boolean`  `createNewFile()`  当且仅当具有此名称的文件尚不存在时，以原子方式创建由此抽象路径名命名的新空文件。
- `boolean`  `delete()`  删除此抽象路径名表示的文件或目录。
- `boolean`  `exists()`  测试此抽象路径名表示的文件或目录是否存在
- boolean mkdir() 创建单个目录   
- boolean mikdirs() 创建多级目录

​    //注意  ：  这里的file只是一个Java对象，只有使用了createNewFile()方法之后才会真正地在磁盘中创建一个文件

例子:

```
public static void createNewFile(){
    File f1=new File("E:/PR/zlc.txt");
    //如果是相对路径，如果没有前面的src，就在当前目录创建文件
    //如果是绝对路径，那中间推荐使用 / 而不是\\
    //注意  ：  这里的file只是一个Java对象，只有使用了createNewFile()方法之后才会真正地在磁盘中创建一个文件
    if(f1.exists()) {
        System.out.println("文件已经存在");
    }else {
        try {
            f1.createNewFile();
                //注意  ：  这里的file只是一个Java对象，只有使用了createNewFile()方法之后才会真正地在磁盘中创建一个文件
            System.out.println("文件创建成功");
            //注意:创建文件的路径必须存在否则会抛出异常，比如  new File("E:/")
        } catch (Exception e) {
            // TODO: handle exception
        }
        System.out.println("文件的绝对路径" + file.getAbsolutePath());
        System.out.println("文件的父级目录" + file.getParentFile());
        System.out.println("文件的大小" + file.length());
        System.out.println("是不是一个文件" + file.isFile());
        System.out.println("是不是一个目录" + file.isDirectory());
    }
}
```

(2)  一些概念

目录也是文件，是一种特殊文件，叫目录文件，简称目录。
目录是文件系统对象，属于文件系统的概念
术语目录指的是文档文件和文件夹的结构化列表存储在计算机上的方式。它与包含姓名、号码和地址列表的电话簿相当，并且不包含实际文件本身
目录并不是真的把文件放在里面。目录是一个“特殊的文件”，它知道文件的存储位置（通过 inode）。这就说明了为什么它被称为目录。目录用来保存文件项目的索引，而不用保存文件项目本身。Linux 和 UNIX 中的目录并不保存它里面的文件。它们只是记录文件位置的信息

文件夹不一定是磁盘上的物理目录，例如，它可以是Windows中的打印机文件夹或控制面板文件夹
文件夹是图形用户界面对文档容器的隐喻
文件夹是GUI对象
文件夹通常用图标描绘，视觉上类似于物理文件夹

文件就是目录文件以外的普通文件，简称文件。

总结：大部分情况下文件夹与目录的含义相同。

(3) 关于同时创建目录和文件

```
public static void createNewDirectory(){
    File file = new File("E:/PR/java/zlc/haha.txt");
    if(!file.exists()){
        try {
            file.getParentFile().mkdirs();
            file.createNewFile();
            System.out.println("目录创建成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

最后结果就是在E盘下面创建了一个    java/zlc/haha.txt

#### 2.stream流

**（1）** 

字节流
java.io.InputStream 字节输入流
java.io.OutputStream 字节输出流
字符流
java.io.Reader 字符输入流
java.io.Writer 字符输出流
注意：

四大家族的首领都是抽象类。(abstract class)
所有的流都实现了：
java.io.Closeable接口，都是可关闭的，都有 close() 方法。
流是一个管道，这个是内存和硬盘之间的通道，用完之后一定要关闭，不然会耗费(占用)很多资源。养成好习惯，用完流一定要关闭。
所有的 输出流 都实现了：
java.io.Flushable接口，都是可刷新的，都有 flush() 方法。
养成一个好习惯，输出流在最终输出之后，一定要记得flush()刷新一下。这个刷新表示将通道/管道当中剩余未输出的数据强行输出完（清空管道！）刷新的作用就是清空管道。
**ps**：**`如果没有flush()可能会导致丢失数据`**。

在java中只要“**类名**”以 **`Stream`** 结尾的都是**字节流**。以“ **`Reader/Writer`** ”结尾的都是**字符流**。

**(2)java 中 的十六个流**

文件专属：
java.io.FileInputStream（掌握）
java.io.FileOutputStream（掌握）
java.io.FileReader
java.io.FileWriter
转换流：（将字节流转换成字符流）
java.io.InputStreamReader
java.io.OutputStreamWriter
缓冲流专属：
java.io.BufferedReader
java.io.BufferedWriter
java.io.BufferedInputStream
java.io.BufferedOutputStream
数据流专属：
java.io.DataInputStream
java.io.DataOutputStream
标准输出流：
java.io.PrintWriter
java.io.PrintStream（掌握）
对象专属流：
java.io.ObjectInputStream（掌握）
java.io.ObjectOutputStream（掌握）
File文件类
java.io.File

**补充：Windows/Linux小知识点**

Windows：`D:\Soft\QQ\Plugin`
Linux：   `D:/Soft/QQ/Plugin`

#### **(3) IO四大家族之节点流**

##### 1.字节流

##### FileInputStream:

一般情况下，我们应该优先选取BufferedInputStream&BufferedOutputStream。

用途：文件字节输入流，万能的，任何类型的文件都可以采用这个流来读

实例:

```
public static void readTxt(){
    byte[] buf = new byte[1024];//意思是一次读取1024个字节
    int readData = 0;
    FileInputStream fileInputStream = null;
    try {
        fileInputStream = new FileInputStream("E:/zlc.txt");
        while((readData = fileInputStream.read(buf))!=-1){
            System.out.print(new String(buf,0,readData));

        }
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            fileInputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



##### **FileOutputStream**:

```
public static void putTxt(){
    FileOutputStream fileOutputStream = null;
    try {
        fileOutputStream = new FileOutputStream("e:/zlc.txt",true);
        //这个默认是false ，写true 意思就是不会覆盖之前的内容
        fileOutputStream.write("你好世界".getBytes());
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            fileOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


}
```

##### 图片copy :

```
    public static void copyPicture(){
        FileInputStream fileInputStream = null;
        FileOutputStream outputStream = null;
        byte[] bytes = new byte[1024];
        int readData = 0;
        try {
            fileInputStream = new FileInputStream("e:\\img.jpg");
            outputStream = new FileOutputStream("e:\\copyimg.jpg");
            while((readData = fileInputStream.read(bytes)) != -1){
                outputStream.write(bytes,0,readData);
                outputStream.flush();//良好的素质程序员就要学会自己去冲
            }
            System.out.println("Good copy img,my master!");
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                fileInputStream.close();
                outputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
    }
```



##### 2.**字符流**  

##### **FileReader**:

```
public static void test1(){
    FileReader fileReader  = null ;
    char[] data = new char[1024];
    int readLength = 0;
    try {
        fileReader = new FileReader("e:/zlc.txt");
        while((readLength = fileReader.read(data)) != -1){
            System.out.println(new String(data,0,readLength));
        }
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            fileReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

##### **FileWritter**:

```
public static void test1(){
    FileWriter fileWriter = null;
    try {
        fileWriter  = new FileWriter("e:/zlc.txt",true);
        fileWriter.write("我是你爹");
        fileWriter.flush();//良好的素质程序员就是要自己去冲
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

##### (3)字符流和字节流的区别：

字节流   可以用来操作二进制文件 如 图片  视频之类的,这个操作文本信息不太好用有很多弊端

字符流    不能处理二进制文件，但是用来处理文本信息十分快捷



#### (4)IO四大家族之处理流

**(优先使用处理流，是节点流的改良版，性能更好一点)**



##### **BufferdInputStream**:

 一般情况下，我们应该优先选取BufferedInputStream&BufferedOutputStream。   

```
public static void test1(){
    BufferedInputStream bufferedInputStream = null;
    byte[] bytes = new byte[1024];
    int readLine = 0;
    try {
        bufferedInputStream = new BufferedInputStream(new FileInputStream("e:/zlc.txt"));
        while((readLine = bufferedInputStream.read(bytes)) != -1){
            System.out.println(new String(bytes,0,readLine));
        }
    } catch (IOException e) {
        e.printStackTrace();
    }finally{
       // 忘了close()了
    }
}
```



##### **BufferdOutputStream**:

```
public static void test1(){
    BufferedOutputStream bufferedOutputStream = null;
    try {
        bufferedOutputStream = new BufferedOutputStream(new FileOutputStream("e:/zlc.txt",true));
        bufferedOutputStream.write("现在是晚上".getBytes());
        bufferedOutputStream.flush();
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            bufferedOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



##### **BufferdReader**

（优先选择BufferdReader而不是FileReader,因为BufferdReader自带缓冲区，不需要你自己new byte[]）

```
public static void test1(){
    BufferedReader bufferdReader = null;
    String readLine = "";
    try {
        bufferdReader = new BufferedReader(new FileReader("e:/zlc.txt"));
        while((readLine = bufferdReader.readLine()) != null){
        //注意    BufferdReader的readLine方法是直接读取一整行（一整行是指遇见换行符\n），回车符\r中的任何一个或者
        //   		随后的换行符都会终止,返回Null
        //同时BufferdReader也支持原先的read()方法
            System.out.println(readLine);
        }
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            bufferdReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

##### **BufferdWriter**

```
public static void test1(){
    BufferedWriter bufferedWriter = null;
    try {
        bufferedWriter = new BufferedWriter(new FileWriter("e:/zlc.txt",true));
        bufferedWriter.write("好，那么好");
        bufferedWriter.newLine();
        //newLine（）换行的作用
        //建议你写一句话，就换一次行，因为有时候不止一句话，好习惯
        bufferedWriter.write("空气中充满了快活的气息");
        bufferedWriter.newLine();
        bufferedWriter.flush();
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            bufferedWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



#### (5)四大家族之转换流



#### (6)四大家族之打印流









### 二.多线程



#### 1.基础知识





#### 2.线程池





#### 3.悲观锁与乐观锁



**悲观锁:** 悲观锁在操作数据的时候比较悲观，**认为别人会同时修改数据。**

​			因此操作数据时直接**把数据锁住**，直到操作完成后才会释放锁；上锁期间其他人不能修改数据。

**//实现方式**

```
数据库中的行锁，表锁，读锁（共享锁），写锁（排他锁），以及syncronized实现的锁均为悲观锁






```





**乐观锁**:乐观锁在操作数据的时候比较乐观，**认为别人不会同时修改数据。**

​			因此乐观锁**不会上锁**,只是在更新的时候判断一下在此期间别人是否修改了数据；如果别人修改了数据则放弃操作，否则执行操作

**//实现方式1:CAS（Compare And Swap）**

```
操作流程:
 	 1) 需要读写的内存位置(V)
     2) 进行比较的预期值(A)
     3) 拟写入的新值(B)
操作逻辑:
        涉及到三个操作数，数据所在的内存值，预期值，新值。当需要更新时，判断当前内存值与之前取到的值是否相等，若相等，则用新值更         新，若失败则重试，一般情况下是一个自旋操作，即不断的重试。
一个问题:
	许多CAS的操作是自旋的：如果操作不成功，会一直重试，直到操作成功为止。
    这里引出一个新的问题，既然CAS包含了Compare和Swap两个操作，它又如何保证原子性呢？
    答案是：CAS是由CPU支持的原子操作，其原子性是在硬件层面进行保证的。



```

**//实现方式2：版本号(比较常用)**

```
一般是在数据表中加上一个数据版本号version字段，表示数据被修改的次数，当数据被修改时，version值会加一。当线程A要更新数据值时，在读取数据的同时也会读取version值，在提交更新时，若刚才读取到的version值为当前数据库中的version值相等时才更新，否则重试更新操作，直到更新成功。
```



**//区别与应用场景**























































































































































# Java前端



### 三.javascript

**JavaScript是运行在浏览器上的脚本语言。简称JS**



| ![lamp](https://www.runoob.com/images/lamp.jpg) | 那些老旧的实例可能会在 <script> 标签中使用 type="text/javascript"。现在已经不必这样做了。JavaScript 是所有现代浏览器以及 HTML5 中的默认脚本语言 |
| ----------------------------------------------- | ------------------------------------------------------------ |
|                                                 |                                                              |

1.入门:

[最通俗易懂的JavaScript入门教程-CSDN博客](https://blog.csdn.net/jiahuan_/article/details/105895421)

#### 1.一些不熟悉的知识

##### (1)**1.JS中的函数定义	**

语法格式：
第一种方式：
function 函数名（形式参数列表）{
函数体；
}
第二种方式：
函数名=function(形式参数列表）{
函数体；
}**

//JS中的函数不需要指定返回值类型，返回什么类型的数据都没问题。

//在调用函数的时候，如果没有传参数的值，或则传了一部分，剩下未传的参数默认赋值undefined。

例子：

![image-20231217173609095](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217173609095.png)

//函数中的return可以真的返回数值，也可以用来退出函数





##### (2)js中的重载

**JS的函数不能重载。**
如果出现同名函数，后面定义的函数会把前面定义的函数覆盖。
因此JS函数不能重名。分辨函数就是根据函数名来分辨。



##### (3)JS数据类型

一些额外知识{

数据类型有:原始类型，引用类型。
原始类型：Undefined,Number,String,Boolean,Null
引用类型:Object以及子类。

**细节:在ES6规范后，又基于以上6种类型添加了一种新的类型：Symbol。**

}

**值类型(基本类型)**：字符串（String）、数字(Number)、布尔(Boolean)、空（Null）、未定义（Undefined）、Symbol。

**引用数据类型（对象类型）**：对象(Object)、数组(Array)、函数(Function)，还有两个特殊的对象：正则（RegExp）和日期（Date）。

在 JavaScript 中有 6 种不同的数据类型：

- string
- number
- boolean
- object
- function
- symbol

3 种对象类型：

- Object
- Date
- Array

2 个不包含任何值的数据类型：

- null
- undefined
  //////////////////////////////////////////////////////////////////////////////

- **Number**:
  NaN，表示Not a Number不是一个数字，但是属于Number类型。

​		0,-1,123,…小数，复数，无穷大都是属于number类型。

​		除数为0时，结果为无穷大。

![image-20231218141548431](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231218141548431.png)

- **Boolean**

NaN,0,"",null,undefined会自动转换成false.

- **String**

1.在JS当中字符串可以使用单引号和双引号。

2.在JS当中，怎么创建字符串对象

第一种：var s=“sag”;（小String，属于String类型）
第二种：var a2= new String(“ab”);（大String，属于Object类型）
Sting是一个内置的类，可以直接使用。

**不要创建 String 对象。它会拖慢执行速度，并可能产生其他副作用：**

3.无论是小String还是大Sting字符串的长度相同。其中又一个length属性求长度(x.length)

常用函数：
indexof: 获取指定字符串在当前字符串中第一次出现的索引
lastIndexof
replace
substr
substring
toLowerCase
toUpperCase
spilt 拆分字符串

例如:alert(“fasdf".indexof(“sdf”));

replace只替换最前面一个子字符串
如果想全部替换需要使用正则表达式。

substr和substring的区别。
substr(startIndex length)

substring(startIndex endIndex)左闭右开。

- **Object**
  //感觉和Java 的 object超类没什么太大区别

**Object类的函数：**

toString()
valueof()
toLocalString()

































##### (4)typeof运算符

JS中有一个运算符叫做typeof,这个运算符可以在程序的运行阶段动态地获取变量的数据类型。

typeof运算符的语法格式：
typeof 变量名

typeof运算符的运算结果时以下6个字符串(全小写）结果之一：
“undefined"
“number”
“string”
“boolean”
“object”
“function”

var d=null;
alert(typeof d);//“object”



##### (5) == 和 ===

比较过程：

　　双等号==： 

　　（1）如果两个值类型相同，再进行三个等号(===)的比较

　　（2）如果两个值类型不同，也有可能相等，需根据以下规则进行类型转换在比较：

　　　　1）如果一个是null，一个是undefined，那么相等

　　　　2）如果一个是字符串，一个是数值，把字符串转换成数值之后再进行比较

　　

　　三等号===:**绝对相等，即数据类型与值都必须相等。**

　　（1）如果类型不同，就一定不相等

　　（2）如果两个都是数值，并且是同一个值，那么相等；如果其中至少一个是NaN，那么不相等。（判断一个值是否是NaN，只能使用isNaN( ) 来判断）

　　（3）如果两个都是字符串，每个位置的字符都一样，那么相等，否则不相等。

　　（4）如果两个值都是true，或是false，那么相等

　　（5）如果两个值都引用同一个对象或是函数，那么相等，否则不相等

　　（6）如果两个值都是null，或是undefined，那么相等

**同理还有!=  和!==**

##### (6)数组

var cars=new Array("Saab","Volvo","BMW");

//和Java不同，数组里面可以是任何东西

下标也是从0开始的

##### (7)对象

对象由花括号分隔。在括号内部，对象的属性以名称和值对的形式 (name : value) 来定义。属性由逗号分隔：

var person={
firstname : "John",
lastname : "Doe",
id    : 5566
};

**声明变量类型**

当您声明新变量时，可以使用关键词 "new" 来声明其类型：

var carname=new String;
var x=   new Number;
var y=   new Boolean;
var cars=  new Array;
var person= new Object;

**对象属性有两种寻址方式：**

name=person.lastname;
name=person["lastname"];



##### (9)this

和java 的 this基本一样



##### (10)if while swich等

和Java基本一样，不过while可以直接遍历

cars=["BMW","Volvo","Saab","Ford"];

 var i=0; 

while (cars[i])

 {    document.write(cars[i] + "]");  i++; }

##### (11)输出

JavaScript 可以通过不同的方式来输出数据：

- 使用 **window.alert()** 弹出警告框。
- 使用 **document.write()** 方法将内容写到 HTML 文档中。
- 使用 **innerHTML** 写入到 HTML 元素。
- 使用 **console.log()** 写入到浏览器的控制台。

##### (12)异常

try {    ...    //异常的抛出 } catch(e) {    ...    //异常的捕获与处理 } finally {    ...    //结束处理 }

也同样有throw 抛出异常

和Java一致

##### (13)获取表单信息

function validateForm() {  var x=document.forms["myForm"]["fname"].value;  if (x==null || x=="")  {    alert("姓必须填写");    return false;  } }



以上函数在 form 表单提交时被调用:

![image-20231217192723768](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231217192723768.png)

还可以使用   let fname = document.getElementByID("xx")

##### (15)json与Js

| 函数                                                         | 描述                                           |
| :----------------------------------------------------------- | :--------------------------------------------- |
| [JSON.parse()](https://www.runoob.com/js/javascript-json-parse.html) | 用于将一个 JSON 字符串转换为 JavaScript 对象。 |
| [JSON.stringify()](https://www.runoob.com/js/javascript-json-stringify.html) | 用于将 JavaScript 值转换为 JSON 字符串。       |



##### (16)href="#"与href="javascript:void(0)"的区别

**#** 包含了一个位置信息，默认的锚是**#top** 也就是网页的上端。

而javascript:void(0), 仅仅表示一个死链接。

在页面很长的时候会使用 **#** 来定位页面的具体位置，格式为：**# + id**。

如果你要定义一个死链接请使用 javascript:void(0) 。

![image-20231218121337061](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231218121337061.png)



##### (17)异步编程

**回调函数**

回调函数就是一个函数，它是在我们启动一个异步任务的时候就告诉它：等你完成了这个任务之后要干什么。这样一来主线程几乎不用关心异步任务的状态了，他自己会善始善终。

**实例**

setTimeout(function () {    document.getElementById("demo").innerHTML="RUNOOB!"; }, 3000);

//这段程序中的 setTimeout 就是一个消耗时间较长（3 秒）的过程，它的第一个参数是个回调函数，第二个参数是毫秒数，这个函数执行之后会产生一个子线程，子线程会等待 3 秒，然后执行回调函数 "print"，在命令行输出 "RUNOOB!"。

当然，JavaScript 语法十分友好，我们不必单独定义一个函数 print ，我们常常将上面的程序写成：

**和线程差不多一个意思**

**关于ajax前面有专门讲解的章节**



##### (18)注意事项

```
<script src="js/js1.js"></script>   //结尾必须是</script> 不能是  </>  不然会有大问题!!!!
```



##### (19)for循环

For/In 循环

JavaScript for/in 语句循环遍历对象的属性：

实例

var person={fname:"Bill",lname:"Gates",age:56}; 

  for (x in person)  // x 为属性名

 {    txt=txt + person[x]; }



#### 2.ES6新特性

##### (1)**变量声明：const和let**

**ES6推荐使用let声明局部变量**，相比之前的var（无论声明在何处，都会被视为声明在函数的最顶部），let具有块级作用域（即在使用let的那一对大括号 {}内起作用），可以避免变量提升和污染全局作用域的问题。

const则用来声明常量，即一旦赋值就不能再改变。const也具有块级作用域，并且必须在声明时就初始化。const适合用来定义不会改变的值，如PI、URL等。

```js
// 使用var
var a = 1;
if (true) {
  var a = 2; // 这里会覆盖上面的a
}
console.log(a); // 输出2

// 使用let
let b = 1;
if (true) {
  let b = 2; // 这里不会影响外面的b
}
console.log(b); // 输出1

// 使用const
const PI = 3.14;
PI = 3.15; // 报错：Assignment to constant variable.

const URL = "https://www.bing.com";
URL = "https://www.google.com"; // 报错：Assignment to constant variable.
```



##### **(2) 解构赋值**

解构赋值是一种从数组或对象中提取数据并赋值给变量的简洁写法。它可以减少代码量，提高可读性，并且支持默认值、嵌套结构、别名等特性。

```js
// 数组解构：按照数组元素位置对应赋值给变量
let [f, g, h] = [1, 2, 3];
console.log(f); // 1
console.log(g); // 2
console.log(h); // 3

// 对象解构：按照对象属性名对应赋值给同名变量（也可以使用别名）
let {name, age} = {name: "Alice", age: 18};
console.log(name); // Alice
console.log(age); // 18

let {name: i, age: j} = {name: "Bob", age: 19};
console.log(i); // Bob
console.log(j); //19

// 默认值：如果没有匹配到相应的数据，则使用默认值（如果有）
let [k, l=0] = [1];
console.log(k); //1 
console.log(l); //0 

let {m=0, n=0} = {m:1};
console.log(m); //1 
console.log(n); //0
// 嵌套结构：可以解构嵌套的数组或对象
let [o, [p, q]] = [1, [2, 3]];
console.log(o); // 1
console.log(p); // 2
console.log(q); // 3

let {r: {s, t}} = {r: {s: 4, t: 5}};
console.log(s); // 4
console.log(t); // 5

// 解构赋值的应用场景：交换变量、函数参数、返回值等
let u = 6;
let v = 7;
[u, v] = [v, u]; // 不需要使用临时变量来交换u和v的值
console.log(u); // 7
console.log(v); // 6

function foo([x, y]) {
  return x + y;
}
console.log(foo([8,9])); //17

function bar() {
  return [10,11];
}
let [w,z] = bar();
console.log(w); //10 
console.log(z); //11
```



##### **(3) 箭头函数**

箭头函数是一种使用 => 符号定义函数的简洁写法 。它可以省略 function 关键字、参数括号、返回值括号等，使得代码更加简洁和清晰。箭头函数还有一个重要的特性，就是它不会改变 this 的指向，即箭头函数内部的 this 始终指向定义时所在的对象。

```js
// 普通函数和箭头函数的对比
function add(x,y) {
    return x + y;
}

let add = (x,y) => x + y; // 省略了 function 关键字、参数括号、返回值括号

// 如果只有一个参数，可以省略参数括号；如果没有参数，必须使用空括号
let square = x => x * x;

let hello = () => console.log("Hello");

// 如果有多条语句，需要使用大括号包裹，并且显式返回（如果需要）
let max = (x,y) => {
    if (x > y) {
        return x;
    } else {
        return y;
    }
};

// 箭头函数不会改变 this 的指向，即箭头函数内部的 this 始终指向定义时所在的对象
let obj = {
    name: "Alice",
    sayHi: function() {
        console.log(this.name); // Alice
        setTimeout(function() {
            console.log(this.name); // undefined （因为setTimeout中的this指向window）
        },1000);
        setTimeout(() => {
            console.log(this.name); // Alice （因为箭头函数中的this指向obj）
        },1000);
    }
};
obj.sayHi();
```



##### **(4) 模板字符串**

模板字符串是一种使用反引号 `` 包裹字符串，并且支持插入变量或表达式的新语法 。它可以避免使用 + 号连接字符串和变量，并且支持多行字符串和标签模板等特性。

```js
// 使用模板字符串插入变量或表达式，用 ${} 包裹即可（注意是反引号而不是单引号）
let name = "Bob";
let age = 19;
let message = `Hello ${name}, you are ${age} years old.`; 
console.log(message);

// 使用模板字符串可以直接换行，不需要使用 \n 或者 + 号连接多行字符串
let poem =
`Do not go gentle into that good night,
Old age should burn and rave at close of day;
Rage, rage against the dying of the light.`; 
console.log(poem);

// 使用标签模板可以自定义模板字符串的处理方式（标签是一个函数名）
function tag(strings,...values) {
    let result = "";
    for (let i=0; i<strings.length; i++) {
        result += strings[i];
        if (i < values.length) {
            result += values[i].toUpperCase(); // 将变量转为大写
        }
    }
    return result;
}

let name = "Alice";
let message = tag`Hello ${name}, how are you?`; // 使用tag函数处理模板字符串
console.log(message); // Hello ALICE, how are you?
```





##### (5)类与继承

class Runoob {

  constructor(name, url) {  

  this.name = name;    this.url = url; 

​				 }

 }

//class 内部  有一个构造器/构造函数  

**定义好类后，我们就可以使用 new 关键字来创建对象：**



**ES6 引入了 class 关键字，使得定义类和继承更加清晰，extends 关键字用于建立继承关系，super 关键字用于在子类构造函数中调用父类的构造函数。**

**和Java差不多,不过class里面好像只能写构造器和方法，不能有属性**



**JavaScript 静态方法**

静态方法是使用 static 关键字修饰的方法，又叫类方法，属于类的，但不属于对象，在实例化对象之前可以通过 **类名.方法名** 调用静态方法。

静态方法不能在对象上调用，只能在类中调用。

如果你想在对象 中使用静态方法，可以作为一个参数传递给它：









#### 3.DOM节点操作

##### (1)修改HTML

**介绍：**

通过可编程的对象模型，JavaScript 获得了足够的能力来创建动态的 HTML。

- JavaScript 能够改变页面中的所有 HTML 元素
- JavaScript 能够改变页面中的所有 HTML 属性
- JavaScript 能够改变页面中的所有 CSS 样式
- JavaScript 能够对页面中的所有事件做出反应

###### a.三种查找方式

**通过ID查找HTML元素**

var x=document.getElementById("intro");

**通过标签名去查找HTML元素**

var x=document.getElementById("main");
var y=x.getElementsByTagName("p");

**通过类名去查找HTML元素**

var x=document.getElementsByClassName("intro");

###### b.修改HTML文本内容

如需改变 HTML 元素的内容，请使用这个语法：

document.getElementById(*id*).innerHTML=*新的 HTML*

//例子:

<html>
<body>

<p id="p1">Hello World!</p>

<script>
document.getElementById("p1").innerHTML="新文本!";
</script>

</body>
</html>

###### **c.修改HTML属性**

如需改变 HTML 元素的属性，请使用这个语法：document.getElementById(*id*).*attribute=新属性值*

<!DOCTYPE html>
<html>
<body>

<img id="image" src="smiley.gif">

<script>
document.getElementById("image").src="landscape.jpg";
</script>

</body>
</html>

##### (2)修改CSS样式

如需改变 HTML 元素的样式，请使用这个语法：

document.getElementById(*id*).style.*property*=*新样式*

<script> document.getElementById("p2").style.color="blue"; document.getElementById("p2").style.fontFamily="Arial"; document.getElementById("p2").style.fontSize="larger"; </script>



##### (3)事件

下面是一些常见的HTML事件的列表:

| 事件        | 描述                                 |
| :---------- | :----------------------------------- |
| onchange    | HTML 元素改变                        |
| onclick     | 用户点击 HTML 元素                   |
| onmouseover | 鼠标指针移动到指定的元素上时发生     |
| onmouseout  | 用户从一个 HTML 元素上移开鼠标时发生 |
| onkeydown   | 用户按下键盘按键                     |
| onload      | 浏览器已完成页面的加载               |

HTML 事件的例子：

- 当用户点击鼠标时
- 当网页已加载时
- 当图像已加载时
- 当鼠标移动到元素上时
- 当输入字段被改变时
- 当提交 HTML 表单时
- 当用户触发按键时



###### **a.onclick事件**

![image-20231218134558881](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231218134558881.png)

###### b.onload 和 onunload 事件

onload 和 onunload 事件会在用户进入或离开页面时被触发。

onload 事件可用于检测访问者的浏览器类型和浏览器版本，并基于这些信息来加载网页的正确版本。

onload 和 onunload 事件可用于处理 cookie。

###### c.onchange事件

onchange 事件常结合对输入字段的验证来使用。

下面是一个如何使用 onchange 的例子。当用户改变输入字段的内容时，会调用 upperCase() 函数。

实例

<input type="text" id="fname" **onchange**="upperCase()">



###### d.onmouseover和onmouseout事件

onmouseover 和 onmouseout 事件可用于在用户的鼠标移至 HTML 元素上方或移出元素时触发函数

**<d.iv onmouseover="mOver(this)" onmouseout="mOut(this)" style="background-color:#D94A38;width:120px;height:20px;padding:40px;">Mouse Over Me</div>**
**<scri.pt>**
**function mOver(obj){**
	**obj.innerHTML="Thank You"**
**}**
**function mOut(obj){**
	**obj.innerHTML="Mouse Over Me"**
**}**
**</scri..pt>**





###### e.onmousedown、onmouseup 以及 onclick 事件

onmousedown, onmouseup 以及 onclick 构成了鼠标点击事件的所有部分。首先当点击鼠标按钮时，会触发 onmousedown 事件，当释放鼠标按钮时，会触发 onmouseup 事件，最后，当完成鼠标点击时，会触发 onclick 事件。





##### (4)DOM EventListener

自己去**查文档**吧，这个比起直接在 标签中使用 'onclick 之类的' 有一个特性那就是可以重复添加事件，想加几个加几个反正不会覆盖,想加哪种类型的都可以，全加一遍都无所谓.



(5)DOM 元素

你可以直接使用代码去增删改查DOM元素，不过我感觉没什么用，用到再去**文档里面查**吧



(6)HTMLCollection对象

```
var myCollection = document.getElementsByTagName("p");
```

此时这里的myCollection就获取了所有的p标签，可以通过下标从0开始来获取 var y = myCollection[0];

length属性:   let length1 = mytCollection.length;

**注意**

**HTMLCollection 不是一个数组！**

HTMLCollection 看起来可能是一个数组，但其实不是。

你可以像数组一样，使用索引来获取元素。

HTMLCollection 无法使用数组的方法： valueOf(), pop(), push(), 或 join() 。



##### (5)Window对象- 浏览器对象模型

###### **a.一些其他方法：**

- window.open() - 打开新窗口
- window.close() - 关闭当前窗口
- window.moveTo() - 移动当前窗口
- window.resizeTo() - 调整当前窗口的尺寸



###### **b.弹窗**

可以在 JavaScript 中创建三种消息框：警告框、确认框、提示框。

- **警告框**

警告框经常用于确保用户可以得到某些信息。

当警告框出现后，用户需要点击确定按钮才能继续进行操作。

语法：window.alert("*sometext*");   window可以省略，这就是我们平时常用的 alert("xxx");

- **确认框**

确认框通常用于验证是否接受用户操作。

当确认框弹出时，用户可以点击 "确认" 或者 "取消" 来确定用户操作。

当你点击 "确认", 确认框返回 true， 如果点击 "取消", 确认框返回 false。

**语法**:window.confirm("*sometext*"); window可以省略.

**var r=confirm("按下按钮");**
**if (r==true)**
**{**
    **x="你按下了\"确定\"按钮!";**
**}**
**else**
**{**
    **x="你按下了\"取消\"按钮!";**
**}**





- **提示框**

提示框经常用于提示用户在进入页面前输入某个值。

当提示框出现后，用户需要输入某个值，然后点击确认或取消按钮才能继续操纵。

如果用户点击确认，那么返回值为输入的值。如果用户点击取消，那么返回值为 null。

**语法**:window.prompt("*sometext*","*defaultvalue*");window可以省略.

//例子:

var person=prompt("请输入你的名字","Harry Potter");
if (person!=null && person!="")
{
  x="你好 " + person + "! 今天感觉如何?";
  document.getElementById("demo").innerHTML=x;
}

###### c.计时事件

**JavaScript 计时事件**

通过使用 JavaScript，我们有能力做到在一个设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行。我们称之为计时事件。

在 JavaScript 中使用计时事件是很容易的，两个关键方法是:

- setInterval() - 间隔指定的毫秒数不停地执行指定的代码。
- setTimeout() - 在指定的毫秒数后执行指定代码。

**注意:** setInterval() 和 setTimeout() 是 HTML DOM Window对象的两个方法。



**如何停止执行setinterval()?**

clearInterval() 方法用于停止 setInterval() 方法执行的函数代码。

**语法**:window.clearInterval(*intervalVariable*),window可以省略.

要使用 clearInterval() 方法, 在创建计时方法时你必须使用全局变量：

myVar=setInterval("*javascript function*",*milliseconds*);

然后你可以使用 clearInterval() 方法来停止执行。

**如何停止执行settimeout()?**

window.clearTimeout() 方法用于停止执行setTimeout()方法的函数代码。



### 四.jquery

### 五.vue2

#### 1.一图胜千言

![img](https://img-blog.csdnimg.cn/7875ac68ff5448dea0bb4471e5c78a91.png)

- **M：Model 模型，包括一些数据和操作**

-  **V：View 视图， 页面渲染结果**
- **VM：View-Model,模型与视图的双向操作（无需开发人员干涉）**
- **在MVVM之前，开发人员从后端获取需要的数据模型，然后通过DOM操作Model渲染到View中。当用户操作视图，我们还需要通过DOM获取View的数据，然后同步到Model中。**
- **而MVVM中的VM要做的事情就是把DOM操作完全封装起来，开发人员不用在关心Model和View之间是如何互相影响的**
- **只要我们Model发生了改变，View上就会自然表现出来**
- **同理当用户改变了view, Model上的数据也会跟着改变**
- 结果:**把开发人员从繁琐的DOM操作中解脱出来，把关注点放在如何操作Model上，大大提高了开发效率**







#### 2.快速入门

![image-20231219135002719](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231219135002719.png)



**注意事项:**

- 要求script写在html标签后面
- **注意如果插值表达式是在标签体内使用，如果想在标签属性上写就需要使用v-bind**
- 注意  一个script引入vue.js，还有一个负责写代码，别只写一个哦！！！！



#### 3.基本语法知识

一个Vue对象里面有 ul  ,   data ,   methods (**注意不要忘了末尾的s**) ,   computed  , .....





##### 1.vue生命周期

![img](https://img-blog.csdnimg.cn/2021071114294270.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDczODEx,size_16,color_FFFFFF,t_70)



##### 2.插值操作

**a.Mustache:胡子/胡须**

- 之所以叫胡子表达式是因为，使用{{}}两个大括号

比如:<h1.>我是{{name}}<h1.>

- mustache语法中,不仅仅可以直接写变量,也可以写简单的表达式

<h.2>{{firstName + ' ' + lastName}}</h.2>

- **注意Mustache是在标签体内，而不是标签属性.比如你想引入图片用Mustache就不行**



**b.v-once**

- 但是，在某些情况下，我们可能不希望界面随意的跟随改变
  - 这个时候，我们就可以使用一个Vue的指令

//例子:

<di.v id="app">

  <h.2>{{message}}</h2>
  <h.2 **v-once**>{{message}}</h2>

</di.v>

<!-- v-once: 
该指令后面不需要跟任何表达式(比如之前的v-for后面是由跟表达式的)
该指令表示元素和组件(组件后面才会学习)只渲染一次，不会随着数据的改变而改变 -->
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    }
  })
  // 指令的本质就是自定义属性
**c.v-text**

- v-text作用和Mustache比较相似：都是用于将数据显示在界面中
- v-text通常情况下，接受一个string类型
- 专门用来显示文本信息的

![img](https://img-blog.csdnimg.cn/20210711160049128.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDczODEx,size_16,color_FFFFFF,t_70)





**d.v-pre**

- v-pre用于跳过这个元素和它子元素的编译过程，用于显示原本的Mustache语法。
- 比如下面的代码：
  - 第一个h2元素中的内容会被编译解析出来对应的内容
  - 第二个h2元素中会直接显示{{message}}

![img](https://img-blog.csdnimg.cn/20210711160258211.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDczODEx,size_16,color_FFFFFF,t_70)



//其他的一些用到再说吧

##### 3.绑定属性(v-bind)

###### **a.介绍:**

//上面的指令主要作用是将值/内容插入到我们模板的内容当中，但是，除了内容需要动态来决定外，某些属性我们也希望动态来绑定

- 比如动态绑定a元素的href属性
- 比如动态绑定img元素的src属性



- 这个时候，我们可以使用v-bind指令：
  - 作用：动态绑定属性
  - 缩写：:
  - 预期：any (with argument) | Object (without argument)
  - 参数：attrOrProp (optional)

**作用:v-bind用于绑定一个或多个属性值，或者向另一个组件传递props值**



###### **b.v-bind基础**

- 在开发中，有哪些属性需要动态进行绑定呢？
  - 还是有很多的，比如图片的链接src、网站的链接href、动态绑定一些类、样式等等
  - 比如通过Vue实例中的data绑定元素的src和href，代码如下

```
<div id="app">
    <a v-bind:href="test">ddd</a>
    <img v-bind:src="img_src" width="200px">
</div>
<script src="vue.js"></script>
<script>
    let myvue = new Vue({
        el:"#app",
        data:{
            test:"https://blog.csdn.net/qq_23073811/article/details/118651507",
            img_src:"test.jpg"
        }
    })
</script>
```



**注意:在开发中，我们通常会使用简写(也就是一个:)的形式，因为这样更加简洁。**



###### c.v-bind绑定class

- 很多时候，我们希望动态的来切换class，比如：
  - 当数据为某个状态时，字体显示红色。
  - 当数据另一个状态时，字体显示黑色

- 绑定class有两种方式
  - 对象语法(掌握)
  - 数组语法(了解)



- 绑定方式：对象语法
- 对象语法的含义是:class后面跟的是一个对象。
  - 对象语法有下面这些用法：

```html
用法一：直接通过{}绑定一个类
<h2 :class="{'active': isActive}">Hello World</h2>
 
用法二：也可以通过判断，传入多个值
<h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>
 
用法三：和普通的类同时存在，并不冲突
注：如果isActive和isLine都为true，那么会有title/active/line三个类
<h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello World</h2>
 
用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">Hello World</h2>
```



###### d.v-bind绑定style

![image-20231220121754397](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20231220121754397.png)







##### 4.计算机属性

**我们可能需要对数据进行一些转化后再显示，或者需要将多个数据结合起来进行显示**

- 比如我们有firstName和lastName两个变量，我们需要显示完整的名称。
- 但是如果多个地方都需要显示完整的名称，我们就需要写多个{{firstName}} {{lastName}}



自己去查吧，懒得记了.很简单



##### 5.事件监听

**v-on**



![img](https://img-blog.csdnimg.cn/20210712180147352.png)



- 注：v-on也有对应的语法糖：
  - v-on:click可以写成@click 



##### 6.条件判断符号

**v-if , v-else-if , v-else**

```
<div id="app">
    <h1 v-if="score>=80">优秀</h1>
    <h1 v-else-if="score>=70">良好</h1>
    <h1 v-else="score>60">及格</h1>
</div>
```



5.(掌握)v-show的使用以及和v-if的区别
v-show的用法和v-if非常相似，也用于决定一个元素是否渲染：
v-if和v-show对比
v-if和v-show都可以决定一个元素是否渲染，那么开发中我们如何选择呢？
v-if当条件为false时，压根不会有对应的元素在DOM中。
v-show当条件为false时，仅仅是将元素的display属性设置为none而已。
**开发中如何选择呢？**
**当需要在显示与隐藏之间切换很频繁时，使用v-show**
**当只有一次切换时，通过使用v-if**





##### 7.遍历

- 当我们有一组数据需要进行渲染时，我们就可以使用v-for来完成。
  - v-for的语法类似于JavaScript中的for循环。
  - 格式如下：item in items的形式。





```
<div id="app">
    <ul>
        <li v-for="item in movies">{{item}}</li>
    </ul>
</div>
```



```
let myVue = new Vue({
    el:"#app",
    data: {
        isActive:false,
        color:"red",
        score:75,
        movies:[
            '星际穿越','电锯惊魂','宝宝巴士','万历千年'
        ]
    },
```



//如果是以键值对的形式存储的

![img](https://img-blog.csdnimg.cn/20210712203733325.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDczODEx,size_16,color_FFFFFF,t_70)







##### 8.表单绑定v-model

快速案例

```
<div id="app">
    <input type="text" v-model="message">
    <h3>{{message}}</h3>
</div>
```





**v-model的原理**

- v-model其实是一个语法糖，它的背后本质上是包含两个操作：
  - 1.v-bind绑定一个value属性
  - 2.v-on指令给当前元素绑定input事件



**v-model还可以结合许多其他标签，这里就举几个例子**



  <div id="app">
    <label for="male">
      <!-- 需要加相同的name 否则可以多选 -->
      <!-- <input type="radio" id="male" value="男" name="sex">男 -->
      <!-- 一旦v-moddel绑定的是同一个变量，name可以不用写 -->
      <input type="radio" id="male" value="男" v-model="sex">男
    </label>
    <label for="female">
      <input type="radio" id="female" value="女" v-model="sex">女
    </label>
    <label for="other">
      <input type="radio" id="other" value="其他" v-model="sex">其他
    </label>
    <h2>您选择的性别是: {{sex}}</h2>
  </div>


  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊',
        sex: '女' // 可以给radio默认值
      }
    })
  </script>



  <div id="app">
    <!--1.checkbox单选框 -->
    <!-- 
      v-model即为布尔值true/false。
      此时input的value并不影响v-model的值
 -->
    <label for="agree">
      <input type="checkbox" id="agree" v-model="isAgree">同意协议
    </label>
    <h2>您选择的是: {{isAgree}}</h2>
    <button :disabled="!isAgree">下一步</button>

    <!--2.checkbox多选框-->
    <!-- 
      当是多个复选框时，因为可以选中多个，所以对应的data中属性是一个数组。
      当选中某一个时，就会将input的value添加到数组中。
   -->
    <input type="checkbox" value="篮球" v-model="hobbies">篮球
    <input type="checkbox" value="足球" v-model="hobbies">足球
    <input type="checkbox" value="乒乓球" v-model="hobbies">乒乓球
    <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
    <h2>您的爱好是: {{hobbies}}</h2>

     <!-- 值绑定 动态的给value赋值 -->
    <label v-for="item in originHobbies" :for="item">
      <input type="checkbox" :value="item" :id="item" v-model="hobbies">{{item}}
    </label>
  </div>

  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊',
        isAgree: false, // 单选框

        hobbies: [], // 多选框,
        originHobbies: ['篮球', '足球', '乒乓球', '羽毛球', '台球', '高尔夫球']
      }
    })









v-model 修饰符的使用
lazy修饰符：
默认情况下，v-model默认是在input事件中同步输入框的数据的。
也就是说，一旦有数据发生改变对应的data中的数据就会自动发生改变。
lazy修饰符可以让数据在失去焦点或者回车时才会更新
number修饰符：
默认情况下，在输入框中无论我们输入的是字母还是数字，都会被当做字符串类型进行处理。
但是如果我们希望处理的是数字类型，那么最好直接将内容当做数字处理。
number修饰符可以让在输入框中输入的内容自动转成数字类型
trim修饰符：
如果输入的内容首尾有很多空格，通常我们希望将其去除
trim修饰符可以过滤内容左右两边的空格
![img](https://img-blog.csdnimg.cn/20210714154638782.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDczODEx,size_16,color_FFFFFF,t_70)



































