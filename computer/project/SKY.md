# SKY



## Day1

1.md5加密

```
//密码比对
//对前端密码进行 Md5加密
password = DigestUtils.md5DigestAsHex(password.getBytes());
if (!password.equals(employee.getPassword())) {
    //密码错误
    throw new PasswordErrorException(MessageConstant.PASSWORD_ERROR);
}
```

2.threadocal 的  使用

```
public class BaseContext {

    public static ThreadLocal<Long> threadLocal = new ThreadLocal<>();

    public static void setCurrentId(Long id) {
        threadLocal.set(id);
    }

    public static Long getCurrentId() {
        return threadLocal.get();
    }

    public static void removeCurrentId() {
        threadLocal.remove();
    }

}
```

**3.疑问：既然一次Http请求是一次线程，那么它的生命周期是多长？？是不是和一个Http请求的生命周期是一个东西（应该是的）好像得需要深入学习计算机网络后才能有答案**

4.pagehelper的使用!!    原理是什么 后面得去了解一下啊！！

```
        //进行分页
        PageHelper.startPage(setmealPageQueryDTO.getPage(),setmealPageQueryDTO.getPageSize());
		//查询后 各种数据都存在page当中
        Page<Setmeal> page = setmealMapper.queryPage(setmeal);

        return new PageResult(page.getTotal(),page.getResult());
```

5.SpringMVC的消息转换器。。。感觉是很高级的东西，了解一下就可以了





## Day2





#### 2.一个坑

user包下面  和  admin包下面  都有ShopController，这时编译没问题但是**运行项目就会报错**，因为两个ShopController在注入容器中会**重名,造成冲突**，所以需要在@RestController修改注入的名字,@RestController("userShopController"),@RestController("admin...略")**用不同名字来区分，避免冲突**

![image-20240306201500495](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240306201500495.png)





#### 3.未解之谜:gitee 有冲突 ？？？





## Day3

**//微信小程序开发  等学完前端技术栈可以搞一下微信小程序玩玩**



### **1.在Java中的微信开发**



HttpClient 介绍{

作用 ：简单来说就是可以用Java去发送Http请求

核心API ： 

- ​				HttpClient
- ​                HttpClients
- ​               CloseableHttpClient
- ​                HttpGet
- ​                HttpPost

发送请求步骤:{

- ​		创建HttpClient对象
- ​         创建Http对象
- ​         调用Httpclient的execute方法发送请求

}

}



HttpClient 使用

1.导入maven坐标:

```
<!--微信支付-->
<dependency>
    <groupId>com.github.wechatpay-apiv3</groupId>
    <artifactId>wechatpay-apache-httpclient</artifactId>
    <version>0.4.8</version>
</dependency>
//阿里云OSS 的maven依赖就包含这个maven坐标哦！！！
```





**//简单测试---完成向微信发送post和get请求**

```
public class HttpClientTest {

    /*
    * 测试用过HttpClient发送Get方式的请求
    * */
    @Test
    public void testGET() throws IOException {
        //创建httpclient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();

        //创建请求对象
        HttpGet httpGet = new HttpGet("http://localhost:8080/user/shop/status");

        //发送请求,接收响应
        CloseableHttpResponse response = httpClient.execute(httpGet);

        //获取服务器返回的数据，状态码之类的信息
        int statusCode = response.getStatusLine().getStatusCode();
        System.out.println("Get请求的状态码：" + statusCode);
        HttpEntity entity = response.getEntity();
        String s = EntityUtils.toString(entity);
        System.out.println("服务端返回的数据:" + s);

        //关闭资源
        response.close();
        httpClient.close();
    }


    /*
     * 测试用过HttpClient发送Post方式的请求
     * */
    @Test
    public void testPost() throws IOException {
        //创建httpClient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();

        //创建HttpPost对象
        HttpPost httpPost = new HttpPost("http://localhost:8080/admin/employee/login");

        //构建数据
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("username","admin");
        jsonObject.put("password","123456");
        StringEntity entity = new StringEntity(jsonObject.toString());

        //指定请求编码方式
        entity.setContentEncoding("utf-8");
        //指定数据格式
        entity.setContentType("application/json");

        httpPost.setEntity(entity);

        //发送post请求，接收响应
        CloseableHttpResponse response = httpClient.execute(httpPost);

        //解析数据
        HttpEntity entity1 = response.getEntity();
        String s = EntityUtils.toString(entity1);
        System.out.println("响应资源:" + s);

        //关闭资源
        response.close();
        httpClient.close();
    }
}
```





### 2.完成微信登录的收获





2.怪不得我的application-dev.yaml文件经常失效，原来是缩写的问题！！！！！！！！！！！！！！



![image-20240306185129328](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240306185129328.png)





​	

3.通过完成微信登录功能，让我对 如何**完成微信登录**有了很深的理解，同时也**加深了对配置文件的理解**(比如配置文件的作用通常与xxxProperties一个类通过@ConfigurationProperties(prefix = "sky.wechat")来连接在一起)



