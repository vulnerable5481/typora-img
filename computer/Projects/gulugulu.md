



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



- **视频详情页   --->   消息    ---->     个人空间       ---->     个人主页**



- 完善投稿模块
- 学习



- **重构前端知识点**
- **整理本文档中的知识点    尤其是promise**
- 补全redis持久化   与    docker相关的知识   复习之前的知识点







- **redis用户缓存到期，如何删除localStorage?????  应该是pub sub 发布订阅之类的**

- **滚动加载视频！！**  
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
- **复习js高级**
- 还可以制作折线图什么的，用来显示视频数据，嗯嗯，这个应该会用到一些没怎么碰过的东西





- 





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


- **又学会一招，可以给父盒子设置max，达到限定子盒子图片的效果**

```
.crop-left-img-box {
  position: relative;
  padding: 32px;
  align-self: center;
  max-height: 298px;
  max-width: 530px;
  border-radius: 4px;
  text-align: center;
}

.crop-left-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}
```









### 7. 解决模版空值

```
<source :src="randomVideos[index - 1]?.url" type="video/mp4" />
```

如果randomVideos[x]是空怎么办？前端页面就会一直报错，解决方法就是加一个?

通过?就可以防止前段一直报错了！

为什么呢？？？？



### 8. 封面与播放

- 有一个问题，当我实现视频预览效果时，发现重置视频会导致封面又变成了视频第一帧，为此我决定将封面单独拿出来放到视频上方
  这就使得由于封面的存在我的鼠标无法反馈到视频，从而无法触发视频播放

- 问题的解决：通过下面的css属性禁用鼠标事件，从而实现穿透的效果

- ```
  pointer-events: none; /* 禁用鼠标事件 */
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



**接着讲讲 Promise**

```
console.log('Start');

let promise = new Promise((resolve, reject) => {
  console.log('Inside Promise');
  resolve('Resolved!');
});

promise.then((value) => {
  console.log('Then:', value);
});

console.log('End');
```

```
结果： 
    Start
    Inside Promise
    End
    Then: Resolved!
```

```
1.解释：
执行流程：
console.log('Start') 执行，输出 "Start"。
new Promise 被创建，resolve('Resolved!') 被调用。
resolve 并不会立即执行 .then() 中的回调，而是将它放入微任务队列。
当前同步代码执行完毕后，事件循环会开始执行微任务队列中的回调。即 .then() 中的回调会在控制台输出 "Then: Resolved!"。
最后，console.log('End') 执行，输出 "End"。

2.小结:
resolve 实现异步是因为：
    当 resolve 被调用时，Promise 会把其处理结果（value）传递给 then 的回调函数。
    然而，回调函数并不会立即执行，而是被放入微任务队列，待当前执行栈（同步任务）执行完毕后才开始执行。
    这种机制使得 Promise 能够在当前代码执行完毕后异步处理回调，避免了同步阻塞，保证了异步操作的顺序执行。
```



// 梳理一下 这三者的关系







### 6.v-for起始值

**<font color='red'>注意index从1开始</font>**

```
 <div class="feed_card" v-for="index in 11" :key="index">
```





### 8. NaN

- 在js中 NaN意思是 not a number 不是一个数字
- if( number === NaN) 这样是不对的，永远都返回false
- 要使用Number.isNaN()方法





### 9. video的事件

关于addEventListener 事件监听器之类的

还有 document.createElement() **关于js我学的非常不扎实,有空得好好补习**

video是触发事件流程 自己多学习学习



### 10.promise运用

**关于这行代码resolve(url); 为什么要放在seeked事件监听器里面，我想讲几句~~~~**

```
1.首先说明结论：如果不放在seeked事件监听器里面，放在函数最后，这样是无法获取到url的
2.使用promise的原因: loadedmetadata和seeked都是异步函数,如果单纯正常返回url，肯定不行
3.为什么需要放在seeked里面 ： 你想，url什么时候返回？肯定得是正确加载到目标帧后，canvas.toDataURL是同步函数，生成url
  在seeked外面，因为seeked是异步所以跳过直接就返回url了；
  在seeked里面，因为只有完成了seeked函数,promise才算完成，才会调用resolve返回url
