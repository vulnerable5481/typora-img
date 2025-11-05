# 一.前端三板斧



## 1.HTML

 

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

#### ④属性选择器

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
  - 子元素可以继承父元素一些样式，但是只能继承文字等相关样式，但是不会继承浮动啊边框等其他元素

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

#### ①定位组成及语法

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




#### ② 子绝父相

![image-20240330171833737](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330171833737.png)



#### ③ 定位叠放次序

![image-20240330183200722](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330183200722.png)

#### ④ 定位的一些特性

**//目前已知可以给行内元素设置宽度高度的方法:**

- display: block/inline-block  
- float:left;
- position: absolute / fixed

![image-20240330184511724](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240330184511724.png)

浮动只会对之前的元素有影响，而且浮动只会压住下面的标准流盒子，不会压住下面标准流盒子中的文本/图片，标准流盒子中的文字/图片会被挤到一边

但是绝对定位/固定定位 会完完全全地压住盒子和盒子中所有的内容



### 2.7 两种显示隐藏元素

![image-20240331150414524](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240331150414524.png)

![image-20240331150517629](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240331150517629.png)

![image-20240331150946186](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240331150946186.png)



## 3.CSS下篇

### 3.1 精灵图

#### 为什么需要

**//精灵图本质就是一堆图放在一张大图片上去，浏览器向服务器只需要请求一次即可，大大降低页面的加载速度	**

![image-20240520170937036](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240520170937036.png)

#### 如何使用



![image-20240831175847095](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831175847095.png)



`![image-20240903120304641](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240903120542619.png)

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240903120542619.png)









### 3.2 字体图标

![image-20240831180645761](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240831180645761.png)

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

- **<font color='red'>注意弹性布局禁用此属性！！！！</font>**

- 文字默认是和图片的基线对齐，如果想要文字和图片垂直居中对齐只能暴力调xy那可不行，通过vertical-align即可实现


- **<font color='orange'>用于实现图片/文本域 和 文字垂直居中</font>**

- <font color='red'>**vertical-align只能和行内块元素使用，如果是一个盒子可以与display:inline-block搭配使用**</font>

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

![image-20240901120001037](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901120001037.png)

#### ② 视频标签

```
<vedio>
```

#### ③ 音频标签

#### ④ input验证

肯定还是要用正则表达式去验证，但可以用这个当做前端初步验证

![image-20240901121120303](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240901121120303.png)

#### ⑤ 盒子新模型

![image-20240902112915595](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902112915595.png)

**默认是 box-sizing:content-box,如果你修改成了 box-sizing: border-box，就不会撑大盒子了**

```
*{
  margin:0;
  padding:0;
  box-sizing:border-box  //css初始化可以加上这一句，这样就不会有撑大盒子的问题了
}
```

#### ⑥ favicon图标

vue3修改favicon图标的方法

1.使用比特虫网站  生成 .ico图片

2.将其添加到public下面，命名为favicon.ico

3.在index.html 中修改<link rel="shortcut icon" type="image/x-icon" href="./favicon.ico">

![image-20240902122739786](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902122739786.png)





## 4.CSS++

### 4.1 过渡

![image-20240902113306480](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113306480.png)

![image-20240902113438038](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113438038.png)





![image-20240902113715076](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113715076.png)

![image-20240902113853222](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240902113853222.png)









### 4.2 2D转换

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
  实现：思路1：子绝父相   思路2:直接transfrom:translate(0,y)
  明显思路2要更加简单，只需要一行代码就搞定，思路1还需要修改父盒子什么的
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



### 4.3 动画

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





### 4.4 3D转换

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

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509120603382.png)

#### 1.2 数据类型

- 布尔值
  - 空字符串 默认是 false
  - 除了空字符串其他的非布尔值全都会隐式转换成true

#### 1.3 Bob

```
Blob 对象表示一个不可变、原始数据的类文件对象
```



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
xxx.addEventListener('click',function(event){//})

event：这里的event包含了一些事件相关的数据
```

![image-20240509181304225](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509181304225.png)



#### 2.4几个重要知识

- ##### **事件对象**

作用：可以获取事件触发时的相关信息

例如:鼠标点击事件，事件对象就存储了鼠标点在哪个位置等信息，可以实现点哪里哪里就出现特效

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

普通函数的this指向的是window,因为是window调用的函数

简单一句话，谁调用的就指向谁

- **回调函数**

