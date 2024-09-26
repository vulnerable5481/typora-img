# 一.前端三板斧



## 1.HTML



```
z-index : 1可以提高优先级
```



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

//5.超链接标签
	< a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
//6 锚点标签

```

![image-20240902124226085](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902124226085.png)











### 1.2 table与 dl列表

```
//6.表格标签
<table></tabe>是用于定义表格的标签。

<tr></tr>标签用于定义表格中的行

<td></td>用于定义表格中的单元格

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

![image-20240314164001972](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314164001972.png)

```
<ul>
    <li>无序列表</li>
    <li>无序列表</li>
    <li>无序列表</li>
</ul>

<ol>
    <li>有序列表</li>
    <li>有序列表</li>
    <li>有序列表</li>
</ol>




以前还真没怎么用过

**非常适合制作 底部模块**

**实践使用dl dt dd标签最多地方，通常是具有标题，而标题下对应有若干列表简单的（栏目标题+对应标题列表）和标题对应下面有内容**

<dl>
<dt>列表标题</dt>
<dd>列表内容</dd>
<dd>列表内容</dd>
...
</dl>

```







### 1.3 特殊字符

```
空格符	&nbsp;
<	小于号	&lt;
>	大于号	&gt;
&	和	&amp;
￥	人名币	&yen;
©	版权	&copy;
®	注册商标	&reg;
℃	摄氏度	&deg;
±	正负号	&plusmn;
×	乘号	&times;
÷	除号	&divide;
²	平方上标2	&sup2;
³	立方上标3	&sup3;
```







### 1.4 input输入表单元素

![image-20240901121549489](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901121549489.png)

![image-20240314170822396](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314170822396.png)

![image-20240314170836049](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314170836049.png)

































### 1.5 lable标签

**//比如lable标签可以使鼠标点击用户名三个字就触发输入框，输入信息，就是将鼠标点击范围从单一的框变为框加文字的所在的盒子**

![image-20240314171626257](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314171626257.png)





### 1.6 select下拉表单



![image-20240314172009678](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314172009678.png)



### 1.7文本域

row行 cols列

![image-20240314172304685](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314172304685.png)



### 1.8Element语法



![image-20240315122337048](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240315122337048.png)



![image-20240315122621491](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240315122621491.png)





## 2.CSS上篇



### 2.0 CSS初始化与书写顺序

​	

```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
em,
i {
    font-style: normal;
}
li {
  list-style: none;
}
img {
  /* 低版本浏览器兼容 */
  border: 0;
  /* 解决图片底部空白缝隙问题 */
  vertical-align: middle;
}
button {
   cursor: pointer;
}
/* 清除浮动 */
.clearfix::after{
    visibility: hidden;
    clear:both;
    display: block;
    content:".";
    height: 0;
}
```



![image-20240326145754863](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326145754863.png)







### 2.1 选择器



#### ① 基础选择器

![image-20240314205404290](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240314205404290.png)



#### **②复合选择器**

![image-20240318173738463](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318173738463.png)

![image-20240318174323877](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318174323877.png)

![image-20240318174919766](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318174919766.png)



#### ③伪类选择器

![image-20240318175411067](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318175411067.png)

![image-20240325130848922](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325130848922.png)

#### ④	属性选择器

比如  .box input[type=text]{  color:pink     },怎么说呢，感觉还是比较便捷的!

![image-20240901131040812](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901131040812.png)

#### ⑤结构伪类选择器

![image-20240901131645431](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901131645431.png)

![image-20240901132041514](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901132041514.png)

#### ⑥ 伪元素选择器

<font color='orange'>**伪元素选择器 个人理解：就是父盒子里面的子盒子 只不过在dom里面是隐藏的，提高可读性，挺便捷的**</font>

**<font color='red'>注意：必须要写 content,这个容器里面必须要有内容！！！！</font>**

![image-20240901132633416](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901132633416.png)

![image-20240901133831146](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901133831146.png)



**利用 ::before 实现 便捷遮罩层!**

```
  .box1 {
    position: relative;
    width: 100px;
    height: 100px;
    margin: 0 auto;
    background-color: red;
  }
  .box1::before {
    content: "";
    display: none;
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.3);
  }
  .box1:hover::before {  
    display: block;
  }
```



























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

**//text-align center left/right center 三种对齐方法     文字水平居中  **    

**//text-indent 可以缩进  px 也可以 em,em就是 单位字体距离**

**//text-decoration 知道underline 添加下划线 和 none 取消下划线   就ok**

**//line-height 控制行高,常用于垂直居中显示，line-height = height的高度     文字垂直居中 **











#### 2.2.3 背景属性

![image-20240319184729040](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240319184729040.png)

**backgroud: url(图片路径) no-repeat x y    通常插入背景图片都是这样的**

**background-size: 100% 100%   //还可以写 cover 和contain**

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240907134154776.png" alt="image-20240907134154776" style="zoom:50%;" />







####  2.2.4 圆形盒子

```
如果是一个正方形->圆形  :  border-radius:50%   数值修改为高度或宽度的一半，或者直接用50%即可
如果是个矩形   ->圆角矩形  :  border-radius:height/2   数值改为高度的一半

border-top-radius 也可以只调正一个地方的角度

border-radius: 0 0 0 0   按照顺时针角度设置
```



#### 2.2.5 盒子阴影

盒子阴影一般推荐 rgba(0,0,0,0.3)

![image-20240325184453503](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325184453503.png)

![image-20240325184419127](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325184419127.png)





#### 2.26 文字阴影



![image-20240325184520481](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325184520481.png)











### 2.3 CSS的元素显示模式



-  块元素:**< h1 >~< h6 >、< p >、< div >、< ul >、< ol >、< li >**
-  行内元素: **< a >、< strong >、< b >、< em >、< i >、< del >、< s >、< ins >、< u >、< span >、< img />、< input />、< select >、< textarea >、< br />、等，其中 < span > 标签是最典型的行内元素。有的地方也将行内元素称为内联元素。**
- 行内块元素:**< img />、< input />、< td >**

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

##### 1.Border边框

```
border:
		border-width: 5px;
		border-style: solid;（实线）  /  dashed（虚线）  / dotted （点线）
		border-color: red;
		border: 1px solid red⭐ ；没有固定顺序 
		border-collapse: collapse: 用于边框合并,常用于表格中将叠加的表格线变细
border分框写法:
		border-bottom: 1px solid blue
```

**边框会影响盒子大小，一个200px * 200px的盒子  加上border-width: 10px 会变成一个 210px * 210px的盒子**</

**//解决方法：将盒子的长宽减去边框大小，注意左右和上下所以要减去双倍的边框**





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





​	







​	



### 2.5浮动

**三种网页布局 ： 标准流，浮动，定位，开发一个页面往往三者都需要使用**



![image-20240325185923009](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325185923009.png)





![image-20240325190039125](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240325190039125.png)

#### 2.6.1 浮动三特性

**注意浮动之后，只会漂浮在该盒子之前的盒子上面，如果是在后面就不会浮动   !  !  ! ! !   ! !  !   ! !   !   !1**

![image-20240326121836258](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326121836258.png)



![image-20240326121940735](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326121940735.png)





![image-20240326122357841](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326122357841.png)

<font color='red'>**设置为浮动之后，两个浮动模块彼此之间是没有缝隙的！！如果是普通的行内块元素会存在缝隙！！！**</font>

