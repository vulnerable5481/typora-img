# 手动实现第一个全栈项目！！







# 1.jwt



### 1.历史

#### **早期的cookie-session 认证方式**

早期互联网以 web 为主，客户端是浏览器 ，所以 Cookie-Session 方式是早期最常用的认证方式，直到现在，一些 web 网站依然用这种方式做认证。

**认证过程大致如下：**

1. 用户输入用户名、密码或者用短信验证码方式登录系统；
2. 服务端验证后，创建一个 Session 信息，并且将 SessionID 存到 cookie，发送回浏览器；
3. 下次客户端再发起请求，自动带上 cookie 信息，服务端通过 cookie 获取 Session 信息进行校验；

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X2pwZy9pYVdTRG80VGZ5WmdoR05TUTVOWTZWWlU5Y0hBaWNFQ3RUalBScUh5Q1lhSW83a3BqMmdma2FVR2dHWThNRlBYOTJ4UzVUMm84eExZUmRwb3VrWFB1aWNjZy82NDA?x-oss-process=image/format,png)

#### **传统方式的弊端**：

​									   1.**cookie-session认证只能在web场景下使用,**如果是app呢，app就没有cookie,现在的产品有的甚至只有app没有web场景.

​								  2.**cookie不能跨域问题**。拿天猫商城来说，当你进入天猫商城后，会看到顶部有天猫超市、天猫国际、天猫会员这些菜单。而点击这些菜单都会进入不同的域名，不同的域名下的 cookie 都是不一样的，你在 A 域名下是没办法拿到 B 域名的 cookie 的，即使是子域也不行。

​									3.如果是分布式服务，需要考虑 **Session 同步问题**。现在的互联网网站和 APP 基本上都是分布式部署，也就是服务端不止一台机器。当某个用户在页面上进行登录操作后，这个登录动作必定是请求到了其中某一台服务器上。你的身份信息得保存下来吧，传统方式就是存 Session。

接下来，问题来了。你访问了几个页面，这时，有个请求经过负载均衡，路由到了另外一台服务器（不是你登录的那台）。当后台接到请求后，要检查用户身份信息和权限，于是接口开始从从 Session 中获取用户信息。但是，这台服务器不是当时登录的那台，并没存你的 Session ，这样后台服务就认为你是一个非登录的用户，也就不能给你返回数据了。

所以，为了避免这种情况的发生，就要做 Session 同步。一台服务器接收到登录请求后，在当前服务器保存 Session 后，也要向其他几个服务器同步。

​									4.**cookie 存在 CSRF（跨站请求伪造）的风险。**跨站请求伪造，是一种挟制用户在当前已登录的Web应用程序上执行非本意的操作的攻击方法。CSRF 利用的是网站对用户网页浏览器的信任。简单地说，是攻击者通过一些技术手段欺骗用户的浏览器去访问一个自己曾经认证过的网站并运行一些操作（比如购买商品）。由于浏览器曾经认证过，所以被访问的网站会认为是真正的用户发起的操作。



#### Cookie-Session 改造版

由于传统的 Cookie-Session 认证存在诸多问题，那可以把上面的方案改造一下。1、改造 Cookie 既然 Cookie 不能在 APP 等非浏览器中使用，那就不用 cookie 做客户端存储，改用其他方式。改成什么呢？web 中可以使用 local storage，APP 中使用客户端数据库，这样既能这样就实现了跨域，并且避免了 CSRF 。

2、服务端也不存 Session 了，把 Session 信息拿出来存到 Redis 等内存数据库中，这样即提高了速度，又避免了 Session 同步问题；

经过改造之后变成了如下的认证过程：

1. 用户输入用户名、密码或者用短信验证码方式登录系统；
2. 服务端经过验证，将认证信息构造好的数据结构存储到 Redis 中，并将 key 值返回给客户端；
3. 客户端拿到返回的 key，存储到  local storage 或本地数据库；
4. 下次客户端再次请求，把 key 值附加到 header 或者 请求体中；
5. 服务端根据获取的 key，到 Redis 中获取认证信息；



#### **JWT 出场**

这时，JWT 就可以上场了，**JWT 就是一种Cookie-Session改造版的具体实现**，让你**省去自己造轮子的时间**，JWT 还有个好处，那就是你可以不用在服务端存储认证信息（比如 token），**完全由客户端提供**，**服务端只要根据 JWT 自身提供的解密算法就可以验证用户合法性，而且这个过程是安全的。//想一想jwt的数据结构中的签名你就知道怎么一回事了!**



​				

### 2.介绍



```
JSON Web Token（JSON Web令牌）
```

```
是一个开放标准(rfc7519)，它定义了一种紧凑的、自包含的方式，用于在各方之间以JSON对象安全地传输信息。此信息可以验证和信任，因为它是数字签名的。jwt可以使用秘密〈使用HNAC算法）或使用RSA或ECDSA的公钥/私钥对进行签名。
```

```
通过JSON形式作为Web应用中的令牌，用于在各方之间安全地将信息作为JSON对象传输。在数据传输过程中还可以完成数据加密、签名等相关处理。
```



#### **JWT作用：**

**授权**：一旦用户登录，每个后续请求将包括JWT，从而允许用户访问该令牌允许的路由，服务和资源。它的开销很小并且可以在不同的域中使用。如：单点登录。
**信息交换**：在各方之间安全地传输信息。JWT可进行签名（如使用公钥/私钥对)，因此可确保发件人。由于签名是使用标头和有效负载计算的，因此还可验证内容是否被篡改。



#### JWT的数据结构



**头部**

