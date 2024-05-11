# 一.前端三板斧



## 1.HTML

​	



### 1.1总结⭐

直接去看这个

https://blog.csdn.net/weixin_43461520/article/details/110143997

```
//1.文本格式化标签
		加粗：<strong> </strong>或者<b> </b>

        倾斜：<em> </em>或者<i> </i>

        删除线：<del> </del>或者<s> </s>

        下划线：<ins> </ins>或者<u> </u>
//2.段落标签
	<P></P>
//3.盒子标签
	<div></div>是大盒子，一行只能放一个大盒子;
	<span></span>是小盒子，一行可以放多个

//4.图片标签
		<img src="xxxxxx" 属性2="xxxxxx">  
alt	文本	替换文本。图像不能显示的文字
title	文本	提示文本。鼠标放到图像上，显示的文字
width	像素	设置图像的宽度
height	像素	设置图像的高度
border	像素	设置图像的边框粗

//5.超链接标签
	< a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
	
//6.表格标签
<table></tabe>是用于定义表格的标签。

<tr></tr>标签用于定义表格中的行,必须嵌套在< table></ table>标签中

<td></td>用于定义表格中的单元格，必须嵌套在< tr></ tr>标签中

<th></th>表示表格的表头部分，表示表格的第一行或第一列，其中的文本内容加粗居中显示

<thead></thead>用于定义表格的头部。< thead>内部必须拥有< tr>标签，一般是位于第一行

<tbody></tbody>用于定义表格的主体，主要用于放数据本体。

align	left、center、right	规定表格相对周围元素的对齐方式
border	1 或 “”	规定表格单元是否拥有边框，默认为“”，表示没有边框
cellpadding	像素值	规定单元边沿与其内容之间的空白,默认1像素
cellspacing	像素值	规定单元格之间的空白，默认2像素
width	像素值或百分比	规定表格的宽度
height	像素值或百分比	规定表格的高度
rowspan	要合并的单元格个数	合并行单元格，记得要删除多余的单元格
colspan	要合并的单元格个数	合并列单元格，记得要删除多余的单元格


```













### 1.2 table 

![image-20240314164001972](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314164001972.png)



### 1.3 有序无序 自定义列表

![image-20240314165105980](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314165105980.png)



⭐⭐⭐⭐⭐⭐

![image-20240314165501331](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314165501331.png)





### 1.4 input输入表单元素

![image-20240314170822396](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314170822396.png)

![image-20240314170836049](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314170836049.png)



### 1.5 lable标签

**//比如lable标签可以使鼠标点击用户名三个字就触发输入框，输入信息，就是将鼠标点击范围从单一的框变为框加文字的所在的盒子**

![image-20240314171626257](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314171626257.png)





### 1.6 select下拉表单



![image-20240314172009678](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314172009678.png)



### 1.7文本域

![image-20240314172304685](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314172304685.png)





### 1.8Element语法



![image-20240315122337048](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240315122337048.png)



![image-20240315122621491](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240315122621491.png)





## 2.CSS



### 2.0 CSS熟悉书写顺序



![image-20240326145754863](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326145754863.png)







### 2.1四种基础选择器与复合选择器与伪类选择器



![image-20240314205404290](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314205404290.png)



**复合选择器**

![image-20240318173738463](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318173738463.png)

![image-20240318174323877](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318174323877.png)

![image-20240318174919766](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318174919766.png)

![image-20240318175411067](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318175411067.png)

![image-20240325130848922](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325130848922.png)



























### 2.2 各种属性



#### 2.2.1字体属性

![image-20240319183954518](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240319183954518.png)

**//font-size 尽可能不使用默认大小，最好自己去指定大小**

**//font-family  一般不建议修改**

**//font-weight 看上面**

**//font-style italic是斜体，normal是不斜体**

​	





#### 2.2.2   文本属性



![image-20240319184324372](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240319184324372.png)

**//text-align center left/right center 三种对齐方法**

**//text-indent 可以缩进  px 也可以 em,em就是 单位字体距离**

**//text-decoration 知道underline 添加下划线 和 none 取消下划线   就ok**

**//line-height 控制行高,常用于垂直居中显示，line-height = height的高度 **    











#### 2.2.3 背景属性

![image-20240319184729040](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240319184729040.png)

 









### 2.3 CSS的元素显示模式



-  块元素:div
- 行内元素
- 行内块元素

**行内元素转换为块元素(常用！)	:**

**display:block变为块元素**   display:inline 变为行内元素 **display:inline-block 变为行内块元素**



![image-20240325141824675](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325141824675.png)

![image-20240325141840598](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325141840598.png)















### 2.4 CSS三大特性与盒子模型



- 层叠性
- 继承性
  - 子元素可以继承父元素一些样式，但是只能继承文字相关样式，但是不会继承浮动啊边框等其他元素

- 优先级
  - 权重：![image-20240327173935459](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240327173935459.png)










#### 2.5.1网页布局的本质



![image-20240325131138597](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325131138597.png)



#### 2.5.2盒子组成

![image-20240325132217249](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325132217249.png)

C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\

##### 1.Border边框

```
border:
		border-width: 5px;
		border-style: solid;（实线）  /  dashed（虚线）  / dotted （点线）
		border-color: red;
		border: 1px solid red⭐ ；没有固定顺序 
		border-collapse: collapse: 用于边框合并,常用于表格中将叠加的表格线变细
border分框写法:
		border-bottom: 1px dashed blue
```

**边框会影响盒子大小，一个200px * 200px的盒子  加上border-width: 10px 会变成一个 210px * 210px的盒子**

**//解决方法：将盒子的长宽减去边框大小，注意左右和上下要减去双倍的边框**





##### 2.padding内间距

![image-20240325134952622](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325134952622.png)

```
 padding: 5px   意思是上下左右都是5px
 padding: 5Px 10px 上下为5 左右是10px
 padding: 5px 10px 20px: 上是5 左右是10 下是20
 padding: 5px 10px 20px 30px  略
```

**padding也会影响盒子大小**

![image-20240325135714210](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325135714210.png)







##### 3.margin外边距



![image-20240325142237958](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325142237958.png)

![image-20240325144600848](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325144600848.png)

![image-20240325143809887](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325143809887.png)





![image-20240325144420339](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325144420339.png)



**外边距合并现象**

![image-20240325144959114](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325144959114.png)



![image-20240325145524886](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325145524886.png)

![image-20240325145822464](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325145822464.png)





##### 4.圆形盒子

如何将盒子模型变成一个圆？？



```
如果是一个正方形->圆形  :  border-radius:50%   数值修改为高度或宽度的一半，或者直接用50%即可
如果是个矩形   ->圆角矩形  :  border-radius:height/2   数值改为高度的一半

border-top-radius 也可以只调正一个地方的角度

border-radius: 0 0 0 0   按照顺时针角度设置

```

​	



##### 5.盒子阴影



![image-20240325184453503](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325184453503.png)



例子：   一般影子颜色推荐:   rgba(0,0,0,.3)  

![image-20240325184419127](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325184419127.png)





##### 6.文字阴影



![image-20240325184520481](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325184520481.png)





### 2.5浮动

**三种网页布局 ： 标准流，浮动，定位，开发一个页面往往三者都需要使用**



![image-20240325185923009](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325185923009.png)





![image-20240325190039125](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325190039125.png)