```

```
// 生成视频帧图片
function getVideoBase64(time) {
  let url = '';
  const canvas = canvasRef.value;
  const video = videoRef.value;

  video.crossOrigin = 'anonymous'; // 设置跨域 【声明在赋值url之前】
  const ctx = canvas.getContext('2d'); // 获取canvas的2D绘图上下文
  video.muted = true; // 静音操作，防止声音破坏用户体验

  return new Promise((resolve, reject) => {
    // 等待视频元数据加载完成
    video.addEventListener('loadedmetadata', () => {
      // 视频跳转到目标帧
      video.currentTime = time;
    });

    // 等待视频跳转到指定时间点
    video.addEventListener('seeked', () => {
      // 视频帧绘制到canvas
      ctx.drawImage(video, 0, 0, video.videoWidth, video.videoHeight);
      // 生成 视频帧图片url
      url = canvas.toDataURL('image/jpeg');
      //返回 url
      resolve(url);
    });
  });
}
```





### 11. **Vue 响应式更新是异步的**

```
1. 问题是什么：上传文件函数中有先通过一个boolean值，将局部页面换成上传页面，然后触发initCover(file)初始化视频封面的方法，但是报错了，因为const video = videoRef.value 中的videoRef.value是undefined，我百思不得其解
2. 问题的产生：
	Vue 的响应式系统是基于异步更新的，修改 `isEdited.value` 会被 Vue 批量处理，确保多个数据更新不会触发多次渲染。为了提高性能，Vue 会把所有的响应式数据变化（例如你修改 `isEdited`）放入队列中，然后在下一个“事件循环”周期（即下一个宏任务）才执行。也就是说，你修改 `isEdited` 后，马上调用 `initCover(file)`，但是此时 `isEdited` 并没有即时生效，所以 `initCover` 还是根据旧的状态执行。
3. 问题的解决: 
  // 切换内嵌页
  isEdited.value = true;

  // 初始化视频封面
  nextTick(() => {
    initCover(file);
  });
```



### 13.生成标签

```
//在 JavaScript 中，string.trim() 的作用是去除字符串开头和结尾的空白字符，但不会去除字符串中间的空白。
```

```
//在 JavaScript 中，concat 是一个用于连接数组或字符串的方法。注意：需要被一个参数接收
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let result = arr1.concat(arr2);
console.log(result); // 输出: [1, 2, 3, 4, 5, 6]
```

```
//在 JavaScript 中，split 方法用于将一个字符串分割成子字符串数组。它通过指定的分隔符来确定分割的位置。
```

```
有空可以去了解一下js中关于数组字符串的类似stream流的map,filter之类的操作
```





### 14. event

一种比较优雅的获取event的方式

```
@mousedown="(e)=>startResize('rt', e)"
```





### 15. 摁住鼠标左键

- 用于取消摁住鼠标左键导致盒子被包裹的问题

```
user-select: none; /* 禁止选择 */
```

- 用于取消拖拽图片


```
<img draggable="false" >
```





## 三、视频详情页

### 1.监听页面可见性

- handleVisibilitychange该事件可以监听**页面不可见(切换到后台)**; 不可以监听 页面缩小和页面关闭

```
// 监听浏览器标签页的可见性变化
function handleVisibilitychange() {
  // 关闭视频播放
  if (currentPlayingVideo) {
    pauseVideo(currentPlayingVideo);
    currentPlayingVideo = null;
  }
}

onMounted(async () => {
  initCarousel();
  // 等待初始化视频
  await initRandomViews();
  // 监听页面可见性
  document.addEventListener('visibilitychange', handleVisibilitychange);
});