```
回调函数 = 传给别人执行的函数，通常在某个事件或异步操作完成后被调用。

1、比如异步事件回调：在点击之后再去调用对应的方法
document.addEventListener("click", function(event) {
  console.log("页面被点击了！");
});
2、AJAX 请求
  这样的请求也是回调函数，回调是在请求成功和失败后触发
3、事件监听
   在对应的事件触发后，进行回调
and so on ...
```



#### 2.5 事件流

```
1、什么是事件流？
	就是事件触发后在DOM树上按照一定的顺序流动，触发相应相应元素的事件处理函数。
	
2、事件流的三个阶段
	有三个阶段：捕获阶段从document>html>body>..>目标元素，一层层捕获，目标阶段，事件到达目标阶段就触发对应的函数，冒泡阶段则是从目标元素依次向上层冒泡，不断触发父元素对应的事件，捕获阶段我们一般不关注，一般关注的是冒泡阶段，这里除了focus、blur等不冒泡的事件，其他都会被事件流经过

3、事件冒泡
	冒泡就是点击目标元素，会触发目标元素及其父元素的事件，比如触发子元素的click事件，那么也会触发父元素的click事件，这样就形成了一个事件流，会向上层不断冒泡一样的触发事件。【触发的是子元素与父元素同名的事件，比如都是click事件】
```



![image-20240509215801602](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509215801602.png)

#### 2.6事件委托

```
1、事件委托
	就是利用冒泡机制，将子元素的事件绑定给父元素，这样利用冒泡机制委托给父元素。
2、好处：
	假如要给多个子元素绑定相同事件，不如直接只给父元素绑定即可
```



#### 2.7 其他事件

##### ① 页面加载事件

```
1、一般都是写在head部分，当然vue就无所谓了

2、例子：
	// 页面资源加载事件
    window.addEventListener('load', () => {
      console.log('页面所有资源（图片、样式等）都加载完毕！');
    });
    // 页面即将关闭/刷新事件
    window.addEventListener('beforeunload', (event) => {
      event.preventDefault();
      event.returnValue = ''; // Chrome 需要这样才能弹出提示
    });
```

##### ② 页面滚动事件

**//不仅仅是window里面有，普通的事件也有**

![image-20240509224019879](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224019879.png)

![image-20240509224318782](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224318782.png)

![image-20240509224517953](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224517953.png)

![image-20240509224648219](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240509224648219.png)

##### ③ 页面尺寸事件

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

- 增加节点 :演示
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