#### 2.6.1 浮动三特性

![image-20240326121836258](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326121836258.png)



![image-20240326121940735](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326121940735.png)





![image-20240326122357841](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326122357841.png)



![image-20240326122927859](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326122927859.png)

#### 2.6.2浮动元素与标准元素搭配使用







![image-20240326124519492](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326124519492.png)





#### 2.6.3清除浮动

![image-20240326141835582](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326141835582.png)

![image-20240326143455710](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326143455710.png)

![image-20240326142807691](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326142807691.png) 

```
overflow:hidden 
```



**//after伪类元素法（推荐）**

```
        .clearfix:after {
            content: "";
            display: block;
            height: 0;
            clear: both;
            visibility: hidden;
        }
固定这么写
直接在父类元素上面加这个

```









### 2.6定位



#### 2.8.1为什么需要定位

![image-20240330161923651](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330161923651.png)

#### 2.8.2定位组成及语法

![image-20240330162224441](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330162224441.png)



- static(了解）
  - 和普通标准流没有区别 

- relative⭐
  - 选择器 {position: relative;}
  - 特点1:总是按照原来的位置来移动，移动的参照点是自己原来的位置
  - 特点2:原来位置依然会被占有，其他盒子不会上升，**不脱标**

- absolute⭐
  - 特点1:元素在移动时，参照它祖先元素来说的
  - 特点2:如果没有父元素/父元素没有定位，就以浏览器为标准。
  - 特点3:如果父元素，爷元素都有定位，就近原则
  - 特点4: 原来位置可以被其他盒子占有    **脱标**

- fixed⭐
  - 特点1:元素不会随着页面移动而移动，以浏览器的可视串口为参照点移动元素
  - 特点2:跟父元素没有一点关系
  - 特点3:不占有原先位置 **脱标**



#### 2.8.3子绝父相

![image-20240330171833737](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330171833737.png)







#### 2.8.4 定位叠放次序

![image-20240330183200722](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330183200722.png)



#### 2.8.5定位的一些特性⭐

**//目前已知可以给行内元素设置宽度高度的方法:**

- display: block/inline-block  
- float:left;
- position: absolute / fixed

![image-20240330184511724](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330184511724.png)



浮动只会对之前的元素有影响，而且浮动只会压住下面的标准流盒子，不会压住下面标准流盒子中的文本/图片，标准流盒子中的文字/图片会被挤到一边

但是绝对定位/固定定位 会完完全全地压住盒子和盒子中所有的内容









### 2.7显示隐藏元素





![image-20240331150414524](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240331150414524.png)

![image-20240331150517629](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240331150517629.png)

![image-20240331150946186](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240331150946186.png)





















































































## 3.JavaScript



### 1.基础语法对比

#### 1.1变量

**//const 不变的是地址，因为基本类型直接存储在栈里面所以值就是地址，但是引用类型值在堆里面，指针指向堆，只要地址不变，堆里的值变无所谓，数组中的push，pop也是修改堆里的数据，地址没变，但是arr = [xxx],这样地址就变了**

![image-20240509120603382](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509120603382.png)

### 1.2 数据类型

- 布尔值
  - 空字符串 默认是 false
  - 除了空字符串其他的非布尔值全都会隐式转换成true













### 2.DOM-API	

![image-20240509121056093](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509121056093.png)

#### 2.1 操作DOM对象



- **获取DOM对象**

```
//1.返回第一个 ⭐!!!
	document.querySelector('css选择器')   和css各种选择器的写法一摸一样
//2.返回所有
	document.querySelectorAll('css选择器')   
```



- **操作DOM对象**

```
//1.修改文本内容
	xx.innerHTML = xxx       //解析标签   （推荐这个，顶多就是你不写标签呗）
	
//2.修改标签属性 
	xx.src = xxx    //直接 对象.属性 即可
	 	
//3.1直接修改样式属性 （麻烦）
	xx.style.xx    //直接 对象.style.属性 即可
	xx.style.backgroudColor   //如果涉及多个单词，使用小驼峰
//3.2追加类名 ⭐
	xx.classList.add('xx')
	xx.classList.delete('xx')
	xx.classList.toggle('xx')  切换类名
	
//4.操作表达元素
	xxx.type = 'password'
	xxx.value = 'xxx'    
	xxx.checked = true  如果是布尔值

//5.操作自定义对象 ⭐
//还真挺关键的！
	xx.dataset.xxx
```

![image-20240509140552963](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509140552963.png)





#### 2.2 定时器-间歇函数



**使用 setInterval(函数，间隔时间)**

```
setInterval(data => {
	console.log(`每隔三秒发送一次数据:${data}`)
},3000)
```

**setInterval返回的是一个 基本类型id，需要使用let接收**

```
let id = setInterval(xxx,x)
```

**关闭定时器**

```
clearInterval(id)
```



一个例子：我同意协议：原来还可以自杀啊，直接在定时器里面让其自杀

```
    let cur = 5
    let id = setInterval(()=>{
      btn.innerHTML = `我同意该协议(${--cur})`
      if(cur == 0){
        btn.disabled = false
        btn.innerHTML = `我同意该协议`
        clearInterval(id)  
      }
    },1000)
```



一个例子：图片轮播图：关于li的扩展

```
      //修改图片标题
      const title = document.querySelector('.slider-footer p')
      title.innerHTML = sliderData[i].title
      //修改图片
      const img = document.querySelector('.slider-wrapper img')
      img.src = sliderData[i].url
      //修改小圆点 (排他思想)
      document.querySelector('.slider-indicator .active').classList.remove('active')
      document.querySelector(`.slider-indicator li:nth-child(${i+1})`).classList.add('active')
```







#### 2.3 事件监听

```
xxx.addEventListener(函数)     
```

![image-20240509181304225](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509181304225.png)



#### 2.4几个重要知识



- ##### **事件对象**

**作用：可以获取事件触发时的相关信息**

**例如:鼠标点击事件，事件对象就存储了鼠标点在哪个位置等信息，可以实现点哪里哪里就出现特效**

​		**判断用户按下了哪个键，比如按下不同的键有不同的作用**



```
//1.获取事件对象
	任意事件回调函数的参数默认都是事件对象，一般使用event / e 来接收

//2.常见属性
	e.type:当前事件类型
	e.clientX/clientY:获取光标相对于浏览器可见窗口左上角的位置
	e.key: 用户按下的键盘值
	e.target.xxx: 获取触发事件的元素  比如 e.target.style = 'red' ,e.target.tagName = '元素标签名如Li,p'
```



- **环境对象**

**普通函数的this指向的是window,因为是window调用的函数**

**简单一句话，谁调用的就指向谁**



- **回调函数**

![image-20240509185605162](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509185605162.png)







#### 2.5 事件流

##### **定义**

##### **事件执行流程的流动路径**

![image-20240509212656309](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509212656309.png)



##### **捕获阶段(很少使用)**

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509212856720.png)



##### **冒泡阶段(⭐)**

![image-20240509215801602](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509215801602.png)

![image-20240509213011940](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509213011940.png)



##### **阻止冒泡**

##### 阻止默认行为

![image-20240509223306880](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240509223306880.png)





#### 2.6事件委托



##### **引出**

![image-20240509213356085](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509213356085.png)

##### **好处**

![image-20240509213459830](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509213459830.png)