![img](https://res.wx.qq.com/wxdoc/dist/assets/img/api-login.2fcc9f35.jpg)























## Day4





### 1.   使用redis缓存菜品数据



**//此前是用户直接向数据库访问数据，若是访问次数多就会导致卡顿等，该如何解决呢？？**

**//   这里我们使用  Redis 对 菜品进行缓存 ，使用户可以直接从redis(本地缓存)获取 菜品数据(若存在缓存数据)**

**//原理:  redis实质上是将数据存放在内存中，而像Mysql之类的传统数据库只会把索引放在内存，真正的数据都在硬盘	**

![image-20240307161500885](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240307161500885.png)







**//缓存逻辑分析:**

- 每个分类下的菜品保存一份缓存数据(按类型保存)
- 数据库中的菜品有变更时清理缓存数据





```
@GetMapping("/list")
@ApiOperation("根据分类id查询菜品")
public Result<List<DishVO>> list(Long categoryId) {
    //构造redis 中key 的规则 : dish_ + 分类id
    String key = "dish_" + categoryId;

    //查询redis中 是否有缓存数据
    List<DishVO> list = (List<DishVO>) redisTemplate.opsForValue().get(key);
    if(list != null && list.size() > 0){
        //若存在菜品缓存数据，则直接返回
        return Result.success(list);
    }

    //若没有从数据库加载数据，并载入缓存
    Dish dish = new Dish();
    dish.setCategoryId(categoryId);
    dish.setStatus(StatusConstant.ENABLE);//查询起售中的菜品

    list = dishService.listWithFlavor(dish);
    //载入缓存
    redisTemplate.opsForValue().set(key,list);

    return Result.success(list);
}
```









### 2.清理缓存



```
//清理reids中受影响的缓存数据
String key = "dish_" + dishDTO.getCategoryId();
redisTemplate.delete(key);
```



//虽然 * 通配符 不能在delete中使用，但是可以在get中使用.

```
//清理reids中所有"dish_"开头的缓存数据
Set keys = redisTemplate.keys("dish_*");
redisTemplate.delete(keys);
```



//抽象成一个方法

```
/*
* 清理缓存数据
* */
public void cleanCache(String pattern){
    Set key = redisTemplate.keys(pattern);
    redisTemplate.delete(key);
}
```





### 3.Spring cache



#### 3.1  介绍

**//SpringCache是一个基于注解的缓存框架，只需要简单地添加一个注解，就能实现缓存功能**

**//前面两小节我们认识到了redis缓存数据，但是自己写的效率低下，使用Spring cache 提供的注解可以提高效率**

**//缓存的实现可以是reids，此外还有EHCache,Caffeine,使用SpringCache只需要切换缓存实现，不需要修改代码**





#### 3.2  常用注解

**//使用是不是很像  事务管理**

| 注解           | 说明                                                         |
| :------------- | ------------------------------------------------------------ |
| @EnableCaching | 开启缓存注解功能，通常加在启动类上                           |
| @Cacheable     | 在方法执行前先查询缓存中是否有数据，如果有数据，则直接返回缓存数据;如果没有缓存数据，调用方法并将方法返回值放到缓存中     //先查再放,一般加在controller层 |
| @CachePut      | 将方法的返回值放到缓存中   //只放数据                        |
| @CacheEvict    | 将一条或多条数据从缓存中删除                                 |





#### 3.3  例子



- 例1：@CachePut

```
@PostMapping
@CachePut(caccheNames = "userCache",key = "#user1.id") //Key的生成:userCache::1   推荐第一个方法(类似 方法很多)
//@CachePut(caccheNames = "userCache",key = "#result.id") //Key的生成也可以使用result关键字，得到方法return对象的属性
public User save(@RequestBody User user1){  
	xxxxx
	return user1;
}
```



- 例2:   @Cacheable

```
@PostMapping
@Cacheable(cacheNames = "userCache",key = "#id")
//使用该注解，底层反射生成一个代理对象，然后在代理对象里面查询缓存实现(此处为redis)里面的数据，没有的话再执行该方法.
public User queryById(Long id){  
	User user = xxxxx;
	return user;
}
```





- 例3  @CacheEvict

```
//删除一个
@DeleteMapping
@CacheEvict(userNames = "userCache",key = "#id")
public void deleteById(Long id){
xxxxx;
}

//删除所有userCache下的缓存数据
@DeleteMapping
@CacheEvict(userNames = "userCache",allEntries = true)
public void deleteById(Long id){
xxxxx;
}

```











## Day5









### 1.购物车





#### 1.1添加购物车



**//数据库开发:冗余字段，通过设计冗余字段来提高效率，比如此处的购物车中的name  image  amount，都是可以通过各种id查询，但是你想想，只是打开购物车就需要多表查询岂不是降低效率？  空间换时间的思想，通过在购物车表中设计几个冗余字段，只需要查询一个购物车即可。但是冗余字段最好不要太多，然后字段本身不能是经常修改的，最好是固定值**







## Day6 



### 1.微信支付



**//微信支付时序图**

![image-20240311120809223](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240311120809223.png)















## Day7



### Spring Task



**//Spring Task  是   Spring框架提供的任务调度工具，可以按照约定的时间自动执行某个代码逻辑**

**应用场景  ：     **

- 信用卡每月还款提醒
- 中国移动话费提醒
- 火车售票系统处理未支付订单



**使用步骤**

​			**1.导入maven坐标spring-context(一般都在spring-boot-starter里面就包含了)**

​			**2.启动类添加注解 @EnableSchedualing开启任务调度**

​			**3.自定义定时任务类，使用 Cron表达式(表达式直接去网站搜，有生成器)**



**例子:**

![image-20240313185003147](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240313185003147.png)





### Websocket协议

**//相比之前用的http协议，websocket协议只需要一次握手即可建立长连接,可进行双向数据传输**

**///http协议和websocket协议 底层都是TCP连接**



#### 1.**应用场景:**

- 视频弹幕
- 网页聊天
- 体育实况更新
- 股票基金报价实时更新



#### 2.maven坐标

<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-websocket</artifactId>
</dependency>



## Day8



- 1.学习websocket
- 2.学习使用Java播放音频和视频（IO流的流畅使用）
- 3.学习使用Apache ECharts





 































































































































































