![image-20240326122927859](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326122927859.png)

#### 2.6.2浮动元素与标准元素搭配使用







![image-20240326124519492](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326124519492.png)





#### 2.6.3清除浮动

![image-20240326141835582](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326141835582.png)

![image-20240326143455710](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326143455710.png)





清除浮动的本质

![image-20240520133023423](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240520133023423.png)











清除浮动有四种方式

![image-20240326142807691](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240326142807691.png)

**1.父类添加overflow:hidden** 

```
1.overflow:hidden 
//方便，但是有一个问题就是如果你设置了高度为90px宽由子元素撑开，但要是有元素超过父元素的高就直接不显示了
```



**2.after伪类元素法（推荐）**

```
        .clearfix:after {
            content: "";
            display: block;
            height: 0;
            clear: both;
            visibility: hidden;
        }
固定这么写
直接在父类元素上面加这个类即可

```

**3.双伪元素清除浮动**

//是after伪类元素法的升级和优化

![image-20240902112610013](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902112610013.png)





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
- sticky(了解)
  - 粘性定位




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









## 3.CSS下篇



### 3.1 精灵图



#### 为什么需要

**//精灵图本质就是一堆图放在一张大图片上去，浏览器向服务器只需要请求一次即可，大大降低页面的加载速度	**

![image-20240520170937036](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240520170937036.png)

#### 如何使用

<font color='orange'>**比较简单，用到在说吧**</font>

![image-20240831175847095](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831175847095.png)



`![image-20240903120304641](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240903120542619.png)

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240903120542619.png)









### 3.2 字体图标





#### 引入

![image-20240831180414231](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831180414231.png)

![image-20240831180601643](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831180601643.png)



#### 使用

**<font color='orange'>直接使用别人做好的，就够用了</font>**

**用到再说，引用也很简单，后续追加也简单**

![image-20240831180645761](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831180645761.png)

```
  .shopcar::before {
    position: relative;
    top: 1px;
    left: 10px;
    content: "\e902";  //使用这个 不好直接复制图标
    font-family: 'icomoon';
    color: #b1191a;
  }
```









### 3.3 用户界面样式

#### ①鼠标样式

![image-20240831183919926](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831183919926.png)

#### ② 轮廓线

这样就可以去掉默认的蓝色边框，比如Input和文本域

```
input {outline:none}
或者 {outline:0}
```



#### ③ 禁止文本拖拽

```
textarea{
	resize:none;
}
```





### 3.4 vertical-align

文字默认是和图片的基线对齐，如果想要文字和图片垂直居中对齐只能暴力调xy那可不行，通过vertical-align即可实现

**<font color='orange'>用于实现图片/文本域 和 文字垂直居中</font>**

<font color='red'>**vertical-align只能和行内块元素使用，如果是一个盒子可以与display:inline-block搭配使用**</font>

![image-20240831184803093](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831184803093.png)





**案例：**

![image-20240831185005500](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831185005500.png)



### 3.5 图片底部空隙问题

**直接给图片添加 border边框，会发现地下多出来一块，那其实是给文字预留的底线空间**

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831185651760.png)

**解决：1.给图片添加virtal-align:middle/top/bottom(推荐使用)**

​          **2.把图片转换为块级元素,display:block,只有行内块才有基线底线问题**



### 3.6 文字溢出显示省略号



1.  white-space:nowrap    //强制单独一行内显示文本
   **默认为normal：超过一行就换行**
2. overflow: hidden //超出的部分隐藏
3. text-overflow: ellipsis //省略号代替超出的部分





### 3.7 新特性



#### ① 语义化dIv

本质就是div 只不过语义化了，你想 <div class = "header/nav/footer"></div>或者直接<header></header><footer都可以

随便你  爱用div就div  想语义化就用这个  反正没什么区别	

![image-20240901120001037](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901120001037.png)

#### ② 视频标签





#### ③音频标签



#### ④ input验证

肯定还是要用正则表达式去验证，但可以用这个当做前端初步验证

![image-20240901121120303](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901121120303.png)





#### ⑤  盒子新模型

![image-20240902112915595](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902112915595.png)

**默认是 box-sizing:content-box,如果你修改成了 box-sizing: border-box，就不会撑大盒子了**

```
*{
  margin:0;
  padding:0;
  box-sizing:border-box  //css初始化可以加上这一句，这样就不会有撑大盒子的问题了
}
```





#### ⑥ 过渡



![image-20240902113306480](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113306480.png)

![image-20240902113438038](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113438038.png)



![image-20240902113547506](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113547506.png)

![image-20240902113715076](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113715076.png)

![image-20240902113853222](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113853222.png)



#### ⑦ favicon图标

vue3修改favicon图标的方法

1.使用比特虫网站  生成 .ico图片

2.将其添加到public下面，命名为favicon.ico

3.在index.html 中修改<link rel="shortcut icon" type="image/x-icon" href="./favicon.ico">

![image-20240902122739786](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902122739786.png)



#### 



## 4.CSS++



### 4.1 2D转换



#### 2D位移



**①作用：移动盒子，类似定位**

<font color='red'>**对行内元素无效**</font>

```
transform: translate(x,y)
transform: translateX(x)
transform:translateY(y)


transform:translate(50%,50%)
此处的50%是参照盒子本身的大小，这样以后就不需要自己计算px了，直接使用2D移动很方便
```

![image-20240905123426445](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905123426445.png)

**<font color='orange'>②定位，2D位移，内外边距的区别</font>**

- 定位，内外边距，2D转换，三者都可以实现盒子的移动
- 区别：内外边距 与 绝对定位 会影响布局，但是相对定位 与 2D转换 不会影响 布局
- 应用：比如实现鼠标移动到一个商品图片，该图片便向上移动的效果
  实现：思路1：字绝父相   思路2:直接transfrom:translate(0,y)
  明显思路2要更加简单，只需要一行代码就搞定，思路1还涉及到父盒子什么的
- 总结：三者各有应用场景,没有优劣 ! **灵活使用！**



③ 定位+2D移动

以往我们实现大盒子内小盒子的移动，通常都是子绝父相+调整小盒子的margin/大盒子的padding,现在更推荐
使用子绝父相+2D移动，这样就不需要计算内外边距了，同时盒子大小改变也会自动修改距离



例子：

```
  有父盒子a 子盒子b，实现无论a，b大小怎么变，b始终在a的中心显示
  .a{
    position: relative;
    width: 500px;
    height: 500px;
    margin: 0 auto;
    background-color: pink;
  }
  .b{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);    //简单的小学几何题
    width: 100px;
    height: 100px;
    background-color: red;
  }
