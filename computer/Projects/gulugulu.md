



# <font color='red'>单独整理</font>

- js中的遍历  ：Object.keys(xxx).forEach( item => {})
- 将前后端通用板块 抽取成一个项目模版！
- 自定义字体ww文件 , ,  base.css文件的使用与学习, 
- **关于Bean的声明周期，可以研究一下 【也就是说你的Spring底子其实很垃圾的，有空真得好好补一下！！！！】**



![image-20241016203429129](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241016203431925.png)

![image-20241016203554759](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241016203554759.png)













# 预备



## 1.涉及技术





### 前端

1. Vue3
2. elementUI





### 后端



1. SpringBoot + Mybatis-Plus
2. Mysql + Redis
3. Netty + websocket
4. 视频流处理 ffmeg







# Plan



## 1.现在进行时

​		接下来的计划: 主要重心放在文件上传的前端页面 以及 后端代码

- 投稿的前端页面







- **退出登录** 
- **redis用户缓存到期，如何删除localStorage?????**
- **<font color='red'>多线程优化文件上传</font>**
- <font color='red'>**阿里云碎片的清除**</font>



- **滚动加载视频！！**  
- 补全redis持久化
- **完善首页轮播图**
- 学习Netty,开始研究通信







## 2.待完善的点

- banner悬浮
- **这两个界面都使用那种方式让字体 掉落到  页面**
- 按需加载elUI
- todo:短信 注册/登录
- **<font color='red'>响应式·首页</font>**







## 3.未来进行时

- 研究一下日志！！！！！！
- 设计会员模块
- **视频编码转码:视频如果不是mp4格式，使用ffmeg大文件转码**
- 协同过滤
- webrtc 直播





# 前端收获



## 一、首页制作





### 1.v-bind与图片

在 Vue 3 中，使用 `ref` 创建的变量不能直接使用字符串路径加载图片。你需要使用 `require` 或 `import` 来处理静态资源。可以这样修改你的代码：

**<font color='red'>直接使用'@/assets/img/login-register/left.png',Vue是无法识别 @的！</font>**

```
let leftimg = ref(require('@/assets/img/login-register/left.png'))
let rightimg = ref(require('@/assets/img/login-register/right.png'))
```

或者，如果你使用的是 ES 模块语法，也可以直接导入图片：

```
import leftImage from '@/assets/img/login-register/left.png';
import rightImage from '@/assets/img/login-register/right.png';

let leftimg = ref(leftImage);
let rightimg = ref(rightImage);
```









### 3.解构X响应式

- **<font color='red'>不允许解构props里面的响应式内容,除非你只是单纯的获取,而不修改</font>**

- ```
  父组件给子组件一个属性 const show = ref(true)
  子组件:
  	const props = defineProps({
  		show:{
  			type:Boolean,
  			default:false,
  		}
  	})
  	const {show} = props //这里解构就会导致失去响应式，原因不用多说吧
  ```

- ```
  解决1：
  	直接使用props.xxx
  
  解决2：computed (最佳实践)
  	const xxx = computed(()=>{p})
  ```
  
  

### 4. :style

**在Vue中，设置style属性需要通过驼峰命名法 ! **

```
:style="{ backgroundColor: img.color }"
```





### 5. flex布局

**//使用flex分配空间，需要指明高度、宽度； 如果不指明，且空间内没有具体的组件占据，则实际大小 ＜＝ 分配的空间**

```
.video-card_item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
}

.video-body {
  flex: 6.5;
  width: 100%;    //指明高度、宽度
  height: 100%;	  //指明高度、宽度
  background-color: red;
}

.video-card_footer {
  flex: 3.5;
  width: 100%;   //指明高度、宽度
  height: 100%;  //指明高度、宽度
  background-color: green
}
```

### 6. 图片溢出！

- **<font color='red'>彻底解决图片溢出问题！</font>**

- 图片溢出问题是什么

  - ```
    父盒子里有两个子盒子，使用flex布局之后，当你希望在子盒子1中放入一张图片，但图片大小超过子盒子1，导致破坏设置的flex布局
    ```