#### 2.7 其他事件

##### 页面加载事件

**//一般写在head**

![image-20240509223757732](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509223757732.png)



##### 页面滚动事件⭐

**//不仅仅是window里面有，普通的事件也有**

![image-20240509224019879](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224019879.png)

​	



![image-20240509224318782](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224318782.png)

![image-20240509224517953](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224517953.png)

![image-20240509224648219](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224648219.png)



##### 页面尺寸事件

```
window.scrollTo(0,0)   跳转到顶部
```









#### 2.8 获取dom对象的html元素 

##### **获取一个盒子的宽度高度？**

![image-20240510122858166](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240510122858166.png)

```
//1. dom对象.clientWidth
	 dom对象.clientHeight
```



****





##### 获取距离页面的滚动位置

![image-20240509224318782](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224318782.png)

![image-20240510124517389](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240510124517389.png)

```
//1.不包含padding,border  ，可读可写
	使用documentElement就可以获取html元素
	const n = document.documentElement.scrollTop
	
	
//2.获取元素距离父级元素的可视化高度与宽度， 只能读
	dom对象.offsetLeft/offsetTop
```







##### 另外一个方法(了解？)

**//这个貌似一口气获得了所有的宽高属性哎**

```
dom对象.getBoudingClientRect()
```

![image-20240510132044304](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240510132044304.png)

##### 



 

##### 滚动跳转



方法一：window.scrollTo(x,y)





方法二: document.documentElement.scrollTop = xxx.offsetTop





















#### 2.9 时间函数



```
//1.const d = new Date()

//2.时间戳
	2.1 d.getTime()
	2.2 Date.now()
	2.3 +new Date()
```



#### 2.10 节点操作

![image-20240510212715023](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240510212715023.png)



- 查询节点
  - xx.parentNode
  - xx.childrien
  - xxx.nextElementSibling/previousElementSibling

- 增加节点 :演示⭐
  - const ul = document.querySelector('ul')
  - const li= document.createElement("li")
  - li.appendChild/insertBefore(li,ul.children[0])
- 克隆节点
- 删除节点
  - xx.remove(child)







#### 2.11 M端事件

**//移动端事件，主要服务于手机，平板之类的触屏事件**

**//不过用于PC端，只要你的鼠标在页面移动好像就算是触摸了！！！！！，也许以后有奇效!**

![image-20240510221650931](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240510221650931.png)







#### 2.12 Swiper插件



**//一个很强大的开源插件，只需要cv修改部分代码，就可以实现很多功能**

![image-20240510224109619](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240510224109619.png)













### 3.BOM



#### 3.1 window对象

**//实际上我们之前就接触了很多BOM相关的api，比如定时器，获取当前滚动位置；**



![image-20240511115039272](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511115039272.png)



#### 3.2 定时器-延时函数

- 延时函数仅执行一次


```
setTimeout(回调函数，等待的毫秒数)
```

- 清除延时函数

```
let timer = setTimeout(回调函数,等待毫秒数)
clearTimeout(timer)   
```











#### 3.3 JS执行机制

- 引子
  - ![image-20240511115542291](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511115542291.png)



![image-20240511115603345](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511115603345.png)

![image-20240511115732109](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511115732109.png)

![image-20240511115745875](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511115745875.png)

**//简单来说就是执行栈全部执行完就执行消息队列里的任务，消息队列执行完再取执行栈看看有无任务，以此往复循环**

![image-20240511120926321](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511120926321.png)



![image-20240511121133346](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511121133346.png)

























## 4.案例和技巧



#### 1.文字的居中



**//line-height可以实现单行文字的上下移动**

```
height: x px;
line-height: x px;  // line-height = height 可以实现垂直居中
text-align: center  //可以使单行文字居中

```

**//一个水平方向居中，一个竖直方向居中，两者结合可以实现垂直居中！！**

**//一般情况不建议 margin + padding 去实现 垂直居中**











#### 2.链接(li + a)



**//有一个细节那就是如果要浮动，我们是将float给li 还是给 a???**

**//解答：一般都是给li    ，不过看情况，灵活选择**

![image-20240330133912312](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330133912312.png)

















#### 3.盒子宽度警告



除了盒子，不要随意指定盒子内部元素的宽度,高度也有时候不需要设置







#### 4.margin:0 auto的失效

如果是块级元素/行内块级元素，使用margin: 0 auto;都会使其居中，但是如果是浮动的,float:left就会导致margin:0 auto;失效，指明margin: 10px还是可以使用，这是为什么呢？？

//解答：因为margin: 0 auto 是根据文档位置计算的，浮动使其脱离文档，导致计算公式无法计算，但是指明margin依然可以正常使用！



使用position: absolute 绝对定位也会使margin: 0 auto 失效



**//有一个小技巧解决这种绝对定位引起的失效问题:可以先走到中间(top:50%),然后往回走自身宽度的一半即可()**

**//垂直居中也是一个道理**



#### 5.固定在版心右侧位置	



![image-20240330174603275](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330174603275.png)





## 5.一些功能的实现



### 1.tab栏切换

```
<body>
  <div class="tab">
    <div class="tab-nav">
      <h3>每日特价</h3>
      <ul>
        <li><a class="active" href="javascript:;" data-id="0">精选</a></li>
        <li><a href="javascript:;" data-id="1">美食</a></li>
        <li><a href="javascript:;" data-id="2">百货</a></li>
        <li><a href="javascript:;" data-id="3">个护</a></li>
        <li><a href="javascript:;" data-id="4">预告</a></li>
      </ul>
    </div>
    <div class="tab-content">
      <div class="item active"><img src="./images/tab00.png" alt="" /></div>
      <div class="item"><img src="./images/tab01.png" alt="" /></div>
      <div class="item"><img src="./images/tab02.png" alt="" /></div>
      <div class="item"><img src="./images/tab03.png" alt="" /></div>
      <div class="item"><img src="./images/tab04.png" alt="" /></div>
    </div>
  </div>
  <script>
    //绑定事件
    document.querySelector('.tab-nav ul').addEventListener('click',function(e){
      //只要我们点击a标签 事件才触发
      if(e.target.tagName === 'A'){
        //修改a标签
        document.querySelector('.tab-nav .active').classList.remove('active')
        e.target.classList.add('active')
        //修改大盒子
        const i = +e.target.dataset.id // 隐式转换成 Number类型，避免下面的字符串 0 + 1 = 01
        document.querySelector('.tab-content .active').classList.remove('active')
        document.querySelector(`.tab-content .item:nth-child(${i+1})`).classList.add('active')
      }
    })
  </script>

</body>

</html>
```





### 2.导航栏

**如果使用透明度也可以但就不会有上下滑动的效果**

```
<body>
    <div class="header">我是顶部导航栏</div>
    <div class="content">
        <div class="sk">秒杀模块</div>
    </div>
    <div class="backtop">
        <img src="./images/close2.png" alt="">
        <a href="javascript:;"></a>
    </div>
    <script>
        document.querySelector('.header').style.top = '-80px'
        const sk = document.querySelector('.sk')
        //页面滚动事件
        window.addEventListener('scroll',function(){
            //当页面滚动到秒杀模块，就改变头部的top值
            const scrollLength = document.documentElement.scrollTop
            if(scrollLength >= sk.offsetTop && scrollLength <= (sk.offsetTop + sk.clientHeight)){
                document.querySelector('.header').style.top = 0
            }else{
                document.querySelector('.header').style.top = '-80px'
            }
        })
    </script>
</body>

</html>
```