```







#### 2D旋转

**<font color='orange'>                        配合过渡很好用哦！！！！！！！！！！！1</font>**

```
transform: rotate(-45deg)  //逆时针旋转四十五度
```

![image-20240905125759358](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905125759358.png)



#### 2D中心点

![image-20240905130817689](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905130817689.png)



#### 2D缩放

**<font color='red'>最关键的优点：可以设置转换中心点缩放；不影响其他盒子布局！！！扩大的部分会浮在其他盒子上面</font>**

![image-20240905141435845](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905141435845.png)



### 4.2 动画

#### 	① 使用

```
//定义动画
@keyframes 动画名字 {
    0% { 初始状态可以省略，你直接不写这行代码也无所谓}
    25% {
      transform: translate(400px , 0);
    }
    50% {
      transform: translate(400px , 400px);
    }
    75% {
      transform: translate(0 , 400px);
    }
    100% {
      transform: translate(0 , 0);
    }
}
.box {
	略
	//调用动画
	animation-name:动画名字;
	animation-duration:10s;
}
```



#### ② 属性

联合写法:  animation: name 10s ease infinite

![image-20240905150401004](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905150401004.png)



#### ③ steps

animation-timing-function:steps()  步数的妙用

- **制作进度条**
- **实现单个文字逐个显示**
- **定格动画**





### 4.3 3D转换

![image-20240905181339323](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905181339323.png)



#### ① 3D位移

```
transform: translate3D(x,y,z)   //注意不能用百分之 只能是px
//z轴 需要配合透视才有效果
```







#### ② 透视

![image-20240905184427575](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905184427575.png)

```
要在被观察元素的父盒子上面加入Perspective
父盒子{
	perspective: n px   //    n距离相当于视距，n越小离得越近图就越大
}
```





#### ③ 3D旋转

**<font color='red'>配合透视效果很好</font>**

```
transform: rotateX(180deg);   
transform: rotateY(180deg);
transform: rotateZ(180deg);  
```



#### ④ transfo rm-style



![image-20240905201453710](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905201453710.png)



























## 5.JavaScript



### 1.基础语法对比

#### 1.1变量

![image-20240509120603382](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509120603382.png)

#### 1.2 数据类型

- 布尔值
  - 空字符串 默认是 false
  - 除了空字符串其他的非布尔值全都会隐式转换成true

#### 1.3  !==

不同于后端，js中的不等于要用 !== , !=不够严谨，原因很简单，自己去查



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
	
//4.操作表单元素
	xxx.type = 'password'
	xxx.value = 'xxx'    
	xxx.checked = true  如果是布尔值

//5.操作自定义对象 ⭐
//还真挺关键的！
	xx.dataset.xxx
```

![image-20240509140552963](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509140552963.png)





#### 2.2 定时器-间歇函数

**//setInterval每隔一段时间都会执行一次；setTimeout只会在指定时间到后执行一次	**





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

<font color="red">**setInerval是可以在函数体内自杀的！！！**</font>





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
  - <font color="red">**注意无法在settimeout函数体中clearTimeout，因为此时函数还在运作，是不能自杀的**</font>


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



#### 3.4 location对象

**//总之location对象可以获取页面URL属性，可以刷新页面，可以从当前页面跳转**

![image-20240516123412218](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240516123412218.png)



#### 3.5 navigation对象和history对象

**navigation对象的主要作用就是里面有很多关于浏览器的信息**

**可以用来判断当前是移动端还是PC，PC跳转到哪个页面，移动端跳转到哪个页面**



**history对象的主要作用就是操纵浏览器历史记录，可以back/forward**

**比如vue中的下面几个方法底层都是用的history对象**

```
		this.$router.back() // 后退一步
		this.$router.forward()  //前进一步
		this.$router.go(N)  //整数前进N步   负数倒退N步
```



#### 3.6 本地存储 



##### ①localStorage

![image-20240516124507755](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240516124507755.png)

**//生命周期：永久存储在本地电脑，需要手动删除，不过好像有时间限制到期删除，否则关闭页面也会存在**

```
1.增/改
localStorage.setItem(k,v)

2.查
localStorage.getItem(k)

3.删
localStorage.removeItem(k)

//如果要存储对象，需要将其转换成json字符串,用的时候再反序列化就ok了
localStorage.setItem(k,Json.stringfy(v))
Json.parse(json字符串)
```









##### ②sessionStorage

只有一点不同：生命周期仅限当前页面，关闭则数据丢失。





### 4.js进阶



#### 4.1 解构赋值

**多级解构  /  解构嵌套**

![image-20240516144832622](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240516144832622.png)

- **修改变量名**

![image-20240516150431885](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240516150431885.png)





- <font color='orange'>**结构赋值的本质**</font>

**// const {name,age,sex} = person**

//**本质等于    const name = person.name ,  const age = person.age , const sex = person.sex**





- <font color='orange'>**结构赋值与三元运算符**</font>

```
    updateShowStatus(brand) {
      let {brandId,showStatus} = brand
      this.$http({
      url: this.$http.adornUrl('/product/brand/update'),
      method: 'post',
      data: this.$http.adornData({brandId,showStatus:showStatus==true?1:0},false)
      })
    }

```









#### 4.2 数组常用方法



- **map:**数组.map 返回的是新数组，里面可以对原数组进行改动;map比forEach更常用
- **filter:**过滤数组中的一些数据，返回符合条件后的新数组  比如return item >= 20
- 用到自己搜呗







#### 4.3 内置构造函数常用方法

![image-20240517100231229](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240517100231229.png)





#### 4.4 原型对象与原型链

个人理解就是将java中的一个完整父类中的构造函数独立出去然后通过prototype与constructor互相连接起来，实例对象则通过_proto_这个隐式属性指向构造函数的原型对象	

这样一层一层向上查找就会形成一个链式结构，我们称为**`原型链`。**

![image-20240517101735224](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240517101735224.png)



#### 4.5 异常处理

就是try catch finally



#### 4.6 防抖

![image-20240517102714205](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240517102714205.png)



例子：

```js
  function debounce(fn, t) {
      //声明定时器变量
      let timeId
      return function () {
        // 如果有定时器就清除
        if (timeId) clearTimeout(timeId)
        // 开启定时器 
        timeId = setTimeout(function () {
          fn() //执行逻辑
        }, t)
      }
    }
```







#### 4.7 节流

![image-20240517115513721](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240517115513721.png)



例子:

```js
function(fn,t){
    let timer = null
    return function(){
        //如果没有定时器
        if(!timer){
            timer = setTimeout(()=>{
                fn()//执行逻辑
                //程序执行完成，清除定时器
                timer = null
            },t)
        }
    }
}
```

![image-20240517122326027](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240517122326027.png)





















## 6.案例和技巧



#### 1.文字的居中



**//line-height可以实现单行文字的上下移动**

```
height: x px;
line-height: x px;  // line-height = height 可以实现文字垂
text-align: center  //可以使单行文字居中

```

**//一个水平方向居中，一个竖直方向居中，两者结合可以实现垂直居中！！**

**//一般情况不建议 margin + padding 去实现 垂直居中**



关于图片与文字的垂直居中要使用到 vircal-align







#### 3.盒子宽度警告



除了盒子，不要随意指定盒子内部元素的宽度,高度也有时候不需要设置







#### 4.margin:0 auto的失效

如果是块级元素/行内块级元素，使用margin: 0 auto;都会使其居中，但是如果是浮动的,float:left就会导致margin:0 auto;失效，指明margin: 10px还是可以使用，这是为什么呢？？

//解答：因为margin: 0 auto 是根据文档位置计算的，浮动使其**脱离文档，导致计算公式无法计算**，但是指明margin依然可以正常使用！

//如果margin:0 auto在 margin-xxx: 10px 的后面也会失效，在前面就有效

使用position: absolute 绝对定位也会使margin: 0 auto 失效



**//有一个小技巧解决这种绝对定位引起的失效问题:可以先走到中间(top:50%),然后往回走自身宽度的一半即可()**

**//垂直居中也是一个道理**