```
1、navigation对象的主要作用就是里面有很多关于浏览器的信息
   可以用来判断当前是移动端还是PC，PC跳转到哪个页面，移动端跳转到哪个页面

2、history对象的主要作用就是操纵浏览器历史记录，可以back/forward

3、vue中的下面几个方法底层都是用的history对象
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

​	**<font color='red'>节流和防抖本质都是优化高频率执行代码的一种手段,mouseEnter,mouseLeave,scroll等事件触发，会不断地触发，极大地浪费资源，为了优化性能，需要节流与防抖</font>**

- 定义

  - ```
    n 秒后在执行该事件，若在n 秒内被重复触发，则重新计时.
    ```

- 模版

  - ```
    // timeId是定时器变量
    function debounce(){
    	//如果有定时器就清除
    	if(timeId){
    		clearTimeout(timeId)
    	}
    	//开启新的定时器
    	timeId = setTimeout( () = > {
    		//执行逻辑
    	},t)
    }
    ```

- 例子

  - ```
    // 悬浮头像时，气泡的显隐
    function handleMouseEnter() {
      clearTimeout(outTimer); // 这里要清除隐藏的计时器，否则在0.2秒内出入头像，会导致头像变大但气泡突然消失
      inTimer = setTimeout(() => {
        popoverDisplay.value = "";
        isAvatarBig.value = true;
      }, 100);
    }
    function handleMouseLeave() {
      clearTimeout(inTimer); // 清除显示计时器防止快速经过头像时的气泡闪烁
      outTimer = setTimeout(() => {
        popoverDisplay.value = "none";
        isAvatarBig.value = false;
      }, 200);
    }
    ```

    

#### 4.7 节流

- 定义

  - ```
    n 秒内只运行一次，若在n 秒内重复触发，只有一次生效
    ```

- 模版

  - ```
    function test(){
    	//如果有定时器,则
    	if(timeId){
    		return;
    	}
    	//如果没有定时器
    	timeId = setTimeout(()=>{
            // fn 写在 setTimeout 内则是等待 delay 后才能执行，之后可以再次触；即先等待再触发
            // fn 写在 setTimeout 外是执行后等待 delay 才能再次触发，即先触发再等待
    		//执行逻辑
    		//程序执行完全，清除定时器
    	},t)
    }
    ```

  

  





### 5.ES6

#### ①导入

- **<font color='red'>默认导入</font>**
  - import userApi from '@/apis/userApi.js'
- <font color='red'>**命名导入**</font>
  - import { login register userName } from '@/apis/userApi.js'



#### ②导出

- <font color='red'>**默认导出**</font>
  - **定义**：使用 `export default` 关键字导出一个默认的实体（函数、类、对象等），一个模块只能有一个默认导出。
  - **语法**：默认导出时，不需要为导出的实体指定名称。
  - **导入方式**：导入时可以不使用大括号，并且导入的名称可以与导出时的名称不同。

- <font color='red'>**命名导出**</font>
  - **定义**：当一个模块中使用 `export` 关键字导出函数、变量或类时，我们称之为命名导出。
  - **语法**：使用 `export` 关键字导出多个不同的实体，导出时必须指定名称。
  - **导入方式**：导入时需要使用大括号 `{}` 来指定导出的名称。







#### ③异步处理

- 所谓异步处理，就是让你先暂时跳过回调函数，执行完整个异步操作之后，再折回去调用回调函数 ! ! ! !

- ```
  function asyncOpeation(){
  	return new Promise((resolve,reject) => {
  		setTimeout(() =>{
  			console.log('回调函数被执行')
  			resolve("操作完成"); // 解析 Promise，返回结果
  		},2000)
  	})
  }
  // 调用异步操作
  asyncOperation().then(result => {
      console.log(result) // 这里在异步操作完成后调用xx
  });
  // 立即输出内容
  console.log("开始异步操作")
  ```



#### ④异步最佳实践

- ES6抛弃了以往ajax那种冗余的写法，转而使用 Promise

- ```
  //定义异步操作
  function test = new Promise((resolve,reject) => {
  	//如果有回调函数，则在执行完整个异步操作后，最后执行回调函数
  	const message = function xxx(){}
  	//resolve会返回异步操作成功的结果,reject则返回失败
  	     if (success) {
              resolve("操作成功"); // 操作成功时调用 resolve
          } else {
              reject("操作失败"); // 操作失败时调用 reject
          }
  	
  })
  //可以使用.then来接收异步操作完全后的结果
  test.then(result => {
  	console.log(result);//异步操作的结果
  })
  //  async/await
  	//async 用来声明表示该方法是一个异步操作，但是你不写也没事，除非你想要使用await
  async function haha() {
  	//await表示等待异步操作完成，程序会卡在这里
  	console result = await test();
  }
  ```

  



### 6.实用api



#### ①FileReader

































## 6.flex布局



### 1. 注意事项

- 当我们给父元素display:flex, 子元素的float,clear,vertical-align属性都将失效



















### 2. 父项属性

#### ①flex-direction

**<font color='red'>设置主轴</font>**

```
1.按照X轴 （默认）
	flex-direction:row

2.按照X轴翻转
	flex-direction:row-reverse

3.按照Y轴
	flex-direction:column

4.按照Y轴翻转
	flex-direction:column-reverse
```



#### ② justify-content

**<font color='red'>注意flex布局中没有justify-items，这个属性是grid布局中的!!!!!</font>**

**<font color='red'>设置主轴上的子元素排列方式</font>**

```
1.从左开始 （默认）
	justify-content:flex-start
	
2.从右开始
	justify-content:flex-end

3.在主轴居中对齐 
	justify-content:center
	
4.平分剩余空间
	justify-content:space-around  :左右两端距离只有中间的一半，中间是完全平分
	justify-content:space-evenly  :全部完全平分剩余空间
	
5.先两边贴边，再平分空间
	justify-content:space-between
```



#### ③flex-wrap

**<font color='red'>设置子元素是否换行</font>**

- 如果我们使用的浮动，一行放不下盒子，就会将多余的放在下一行，但是在弹性布局中，**默认是不换行的**，会自动缩小每一个盒子，让其挤在一行

- ```
  1.允许子元素换行
  	flex-wrap:wrap
  
  2.默认不换行
  	flex-wrap:nowrap
  ```

  



#### ④align-items

**<font color='red'>设置测轴上的子元素排列方式(单行)</font>**

```
1.从上到下
	align-items:flex-start
	
2.从下到上
	align-items:flex-end
	
3.垂直居中
	align-items:center

4.拉伸(默认)
	align:items:stretch