### 3.页面滚动



```
 <!-- 电梯 -->
  <div class="xtx-elevator">
    <ul class="xtx-elevator-list">
      <li><a href="javascript:;" data-name="new">新鲜好物</a></li>
      <li><a href="javascript:;" data-name="popular">人气推荐</a></li>
      <li><a href="javascript:;" data-name="brand">热门品牌</a></li>
      <li><a href="javascript:;" data-name="topic">最新专题</a></li>
      <li><a href="javascript:;" id="backTop"><i class="sprites"></i>顶部</a></li>
    </ul>
  </div>
  <script>
    (function () {
      //1.滚动显示电梯
      const elevator = document.querySelector('.xtx-elevator')
      const entry = document.querySelector('.xtx_entry')
      window.addEventListener('scroll', function () {
        const scrollLength = document.documentElement.scrollTop
        elevator.style.opacity = scrollLength >= entry.offsetTop ? 1 : 0
      })
      //2.点击顶部跳转
      const backTop = document.querySelector('#backTop')
      backTop.addEventListener('click', function () {
        window.scrollTo(0, 0)
      })
    })();

    (function () {
      //3.电梯跳转
      const list = document.querySelector('.xtx-elevator-list')
      list.addEventListener('click', function (e) {
        if (e.target.tagName === 'A') {
          //排他思想
          const old = document.querySelector('.xtx-elevator-list .active')
          if (old) {
            old.classList.remove('active')
          }
          //添加active
          e.target.classList.add('active')
          //跳转
          const go = document.querySelector('.xtx_goods_' + e.target.dataset.name)
          document.documentElement.scrollTop = go.offsetTop
        }
      })
    })();


    (function () {
      //4.滚到哪里，哪里高亮
      const list = document.querySelector('.xtx-elevator-list')
      window.addEventListener('scroll', function (e) {
        //排他思想
        const old = document.querySelector('.xtx-elevator-list .active')
        if (old) {
          old.classList.remove('active')
        }
        //还真是将各个模块的高度获取啊，懒得获取了，很简单那
      })
    })()

  </script>
```







# 二.Vue



## 1.Vue核心



### 一些知识点	



#### 1.知识点

```
1.el的两种写法
el:'#app'  ; 

挂载
const app =  new Vue({xxx})  app.$mout(app);

2.data必须使用函数式
data:function(){        可简化成 data(){  }
	return {
		name: 'zlc'
	}
}
```

#### 2.MVVM模型

![image-20240504193007719](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240504193007719.png)

#### 3.vue的数据代理

**//你写在data里面的数据，vue会将其加工(生成get,set)到vue.\_data里面，然后vue实例根据vue._date生成数据名，然后只要调用set就将变化更新到视图上**

**所谓的数据代理，就是vue实例中的data的数据是通过_data的get获取值，通过__data的set来修改值**

**//数据代理的好处就是方便我们的编码**