#### 5.固定在版心右侧位置	

 

![image-20240330174603275](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330174603275.png)





#### 6.操纵placeholder

```
.search input::placeholder {
    font-size: 14px;
    color: #bfbfbf;
} 
```





### 7.margin负值的妙用

比如ul中五个li的盒子并排，如果有border则会导致重叠变粗，如何解决呢？

![image-20240831202758242](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831202758242.png)



我们可以将每一个li盒子的右侧或者左侧border删除，但不能完美解决问题

**使用margin负值即可解决**

![image-20240831203029205](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831203029205.png)

### 8.margin负值妙用2

还是接着上面的问题，如果我们要实现这样一个功能:鼠标移动到哪个li就使其边框变成blue

```
ul li:hover{

	border: 1px solid blue

}
```

此时会出现一个问题，由于我们刚刚margin负值使右边的li盒子压住了当前的盒子导致有一边无法变成蓝色

解决方法：

1. 添加 positive:relative   // 相对定位会压住其他盒子
2. 如果出现定位冲突  使用优先级解决

### 9.行内块元素的妙用



如果你想将一个东西快速水平居中 垂直居中，可以将其设置成行内块元素，然后将其父盒子设置text-alin:center,line-hegiht:height即可





























## 7.一些功能的实现



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

### 4.记录上一次视频播放位置

![image-20240517123201942](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240517123201942.png)





### 5.制作三角形

```
    .haha {
      width: 0;
      height: 0;
      border: 100px solid transparent;
      border-top-color: pink;
    }
```



### 6. 文本域空白区域

![image-20240831184445664](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831184445664.png)

如果<textarea></textarea>不在同一行会出现空白区域，你放在同一行就完事了



## 8. 移动端

### 8.1 区别



#### ① 视口

最标准的视口：

```
 <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,
 user-scalbale=0">  
```



![image-20240907132115988](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240907132115988.png)

#### ② 二倍图

**<font color='red'>一句话概括：PC端的准备的图片在移动端可能被放大，放大后就模糊了。解决思路就是：比如移动端物理像素比是2，原先图片是50px*50px,现在准备100px*100px的二倍图，手动css代码修改为width,height=50px，然后在移动端自动放大二倍后也不会出现模糊的情况</font>**

![image-20240907133002338](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240907133002338.png)

![image-20240907133629784](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240907133629784.png)









# 二.Vue



## 1.Vue核心



### 一些知识点	





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



![image-20240506141316420](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506141316420.png)





- **问题的解决**

**可以调用数组里的那七个api，也可以使用Vue.set(target,key,value),这个问题在vue3中已经不存在了！！！！**

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

![image-20240319141444920](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240319141444920.png)





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

![image-20240319143003748](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240319143003748.png)











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

**<font color='orange'>v-model 一般只用于表单属性</font>**

![image-20240506144227751](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506144227751.png)

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

![img](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/20210712190852410.png)





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

![image-20240506145621186](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506145621186.png)





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

```
1. beforeCreate
官网：在实例初始化之后,进行数据侦听和事件/侦听器的配置之前同步调用。

详细：在这个阶段，数据是获取不到的，并且真实dom元素也是没有渲染出来的

2. created
官网：在实例创建完成后被立即同步调用。在这一步中，实例已完成对选项的处理，意味着以下内容已被配置完毕：数据侦听、计算属性、方法、事件/侦听器的回调函数。然而，挂载阶段还没开始，且 $el property 目前尚不可用。

详细：在这个阶段，可以访问到数据了，但是页面当中真实dom节点还是没有渲染出来，在这个钩子函数里面，可以进行相关初始化事件的绑定、发送请求操作

3. beforeMount
官网：在挂载开始之前被调用：相关的 render 函数首次被调用。

详细：代表dom马上就要被渲染出来了，但是却还没有真正的渲染出来，这个钩子函数与created钩子函数用法基本一致，可以进行相关初始化事件的绑定、发送ajax操作

4. mounted
官网：实例被挂载后调用，这时 el 被新创建的 vm.$el 替换了。如果根实例挂载到了一个文档内的元素上，当 mounted 被调用时 vm.$el 也在文档内。
注意 mounted 不会保证所有的子组件也都被挂载完成。如果你希望等到整个视图都渲染完毕再执行某些操作，可以在 mounted 内部使用 vm.$nextTick：

详细：挂载阶段的最后一个钩子函数,数据挂载完毕，真实dom元素也已经渲染完成了,这个钩子函数内部可以做一些实例化相关的操作

5. beforeUpdate
官网：在数据发生改变后，DOM 被更新之前被调用。这里适合在现有 DOM 将要被更新之前访问它，比如移除手动添加的事件监听器。

详细：这个钩子函数初始化的不会执行,当组件挂载完毕的时候，并且当数据改变的时候，才会立马执行,这个钩子函数获取dom的内容是更新之前的内容

6. updated
官网：在数据更改导致的虚拟 DOM 重新渲染和更新完毕之后被调用。
当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用计算属性或 watcher 取而代之。

详细：这个钩子函数获取dom的内容是更新之后的内容生成新的虚拟dom，新的虚拟dom与之前的虚拟dom进行比对，差异之后，就会进行真实dom渲染。在updated钩子函数里面就可以获取到因diff算法比较差异得出来的真实dom渲染了。

7. beforeDestroy
官网：实例销毁之前调用。在这一步，实例仍然完全可用。

详细：当组件销毁的时候，就会触发这个钩子函数代表销毁之前，可以做一些善后操作,可以清除一些初始化事件、定时器相关的东西。

8. destroyed
官网：实例销毁后调用。该钩子被调用后，对应 Vue 实例的所有指令都被解绑，所有的事件监听器被移除，所有的子实例也都被销毁。
详细：Vue实例失去活性，完全丧失功能
```



#### ③两个最重要常用的钩子函数



**mouted  和  updated**







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







## 3.Vue技术·上篇



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









### 3.2 ref捉dom

<font color='red'>相当好用啊，不用js那么麻烦的获取了！！！！</font>

**//某些特殊场景我们确实需要获取dom元素，不建议使用js获取，可以使用vue提供的ref**

**//如果只是单纯地获取html标签，那传统的js代码和vue提高的ref确实没区别，但要是针对组件区别就大了！！！**

**//vue的ref可以获取组件实例对象**

```
使用方法:比如获取一个input的dom元素
import {ref} from 'vue'
<input type='text' ref='zlc'>
//名字必须和上面保持一致
const zlc = ref()
```





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



**vue3 中 如何使用props**

```
import {defineProps} from 'vue'

defineProps(['name','student'])//比如父组件传给子组件数据
但是 这里接收到的数据 只能使用大胡子打印，不能直接获取
需要重新接收 才能 对其操作
比如 let props = defineProps(['name','student'])
console.log(props.name)这样就可以取到了
```











**{备注：props是只读的，Vue底层会检测你对props的修改，如果进行了修改，就会发出警告，若业务确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据}**

**//如果你传的是一个基本类型的数据，修改的话vue会直接报错；但是如果你传的是一个对象,修改对象中的一个基本数据类型是不会报错的，只是vue不建议你这么写！！！！**





### 3.4 组件通信

#### 1.props

**<font color='orange'>实现父子通信</font>**