onBeforeUnmount(() => {
  // 清理事件监听
  document.removeEventListener('visibilitychange', handleVisibilitychange);
});
```



### 3. input

关于input 里面可以绑定的方法以及属性，比如@input @change 里面的e 怎么用 之类的 有时间可以多去了解诶



### 4.文本换行

今天说一种简单的方法：给展示文本框内容的页面标签添加以下的style即可!



 style= 
 "white-space: pre-wrap;" 

下面我们复习一下white-space 的属性设置：


normal	默认。空白会被浏览器忽略。
pre	空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。
nowrap	文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。
pre-wrap	保留空白符序列，但是正常地进行换行。
pre-line	合并空白符序列，但是保留换行符。
inherit	规定应该从父元素继承 white-space 属性的值。





### 5.hole

**关于v-for的index的一个坑**

```
在 HTML 中，id 是一个全局唯一的标识符。如果你将 id="index" 用在多个元素上，可能会导致 HTML 中有多个相同的 id 值，这是不符合规范的。因此，应该避免在 v-for 循环中使用相同的 id 值。
```





### 6. 隐藏v-for的第一个元素

- **<font color='red'>直接通过  .slice()方法，这个方法可以切割字符串，也可以切割数组</font>**
  - .slice(1)就是跳过下标0，直接从下标1开始,以此类推，就可以自由选择范围去展示 ！

```
<div class="comment-item2" v-for="(commentChild, index) in comment.children.slice(1)" :id="'commentChild-' + index">
```



### 7. 获取子组件的ref.value

```
如果直接获取貌似是不行的，但是可以暴露一个方法，方法里面返回就可以了

defineExpose({
  getVideoRefValue() {
    return videoRef.value; 
  },
});

```



### 8. 计算属性中ref未加载

**注意，在计算属性中ref刚开始是没有加载出来的**

```
const trails = computed(() => {
  if (videoRef.value) {
    return videoRef.value.videoHeight / trailHeight;
  }
  return 0; // 如果 videoRef 还没有初始化，返回一个默认值
});
```



### 9. js中连续判断

**必须拆分成两部分去写**

```
if( a <= x <= b) 是错误的
这样在js中会被解释成  a<=x 得到一个boolean   进而变成了 boolean<= n 会得到意外的错误
```



### 10. js中的宽高

// 有空可以总结一下js中所有表示宽高的api

```
      const danmuWidth = lastDanmu.clientWidth; // 弹幕长度
      // 弹幕距离左边的距离 (注意这里有个坑：此处计算的距离其实是dom元素被创建时距离左边的距离，没有考虑到动画的translateX())
      // const leftDistance = lastDanmu.offsetLeft;
      const leftDistance = lastDanmu.getBoundingClientRect().left; // 弹幕距离左边的距离 (这个方法就考虑到了动画等因素的影响)
```



### 11. 自定义属性

**// 在我研究如何可以更加流程地设计全屏与未全屏的弹幕滚动动画时，我找到了一个不错的解法**

可以利用calc 、var 和 自定义CSS属性来解决

```
      // 设置动画
      danmuElement.style.setProperty('animation-duration', `10s`);
      danmuElement.style.setProperty('--video-width', `${trackWidth}px`);
      
      /* 滚动的动画 */
@keyframes danmuLeftToRight {
  0% {
    transform: translateX(var(--video-width)); /* 从右侧开始 */
  }
  100% {
    transform: translateX(calc(-1 * var(--video-width))); /* 向左移动，离开视口 */
  }
}
```





### 12. dom渲染

**关键在于 **浏览器的渲染机制和样式计算

```
在 JavaScript 中，当你修改 DOM 元素的样式时，浏览器并不会立即重新计算样式和重新渲染页面。浏览器的渲染是一个异步过程，它会合并多个样式更新操作，然后在下一个绘制周期中一起进行更新。

在你的原始代码中，当你在暂停视频时立即设置 animation-play-state，可能浏览器尚未完成 DOM 更新或样式计算，因此，样式的更新可能没有立刻生效。由于动画的 animation-play-state 是通过计算样式来控制的，它的更新并不总是即时的，可能会在浏览器的下一次渲染周期内生效。