**(<font color="green">既然vue实例的 \_data已经有了真实数据，为什么还要在vue实例再创建数据呢？因为你每次都要\_data.xxx获取属性不麻烦吗，直接 使用 xx多方便，所以vue实例中的data的数据是通过___data的get获取值，通过_____data的set来修改值，这样就可以直接使用属性名，而不用加-data.xxx</font> ）**

![image-20240504201600879](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240504201600879.png)







#### 4.vue视图更新

- **问题引出：第二种方式修改数据，虽然内存上确实修改成功，但是vue没有监视到这种更新，视图不会变。**

![image-20240506132222822](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506132222822.png)

- **vue如何检测对象更新？**

所有对象的数据全部都是由set和get方法构成，只要修改数据就必须使用set方法，一旦使用set方法，vue就会更新视图
**也就说，set方法与视图的更新密切相关！！！一旦视图不更新就要思考是不是和该数据的set有关！**

比如，像这种，直接写了一个属性sex ,然后给予一个值 '男'，这个属性压根没有get set方法怎么可能会在视图上显示出来！

![image-20240506134152240](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506134152240.png)



- **vue如何检测数组更新**

数组里的属性没有set,get，数组里的对象肯定可以有，vue如何检测数组更新？

![image-20240506140647104](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506140647104.png)



![image-20240506141316420](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506141316420.png)





- **问题的解决**

**可以调用数组里的那七个api，也可以使用Vue.set(target,key,value)**

addSex(){

​		Vue.set(this.student,'sex','男')

}



**//总结**

![image-20240506142422659](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506142422659.png)









#### 5.使用属性方法加不加this



- 模板里面是不需要加this的
- js里面需要加this的













### 1.1插值操作(标签内容绑定)



#### (1)Mustache(大胡子)语法



注意: 可以直接写变量，还可以完成**简单的js表达式,计算**

```
</head>
<body>
    <div class="app">{{message1}}，{{1+1}},{{Date.now()}}</div>
    
    <script type="text/javascript" src="../js/vue.js"></script>
    <script>
            const app = new Vue ({
            el:'.app',  
            data:{
                message1: '你好, zlc'
            }
        })
    </script>
    
</body>
```



#### (2)v-once

在某些场景我们可能不希望界面随意跟随改动，这时候我们可以使用该指令

- v-once:
  - 该指令后面不需要跟任何表达式(比如之前的v-for后面是跟表达式的)
  - 该指令表示元素和组件(组件后面才会学习)**只渲染一次**，不会随着数据的改变而改变。
  - 代码如下：

![image-20240319141444920](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240319141444920.png)





#### (3)v-html

- 某些情况下，我们从服务器请求到的数据本身就是一个HTML代码
  - 如果我们直接通过{{}}来输出，会将HTML代码也一起输出。
  - 但是我们可能希望的是按照HTML格式进行解析，并且显示对应的内容。

89

```vue
    <div id="app">
        <div v-html="url">\</div>
    </div>


    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            data(){
                return {
                    url:'<a href="http://www.baidu.com">百度一下</a>'
                }
            }
        })
    </script>
```





#### (4)v-pre

原封不动的显示出来，而不会渲染

![image-20240319143003748](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240319143003748.png)





#### (5)v-cloak



//现在好像不会有延迟问题了，所以这个应该没什么用了









### 1.2 v-bind 标签属性绑定

​	

**//v-bind 一般都是标签属性的东西**

**//语法糖写法   :src="imgUrl"**,只需要写一个:即可,v-bind可以省略

 <font color="red">**v-bind的实质就是将引号里面的东西当成js代码而不是字符串看待！！！！！！**</font>

```vue
    <div id="app">
        <img v-bind:src="imgUrl" alt="图片错误">
    </div>


    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            data: {
                imgUrl: 'https:xxx..服务器穿过来的图片路径'
            }
        })
    </script>
```

通过动态绑定class 来实现  按下一个按钮切换字体颜色/也可以实现 鼠标悬停改变颜色



```vue
    <style>
        .active{
            color:red;
        }
    </style>
</head>
<body>
    <div class="app">
        <h2 v-bind:class="{active:isActive,line:isLine}">{{message1}}</h2>
        <button v-on:click="update">按钮</button>
    </div>
    
    <script type="text/javascript" src="../js/vue.js"></script>
    <script>
            const app = new Vue({
            el:'.app',
            data:{
                message1: '你好，zlc',
                isActive:true,
                isLine:true
            },
            methods: {
                update: function(){
                    this.isActive = !this.isActive
                }
            }
        })
    </script>
</body>
</html>
```

```vue
    <style>
        .active{
            color:red;
        }
    </style>
</head>
<body>
    <div class="app">
        <h2 v-bind:class="getClasses()">{{message1}}</h2>//如果这个对象很复杂就可以通过调用函数的方式来实现
        <button @click="update">按钮</button>
    </div>
    
    <script type="text/javascript" src="../js/vue.js"></script>
    <script>
            const app = new Vue({
            el:'.app',
            data:{
                message1: '你好，zlc',
                isActive:true,
                isLine:true
            },
            methods: {
                update(){
                    this.isActive = !this.isActive
                },
                getClasses(){
                    return {active:this.isActive,line:this.isLine}
                }
            }
        })
    </script>
</body>
```

```
<div><h2 class="basic" :class="mood">{{message1}}</h2></div> 
<button @click="update">按钮</button>

data(){
	return {
		mood = sad
	}
}
methods:{
	update(){
		this.mood = happy
	}
}
```



**//v-bind绑定style属性**

v-bind可以动态绑定style的属性，格式为：style="{key(属性名):value(属性值)}，此处要注意属性值是否带引号，带引号时为字符串，不带引号时[vue](https://so.csdn.net/so/search?q=vue&spm=1001.2101.3001.7020)会认为它是一个变量。

如果key与value重名就可以简写为 :style="{key}"

```
        <h2 :style="{opacity}">你好啊</h2>		简写
        <h2 :style="{opacity:opacity}></h2>  完整写法
                    data(){
                return{
                    opacity: 1
                }
            },
```







### 1.2 v-model 数据双向绑定



**//可以双向绑定数据，即在一个输入框中你输入的信息也会实时影响vue实例中的数据**

**//注意:只能用于表单属性，或句话说 只能用于  有value属性的标签**

![image-20240506144227751](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506144227751.png)

```
//1.checkbox，如果绑定的是布尔值，那么勾选与不勾选将直接影响布尔值;
			  如果绑定的是数组，那么勾选与不勾选 影响的是数组中有无该数据
```











**//表单修饰符**

```
//1.lazy
在默认情况下，v-model 在每次 input 事件触发后将输入框的值与数据进行同步 (除了上述输入法组合文字时)。你可以添加 lazy 修饰符，从而转变为使用 change 事件进行同步：

<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg" >

//2.number
如果想自动将用户的输入值转为数值类型，可以给 v-model 添加 number 修饰符：

<input v-model.number="age" type="number">

//3.trim
如果要自动过滤用户输入的首尾空白字符，可以给 v-model 添加 trim 修饰符：

```

**//总结**

![image-20240506144631933](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506144631933.png)









### 1.3 v-for



- 当我们有一组数据需要进行渲染时，我们就可以使用v-for来完成。
  - v-for的语法类似于JavaScript中的for循环。
  - 格式如下：v-for=" item in items  :key = "xxx" ",这里的key作为唯一标识，必须得写！！！
  - 格式还可以另一种写法v-for=" (item,index) in items  :key = "index" ",利用数组index角标作为唯一标识(但是一般别这么做)



**从数组中循环取出数据**

```vue
<body>
    <div id="app">
        <li v-for="student in students" :key="student.id">
            {{student.id}}-{{student.name}} <!--也可以直接{{student}}取出整体-->
        </li>
    </div>

<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el:'#app',
        data: {
            students: [
                {id:'001',name:'赵联城',age:20},
                {id:'002',name:'赵城联',age:21},
                {id:'003',name:'赵某人',age:22}
            ]
        }
    })

</script>
```

**从对象中循环取出数据** :  需要注意参数列表是固定的	  先是取出value然后取出key，最后是index

```vue
        <li v-for="(value,key,index) in students[0]" :key="index">
            {{key}}-{{value}}
        </li>
```





- 如果在遍历的过程中，我们需要拿到元素在数组中的索引值呢？
- 语法格式：v-for=(item, index) in items
- 其中的index就代表了取出的item在原数组的索引值。



实现  点击哪个列表，该列表就变成红色

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .active{
            color: red;
        }
    </style>
</head>
<body>
    <div id="app">
        <li :class="{active:index==currentIndex}" @click="change(index)" v-for="(item,index) in movies">{{item}}</li>
    </div>

<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el:'#app',
        data: {
            movies: ['海贼王','火影忍者','名侦探柯南','进击的巨人'],
            currentIndex: 0
        },
        methods: {
            change: function(index){
                this.currentIndex = index;
            }
        }
    })

</script>

</body>
</html>
```





**//总之就是 使用V-for时  必须添加:key=“唯一标识一般都是id"**

![image-20240506122313905](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506122313905.png)



















### 1.4计算属性与监视



///计算属性的set,get方法知道有这个东西就Ok，一般是不会使用的

**//为什么推荐使用计算属性，而不是写一个函数来获取属性？**因为你写成函数那么用几次该属性就需要调用几次该函数，没有缓存，效率低。**但是你使用计算属性，只会调用一次就会一直获取到该属性，后续再使用该属性可以直接使用**.



**//计算机属性**

```vue
    <div class="app">
        姓:<input type="text" v-model="firstname"><br>
        名:<input type="text" v-model="lastname"><br>
        全名: <span>{{fullName}}</span>
    </div>
    
    <script type="text/javascript" src="../js/vue.js"></script>
    <script>
            const app = new Vue ({
            el:'.app',
            data(){
                return {
                    firstname:'张',
                    lastname:'三'
                }
            },
            computed:{
                fullName(){
                      //这里是一个语法糖 其实是调用的fullName的get方法
//一个细节:我们不能直接获取data中的属性，但是get方法里面默认将this指向了vm实例，这样我们就可以this.属性获取data里面的属性
                    return this.firstname + "-" + this.lastname
                }
            }
 
        })
    </script>
```





**监听器**

**基本上不用watch来实现数据监听，因为太麻烦了，但是watch可以监听路由变化！**

<font color="red">**创建时间**</font>：**immediate: false(默认刚开始不自动生成)，当属性发生变化时再调用，如果将immediate设置为true,参考列表过滤也许有奇效！！！！！**



```js
// 监视属性配置项
watch: {
    // 监视isSunny属性
    imeediate: true/false,
    isHot: {
        // handler函数名称是固定的，不能随意更改,固定有两个参数一个是修改前的旧数据，一个是修改后的新数据
        handler(newValue, oldValue) {
            console.log("new:"newValue, "old:"oldValue)
        }
    }
}
```



<font color="red">**建议**</font>：**计算属性也可以实现很多属性监视，能够使用计算属性就使用，实在不行才使用监视属性**

![image-20240504214603128](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240504214603128.png)













### 1.5事件监听v-on

**v-on:xxxx ,  @xxx   xxx为绑定的一个事件** 

**//语法糖：缩写为@**

​	

当通过methods中定义方法，以供@click调用时，需要注意参数问题：

情况一：如果该方法不需要额外参数，那么方法后的括号()可以不添加。

但是注意：如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去，**可以在参数列表写一个名字获取event**

情况二：如果需要同时传入某个参数，同时需要event时，可以通过$event传入事件,否则传入的参数会顶替掉even。



**//v-on修饰符, 可以代替以往写js代码的形式**

```
methods:{
	showInfo(e){
		e.preventDefault()   //老旧的使用js  api
		alter('你好!')
	}
}
//1.阻止默认行为     //比如一个超链接，点击就跳转，阻止默认行为就不跳转
//2.事件冒泡        //比如父标签有一个@click子标签也有一个一摸一样的@click，这时点击子标签就会触发两次，这就是典型的事件冒泡
```

![img](https://img-blog.csdnimg.cn/20210712190852410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDczODEx,size_16,color_FFFFFF,t_70)





### 1.6 键盘监听

1. `@keydown`：监听键盘按下事件。
2. `@keyup`：监听键盘抬起事件。

```
name:<input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo">
            methods:{   
                showInfo(){
                    alert('请输入名字')
                }
            }
            