```

// Parent.vue 传送
<template>
    <child :msg="msg"></child>
</template>
​
// Child.vue 接收
export default {
  // 写法一 用数组接收
  props:['msg'],
  // 写法二 用对象接收，可以限定接收的数据类型、设置默认值、验证等
  props:{
      msg:{
          type:String,
          default:'这是默认数据'
      }
  },
  mounted(){
      console.log(this.msg)
  },
```

#### 2.父子双向绑定

和 <font color='red'>.sync 类似</font>，可以实现将父组件传给子组件的数据为双向绑定，子组件通过 $emit 修改父组件的数据

```

// 最简单的 v-model实现 父组件 Home 
<template>
  <div class="">
    <HelloWorld v-model="value"></HelloWorld>
    {{ value }}
  </div>
</template>
​
<script>
import HelloWorld from "../components/HelloWorld.vue";
export default {
  data() {
    return {
      value: "我是Home里的数据 响应式的",
    };
  },
  components: { HelloWorld },
};
</script>
// 子组件 HelloWorld
<template>
  <input :value="value" @input="handlerChange" />
</template>
<script>
export default {
  props: ["value"],
  methods: {
    handlerChange(e) {
       // 一定要是 input 事件
      this.$emit("input", e.target.value);
    },
  },
};
</script>

                        
原文链接：https://blog.csdn.net/qq_54753561/article/details/122281196
```

<font color='red'>.sync实现父子双向绑定</font>

**稍微讲解一下.sync修饰符,用于实现父组件与子组件之间的双向绑定**

```
//父组件
<HelloWorld :val.sync="val"></HelloWorld>
//子组件
this.$emit('update:val', newValue);
意思是子组件向父组件发送一个事件，事件名为 update:val，并将输入框的值作为参数传递。父组件监听这个事件后，可以更新自己的数据，达到双向绑定的效果。这里的 update:val 是约定的命名，用于与 .sync 修饰符配合使用。
这里的newValue一般都是Input框,这样写：this.$emit("update:val", event.target.value)
```

```

// 父组件 Home
<template>
  <div class="">
    <HelloWorld :val.sync="val"></HelloWorld>
    {{ val }}
  </div>
</template>
​
<script>
import HelloWorld from "../components/HelloWorld.vue";
export default {
  data() {
    return {
      val: "我是Home里的数据 响应式的",
    };
  },
  components: { HelloWorld },
};
</script>
​
// 子组件  HelloWorld
<template>
  <input class="i911-sync" :value="val" @input="handleInput" />
</template>
<script>
export default {
  name: "HelloWorld",
  props: {
    val: {
      type: String,
      default: "",
    },
  },
  methods: {
    handleInput(event) {
      this.$emit("update:val", event.target.value);
    },
  },
};
</script>

```



#### 3.ref

```
//父组件
<HelloWorld ref="child"></HelloWorld>
这样就直接使用了
vue2:this.$refs.child.xxxx
vue3:const child = r
```











### 3.5 Vue插件

**//功能：增强Vue**

**//本质就是包含install()方法的一个对象。install方法第一个参数默认是Vue原型，第二个以后的参数是插件使用者传递的数据**

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

**//作用:子组件 ===> 父组件，子组件传数据给父组件**

已经初步有mitt的感觉了

**使用演示：**

![image-20240530212638977](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240530212638977.png)













### 3.8 mitt

**//作用：实现任意组件通信**

**//vue2 的全局事件总线 ，pubsub，mitt本质都是提前绑定事件**



//配置mitt

```
1.npm i mitt //下载mitt

2.utils/emitter.js    //配置emitter.js

3.import mitt from 'mitt'    //emitter.js里面的内容
  const emitter =  mitt()
  export default emitter
```

//使用mitt

**使用技巧：哪个组件要数据，哪个组件就要绑定事件；哪个组件给数据，哪个组件就要触发事件**

理由：你想一下，如果一个组件有数据还需要绑定事件吗，直接调用方法不完事了？

```
比如现在随便在一个组件
import mitt from '@/utils/emitter'

emitter.all.xxx  			 //拿到所有绑定的事件,有很多便捷的api
emitter.emit('方法'，数据)			//触发事件
emitter.off('方法')				//解绑
emitter.on('方法')				//绑定

```



```
<template>
    <h1>父组件</h1>
    <Child></Child>
</template>

<script setup>
import {ref,reactive} from 'vue'
  import Child from './components/Child.vue'
  import emitter from '@/utils/emitter'

  emitter.on('getName',(name) => {
    console.log(name)
  })


</script>
<style>

</style>
```

```
<template>
<h2>子组件</h2>
</template>

<script setup>
  import {ref,reactive} from 'vue'
  import emitter from '@/utils/emitter'

  let myname = ref('赵联城')

  emitter.emit('getName',myname.value)  



</script>

<style>

</style>
```







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

**/其实$nextTick()也是一个钩子函数**

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









## 4.Vue技术·下篇



### 4.1 axios配置代理

**简介：通过配置vue的vue.comfig.js**

![image-20240511125441943](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511125441943.png)

**那么如何开启代理服务器呢？？？？**

- 方法一：nginx （专业）
- 方法二:   vue-cli （用于自己学习）



**使用**

```
1.npm i axios

2.api/http.js

//配置axios
import axios from "axios";

const service = axios.create({
  baseURL:'http://localhost:8080',
  timeout:5000
})
//请求拦截器
service.interceptors.request.use((config) => {
   请求拦截器需要返回config！！！
  return config
},e => Promise.reject(e))
//响应拦截器
service.interceptors.response.use(res => res.data,e=>{
  return Promise.reject(e)
})

export default service
```



实在是受不了了，不知道为什么配置代理一直失败，干脆直接后端解决跨域问题了！

```
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOriginPatterns("*")
                .allowedMethods("GET", "HEAD", "POST", "PUT", "DELETE", "OPTIONS")
                .allowCredentials(true)
                .maxAge(3600)
                .allowedHeaders("*");

    }

}
```



### 4.2 插槽



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











### 4.3 Pinia

<font color="red">**Vue3使用Piano,Vue2才使用vueX**</font>

#### ① 引出

**//当组件间的通信变得复杂，那么全局事件总线实现起来就很麻烦**

**// Pinia相当于一个仓库 存放着 一些通用的数据**

![image-20240511155252491](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511155252491.png)

#### ②使用

```
1.下载pinia
 npm i pinia
 
2.main.js中配置

import { createApp } from 'vue'
import App from './App.vue'
//引入Pinia
import {createPinia} from 'pinia'

createApp(App).mount('#app')
//创建pinia
const pinia = createPinia()
//安装Pinia
app.use(pinia)

3.新建store文件夹
  里面比如User.js 就和用户相关的公用数据
  
4.配置store/count.js
	import {defineStore} from 'pinia'
	
	const useCountStore = defineStore('此处规范建议为文件名:count',{
	//真正存储数据的地方
	 state(){
	 	return {
	 		sum:6
	 	}
	 }
	})
	
	
	export default useCountStore
	
5.使用store
import {useCountStore} from '@/store/count.js'
const countStore = useCountStore()
//取出state中的数据
console.log(countStore.sum)
```

































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
//引入路由器
import router from './router'


const app = createApp(App)
//使用路由
app.use(router)
app.mount()

```







#### ③ 配置路由

在src下面生成一个目录router/index.js,内容如下：

**结构一**

```js
//引入一些需要使用的方法
import {
createRouter,
  createWebHashHistory,
} from 'vue-router'