```



#### ⑤align-content

**<font color='red'>设置侧轴子元素排行方式（多行）</font>**

```
除了上面四个属性，还多了两个
5.一个行贴上面，一行贴下面
	align-content:space-between

6.平分空间
	align-content:space-around
```





#### ⑥flex-flow

**<font color='red'>flex-direction和flex-wrap的复合属性</font>**

```
flex-flow:row wrap
```



### 3. 子项属性



#### ①flex

```
用来表示占据父盒子的几分   
a,b,c{
flex:1   //a,b,c各占据一份也就是各自1/3
}
```







## 7.响应式设计思路





### 7.1rem与媒体查询



#### ① rem

- rem也是单位，和em差不多，只不过rem = **<font color='red'>html</font>**中的font-size ， em = 父元素font-size 
- 默认 html 的 font-size = 16px  



#### ② 媒体查询

- **语法：** @media 【类型】 and ()

- **<font color='red'>类型=all可以省略</font>**

- 【**类型**】：  all   ,    screen（电脑手机平板屏幕）   ,  print(打印机or打印机预览)

- ```
  @media (min-width: 1367px) and (max-width: 1700.9px) {
      .channel-items__left {
          padding-right: 30px;
          grid-template-columns: repeat(11,1fr);
      }
  }
  ```

  

### 7.2 grid布局

**<font color='red'>对于响应式布局，grid非常好用</font>**



#### ①容器属性

- **<font color='red'>grid基本属性</font>**

  - ```
    .test{
      /* 声明一个容器 */
      display: grid;
      /*  声明容器按照列/行排列
      grid-auto-flow: rows  //默认是优先按照行排列
      //强调一点：grid-auto-flow:rows dense,加了dense会自动用下面小块填补上面空白
      /*  声明列的宽度  */
      grid-template-columns: repeat(3, 200px);
      /*  声明行的高度  */
      grid-template-rows: repeat(2, 200px);
      /*  声明行间距和列间距  */
      gap: 20px; //行间距列间距可以拆开写  columns-gap / row-gap
      /*  和flex的差不多  */
      【flex布局中没有justify-items!!!!!!!!!!!!!!别搞混了！！！！！】
      对内justify-items:strech(默认)/start/end/center
      对内alin-items:同上
      对外justify-content:strech(默认)/start/end/center
      对外alin-content:同上
    }
    ```

- **<font color='red'>进阶使用</font>**

  - **grid-template-areas 与 grid-area**

  - ```
    .text{
    	...同上 故略
    	  grid-template-areas:
        ". header  header"
        "sidebar content content";
    }
    .sidebar {
      grid-area: sidebar;
    }
    
    .content {
      grid-area: content;
    }
    
    .header {
      grid-area: header;
    }
    ```

  - **grid-auto-columns 属性和 grid-auto-rows 属性**

  - ```
    隐式和显示网格：显式网格包含了你在 grid-template-columns 和 grid-template-rows 属性中定义的行和列。如果你在网格定义之外又放了一些东西，或者因为内容的数量而需要的更多网格轨道的时候，网格将会在隐式网格中创建行和列
    假如有多余的网格（也就是上面提到的隐式网格），那么它的行高和列宽可以根据 grid-auto-columns 属性和 grid-auto-rows 属性设置。它们的写法和 grid-template-columns 和 grid-template-rows 完全相同。如果不指定这两个属性，浏览器完全根据单元格内容的大小，决定新增网格的列宽和行高
    
    ```


- **<font color='red'>响应式用法</font>**

- 这里的1fr就类似flex布局中 用“ flex:1 ”去等分划分区域一样，使用fr就可以实现响应式布局~~~~

  ```
  grid-template-columns:1fr 1fr 1fr
  ```

  





#### ②项目属性

- 通过控制网格线可以分别定位在哪根网格线，从而指定项目的位置

  - ```
    grid-column-start 属性：左边框所在的垂直网格线
    grid-column-end 属性：右边框所在的垂直网格线
    grid-row-start 属性：上边框所在的水平网格线
    grid-row-end 属性：下边框所在的水平网格线
    若有冲突，使用z-index决定优先级
    ```

  - ```
    .grid-item {
      grid-column: span 2; /* 从起始列开始，该元素占用2列 */
      /* 跨越从第1列到第3列，占据两个网格列的宽度，等价于 grid-column: span 2; */
      grid-column: 1/3;
      /* 跨越从第1行到第3行，占据两个网格行的高度 等价于 grid-r: span 2*/
      grid-row: 1/3;
    }
    ```

    









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



























































# 二.Vue2、3



## 1.Vue核心



### 一些知识点	



#### 1. vue-cli创建项目

vue2的脚手架：vue init 项目名

vue3的脚手架：vue create 项目名



#### 2.MVVM模型

![image-20240504193007719](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240504193007719.png)

#### 3.vue的数据代理【数据劫持】

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

**可以调用数组里的那七个api，也可以使用Vue.set(target,key,value),<font color='red'>这个问题在vue3中已经不存在了！</font>！！！**

addSex(){

​		Vue.set(this.student,'sex','男')

}



**//总结**

![image-20240506142422659](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240506142422659.png)









### 1.1插值操作(标签内容绑定)



#### (1)Mustache(大胡子)语法



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











### 1.2 v-bind

 <font color="red">**v-bind的实质就是将引号里面的东西当成js代码而不是字符串看待！！！！！！**</font>









### 1.2 v-model



**//可以双向绑定数据，即在一个输入框中你输入的信息也会实时影响vue实例中的数据**

**<font color='red'>v-model 一般只用于表单属性</font>**

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

**从数组中循环取出数据**

```
<li>
    <li v-for="student in students" :key="student.id">
    {{student.id}}-{{student.name}} <!--也可以直接{{student}}取出整体-->