```

![image-20240504204050490](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240504204050490.png)

![image-20240504204448563](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240504204448563.png)







### 1.7 v-if、v-else-if、v-else,v-show



- v-if适合用于**切换频率低**的场景
- v-if与v-else-if,v-else搭配使用时 结构不能被打断
- v-if如果判断是false，那么就直接不生成相关代码

```vue
<body>
    <div id="app">
        <h1 v-if="isShow">true</h1>
        <h1 v-else>false</h1>
        <button @click="change">按钮</button>
    </div>


    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            data: {
                isShow:true
            },
            methods: {
                change(){
                    this.isShow = !this.isShow;
                }
            }
        })
    </script>
</body>
```



- v-show 和 v-if差不多，适合用于**切换频率高**的场景
- v-show如果判断是false，那么会生成相关代码，但是样式被隐藏起来了



**//一个关于组件化的知识**

```
//下面每个都做了相同的判断，太不合理了，怎么解决呢？
<h2 v-if="isright">你好1</h2>
<h2 v-if="isright">你好2</h2>
<h2 v-if="isright">你好3</h2>
//第一种，用div包起来, 但是这样有一个问题就是破坏了原有的css结构，可能造成css冲突
<div class="abc" v-if="isright"
	<h2>你好1</h2>
    <h2>你好2</h2>
    <h2>你好3</h2>
</div>
//第二种，template,这样虽然包裹了但是不会破坏css结构，这一层只是逻辑层，不是真实存在的css层
<template class="abc" v-if="isright"   //注意这里只能使用v-if不能用v-show
	<h2>你好1</h2>
    <h2>你好2</h2>
    <h2>你好3</h2>
</template>
```





### 1.8 自定义指令

![image-20240506145621186](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506145621186.png)





### 1.9 vue生命周期

#### ①引出生命周期

实现效果：   让一段文字的透明度从0->1再从1->0来回重复 

**changeOpacity方法不能看模板初始化的时候就调用，这时候需要用到生命周期的一些关键方法**

```
<body>
    <div id="app">
        <h2 :style="{opacity}">你好啊</h2>
        <h2>{{name}}</h2>
    </div>
    
    <script src="../js/vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data(){
                return{
                    name: 'zlc',
                    button: true,
                    opacity: 1
                }
            },
            methods: {
            	//修改透明度的方法
                changeOpacity(){
                        setInterval(() => {
                        if (this.button == true) {
                            this.opacity -= 0.01
                        } else {
                            this.opacity += 0.01
                        }
                        if (this.opacity <= 0 || this.opacity >= 1) this.button = !this.button
                    }, 16)
                }
            },
            mounted(){
                    this.changeOpacity()
                }
        })
    </script>
</body>
```



#### ②生命周期

- **挂载流程**
- **更新流程**
- **销毁流程**





#### ③知道两个重要的钩子函数



mouted  和  updated







### 2.初学案例



### ①列表过滤

```
<body>
    <div id="app">
        <input type="text" placeholder="请输入名字" v-model="keyWord" @keyup.enter="query">
        <ul>
            <li v-for="p in fpersons" :key="p.id">
                {{p.name}}------{{p.age}}
            </li>
        </ul>
    </div>



    <script src="../js/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                keyWord: '',
                persons:[
                    { id: '001', name: '1zlc', age: 18 },
                    { id: '002', name: 'zlc1', age: 18 },
                    { id: '003', name: 'zlc2', age: 18 },
                    { id: '004', name: 'zl2c', age: 18 }
                ],
                Fpersons:[]
            },
            methods: {
            },
            //使用监视属性实现
            watch: {
                keyWord:{
                    immediate: true,
                    handler(val) {
                        this.fpersons = this.persons.filter((p) =>{
                            return p.name.indexOf(val) !== -1
                        })
                    }
                }
            //使用计算属性实现（优先使用计算属性）
            computed:{
                fpersons(){
                    return this.persons.filter((p) =>{
                        return p.name.indexOf(this.keyWord) !== -1
                    })
                }
            }
            }
        })
    </script>
</body>
```









## 2.Vue组件化编程



### 2.1组件的构成



**一个Vue组件包括三个部分 <template></template>**,<script></script>,<style></style>**三个部分**





### 2.2组件的创建

**//此处的test就称之为组件实例对象(vc)**

```
const test = Vue.extend({
	template:``,   //写html
	data(){        //必须使用函数式，因为函数式每次都return一个新对象，保证数据是全新的
		return {
			xxx
		}
	}
})
// 还有简写版本


```

![image-20240506181743102](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506181743102.png)

**//一个重要的内置对象VueComponent.prototype._proto__ == Vue.prototype**

**//为什么要有这个关系？让组件实例对象(vc)也可以访问到Vue原型上的属性和方法**

![image-20240506184259276](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506184259276.png)





### 2.3 组件的注册



```
new Vue({
	components:{
		App,
		School
	}
})
```





### 2.4 组件的使用



**//写组件标签**

```
//比如我们有一个School组件
可以直接在div中写 <School></School>
```







### 2.5 开发经典模板



![image-20240506205724978](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506205724978.png)



**main.js**

```
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```

**App.vue**

```
<template>
  <div>
    <School></School>
  </div>
</template>

<script>
    //引入组件
    import School from './components/School.vue'

export default {
    name: 'App',
    components:{
        School
    }
}
</script>

<style>

</style>
```

**index.html**

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <title>vue_test</title>
  </head>
  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```

**compoments下的各种组件**







### 2.6 组件可以嵌套使用



## 3.Vue技术



### 3.1 render渲染

**//详情去看视频**



**vue脚手架生成的main.js为什么要使用render渲染而不使用模板？**

```
  render: h => h(App)  
```

**//我们import Vue from 'vue'，实际上引入的是残缺版本的vue，只有核心缺少了模板解析器(缺少的是解析Js中的模板解析器，vue文件的模板解析器还是一直存在的)，所以需要使用别的方法来替代使用template模板**

**//render的使用方法**

```
render(createElement){
	return createElement('h1','你好啊')
}
//只有一个参数 一行任务，不需要this，可以使用箭头函数
render: zlc => zlc('h1','你好啊')
如果是组件则可以直接写组件名
render: zlc => zlc(App)
```



![image-20240506211230109](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506211230109.png)









### 3.2 ref

**//某些特殊场景我们确实需要获取dom元素，不建议使用js获取，可以使用vue提供的ref**

