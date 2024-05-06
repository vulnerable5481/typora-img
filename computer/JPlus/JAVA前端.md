# 一.前端三板斧



## 1.HTML

​	



### 1.1字体,img

![image-20240314160542448](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314160542448.png)

### 1.2 table 

![image-20240314164001972](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314164001972.png)



### 1.3 有序无序 自定义列表

![image-20240314165105980](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314165105980.png)



⭐⭐⭐⭐⭐⭐

![image-20240314165501331](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314165501331.png)





### 1.4 input输入表单元素

![image-20240314170822396](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314170822396.png)

![image-20240314170836049](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314170836049.png)



### 1.5 lable标签

**//比如lable标签可以使鼠标点击用户名三个字就触发输入框，输入信息，就是将鼠标点击范围从单一的框变为框加文字的所在的盒子**

![image-20240314171626257](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314171626257.png)





### 1.6 select下拉表单



![image-20240314172009678](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314172009678.png)



### 1.7文本域

![image-20240314172304685](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314172304685.png)





### 1.8Element语法



![image-20240315122337048](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240315122337048.png)



![image-20240315122621491](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240315122621491.png)





## 2.CSS



### 2.0 CSS熟悉书写顺序



![image-20240326145754863](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326145754863.png)







### 2.1四种基础选择器与复合选择器与伪类选择器



![image-20240314205404290](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240314205404290.png)



**复合选择器**

![image-20240318173738463](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240318173738463.png)

![image-20240318174323877](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240318174323877.png)

![image-20240318174919766](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240318174919766.png)

![image-20240318175411067](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240318175411067.png)

![image-20240325130848922](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325130848922.png)



























### 2.2 各种属性



#### 2.2.1字体属性

![image-20240319183954518](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240319183954518.png)

**//font-size 尽可能不使用默认大小，最好自己去指定大小**

**//font-family  一般不建议修改**

**//font-weight 看上面**

**//font-style italic是斜体，normal是不斜体**

​	





#### 2.2.2   文本属性



![image-20240319184324372](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240319184324372.png)

**//text-align center left/right center 三种对齐方法**

**//text-indent 可以缩进  px 也可以 em,em就是 单位字体距离**

**//text-decoration 知道underline 添加下划线 和 none 取消下划线   就ok**

**//line-height 控制行高,常用于垂直居中显示，line-height = height的高度 **    











#### 2.2.3 背景属性

![image-20240319184729040](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240319184729040.png)

 









### 2.3 CSS的元素显示模式



-  块元素:div
- 行内元素
- 行内块元素

**行内元素转换为块元素(常用！)	:**

**display:block变为块元素**   display:inline 变为行内元素 **display:inline-block 变为行内块元素**



![image-20240325141824675](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325141824675.png)

![image-20240325141840598](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325141840598.png)















### 2.4 CSS三大特性与盒子模型



- 层叠性
- 继承性
  - 子元素可以继承父元素一些样式，但是只能继承文字相关样式，但是不会继承浮动啊边框等其他元素

- 优先级
  - 权重：![image-20240327173935459](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240327173935459.png)










#### 2.5.1网页布局的本质



![image-20240325131138597](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325131138597.png)



#### 2.5.2盒子组成

![image-20240325132217249](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325132217249.png)

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

![image-20240325134952622](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325134952622.png)

```
 padding: 5px   意思是上下左右都是5px
 padding: 5Px 10px 上下为5 左右是10px
 padding: 5px 10px 20px: 上是5 左右是10 下是20
 padding: 5px 10px 20px 30px  略
```

**padding也会影响盒子大小**

![image-20240325135714210](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325135714210.png)







##### 3.margin外边距



![image-20240325142237958](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325142237958.png)

![image-20240325144600848](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325144600848.png)

![image-20240325143809887](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325143809887.png)





![image-20240325144420339](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325144420339.png)



**外边距合并现象**

![image-20240325144959114](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325144959114.png)



![image-20240325145524886](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325145524886.png)

![image-20240325145822464](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325145822464.png)





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



![image-20240325184453503](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325184453503.png)



例子：   一般影子颜色推荐:   rgba(0,0,0,.3)  

![image-20240325184419127](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325184419127.png)





##### 6.文字阴影



![image-20240325184520481](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325184520481.png)





### 2.5浮动

**三种网页布局 ： 标准流，浮动，定位，开发一个页面往往三者都需要使用**



![image-20240325185923009](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325185923009.png)





![image-20240325190039125](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325190039125.png)

#### 2.6.1 浮动三特性