解决：Vue框架中可以使用nextTick()，原生js中可以使用setTimeOut(()->{},0)推迟到下一个事件循环执行
```



## 四、 消息中心



### 1、填充剩余空间

当你有一个大盒子，里面有上下两个小盒子，此时上盒子已经填充完毕，如何让下盒子自动填充剩余空间？

**思路：**

1. 通过calc()计算   （有时候不太行）
2. flex-grow:1
3. flex:1 flex 2 分配

```
答：  大盒子:{
	display:flex;
	flex-description:column;
}
	上盒子:{
	width:100%;
	height:30px;
}
	 下盒子:{
	  width: 100%;
  		flex-grow: 1;	  /* 让 下盒子填充剩余空间 */
}
```




























# 前端突破





## 一、首页制作





### 1.仿B站滑动图









### 3.气泡防抖





## 二、投稿制作



### 1.文件分片上传

- **有个有趣的预热，那就是你第一次个服务器上传文件，需要网络的三次握手导致第一次比较慢，可以搞个上传预热，就是当浏览器加载的时候，偷偷给服务器发送随便一个小图片或者什么东西，先创建连接**



### 2. 视频帧图片





### 3.裁剪框



## 三、视频详情页

### 1.自定义video

```
直接用原生的Video标签，取消原生的样式即可获得一个自定义video,想怎么改就怎么改！
```





### 2. 全屏

- 实现全屏：通过一些自带的api即可

  - **<font color='red'>元素可以直接调用api实现全屏,注意api是异步的</font>** `videoElement` 用于请求进入全屏  ;   你想要让哪个元素进入全屏，就应该对该元素调用相应的方法

  -  **<font color='red'>document VS xxElement :</font>**   `document` 用于退出全屏  ;   当你退出全屏时，应该使用 `document` 对象来退出全屏，因为退出全屏是针对整个浏览器窗口的，而不是某个特定的元素。

  - <font color='red'>**如何控制全屏后的样式：**</font> 结构一般都是player-> video && controls  ；我们不让Video全屏，我们让palyer元素全屏不就好了！

  -  **<font color='red'>是否全屏:</font>**  浏览器提供了一个标准属性 `document.fullscreenElement`，它会返回当前全屏显示的元素。如果不是全屏状态，它将返回null

  - ```
    // 控制全屏
    function changeFullScreen() {
      const guluPlayerElement = guluPlayer.value;
    
      // 检查当前是否是全屏模式
      if (!document.fullscreenElement && !document.webkitFullscreenElement && !document.mozFullScreenElement && !document.msFullscreenElement) {
        // 如果当前不是全屏，进入全屏
        if (guluPlayerElement.requestFullscreen) {
          guluPlayerElement.requestFullscreen(); // 标准浏览器方法
        } else if (guluPlayerElement.mozRequestFullScreen) {
          guluPlayerElement.mozRequestFullScreen(); // Firefox
        } else if (guluPlayerElement.webkitRequestFullscreen) {
          guluPlayerElement.webkitRequestFullscreen(); // Chrome, Safari 和 Opera
        } else if (guluPlayerElement.msRequestFullscreen) {
          guluPlayerElement.msRequestFullscreen(); // IE/Edge
        }
      } else {
        // 如果当前是全屏，退出全屏
        if (document.exitFullscreen) {
          document.exitFullscreen(); // 标准浏览器方法
        } else if (document.mozCancelFullScreen) {
          document.mozCancelFullScreen(); // Firefox
        } else if (document.webkitExitFullscreen) {
          document.webkitExitFullscreen(); // Chrome, Safari 和 Opera
        } else if (document.msExitFullscreen) {
          document.msExitFullscreen(); // IE/Edge
        }
      }
    }
    ```

- 如何隐藏全屏后的样式:

  - ```
    /* 隐藏全屏后的样式 */
    video::-webkit-media-controls {
      display: none; /* 隐藏所有浏览器默认控件 */
    }
    ```

    

















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



**目前找到的一个解法:  ** 利用ApplicationContext
**前提： 1. Bean必须多例**

```
@Resource
private ApplicationContext applicationContext;

 OSS ossClient = applicationContext.getBean(OSS.class);
```



### ⑥ 接收数据

![image-20241120203448669](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241120203448669.png)









# 后端突破

## 1.视频分片上传













































































































































































































































































