</li>
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

- **<font color='red'>v-if 与 v-show的区别</font>**
- **//一个关于组件化的知识**

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

**<font color='red'>update , mounted常用</font>**

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

















## 2.Vue组件化编程







## 3.Vue技术



### 3.2 ref获取dom

### 3.3 props

### 3.4 组件通信

#### 1.props父子单向绑定

#### 2.props父子双向绑定

和 <font color='red'>.sync 类似</font>，可以实现将父组件传给子组件的数据为<font color='red'>双向绑定</font>，子组件通过 $emit 修改父组件的数据





<font color='red'>**<Child.  v-bind?v-model? = "data"><./Child>,此处应该是v-bind  or  v-model**</font>

**使用 `v-model`**：如果希望 `HelloWorld` 组件能够更新父组件的 `value`，并实现双向绑定。

**使用 `v-bind`**：如果只需要从父组件向子组件单向传递数据，不希望子组件修改数据。

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

 
//  Vue2版本 子组件 HelloWorld
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

//Vue3版本 子组件 HelloWorld
<template>
  <input :value="modelValue" @input="handlerChange" />
</template>

<script setup>
// 接收父组件传递过来的 v-model
const props = defineProps({
  modelValue: String, // 用于 v-model 的默认 prop
});

// 用于发出更新父组件数据的事件
const emit = defineEmits(['update:modelValue']);