- 问题的解决:  

  - ```
    1. overflow:hidden
    子盒子1 {
      flex: 6.5;
      width: 100%;
      height: 100%;
      overflow: hidden; /* 防止内容溢出 */
    }
    
    2.子绝父相，picture和父盒子使用定位即可解决
    该思路可以解决大部分父盒子空间正确，子盒子空间过大/小的问题
    ```

- **<font color='red'>类似问题：picture标签默认不会继承父盒子的高宽，设置100%无效</font>**

- 解决

  - ```
    子绝父相，picture和父盒子使用定位即可解决
    ```

- 拓展

  - ```
    该思路可以解决大部分父盒子空间分配正确，子盒子空间过大/小的问题
    ```

    















## 二、投稿制作

### 1.获取file

- ```
  <input type="file" ref="fileInput" @change="upload" />
  
  //1.使用event获取
  const files = e.target.files[0]
  const file = files[0]
  //2.Vue3推荐使用ref
  const fileInput = ref()
  const files = fileInput.files
  const file = files[0]
  ```



### 2.@change="upload()"

**为什么加括号会立即调用一次该方法，而不是在事件触发时调用？**

答：简单一句话，一个作为事件处理器传递给Vue，一个是直接调用方法

```
@change="upload"Vue在触发的时候会自动将事件对象（$event）传入参数中，这样你就能访问原生事件的一些信息
@change="upload（）"Vue 的事件绑定机制会在事件触发时自动调用绑定的处理函数。如果你在模板中加上括号，这相当于你在模板中直接调用了 upload() 方法，而不是将 upload 方法作为事件处理器传递给 Vue。这样，upload() 会在组件渲染时立即执行一次，而不是在 change 事件发生时执行。
```



### 3.窗口关闭刷新事件

**大概就是利用window.addEventListener之类的添加删除方法**

<font color='red'> 以后慢慢研究~~~</font>

```
// onMounted(() => {
//   // 释放阿里云连接
//   window.addEventListener('beforeunload', releaseOss);
// });

// onUnmounted(() => {
//   window.removeEventListener('beforeunload', releaseOss);
// });
```



### 4. 异步与await

```
// 初始化随机视频
async function initRandomViews() {
  console.log('初始化随机视频~~~');
  // getRandomViews().then(({ data }) => {
  //   randomVideos = data;
  // });
  const { data } = await getRandomViews();
  randomVideos = data;
  console.log('初始化完毕，返回随机视频');
}


onMounted(() => {
  initCarousel();
  initRandomViews();
  console.log('我要打印数据:', randomVideos);
});
```

- **解析**

  - 顺序： 1. 初始化随机视频~ 2. 我要打印数据：[] 3. 初始化完毕，返回随机视频
  - 结论： 虽然你在执行initRandomViews()方法里面时会阻塞在 getRandomViews，但是await只会阻塞initRandomViews方法内部，而不会阻塞onMounted方法，所以在initRandomViews被阻塞的时间，onMouned的方法就会继续执行

- **正确顺序:**

- ```
  // 初始化随机视频
  async function initRandomViews() {
    console.log('初始化随机视频~~~');
    // getRandomViews().then(({ data }) => {
    //   randomVideos = data;
    // });
    const { data } = await getRandomViews();
    randomVideos = data;
    console.log('初始化完毕，返回随机视频');
  }
  
  
  onMounted(async () => {
    initCarousel();
    await initRandomViews();
    console.log('我要打印数据:', randomVideos);
  });
  ```





### 5. 解构空值

- ```
  const {data} = await getRandomViews()
  ```

- 我由于解构了一个空值导致页面直接崩溃报错

- 解决: 检查要解构的对象是否为空

  - ```
    // 初始化随机视频
    async function initRandomViews() {
      const response = await getRandomViews();
      if (response) {
        const { data } = response; // 确保 response 不是 null
      } else {
        console.log('获取随机视频返回为空');
      }
    }
    ```

  
  

### 6.v-for起始值

**<font color='red'>注意index从1开始</font>**

```
 <div class="feed_card" v-for="index in 11" :key="index">
```





### 7.同步width

- 当我在制作进度条的时候，我使用一个计算属性来实时监控获取文件上传百分比，但是当我想要将其与进度条dom对象的width
  实现同步更新，我却发现找不到优雅的方法实现