![image-20240326121836258](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326121836258.png)



![image-20240326121940735](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326121940735.png)





![image-20240326122357841](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326122357841.png)



![image-20240326122927859](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326122927859.png)

#### 2.6.2浮动元素与标准元素搭配使用







![image-20240326124519492](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326124519492.png)





#### 2.6.3清除浮动

![image-20240326141835582](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326141835582.png)

![image-20240326143455710](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326143455710.png)

![image-20240326142807691](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240326142807691.png) 

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

![image-20240330161923651](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240330161923651.png)

#### 2.8.2定位组成及语法

![image-20240330162224441](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240330162224441.png)



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

![image-20240330171833737](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240330171833737.png)







#### 2.8.4 定位叠放次序

![image-20240330183200722](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240330183200722.png)



#### 2.8.5定位的一些特性⭐

**//目前已知可以给行内元素设置宽度高度的方法:**

- display: block/inline-block  
- float:left;
- position: absolute / fixed

![image-20240330184511724](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240330184511724.png)



浮动只会对之前的元素有影响，而且浮动只会压住下面的标准流盒子，不会压住下面标准流盒子中的文本/图片，标准流盒子中的文字/图片会被挤到一边

但是绝对定位/固定定位 会完完全全地压住盒子和盒子中所有的内容









### 2.7显示隐藏元素





![image-20240331150414524](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331150414524.png)

![image-20240331150517629](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331150517629.png)

![image-20240331150946186](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331150946186.png)





















































































## 3.JavaScript



































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

![image-20240330133912312](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240330133912312.png)

















#### 3.盒子宽度警告



除了盒子，不要随意指定盒子内部元素的宽度,高度也有时候不需要设置







#### 4.margin:0 auto的失效

如果是块级元素/行内块级元素，使用margin: 0 auto;都会使其居中，但是如果是浮动的,float:left就会导致margin:0 auto;失效，指明margin: 10px还是可以使用，这是为什么呢？？

//解答：因为margin: 0 auto 是根据文档位置计算的，浮动使其脱离文档，导致计算公式无法计算，但是指明margin依然可以正常使用！



使用position: absolute 绝对定位也会使margin: 0 auto 失效



**//有一个小技巧解决这种绝对定位引起的失效问题:可以先走到中间(top:50%),然后往回走自身宽度的一半即可()**

**//垂直居中也是一个道理**



#### 5.固定在版心右侧位置	



![image-20240330174603275](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240330174603275.png)

























# 二.Vue



## 1.Vue核心



### 一些知识点	



#### 1.知识点

```
1.el的两种写法
el:'#app'  ;  const app =  new Vue({xxx})  app.$mout(app);挂载

2.data必须使用函数式
data:function(){        可简化成 data(){  }
	return {
		name: 'zlc'
	}
}
```

#### 2.MVVM模型

![image-20240504193007719](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240504193007719.png)

#### 3.vue的数据代理

**//理解了这个方法的过程，将非常有助于理解vue的数据代理，进而理解MVVM模型**

![image-20240504194350060](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240504194350060.png)

**//你写在data里面的数据，vue会将其加工(生成get,set)到vue._data里面，然后vue实例根据vue._date生成数据名，然后只要调用set就将变化更新到视图上**

**所谓的数据代理，就是vue实例中的data的数据是通过_data的get获取值，通过__data的set来修改值**

**//数据代理的好处就是方便我们的编码**