// 处理输入的变化
const handlerChange = (e) => {
  emit('update:modelValue', e.target.value); // 更新父组件的值
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
这样就直接使用子组件里面的 数据  or 方法
vue2:this.$refs.child.xxxx
vue3:const child = ref()
```











### 3.5 Vue插件

- 使用方法：在main.js中 使用**Vue.use(xxx)**

### 3.7 自定义事件

**//作用:子组件 ===> 父组件，子组件传数据给父组件**

已经初步有mitt的感觉了

**使用演示：**

![image-20240530212638977](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240530212638977.png)



### 3.9 消息订阅与发布

**//知道这个就好，我们一般都还是更加推荐使用全局事件总线 进行 组件间的通信**



#### ① 下载 pubsub.js

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

<font color='red'>**/其实$nextTick()也是一个钩子函数**</font>

```
主要作用：是将$nextTick()中的回调函数延迟在下一次dom更新数据后调用
		由于Vue是在整个代码执行完之后才去更新DOM , 它能保证你操作的 DOM 是最新的，避免因数据更新未及时反映到 DOM 		导致的错误。
常用场景：包括更新后操作 DOM、触发动画、依赖 DOM 渲染结果的操作等。
```



```
<script setup>
import { ref, nextTick } from 'vue';

const message = ref('Hello World');
const box = ref(null);

const updateMessage = async () => {
  message.value = 'Hello Vue 3';

  await nextTick(); // 等待 DOM 更新完成
  console.log(box.value.textContent); // 确保获取到更新后的 DOM 内容
};
</script>
```

### 3.11 插槽

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













## 4.配置代理

- 前端解决方案：配置vue.config.js        【此外也可以使用Nginx,或者去让后端配置CorsConfig】

  - 原理：当你在vue项目中需要请求后端服务器，可以直接将url中写vue项目运行的url，而非直接写服务器的url

  - 比如vue项目是http://localhost:9090, 服务器是http://localhost:10001,并且配置了api 【如下代码所示】
    当我们需要websocket连接时，可以这样写 const websocket = new WebSocket('ws://localhost:9090/api/服务器ws具体名称')
    服务器的跨域设置比如ws的 .setAllowedOriginPatterns("http://localhost:9090");

  - ```
    const { defineConfig } = require("@vue/cli-service");
    module.exports = defineConfig({
      //关闭严格模式
      lintOnSave: false,
      transpileDependencies: true,
      //配置devServer
      devServer: {
        open: true,
        host: "localhost",
        port: 9090, 
        https: false,
        proxy: {
          // 配置跨域
          "/api": {
            target: "http://localhost:10001",    //这里不需要写/api 因为已经在axios配置了baseURL
            ws: true,    //允许代理websocked相关的请求
            changeOrigin: true,  
            pathRewrite: {
              "^/api": "",
            },
          },
        },
      },
    });
    ```

    









## 5.Vue-router



### 5.1 SPA

- 单页Web应用,single page web application,SPA
- 整个用只有一个页面
- 点击页面的导航栏链接，不会刷新页面，只会做页面的局部更新
- 数据需要通过ajax请求获取



**路由：在前端就是一个键值对，key是路径，value是组件**





### 5.2 路由的基本使用



#### ① 下载路由		

```
npm i vue-router
```



#### ② 注册路由

**<font color='red'>注意这里注册的路由实际就是第三步配置的路由，但是路径可以省略，因为"./router"，JavaScript 模块解析器会自动查找文件夹会默认去一个这里寻找router/index.js</font>**

main.js中，

```
//引入路由器
//这里使用'./router' 是因为JavaScript 模块解析器会自动查找文件夹会自动寻找 router/index.js文件，比较方便，有点类似
   SpringBoot的约定大于配置的  感觉了
import router from './router'


const app = createApp(App)
//使用路由
app.use(router)
app.mount()

```







#### ③ 配置路由

在src下面生成一个目录router/index.js,内容如下：

```js
// history模式
import {
    createRouter,
    createWebHashHistory,
} from 'vue-router'

const Home = () => import '../pages/Home.vue'
const About= () => import'../pages/About.vue'

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







```
docker run -p 3306:3306 --name mysql \
-v /usr/local/docker/mysql/conf:/etc/mysql \
-v /usr/local/docker/mysql/logs:/var/log/mysql \
-v /usr/local/docker/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=123456 \
-d mysql:8.0
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

​	

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



## 6.封装axios



- 1、npm i axios -save

- 2.配置axios,   个人习惯在  utils/httpRequest.js 里面配置

  - ```
    import axios from "axios";
    
    const AxiosService = axios.create({
      baseURL: "/api",
      timeout: 10 * 1000, //请求超时时间
      headers: { "Content-Type": "application/json;charset=UTF-8" },
    });
    
    // 请求拦截器
    AxiosService.interceptors.request.use(
      (config) => {
        //根据你的后端业务来写,如果权限验证，token
        return config;
      },
      (err) => {
        //若出现错误，则直接报错
        Promise.reject(err);
      }
    );
    
    // 响应拦截器
    AxiosService.interceptors.response.use(
      (res) => {
        // 这里用于处理返回的结果，比如如果是返回401无权限，可能会是跳回到登录页的操作，结合自己的业务逻辑写
        // 一定结合自己的后端的返回代码进行操作
        // res通常包含后端返回的主要数据。如果你只关心后端返回的数据而不需要访问响应的其他元信息（如状态码、响应头等），那么返回 res.data 会使代码更加简洁。
        return res;
      },
      (err) => {
        // 会将错误传递到调用该请求的代码中，便于后续处理错误。
        return Promise.reject(err);
      }
    );
    
    export default AxiosService;
    
    ```

- 3.封装post get方法   utils/httpRequest.js

  - ```
    import AxiosService from "./http";
    
    const httpRequest = {
      //封装 GET 请求
      get(url, params = {}) {
        //确保每次请求 URL 都是独一无二的，避免因缓存导致的问题
        params._t = Date.now();
        //这里的 { params } 会被 Axios 自动识别添加到请求 URL 上
        return AxiosService.get(url, { params })
          .then((response) => response)
          .catch((error) => {
            console.error("GET 请求失败:", error);
            throw error; //抛出错误，拱调用者处理
          });
      },
      //封装 POST 请求
      //POST请求需要在 body里面放入数据
      post(url, data = {}) {
        //不需要时间戳
        return AxiosService.post(url, data)
          .then((response) => response)
          .catch((error) => {
            console.log("POST请求失败:", error);
            throw error;
          });
      },
    };
    
    export default httpRequest;
    ```

- 4.封装apis/userApis.js

  - **下面两种方式都可以**

  - ```
    import httpRequest from "@/utils/httRequest.js";
    
    const userApi = {
      test(url) {
        // 返回 Promise，调用时可以链式处理响应
        return httpRequest
          .get(url)
          .then((response) => {
            console.log("服务器响应:", response);
            return response; // 返回响应给调用方
          })
          .catch((error) => {
            console.error("请求失败:", error);
            throw error; // 抛出错误供调用方处理
          });
      },
    };
    
    export default userApi;
    ```

  - ```
    import httpRequest from "@/utils/httRequest.js";
    
      function test(url) {
        // 返回 Promise，调用时可以链式处理响应
        return httpRequest
          .get(url)
          .then((response) => {
            console.log("服务器响应:", response);
            return response; // 返回响应给调用方
          })
          .catch((error) => {
            console.error("请求失败:", error);
            throw error; // 抛出错误供调用方处理
          });
      }
    ```

    







# 三、Vue3



## 1 区别



### ① app挂载引入createApp工厂函数

![image-20240514133106804](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514133106804.png)





### ② 静态加载与懒加载

- 静态加载
  - Vue2我们普遍使用静态加载      比如： import Index from 'xxx/index.vue'
  - 也叫同步导入   ，模块会在应用启动时被**立即加载**
  - 适应于小项目
  - 可能会影响首屏加载速度



- 懒加载

  - Vue3我们会经常使用懒加载const Index  = () => import('xxx/index.vue')

  - 只有被使用时才会被加载，减少成本

  - 适应于大项目,但是建议你这样写！





### ③ hook



















## 2 常用API



### 1.拉开序幕的setup

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





### 2.响应式数据



#### ①.ref函数

<font color='red'>**都能定义，但因为底层会直接调用reactive,凡是ref定义的对象类型，需要不停地.value太麻烦，所以ref还是只定义基本数据类型比较好**</font>



- Vue2中的响应式数据

  - ```
    在Vue2中，{data(){return {x:y}}},我们通过底层的数据代理和数据劫持就已经是响应式的数据了，但是Vue3里面我们需要通过ref/reactive主动声明响应式
    ```

    



- ref()返回的是什么
  - ![image-20241012124422019](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241012124422019.png)









#### ②.reactive函数

**<font color='red'>专门定义   对象类型</font>**



- reactive返回的是什么?
  - 返回的是 Proxy对象,   只要看见Proxy代理的xxx对象，那他就是响应式对象！
    ![image-20241012125208798](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241012125208798.png)



- reactive的一个坑 **<font color='red'>reactive会重新分配对象！！！！！</font>**

  - 虽然reactive不需要.value，但是如果你需要将整个数据修改，而非单一属性修改，比如
    const car = reactive({name:'奥拓',price:100}),如果服务器返回一个价格200的宝马,你要怎么修改？

    ```
    //方法一，直接修改
    	结果无效，因为此处的car再也不是响应式对象了，而变成了普普通通的对象了
    function changeCar(){
    	car = {name:'宝马',price:200} //直接变成了普普通通的对象了
    }
    
    //方法二,reactive套娃
    	也不行，因为reactive会重新分配对象，这样此时的car和模版里面的car就不是同一个对象了，修改自然就失败了
    function changeCar(){
    	car = reactive({name:'宝马',price:200}) //
    }
    //方法三, Object.assign(a,b,c)  
    	该方法会将 b c的属性都给 a 
    function changeCar(){
    	Object.assgin(car,{name:'宝马',price:200})   // Object.assgin是浅拷贝
    }
    ```


#### ③ 区别



- 原理不同
  - ref本质还是vue2那一套，你看RefImp里面还有_value这些老东西
  - reactive本质是Proxy代理





#### ④.toRef, toRefs

- 作用:
  - **用来复制reactive中的属性，然后转为ref对象，既保留了响应式，又保留了引用。也就是你从 `reactive` 复制过来的属性进行修改后，除了视图会更新，原有 `ractive` 里面对应的值也会跟着更新 ! ! ! ! ! !**   
  - <font color="red">**toRef和toRefs都是浅拷贝！！！！！**</font>
  - <font color="red">**专门搭配解构赋值很方便！！**</font>



- 例子

  - ```
    const x = toRef(person,'name')
    console.log(x.value)
    
    let {name,age} = toRefs(person)
    console.log(name.value,age.value)
    ```

    



### 4.计算属性

**//将Vue3中计算属性直接变成了一个方法，不过一般都是使用简写形式**

![image-20240514162132335](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514162132335.png)





### 5.watch监视



- Vue3中 watch只能监视四种数据
  - ref,reactive定义的数据
  - 函数返回的一个值(getter函数)
  - 一个包含上述内容的数组

- 具体使用

  - ```
    watch(sum,(newValue,oldValue) => { console.log('我变化了！')})
    ```

- 深度监视

  - **根本原因就是因为如果是ref定义的对象，watch监视的是对象的地址值**

  - reactive定义的对象**<font color='red'>默认开启深度监视</font>**>

  - ref 定义的对象<font color='red'>**需要手动开启深度监视**</font>

  - ```
    watch(person,回调函数)    只有person地址变了才能监视到，单纯的改变person.name是无效的
    
    watch(person,回调函数,{depp:true})  //无论是地址还是属性只要变了就能监视到
    ```

- 关于newValue 与 oldValue的一个细节
  - 如果监视一个对象，假如那个对象的地址变了，也就意味着newValue就指向了新数据，oldValue就指向了之前的旧数据
  - 如果监视一个对象，假如那个对象只是修改了属性，地址没有变化，newValue和oldValue都指向同一块地址，实际上
    这种情况下，newValue和oldValue就是同一个对象

- 五种情况

  - 监视ref定义的对象，需要手动开启深度监视

  - 监视reactive定义的对象，默认已经开启深度监视

  - 监视响应式对象的某一个基础属性，但是属性不在监视范围内，需要通过箭头函数return自身让其变成getter函数

    - ```
      watch(()=>{return person.name},回调函数)  //完整写法
      watch(()=>person.name ,回调函数)   //箭头函数的省略return的写法  
      ```

  - 监视响应式对象的某一个响应式属性

    - ```
      //person.car也是一个响应式对象
      
      //1.只能监视car的某一个属性的改变(即使加上深度监视也无效)
      watch(person.car,回调函数)
      //2.只能监视car的地址
      watch(()=>person.car,回调函数)
      //3.最佳实践,这样属性的变化,地址的变化都可以监视
      watch(()=>person.car,回调函数,{depp:true})
      ```

  - 监视多个数据，即监视数组

    - ```
      watch([()=>persom.name,()=>person.car],回调函数)
      此时的newValue和oldValue就和数组里的结构对应
      ```

      









### 6.生命周期

**![image-20240514180003987](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514180003987.png)**



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

















### 7.动画API







### 8. 组件通信

- defineProps

- defineEmits

  - ```
    父组件:   <Login @changeShow='changeShow'></Login>
    子组件:   const emit = defineEmits(['changeShow'])
    		 const changeShow = (num) => {emit.changeShow(number)}
    ```

- ref 与 defineExpose

  - ```
    父组件: const child = ref()
    	   child.xxxx()
    子组件: defineExpose({xxxx})   //需要把要给父组件的属性/方法暴露出去！
    ```

    
























## 3 其他API



### 1.响应式数据的判断

![image-20240514221553053](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240514221553053.png)







## 4.pinia

- **<font color='red'>vue2 经常使用的是 vueX ; vue3 经常使用的是  pinia</font>**
- **<font color='red'>下面只是搭建环境，具体API自己查文档</font>**

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
//第三步: 安装Pinia
app.use(pinia)
app.mount('#app')
```

```
//1.在src目录下创建 store/index.js
```







## 5.组件库



### 5.1ElementUI-Plus

#### ①::v-deep

其实很简单，用搜索为例子，我当初很想知道如何取消input的蓝色外边框，无非就是outline或者box-shadow作怪，但是我却无论如何都操作不了 这个搜索框，查了半天我终于明白 **如果要操作elmentui组件，需要 ::v-deep 深入**



```
//这是直接修改属性
::v-deep .el-dialog {
  background-color: red;
  border-radius: 12px;
}
```

![image-20241016222015118](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241016222015118.png)

```
//这是修改聊天框里面的.el-input_wrapper颜色的一个案例   
.nav-search-input ::v-deep .el-input__wrapper {
  .el-input ::v-deep .el-input__wrapper{
  box-shadow: none;
  border: 1px solid #e4e8e8;
}
}
```



#### ②done()

//一个坑







# 三.思路





## 1.动画入门



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

  