**//如果只是单纯地获取html标签，那传统的js代码和vue提高的ref确实没区别，但要是针对组件区别就大了！！！**

**//vue的ref可以获取组件实例对象,即可以获取vc**

**//this.$ref.student.$on('xxx',function({**

​		**这里面的this指的是student组件，想使用本组件需要用箭头函数，箭头函数没有自己的this，会向外找，就会找到本组件**

**}))**

![image-20240506212859551](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506212859551.png)





### 3.3 props



```
//1.简单声明接收 (开发中这种简单的用的多)
props:['name','age','sex']

//2.类型限制
props:{
	name:String,
	age:Number,
	sex:String
}

//3.限制类型，限制必要性，指定默认值
props:{
	name:{
		type:String,    //name的类型是字符串
		required:true   //name是必要的
	}，
	age:{
		type:Number,
		default:99    	//默认值
	}
}
```



**{备注：props是只读的，Vue底层会检测你对props的修改，如果进行了修改，就会发出警告，若业务确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据}**

**//如果你传的是一个基本类型的数据，修改的话vue会直接报错；但是如果你传的是一个对象,修改对象中的一个基本数据类型是不会报错的，只是vue不建议你这么写！！！！**





### 3.4 mixin(混入)

所以在vue3就不用混入了

**//类似一个公共函数库,或者工具类**

**//感觉用的不多，除非很多组件都需要频繁使用**

```
一个mixin.js,名字可以随意取
export const timeUtil = {
    methods:{
        NowTime(){
            alert(Date.now())
        }
    },
    mounted() {
        this.NowTime()
    },
}

export const test = {
    data(){
        return {
            x:666
        }
    },
        methods:{
            showX(){
                alert(this.x)
            }
        }
    }
```

**//局部混入**

```
<template>
    <div class="demon">
        <!-- 组件的结构 -->
        <h2>{{msg}}</h2>
        <h2 @click="showInfo">校名:{{name}}</h2>
        <h2>校长:{{leader}}</h2>
        <h2 @click="showX">{{x}}</h2>					//可以正常使用
        <button @click="showInfo">点我提示校长</button>
    </div>
</template>
<script>
    import {timeUtil,test} from '../mixin'			//引入mixin.js中需要用到的vc对象
    // 组件交互代码
    export default {
        name: 'School',
        data(){
            return {
                msg:'你好啊'
            }
        },
        methods:{
            showInfo(){
                alert(this.leader)
            }
        },
        props:['name','leader'],
        mixins:[timeUtil,test]                  //声明
    }
</script>
```



**//全局混入**

//这样所有的vm,vc都会拥有混合里面的内容（慎用）

![image-20240507152322539](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240507152322539.png)







### 3.5 Vue插件

**//功能：增强Vue**

**//本质就是包含intall()方法的一个对象。install方法第一个参数默认是Vue原型，第二个以后的参数是插件使用者传递的数据**

**//Vue.use(),可以写多个；后面我们引入别人写的功能强大的插件，大大加快开发效率**



- 创建一个plugin.js
  - 内容：![image-20240507153648504](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240507153648504.png)
- 使用方法：在main.js中 使用Vue.use(xxx)
  - ![image-20240507153728040](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240507153728040.png)









### 3.6 scopted

比如组件A和组件B样式中都有一个同名的class选择器，这时候将他们都注册到app中，就会发生冲突，后引入的样式会覆盖前面引入的样式

**//解决方法就是加入scopted,本质就是将样式中各种选择器的名字随机生成确保不会重复**

```
<style scopted>
	xxxxxx
</style>
```





### 3.7 自定义事件

**//自定义事件本质是给xx组件的vc绑定的事件**

**//作用:子组件 ===> 父组件，子组件传数据给父组件**



#### ①问题引入

前面我们使用props解决了父组件给子组件传数据/方法的问题，但是那种不够灵活，解耦性低

vue提供的自定义事件帮助我们解决这个问题



#### ②自定义事件使用/演示

**语法：1.创建自定义事件  **

​			**2.触发自定义事件:  this.$emit(自定义事件名字,args)**

​		    **3.解除单个绑定:this.$off(自定义事件名字)**

​			**4.解除多个绑定:this.$off(['xx','xx',.......])**

​			**5.解除所有绑定:销毁绑定组件实例，就可以销毁所有该组件自定义事件！！！！！！！！！！**

​			**//第五条的言外之意就是说，当后面学习路由的时候，出现他杀，自定义事件会失效**

//父组件

```
<MyChild @zlc />

```

//子组件

```
<button @click="test">触发绑定事件</button>

methods:{
	test(){
		//触发事件
		this.$emit('zlc',name,age)
	}
}
```



![image-20240508193751654](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240508193751654.png)







#### ③ 组件使用Js内置事件

组件无法使用直接使用内置事件，直接使用vue会当成自定义事件

```
<student @click="demon"/>   //组件上使用内置事件，vue依然会当成自定义事件从而失效
```



组件使用Js内置事件需要声明

```
<student @click.native="demon"/> 
```















### 3.8全局事件总线

**//前人总结的经验，而非vue设计开发的**



#### ① 实现任意组件通信

![image-20240508200931892](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240508200931892.png)





#### ② 使用流程



![image-20240508205145208](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240508205145208.png)













### 3.9 消息订阅与发布

**//知道这个就好，我们一般都还是更加推荐使用全局事件总线 进行 组件间的通信**



#### ① 下载 pubsub.js库



```
命令行: npm i pubsub-js
```



#### ② 使用流程

```
//1.引入pubsub.js
	import Pubsub from 'pubsub-js'
	Pubsub是一个对象

//2.类比 this.$bus.$on
	this.pubId = Pubsub.subscript('xx',function(){}) //返回的是一个订阅id，用来取消订阅
	可以将方法写在$on/subscript里面，但是必须要用箭头函数，使this指向vc
	或者将方法老老实实写在methods里面，然后this.xxx调用

//3.类比this.$bus.$emit
	Pubsub.publish('xx',参数)

//4.类比this.$bus.$off
	beforeDestroy(){
		Pubsub.unsubscript(this.pubId)    //输入订阅id，就可以取消订阅
	}
```









### 3.10 $nextTick()

**作用:是将$nextTick()中的回调函数延迟在下一次dom更新数据后调用**

**用法：如下案例**



**//一个案例，实现点击编辑就会自动将鼠标焦点锁定输入框**

![image-20240508220200832](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240508220200832.png)

```
<template>
        <li>
            <label>
                <input type="checkbox" v-model="todoObj.done">
                <span v-show="!todoObj.isEdit">{{todoObj.name}}</span>
                <input
                 v-show="todoObj.isEdit"
                 type="text" ref="inputTitle"
                 v-model="todoObj.name"
                 @blur="todoObj.isEdit = false">
            </label>
            <button class="btn btn-editnpm" @click="editTodoObj(todoObj)">编辑</button>
            <button class="btn btn-danger" @click="todoObjDelete">删除</button>
        </li>
</template>

<script>
    export default {
        name: 'MyItem',
        props:['todoObj'],
        methods:{
            changeDone(){
                this.todoObj.done = !this.todoObj.done
            },
            todoObjDelete(){
                if(confirm('是否删除')){
                    this.$bus.$emit('deleteTodoObj',this.todoObj.id)
                }
            },
            editTodoObj(todoObj){
                this.$set(todoObj,'isEdit',true)
                //由于我们当时并没有给todoObj这个类加入idEdit属性，我们这里选择后加入该属性，这就导致我们上面
                //的代码无法及时同步视图，此时视图中还没有文本框，没有文本框这时候设置自动获取焦点是无效的。
                //问题的解决：使用$nextTick(),可以在该函数回调完的最后再去执行
                
                //题外话：vue更新视图是在回调完一整个函数后再回调！！！因为你遇见一个更新就回调效率很慢，vue
                	//   选择全部执行完之后再去更新视图
                this.$nextTick(function(){
                    this.$refs.inputTitle.focus()
                })
            }
        },
    }
</script>

<style>

</style>
```