**(<font color="green">既然已经vue实例_date已经有了真实数据，为什么还要在vue实例再创建数据呢？因为你每次都要__data.xxx获取属性不麻烦吗，直接 使用 xx多方便，所以vue实例中的_data的数据是通过___data的get获取值，通过__data的set来修改值，这样就可以直接使用属性名，而不用加-data.xxx</font> ）**

![image-20240504201600879](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240504201600879.png)







#### 4.vue视图更新

- **问题引出：第二种方式修改数据，虽然内存上确实修改成功，但是vue没有监视到这种更新，视图不会变。**

![image-20240506132222822](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506132222822.png)

- **vue如何检测对象更新？**

所有对象的数据全部都是由set和get方法构成，只要修改数据就必须使用set方法，一旦使用set方法，vue就会更新视图
**也就说，set方法与视图的更新密切相关！！！一旦视图不更新就要思考是不是和该数据的set有关！**

比如，像这种，直接写了一个属性sex ,然后给予一个值 '男'，这个属性压根没有get set方法怎么可能会在视图上显示出来！

![image-20240506134152240](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506134152240.png)



- **vue如何检测数组更新**

数组里的属性没有set,get，数组里的对象肯定可以有，vue如何检测数组更新？

![image-20240506140647104](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506140647104.png)



![image-20240506141316420](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506141316420.png)





- **问题的解决**

**可以调用数组里的那七个api，也可以使用Vue.set(target,key,value)**

addSex(){

​		Vue.set(this.student,'sex','男')

}



**//总结**

![image-20240506142422659](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506142422659.png)























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



前面我们学习了如何插入内容，但实际开发中很多属性是动态的，比如轮换图,超链接，这就需要我们给这些属性动态绑定

**//v-bind 一般都是标签内部的东西**

**//语法糖写法   :src="imgUrl"**,只需要写一个:即可,v-bind可以省略

 

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
method:{
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

.trim
如果要自动过滤用户输入的首尾空白字符，可以给 v-model 添加 trim 修饰符：

**//总结**

![image-20240506144631933](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506144631933.png)









### 1.3 v-for



- 当我们有一组数据需要进行渲染时，我们就可以使用v-for来完成。
  - v-for的语法类似于JavaScript中的for循环。
  - 格式如下：v-for=" item in items  :key = "xxx" ",这里的key作为唯一标识，必须得写！！！
  - 格式还可以另一种写法v-for=" (item,index) in items  :key = "index" ",利用数组index角标作为唯一标识



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

![image-20240506122313905](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506122313905.png)



















### 1.4计算属性与监视



///计算属性的set,get方法知道有这个东西就Ok，一般是不会使用的

**//为什么推荐使用计算属性，而不是写一个函数来获取属性？**因为你写成函数那么用几次该属性就需要调用几次该函数，没有缓存，效率低。**但是你使用计算属性，只会调用一次就会一直获取到该属性，后续再使用该属性可以直接使用**.

<font color="red">**创建时间**</font>：**刚开始就自动生成一次**

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





**监视属性**

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

![image-20240504214603128](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240504214603128.png)













### 1.5事件监听v-on

**v-on:xxxx ,  @xxx   xxx为绑定的一个事件** 

**//语法糖：缩写为@**

​	

当通过methods中定义方法，以供@click调用时，需要注意参数问题：

情况一：如果该方法不需要额外参数，那么方法后的()可以不添加。

但是注意：如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去，**可以在参数列表写一个名字获取event**

情况二：如果需要同时传入某个参数，同时需要event时，可以通过$event传入事件,否则传入的参数会顶替掉even。



**//v-on修饰符, 可以代替以往写js代码的形式**

```
methods:{
	showInfo(e){
		e.preventDefault()   //js
		alter('你好!')
	}
}
//1.阻止默认行为     //比如一个超链接，点击就跳转，阻止默认行为就不跳转
//2.事件冒泡        //比如父标签有一个@click子标签也有一个一摸一样的@click，这时点击子标签就会触发两次，这就是典型的事件冒泡
```

![img](https://img-blog.csdnimg.cn/20210712190852410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDczODEx,size_16,color_FFFFFF,t_70)





### 1.6 键盘监听



**//比如@keyup: 按下某个键松开后才触发，@keydown：按下就触发**

```
name:<input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo">
            methods:{   
                showInfo(){
                    alert('请输入名字')
                }
            }
            
```

![image-20240504204050490](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240504204050490.png)

![image-20240504204448563](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240504204448563.png)







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

**//此处的test也可以称之为组件实例对象(vc)**

```
const test = Vue.extend({
	template:``,   //写html
	data(){        //必须使用函数式，因为函数式每次都return一个新对象，保证数据是全新的
		return {
			xxx
		}
	}
})
```

![image-20240506181743102](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506181743102.png)

**//一个重要的内置对象VueComponent.prototype._proto__ == Vue.prototype**

**//为什么要有这个关系？让组件实例对象(vc)也可以访问到Vue原型上的属性和方法**

![image-20240506184259276](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506184259276.png)





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







### 2.7 render渲染

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



![image-20240506211230109](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506211230109.png)









### 2.8 获取dom元素

**//某些特殊场景我们确实需要获取dom元素，不建议使用js获取，可以使用vue提供的ref**

**//如果只是单纯地获取html标签，那传统的js代码和vue提高的ref确实没区别，但要是针对组件区别就大了！！！**

**//document.getElementById('xx')只会获取组件html结构**

**//vue的ref可以获取组件实例对象,即可以获取vc**

![image-20240506212859551](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240506212859551.png)