头部以 JSON 格式表示，用于指明令牌类型和加密算法。形式如下，表示使用 JWT 格式，加密算法采用 HS256，这是最常用的算法，除此之外还有很多其他的。

```go
{



  "alg": "HS256",



  "typ": "JWT"



}
```

对应上图的红色 header 部分，需要 Base64 编码。

**载荷**

用来存储服务器需要的数据，比如用户信息，例如姓名、性别、年龄等，要注意的是重要的机密信息最好不要放到这里，比如密码等。

```go
{



  "name": "古时的风筝",



  "introduce": "英俊潇洒"



}
```

另外，JWT 还规定了 7 个字段供开发者选用。

- iss (issuer)：签发人
- exp (expiration time)：过期时间
- sub (subject)：主题
- aud (audience)：受众
- nbf (Not Before)：生效时间
- iat (Issued At)：签发时间
- jti (JWT ID)：编号

这部分信息也是要用 Base64 编码的。



**签名**

签名有一个计算公式。

```go
各个签名计算公式基本都是通过 header 和  playload 计算出来的
```





### 3.使用方式

1、在用户登录网站的时候，需要输入用户名、密码或者短信验证的方式登录，登录请求到达服务端的时候，服务端对账号、密码进行验证，然后计算出 JWT 字符串，返回给客户端。

2、客户端拿到这个 JWT 字符串后，存储到 cookie 或者 浏览器的 LocalStorage 中。

3、再次发送请求，比如请求用户设置页面的时候，在 HTTP 请求头中加入 JWT 字符串，或者直接放到请求主体中。

4、服务端拿到这串 JWT 字符串后，使用 base64的头部和 base64 的载荷部分，通过`HMACSHA256`算法计算签名部分，比较计算结果和传来的签名部分是否一致，如果一致，说明此次请求没有问题，如果不一致，说明请求过期或者是非法请求。



### 4.实际例子



```
/*
* jwt  工具类
* */
public class JwtUtils {

    public static final String SIGNATURE = "weofjwiejf";

    /*
    * 生成JWT
    * token  包含  header,payload,signature
    * */

    public static String createJWT(Map<String,String> map){

        // JWT头部分信息【Header】
        Map<String, Object> header = new HashMap<>();
        header.put("alg", "HS256");
        header.put("typ", "JWT");

        // 载核【Payload】
        Map<String, Object> payload = new HashMap<>();
        payload.put("sub", "1234567890");
        payload.put("username",map.get("username"));
        payload.put("admin",true);

        // 声明Token失效时间
        Calendar instance = Calendar.getInstance();
        instance.add(Calendar.SECOND,300);// 300s

        // 创建jwt密匙
        SecretKey key = Keys.secretKeyFor(SignatureAlgorithm.HS256);

        String token = Jwts.builder()
                .setHeader(header)//  默认会自动设置，所以一般不用主动去设置
                .setClaims(payload)// 声明，有效载荷
                .setExpiration(instance.getTime())//设置过期时间
                .signWith(key)//签名,这里采用私钥进行签名,不要泄露了自己的私钥信息
                .compact();//压缩成 xx.xx.xx

        return token;
    }

    /*
    *   解密token
    *  获取token中的 playload
    * */
    public static Claims parseToken(String token){
           return Jwts.parserBuilder().setSigningKey(SIGNATURE).build().parseClaimsJws(token).getBody();
    }

}
```



```
@Slf4j
public class JwtTokenAdminInterceptor implements HandlerInterceptor {

    /*
    * 判断jwt令牌是否有效
    * */
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

        //令牌建议是放在请求头中，获取请求头中令牌
        String token = request.getHeader("token");

        try {
            log.info("jwt验证:{}",token);
            Claims claims = JwtUtils.parseToken(token);
            return true;//放行请求
        } catch (Exception e) {
            e.printStackTrace();
        }
        //如果解密token中有错误 直接打回处理
        return false;
    }
}
```

```
//用户登录
@RequestMapping(value = "/login",method = RequestMethod.POST)
public String login(HttpServletResponse response , @RequestParam Map<String,Object> map){
    log.info("登录用户名：{}",map.get("username"));

    String username = map.get("username").toString();
    if(username == null || "".equals(username)){
        return "error";//返回一个莫须有的  错误界面
    }

    //登录成功后，生成JWT
    HashMap<String, String> payload = new HashMap<>();
    payload.put("username",map.get("username").toString());
    payload.put("age",map.get("age").toString());
    payload.put("address",map.get("address").toString());
    String token = JwtUtils.createJWT(payload);
    
    //将生成的token 添加到请求头中
    response.addHeader("Access-Control-Expose-Headers","token");
    response.addHeader("token",token);

    return "/html/crud/insert.html";
}
```





### 5.一个问题

JWT 有个问题，导致很多开发团队放弃使用它，那就是一旦颁发一个 JWT 令牌，服务端就没办法废弃掉它，除非等到它自身过期。有很多应用默认只允许最新登录的一个客户端正常使用，不允许多端登录，JWT 就没办法做到，因为颁发了新令牌，但是老的令牌在过期前仍然可用。这种情况下，就需要服务端增加相应的逻辑。











# 2.可实现功能



## 1.登录功能

使用jwt,写个拦截器实现hanlerxxx，配置拦截器webconfig

可以考虑责任链模式什么的

搞个多重拦截器



## 2.签到功能

利用redis的bitmap很简单的就可以实现





## 3.地理位置排序⭐

具体实现还得学习es





## 4.秒杀券



## 5.Feed流实现关注推送⭐



## 6.Alioss实现文件上传下载/本地文件实现上传下载



## 7.websocket实现在线互聊⭐



## 8.