- 问题的解决：

  - 只需要一行代码即可解决

  - ```
    :style="{ width: progress + '%' }">
    ```

    

### 8. NaN

- 在js中 NaN意思是 not a number 不是一个数字
- if( number === NaN) 这样是不对的，永远都返回false
- 要使用Number.isNaN()方法来检验

































# 前端突破





## 一、首页制作





### 1.仿B站滑动图





### 2.气泡框

- **头像与气泡框同步**

  - 通过 一个boolean值控制 头像能否变大

  - ```
    <avatar :style:"{'avatar-big': isBig}"
    .avatar-big :{transition:scale(2)}
    ```

    







### 3.气泡防抖





## 二、投稿制作



### 1.文件分片上传

- **有个有趣的预热，那就是你第一次个服务器上传文件，需要网络的三次握手导致第一次比较慢，可以搞个上传预热，就是当浏览器加载的时候，偷偷给服务器发送随便一个小图片或者什么东西，先创建连接**















# 后端收获





## 1.用户模块



### ① 泛型

1. **类的泛型**：`Result<T>` 定义了类的类型参数 `T`，用于实例化时指定数据类型。
2. **方法的泛型**：`public static <T> Result<T> error(int code, String msg)` 中的 `<T>` 定义了方法的类型参数 `T`。这允许这个方法返回 `Result` 类型的对象，仍然保持类型的灵活性。

如果你在方法中不加 `<T>`，而直接返回 `Result<T>`，则编译器会认为你是在使用类中的 `T`，但如果方法本身不接受或不使用 `T`，编译器就会产生错误。

所以，方法中的 `<T>` 声明是必要的，它使得这个方法可以返回 `Result<T>` 类型的对象，并且能够与类中的泛型保持一致。如果没有它，你就无法在方法内部明确指定返回的 `Result` 对象的类型。



### ② salt加密



### ③MySql自动更新时间



- **<font color='red'>问题：</font>Mysql设置createTime和updateTime，时区与中国不匹配的问题**

- **<font color='red'>解决方案</font>：修改时区**
- 遗留的问题：为什么我修改docker里面的mysql的挂载文件 没有效果呢？

```
url: jdbc:mysql://43.134.97.111/gulugulu?useSSL=false&serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf8
serverTimezone=Asia/Shanghai	这个是中国的时区  UTC是全体统一时区，默认比中国慢8h
```





### ④static声明

- 实例级别：只有一个实例，可以被所有引用者访问或操作
- 类级别：有无数个实例,每一个类级别实例对象的属性方法互不相干
- 线程级别：每个线程都有自己独立的数据副本，常见的比如 ThreadLocal<>()

```
    public static final ThreadLocal<UserVo> tl = new ThreadLocal<>();

    public static void setUser(UserVo userVo) {
        tl.set(userVo);
    }为什么加入static final , tl 才能在方法中使用


使用 static final 声明 ThreadLocal<UserVo> tl 的原因如下：

static： tl 本身是线程级别的,每一个线程的ThreadLocal都是新的，需要static声明,这样所有线程都可以访问同一个 ThreadLocal 实例.

final：确保 tl 的引用在初始化后不可改变，增强了代码的安全性和可读性。其他地方不能重新赋值 tl，避免误用。

通过这种方式，setUser() 方法可以直接访问 tl，并且在整个类中都可以使用，保持了代码的清晰性和一致性。
```

### ⑤构造器注入

**<font color='red'>应用启动过程</font>**

- **ApplicationContext 初始化**
- **配置类加载 **: 所有标注了 `@Configuration` 的配置类会被扫描和加载
- **Bean 创建** : 在加载配置类时，Spring 会调用其中的方法来创建和注册所有的 Bean，包括拦截器。此时，任何通过 `@Bean` 注解或其他方式定义的 Bean（如 `StringRedisTemplate`）都会被实例化。
- **InterceptorRegistry 注册** : 注册拦截器



```
public class RefreshTokenInterceptor implements HandlerInterceptor {
	
	//构造器注入，防止空指针
    private final StringRedisTemplate stringRedisTemplate;
    public RefreshTokenInterceptor(StringRedisTemplate stringRedisTemplate) {
        this.stringRedisTemplate = stringRedisTemplate;
    }

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
		//一些逻辑
		return true;
    }
}
```