//创建路由
const router = createRouter({
  history:createWebHashHistory(),
  routes:[
    //默认路由
    {
        path:'/',
        redirect:'/home'
    },
    {
    	path:
    	component:
    }
  ]
})



export default router

```

**结构二:   这个结构可读性更强一些!**

```js
// history模式
import {
    createRouter,
    createWebHashHistory,
} from 'vue-router'

import Home from '../pages/Home.vue'
import About from '../pages/About.vue'

const routes = [
// 路由的默认路径
    {
        path:'/',
        redirect:"/home"
    },
    {
        path: '/home',
        component: Home
    },
    {
        path: '/about',
        component: About
    },
]

// 创建路由对象
const router = createRouter({
    history: createWebHashHistory(),
    routes
})
export default router;
```



#### ④ 使用路由

**router-link这个标签底层是转成a标签，这就注定有些场景下是有局限的**

```
链接标签: <router-link to="/组件名">xxx</router-link>

显示标签: <router-view></router-view>
```









### 5.3 几个注意点



- 1.涉及路由的组件我们放入文件夹pages/views ,普通组件还是放在components
- 2.来回切换组件，组件是在不停地销毁产生
- 3.每个路由相关的组件身上多了两个属性，一个是自身信息的route(传参有用)，一个是共同的router路由器(里面封装很多好用方法)
  - ![image-20240511201359998](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240511201359998.png)





### 5.4 多级路由



区别就两个:

```
//1.在父级下面加入children数组，一定要注意此处的path 不需要加/  ，再说一遍：二级路由不要加 / ,底层会自己加，有点大病的设置
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
						//知道这么写就完事了
<router-link :to='`/home/test1/msg?id=${item.id}&title=${item.title}`'>{{item.id}}</router-link>
```

```
//接收参数，这时候就用到了我们前面学到的多出来的两个属性中的route,里面的query
  <h4>消息编号:{{ $route.query.id }}</h4>
  <h4>消息标题:{{ $route.query.title }}</h4>