### 3.11动画效果

//学习css动画 后 补









## 4.Vue技术2



### 4.1 axios配置代理

**简介：通过配置vue的vue.comfig.js**

![image-20240511125441943](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511125441943.png)

**那么如何开启代理服务器呢？？？？**

- 方法一：nginx （专业）
- 方法二:   vue-cli （用于自己学习）



**使用**

```
自己去搜，很简单	
```









### 4.2 v-resource

**//维护频率低，更推荐axios**











### 4.3 插槽



#### ①默认插槽



**例子演示：直接在组件标签内部写，然后在组件中需要的位置用slot引出**

```
  <div id="app">
    <Category title='美食' :listData='foods'>
      <img src="./assets/logo.png" alt="失败">
    </Category>

    <Category title='游戏' :listData='games'>
      <ul>
        <li v-for="(item,index) in games" :key="index">{{item}}</li>
      </ul>
    </Category>

    <Category title='电影' :listData='movies'>
      <video controls src="#"></video>
    </Category>
  </div>
</template>
```

```
组件
<template>
  <div class="category">
    <h3>{{title}}分类</h3>
      <slot>我是默认的</slot>
  </div>
</template>
```



- **slot标签内部也可以写一些默认的东西类似于 img的alt**

- **style样式也在组件使用位置可以，相当于将要放入插槽的东西的style加载好一块给插槽**

- **style样式也可以在组件内部写，相当于将要放入插槽的东西的style在插槽加载**

  

#### ②具名插槽

用到再说



#### ③作用域插槽⭐

**//非常常用！！！也算是一种比较便捷的子向父 传数据！**！

自己看例子

```
<template>
  <div id="app">
    <Category title='游戏' :listData='games'>
      <template v-slot="zlc">
      <ul>
        <li v-for="(item,index) in zlc.games" :key="index">{{item}}</li>
      </ul>
      </template>
    </Category>

    <Category title='游戏' :listData='games'>
      <template v-slot="zlc">
      <ul>
        <li v-for="(item,index) in zlc.games" :key="index">{{item}}</li>
      </ul>
      </template>
    </Category>
    
    <Category title='游戏' :listData='games'>
      <template v-slot="zlc">
      <ul>
        <li v-for="(item,index) in zlc.games" :key="index">{{item}}</li>
      </ul>
      </template>
    </Category>

  </div>
</template>

```

```
<template>
  <div class="category">
    <h3>{{title}}分类</h3>
      <slot :games="games" msg:"你好">我是默认的</slot>
  </div>
</template>

<script>
      数据在这  games:['LOL','CSGO2','CF','地下城'],
</script>

```











### 4.4 VueX

<font color="red">**Vue3使用Piano,vueX就没什么用了**</font>

#### ① 引出-多组件操作相同数据

**//当组件间的通信变得复杂，那么全局事件总线实现起来就很麻烦**

![image-20240511155006876](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511155006876.png)





![image-20240511155252491](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511155252491.png)





## 5.Vue-router



### 5.1 SPA

- 单页Web应用,single page web application,SPA
- 整个应用只有一个页面
- 点击页面的导航栏链接，不会刷新页面，只会做页面的局部更新
- 数据需要通过ajax请求获取



**路由：在前端就是一个键值对，key是路径，value是组件**





### 5.2 路由的基本使用



#### ① 下载路由		

```
npm i vue-router
```



#### ② 注册路由

main.js中，

```
//引入插件
import VueRouter from 'vue-router'
//引入路由器
import router from './router'
//使用插件
Vue.use(VueRouter)

new Vue({
  render: h => h(App),
  //注册路由
  router:router
}).$mount('#app')

```







#### ③ 配置路由

在src下面生成一个目录router/index.js,内容如下：

```
// 该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router"
//引入组件
import About from '../components/About'
import Home from '../components/Home'

//创建并暴露一个路由器
export default new VueRouter({
  routes:[
    {
      path:'/about',
      component:About
    },
    {
      path:'/home',
      component:Home
    }
  ]
})
```



#### ④ 使用路由

```
链接标签: <router-link to="/组件名">xxx</router-link>

显示标签: <router-view></router-view>
```









### 5.3 几个注意点



- 1.涉及路由的组件我们放入文件夹pages,普通组件还是放在components
- 2.来回切换组件，组件是在不停地销毁产生
- 3.每个路由相关的组件身上多了两个属性，一个是自身信息的route(传参有用)，一个是共同的router路由器(里面封装很多好用方法)
  - ![image-20240511201359998](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511201359998.png)





### 5.4 多级路由



区别就两个:

```
//1.在父级下面加入children数组，一定要注意此处的path 不需要加/  ，再说一遍：二级路由不要加 / ！！
    {
      path:'/home',
      component:Home,
      children:[
        {
          path:'test1',
          component:Test1
        },
        {
          path:'test2',
          component:Test2
        }
      ]
    }
   
//2.router-link的 to  也需要写多级
	<router-link class="test" to="/home/test1">test1</router-link>
```





### 5.5 路由携带参数





#### ①pageURL携带参数

```
<router-link to='/home/test1/msg?id=${item.id}&title=${item.title}'>{{item.id}}</router-link>
											↓↓↓↓
									//知道这么写就完事了
<router-link :to='`/home/test1/msg?id=${item.id}&title=${item.title}`'>{{item.id}}</router-link>
```

```
//接收参数，这时候就用到了我们前面学到的多出来的两个属性中的route,里面的query
  <h4>消息编号:{{ $route.query.id }}</h4>
  <h4>消息标题:{{ $route.query.title }}</h4>
```





**//个人感觉其实都可以**

#### ②page对象携带参数(推荐)

```
<router-link :to='{
	path:'/home/test1/msg',
	query:{
		id:item.id.
		title:item.title
	}
}'>
{{item.id}}
</router-link>
```





#### ③params获取参数

<font color="red">**和占位符一摸一样**</font>

```
//1.配置占位符
		path:'/zlc/:id/:name/:age'
//2.配置数据
		<router-link :to="`/zlc/001/赵联城/18`">xx</router-link>
		or					//如果使用params 必须使用name命名路由，不能使用path
		<router-link :to="{name:'xx',params:{id:item.id,name:xx,age:xx}}">xx</router-link>
//3.获取数据
		$this.params.xxx  简简单单改个params就好了
```















### 5.6 路由命名

**//要是多级路由，整个path会很长，使用路由命名来简化**

**//建议必须路由命名**

```
    {
      name: 'home'   //给路由起名字
      path:'/home',
    }
    
   
//使用
<router-link :to="{name:'home'}">xx</router-link>
```





















# 三.React