## 2.投稿模块



### ① try()妙用

- 利用try()可以实现 自动关闭，释放资源，不需要你手动channel.close()了,可以减少资源泄露的风险。

```
try(FileOutputStream fos = new FileOutputStream(targetPath);
             FileChannel destChannel = fos.getChannel() ){
	//逻辑
}catch{}
```



### ② HTTP状态码

**误打误撞，明白了如何使用HTTP状态码**

```
    @PostMapping("/chunk")
    public ResponseEntity<Result> upload(@ModelAttribute("formData") ChunkVo chunkVo) {
        Result result = uploadService.uploadChunk(chunkVo);
        if (result.getCode() == ErrorConstant.ErrorEnum.UPLOADS_FAIL_MERGEFILE.getCode()) {
            return ResponseEntity.status(HttpStatus.NOT_FOUND).body(result);
        }
        return ResponseEntity.status(HttpStatus.OK).body(result);
    }
```





### ③捕获自定义错误获取信息

<font color='red'>在分片合并失败时，我需要获取所有失败分片的id集合，可以在异常处抛出自定义错误，在外面捕获其携带的数据</font>



### ④@Bean(destroyMethod = "shutdown")

**<font color='red'>使用阿里云连接的时候，我在苦恼如何在正确的时机释放连接，原来还有如此便捷的方法释放连接</font>**

大概思路就是在bean被销毁之前会找bean自身是否带有shutdown方法，若有则调用.







### ⑤ 新Bean

**<font color='red'>当你想要获取一个新的Bean，比如AliOssUtil里面的ossClient每一次要求是新连接，如何实现每一个请求都获取一个全新的Bean呢？</font>**



**目前找到的一个解法:  **
**前提： 1. Bean必须多例**

```
@Resource
private ApplicationContext applicationContext;

 OSS ossClient = applicationContext.getBean(OSS.class);
```













# 后端突破

## 1.视频分片上传



### 1.1 概要

- 介绍

  - ```
    在Web应用程序中，文件上传是比较常见的功能。但是，如果要上传大文件，则可能会出现上传时间过长、网络中断等问题，因此需要实现文件`分片上传`和`断点续传`功能。
    ```

- 思路

  - ```
    1.客户端将文件分成若干个数据块
    2.客户端将每个数据块上传到服务器，并记录每个小块的顺序和信息
    3.服务端获取数据块，将其保存到临时目录中，并最终根据小块的顺序和信息，将小块合并成完整的视频文件。
    4.服务端将合并后的视频文件保存到本地/云服务器中
    4.上传过程中，发生网络中断等错误时，可以恢复上传，并继续从中断的地方继续上传
    ```

- 用到的技术

  - ```
    
    ```

    



### 1.2 疑惑？

- **<font color='red'>前端分片 VS  后端分片</font>**

  - ```
    1.提高用户体验：前端分片可以在用户上传时显示进度，让用户清楚上传状态。
    2.处理网络问题：如果上传过程中出现问题，前端可以重传失败的分片，而不需要给后端重新上传整个文件。
    3.减轻后端负担：后端只需接收和存储分片，减少了需要处理的逻辑。
    ```

    

- **<font color='red'>本地 VS 服务器</font>**

  - **两种肯定都需要去实现，**

  - ```
    本地：
    	优点：
    		访问速度快
    		数据安全性高，不依赖于外部网络。
    		适合小规模、低频使用的场景。
    	缺点：
    		存储空间有限，容易耗尽。
            数据备份和恢复困难，丢失风险较大。
            难以实现共享和远程访问。
    远程服务器
    	优点：	
    		扩展性强，可以根据需求随时增加存储空间。
            数据备份和恢复相对简单。
            适合大型场景
        缺点：
        	成本高；受网络带宽限制，访问速度慢
    ```

    

### 1.3 实现

**<font color='orange'>没什么难点，熟悉File和NIO的操作即可</font>**

- ```
  1.上传单个视频分片,保存到本地
  
  2.文件合并
  
  3.清除临时分片存储目录
  
  4.断点重传 
  ```
  
  











































































































































































































































































