```



#### ②page对象携带参数(推荐！！！)

```
<router-link :to='{
	path:'/home/test1/msg',/name:'xx'
	query/params:{
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





#### ④路由配置参数

//这个感觉没什么用啊

```
          children:[
            {
              name:'msg',
              path:'msg',
              component:Msg,
              //知道这一种就ok了
              //这里会提供一个参数$route里面有query和params的数据
              props($route){
                return {
                  id:$route.query.id,
                  title:$route.query.title
                }
              }
            }
          ]
```



```
接收数据：
        //只需要props接收即可使用
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







### 5.7 路由工作模式

![image-20240515220751223](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240515220751223.png)





### 5.7 replace属性

**//底层还有一个浏览器历史记录栈这么个东西**

![image-20240512095015226](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240512095015226.png)





### 5.8 编程式路由导航



- 引入：<router-link这个标签底层是转换成a标签，具有局限性，比如如果是一个按钮图片跳转，或延迟三秒跳转就无法实现



**路由跳转**

```
methods:{
	xxx(){
		this.$router.push/replace({     //使用router路由器封装的方法
			name:xxx,
			query:{
				xxx
			}
		})
	}
}
```

**路由前进后退**

```
methods:{
	xxx(){
		this.$router.back() // 后退一步
		this.$router.forward()  //前进一步
		this.$router.go(N)  //整数前进N步   负数倒退N步
	} 
}
```





### 5.9 缓存组件

**//如果不写include那么所有在此处展示的组件都不被销毁，注意此处写组件名！**

**//如果想写多个组件，  :include="['xx','xx','xx']"**

![image-20240512101346510](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240512101346510.png)





### 5.10 两个新钩子函数

**<font color="red">路由组件特有的生命周期!</font>**



- **active:当组件激活时,简单来说就是页面出现它就触发**
- **deactive:当组件失活时，简单来说单页面失去它就触发**

```
active(){

},
deactive(){
	
}
```



**例子：**
想要实现“欢迎学习Vue”使用setInterVal实现若隐若现，但是切换组件时，文本框内容保留，setInterVal停止

![image-20240512102417097](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240512102417097.png)



解读：to,from的结构

- name就是 路由配置的name，path就是路由配置的path
- params query就是数据
- **meta就是程序员自己添加的一些数据,比如 meta:{requestAuth:false},通过这个可以判断有无权限跳转**

![image-20240512121357908](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240512121357908.png)









### 5.11 路由守卫





#### ①全局路由守卫⭐

**//核心作用就是：检验是否有权限跳转**



**例子演示：**

```
//1.创建一个路由器不要直接暴露
const router = new VueRouter({   √ 

//2.配置全局前置路由守卫
router.beforeEach((to, from, next) => {
  localStorage.setItem('user','zl1c')
    if(to.meta.requestAuth) {
      if(localStorage.getItem('user') === 'zlc'){//如果用户名是zlc就允许跳转
        next()
      }else{
        alert('用户没有权限') 
      }
    }else{
      next()
    }
})

//3.配置全局后置路由守卫
router.afterEach((to,from) => {
	document.title = to.meta.title  //实现当前在哪个页面就将head标签中的title修改为当前标题
})

//4.暴露路由器
export default router
```



### 5.12 路由器的两种工作模式





**//可以通过nginx解决history的问题**

![image-20240512130148257](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240512130148257.png)

### 5.13 默认路由与重定向

**//将path 变为 redirect中的路径,一般用于默认路由**

![image-20240515133750594](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240515133750594.png)







### 5.14 路由跳转

- <font color='red'>路由跳转</font>

在vue2中我们通常会在全局的接口请求里面设置拦截器，如果登录失效或者说其他情况需要跳转到登录页面或者说其他页面的，我们就使用this.$router.push实现
vue3中同样使用该方式：

```
import { useRouter } from 'vue-router';

const router = useRouter();

router.push()
```

但是控制台会报错：

Cannot read properties of undefined (reading 'push')

这是英文useRoute, useRouter必须写到setup中,强行在函数中使用这两会报undefined,导致无法获取路由数据和路由方法。

此时要修改引入方式：

<font color='orange'>正解：</font>

```
import Vrouter from "@/router"、

const router = Vrouter;

router.push({
	path:'xxx',
	query:{
		//如果传的是对象，需要JSON.stringfy()转换成json字符串才行，不能直接传对象
	}
})
```





- <font color='red'>路由传参</font>

接收数据

```
import { useRoute } from 'vue-router'

const route = useRoute()

const user = JSON.parse(route.query.user)//如果是对象则需要使用JSON.parse()转换！
const userId = route.query?.id
```

































## 6.集中式状态(数据)管理

**vue2 经常使用的是 vueX ; vue3 经常使用的是  pinia**



### 6.1 搭建环境

```
npm i pinia
```

```
import { createApp } from 'vue'
import App from './App.vue'
//第一步：引入pinia
import { createPinia } from 'pinia'

const app = createApp(App)
//第二步：创建Pinia
const pinia = createPinia()
//第三步: 安装Pinia   最好在const app = createApp(App)后面安装Pinia
app.use(pinia)
app.mount('#app')
```

```
//1.在src目录下创建 store文件
```



### 6.2 存储读取

**store下面的count.js文件**

```
import { defineStore } from "pinia";
							//规范：要求使用useXXXStroe当对象名，defireStroe的的第一个参数应该是文件的名字			
export const useCountStore = defineStore('count',{
  //真正存储数据的地方
  state(){
    return {
      sum:6
    }
  }
  //用于响应组件的方法
  	actions里面的this指向useCountStore,里面直接就可以使用属性this.xxx
  actions{
		test(){
			xxxxx
		}
	}
})
```

**组件中的使用**

```
  import { useCountStore } from '@/store/count'; 

  const countStore = useCountStore()  //countStore是一个Porxy
    function add(){
    countStore.sum += n.value 
  }
  function device(){
    countStore.sum -= n.value
  }
```



### 6.3 stroeToRefs



**//关于解构赋值，如果使用toRefs会导致countStore自带的方法出问题，所以要使用pinia提供的一个API代替**

![image-20240515200353800](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240515200353800.png)









### 6.4 修改数据

```
//1.直接修改
	countStore.sum += 1

//2.批处理
	可以一次性修改多个数据，且有提示词
	countStore.$patch({
		sum:888,
		school:'xxx',
		address:'xxx'
	})

//3.调用文件中的actions里面的方法
```





### 6.5 getters

//类比computed





### 6.6 $subcribe

//类比watch



### 6.7 组合式写法

类比setup







## 7. Vue3



### 7.1 工程结构的区别



#### ① app挂载与引入crateAp工厂函数

![image-20240514133106804](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514133106804.png)





#### ②



### 7.2 常用Composition API



#### 1.拉开序幕的setup

```
vue@3.2以上的版本 可以使用setup语法糖
//1.不需要return,不需要组件名
//2.组件名就是文件名
//3.但是import还是不能省略
  <script setup>
    import {ref,reactive,computed} from 'vue'

    let person = reactive({
        firstName:'jack',
        lastName:'ssson',
      })
      person.fullName = computed(() => {
        return person.firstName + person.lastName
      })
  </script>
```



**//如果你使用了setup语法糖，那么还想要指定组件名，可以这样写,直接在script标签属性的name写**

![image-20240515134540882](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240515134540882.png)



![image-20240514133905057](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514133905057.png)

![image-20240514154318848](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514154318848.png)











#### 2.ref函数

**//推荐使用ref函数，因为ref函数接收对象类型，底层就是使用的reactive函数**

**ref在模版里面使用不需要.value**

![image-20240514141234759](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514141234759.png)

![image-20240514140139518](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514140139518.png)



**Proxy是ES6中提出的，它没有Object的get set，是通过**

![image-20240515130425088](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240515130425088.png)

**//如果是数组的话，vue2底层用的是definxxx什么的，不能直接修改，但是vue3底层用的是Proxy可以直接修改**



**//一个注意点：因为你使用ref函数，使其变成refimp引用对象，需要通过引用对象.value获取值，但是如果在reactive中有一个属性使用了ref函数，此时不需要拆解属性，直接就可以使用！！！！**

![image-20240515142728820](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240515142728820.png)



#### 3.reactive函数



![image-20240514141325873](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514141325873.png)

![image-20240515132009064](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240515132009064.png)



![image-20240515132117419](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240515132117419.png)

[你和我一样纠结过vue3的 ref() 和 reactive()吗？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/663590743)



#### 4.计算属性

**//将Vue3中计算属性直接变成了一个方法，不过一般都是使用简写形式**

![image-20240514162132335](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514162132335.png)





#### 5.watch监视

**//反正watch相比计算属性少用**

其他情况就那么写

![image-20240514174253018](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514174253018.png)







#### 6.生命周期

**![image-20240514180003987](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514180003987.png)**



#### 7. hook

**hook == java中的utils工具**



**//那以后是不是都会变成这样，需要修改什么就直接去修改对应的hook**

```
 <script setup>
    import usePoint from '@/hooks/usePoint'
    import .............
	
	 useXXX()
	 useXXX()
	 useXXX()
	 useXXX()
    let XXX = usePoint()
    let XXX = usePoint()
    let XXX = usePoint()
    let XXX = usePoint()
 </script>
```



**例子**

```
//就相当于java中的utils,只不过习惯将里面的js文件命名为useXXXX
//记录鼠标打点xy的工具方法
import {ref,reactive,onMounted,onBeforeUnmount} from 'vue'
export default function(){
  let point = reactive({
    x:0,
    y:0
  })
  //保存鼠标xy
  function savaPoint(event){
    point.x = event.pageX
    point.y = event.pageY
  }

  onMounted(()=>{
    window.addEventListener('click',savaPoint)
  onBeforeUnmount(()=>{
    window.removeEventListener('click',savaPoint)
    })
  })

  return point
}
```

​	

```
<template>
  <div>
    <h2>鼠标的X:{{ point.x }},y:{{ point.y }}</h2>
  </div>
  </template>
  
  <script setup>
    import usePoint from '@/hooks/usePoint'

    let point = usePoint()

  </script>
```





#### 8.toRef与toRefs

**用来复制reactive中的属性，然后转为ref对象，既保留了响应式，又保留了引用。也就是你从 `reactive` 复制过来的属性进行修改后，除了视图会更新，原有 `ractive` 里面对应的值也会跟着更新 ! ! ! ! ! !**   



换句话说，toRef 和 toRefs 就是用来创建响应式的引用的，主要用来取出响应式对象里的属性，或者解构响应式对象，解构出来的属性值依然是响应式属性，**如果不用 toRef 或者 toRefs，直接解构会丢失响应式效果。**



<font color="red">**toRef和toRefs都是浅拷贝！！！！！**</font>

<font color="red">**专门搭配解构赋值很方便！！**</font>

```
const x = toRef(person,'name')
console.log(x.value)

let {name,age} = toRefs(person)
console.log(name,age)
```





### 7.3 其他Composition API



#### 1.响应式数据的判断

![image-20240514221553053](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514221553053.png)







### 7.4 新的组件



#### 1.Fragment(理解)

![image-20240514222146119](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514222146119.png)





#### 2.Teleport







#### 3.Suspense









## 8.Vue UI组件库



### 8.1 ElementUI-Plus



















# 三.React



















# 四 项目经验





## 1.品优购



### ① 版心

可以准备一个版心  

```
/* 版心 */
  .w {
    width: 1200px;
    margin: 0 auto;
  }
```



### ②公共样式

本次项目一些常用的样式 可以提取出来，比如需要某一些字段变成color:red

你要是一个一个去找到修改 太麻烦了

```js
//1.首先准备 公共样式
.style_red {
 	color:red
}
//2.使用公共样式
<ul>
	<li>品优购欢迎您！</li>
	//你看这样是不是更加便捷高效，可读性也更高了呢？
	<li><a href="#" class="style_red">请登录</a></li>
</ul>
```



### ③制作竖线

![image-20240902142117303](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902142117303.png)

**这种竖线的最佳做法：使用li 制作**

具体流程：    将li变成一根竖线

```
        <ul>
        <li><a href="#">我的订单</a></li>
        <li></li>
        <li><a href="#">我的品优购</a></li>
        <li></li>
        <li><a href="#">品优购会员</a></li>
        <li></li>
        <li><a href="#">企业采购</a></li>
        <li></li>
        <li><a href="#">关注品优购</a></li>
        <li></li>
        <li><a href="#">客户端</a></li>
        <li></li>
        <li><a href="#">网站导航</a></li>
      </ul>
```

```
  .shortcut .w .right ul li:nth-child(even) {
    width: 1px;
    height: 12px;
    background-color: #666666;
    margin-top: 10px;
  }
```

### ④ 搜索框制作

**这样的搜索框制作：大盒子里面套一个Input 一个button**

有个坑：input button 的高 不能是100%不然框会下坠

![image-20240902164230158](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902164230158.png)







### ⑤ 购物车数量栏

```
  .count {
    position: absolute;
    top: 1px;
    right: 10px;
    width: 20px;
    height: 20px;
    line-height: 20px;
    text-align: center;
    border-radius: 7px 7px 7px 0;         /、、、!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!、、、!!!!!!!
    background-color: rgb(213, 24, 24);           
    color: #f1f1f1;
  }
```

![image-20240902184239772](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902184239772.png)





### ⑥ 一个注意点

我以前都是给li padding--top 使其上下有距离，但实际上我们应该给每一个li  height！！！！！

![image-20240902201011832](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902201011832.png)



### ⑦排列十二个盒子

**要求：制作如下图所示的十二个排列整齐的盒子**

![image-20240904153832405](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240904153832405.png)

<font color='orange'>难点：如何解决border叠加？ 思路1：margin负值的妙用，但是会导致盒子位置偏移</font>

<font color='orange'>思路2：严格的计算宽度×   此方法麻烦，需要准确的计算</font>

<font color='orange'>思路3：只给每一个li border-right和border-bottom,然后给大盒子border-top(此案例也有了故不用给)和left,但是这样盒子会溢出，如何解决？答：扩大ul 使盒子能被装下，超出的部分切掉即可，这样损失一点点像素也无伤大雅!!!!!!</font>

![image-20240904154244937](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240904154244937.png)



**代码实现**

```
  /* 快报 lifesrvice */
  .newsflash .lifeservice {
    height: 150px;
    border:1px solid #aeadad;   //设置border，其实单独设置左右也可以
    border-top: 0;			//去除重复的上
    border-bottom: 0;		//去除重复的下
    overflow: hidden;	//隐藏超出的部分
  }
  .newsflash .lifeservice ul {
    width: 252px;      //扩大ul的宽
  }
  .newsflash .lifeservice ul li {
    float: left;
    width: 60px;
    height: 50px;
    border-right: 1px solid #aeadad;
    border-bottom: 1px solid #aeadad;
  }
```



### ⑧ 版心的使用

```
.w {
	wight:1200px;
	margin: 0 auto;
}


这个版心的两种使用
第一： 并列类
    <div class="header w"></div>
第二:  嵌套
	<div class="header">
		<div class="w">
		</div>
	</div>
```













# 五.思路





## 1.入门



### 1.1   图片旋转覆盖

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905140758590.png)

- 思路1：伪类选择器+2D旋转+过渡

- <font color='red'>**不用担心影响其他盒子的布局，因为2D转换不会影响其他盒子布局**</font>

- **不止是下面案例所演示的，你给after也可以做到，方法不唯一很多！**

- ```
   //注意超过盒子范围的::after图片要被隐藏
   .box{
   	略
   	overflow:hidden;
   }
   
   //给盒子下面放一张图片
    .box::before {
      content: '';
      display: block;
      width: 100%;
      height: 100%;
      background: url(../assets/images/test1.jpg);
      background-size: 100%,100%;
      transform-origin: left bottom;     //设置旋转中心点
      transform: rotate(90deg);		   //设置 旋转角度
      transition: all .5s;				//设置过渡
    }
    // 当鼠标划过，将旋转清空 即可将图片旋转上去
    .box:hover::before {
      transform: rotate(0);
    }
  ```





### 1.2 扩散效果

![image-20240905172654422](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240905172654422.png)



- 思路：一个点重叠三个圆盒子，动画

- ```
  //中心圆点
  .point {
  	略
  }
  //圆盒子
  .circle {
    position: absolute;
    top: 49%;
    left: 48%;
    transform: translate(-50%, -50%);
    width: 6px;
    height: 6px;
    border-radius: 50%;
    box-shadow: 0 0 12px #009dfd;       //阴影效果
    animation:diffuse 1.2s linear infinite;   //调用动画
  }
  @keyframs diffuse {
  	70% {
  		weight:40px;
  		height:40px;
  		opacity:1;
  	}
  	100%{
  		weight:100px;
  		height:100px;
  		opacity:0;
  	}
  }
  ```

  



### 1.3 文字逐个显示

思路：利用动画的steps,控制好字体大小与一行大小

```
  .w {
    text-align: center;
    overflow: hidden;
    line-height: 50px;
    width: 400px;
    height: 50px;
    background-color: pink; 
    white-space: nowrap;            //强行让文字在一行上，防止影响布局
    animation: test 3s steps(20)    //vital code
  }
  .w span {
    font-size: 20px;
    color: #42233b;
  }
```





### 1.4 图片翻转

- 效果：鼠标经过图片使其翻转并显示后面的图片

```
.w {
  position: absolute;
  top: 40%;
  left: 40%;
  width: 100px;
  height: 100px;
  transition: all 1s;
  perspective: 500px;                  //透视
  transform-style: preserve-3d;		  //让子元素的3d效果呈现
}
.front {
  z-index: 1;
  position: absolute;
  width: 100px;
  height: 100px;
  background: url(../assets/images/test3.jpg);
  backface-visibility: hidden;     //隐藏后背 ！！！！
  background-size: 100% 100%;
}
.back {
  position: absolute;
  width: 100px;
  height: 100px;
  background: url(../assets/images/test4.jpg);
  background-size: 100% 100%;
  transform: rotateY(180deg);
}
.w:hover {
  transform: rotateY(180deg);     //翻转！
}
```





### 1.5 轮播图

![image-20240907122700515](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240907122700515.png)

- 

- 思路：<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240907122831233.png" style="zoom:50%;" />

- ```js
  // 动画：旋转360度
  @keyframes move {
    100% {
      transform: rotateY(360deg);
    }
  }
  .body {
    perspective: 1000px;      //透视
  }
  
  .box {
    position: relative;
    margin: 150px auto;
    width: 300px;
    height: 300px;
    transform-style: preserve-3d;               //
    animation: move 15s linear infinite;        //调用动画
  }
  
  .box div {
    position: absolute;
    top: 0%;
    left: 0%;
    width: 100%;
    height: 100%;
    background: url(../assets/images/test4.jpg) no-repeat;
    background-size: 100% 100%;
  }
  
  // 六个盒子的布局
  //相当于一个六边形 每个边到中心点的距离是一样的，每次旋转六十度，六个就是360度,如果是四个就应该是90度
  .box div:nth-child(1) {
    transform: translateZ(400px);
  }
  
  .box div:nth-child(2) {
    transform:  rotateY(60deg) translateZ(400px);//   先旋转 再移动，旋转六十度 该图的z轴也会旋转六十度
  }
  .box div:nth-child(3) {
    transform: rotateY(120deg) translateZ(400px);
  }
  .box div:nth-child(4) {
    transform: rotateY(180deg) translateZ(400px);
  }
  .box div:nth-child(5) {
    transform: rotateY(240deg) translateZ(400px);
  }
  .box div:nth-child(6) {
    transform: rotateY(300deg) translateZ(400px);
  }
  .box:hover {
    animation-play-state: paused;
  }
  ```

  





















