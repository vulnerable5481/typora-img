

## 一,计算机网络概述



### 1.1 三种交换方式



#### (1) 分组交换⭐

​	![image-20240228103558021](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228103558021.png)





#### (2)电路交换

简单来说，就是用电路直接去连接x台设备

#### (3)报文交换

了解一下即可





### 1.2计算机网络的定义和分类



计算机网络的定义比较复杂，简单来说就是 一些互相连接的，自治的计算机集合   (此处的计算机也包括智能手机之类)



分类：![image-20240228103855408](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228103855408.png)







### 1.3计算机网络的性能指标



- 速率
  ![image-20240228104138303](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228104138303.png)
- 带宽：最大速率
- 吞吐量 :  单位时间总传输的数据量
- 时延 : 通常包括  发送时延，传输时延 ，接收时延，排队时延(可能没有可能有)
- 时延带宽积
- 往返时间
- 利用率
- 丢包率



### 1.4计算机网络体系结构⭐



#### (1)常见的计算机网络体系结构

![image-20240228104408856](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228104408856.png)

**TCP/IP协议的展开**



![image-20240228113407353](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228113407353.png)

#### (2)计算机网络分层的必要性

![image-20240228105019240](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228105019240.png)







#### (3)分层的例子一http请求与响应

//注意：此处假设N1，N2是以太网

**//注意：这些各种层只是我们为了理解和应用而进行的分层，实际上其实是一个整体过程，只是我们分层剖析**



**主机H1中的浏览器发出一个Http请求到路由器的过程**

1.第一步：在应用层  (具体就是在谷歌浏览器)  根据http协议创建一个http报文

![image-20240228105757745](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228105757745.png)

2.第二步：在运输层  添加一个TCP首段 使之成为 TCP报文段（该首部的作用主要是为了区分应用进程，以及实现可靠传输）



![image-20240228105925915](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228105925915.png)



3.第三步，在网络层  添加一个IP首部 ，使之成为 IP数据报(该首部含有目的地址，其主要作用是可以被路由器转发(因为在这里可以得到目的地址))

![image-20240228110040252](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228110040252.png)



4.第四步，在数据链路层 添加一个首部和一个尾部，使之成为一个帧 (首部作用是为了让帧能在一段链路上或一个网络上传输，被相应的目的主机接收； 尾部作用是为了让目的主机检查所接收到的帧是否有误码)



​	![image-20240228110949276](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228110949276.png)





5.第五步，在物理层，将帧看作比特流，由于网络N1是以太网，还会加入前导码(其作用是让目的主机做好接收帧的准备，比如使接收方的时钟同步)

物理层将添加有前导码的比特流转换为响应的信号发送到传输媒体，信号通过传输媒体到达路由器。



![image-20240228111441553](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240228111441553.png)

















## 二.物理层

**//物理层的主要任务就是解决比特0和1在线路上传输的问题**





### 2.1 物理层的基本概念



#### ①四个特性

![image-20240305123648466](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240305123648466.png)

#### ②传输方式



- **串行传输与并行传输**
  - 串行传输就是一个字节一个字节传输
  - 并行传输就是N条线，N个字节N个字节传输
- **同步传输与异步传输**
  - ![image-20240528160355343](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528160355343.png)



















### 2.2 物理层之下的传输媒体

**//大致分为导引型传输媒体 和 非导引型传输媒体**

![image-20240305123811825](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240305123811825.png)

- **导引型传输媒体**
  - **同轴电缆**
    - ![image-20240528153818209](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528153818209.png)
  - **双绞线**
    - ![image-20240528153944979](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528153944979.png)
  - **光纤**
    - ![image-20240528154120469](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528154120469.png)
    - <font color=red>**光在光纤的传播原理**</font>
      ![image-20240528154329948](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528154329948.png)



- **非引导型传输媒体**
  - 无线电波
    - ![image-20240528154836309](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528154836309.png)
  - 微波
    - 由于微波只能直线传播且会穿透电离层，故其地面波传播距离一般在五十公里内，为扩大距离常常使用中继站将收到的微波扩大在发送给下一站。一般微波通信分为两种地面微波接力通信(天线塔作为中继站)，另一种是卫星通信(利用人造地球同步卫星作为中继站，除此之外低轨道卫星通信系统也开始在空间部署并构成了空间高速链路,马斯克的星链是这种吗？)。
    - ![image-20240528155030944](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528155030944.png)
  - 红外线
    - 这个很熟悉，电视遥控器，空调遥控器你懂吧
      ![image-20240528155808843](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528155808843.png)











### 2.3 传输方式



![image-20240305124256236](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240305124256236.png)





### 2.4编码与调制

![image-20240528162120298](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528162120298.png)

![image-20240528163020991](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528163020991.png)

![image-20240528163042354](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528163042354.png)







![image-20240528163432895](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528163432895.png)





![image-20240528163617990](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528163617990.png)





![image-20240528163608462](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528163608462.png)















### 2.5 信道的极限容量

#### ① 码间串扰

![image-20240528164010420](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528164010420.png)

#### ② 奈氏准则

![image-20240528165353179](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528165353179.png)



#### ③ 香农公式

**信息传输速率 = 波特率(码元传输速率) * 每个码元携带信息量**

![image-20240528165848220](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528165848220.png)





#### ④ 真题



![image-20240528170337602](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528170337602.png)

![image-20240528171916622](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528171916622.png)

![image-20240528173526490](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528173526490.png)



![image-20240528174136688](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528174136688.png)















## 三.数据链路层

### 3.0 区分

<font color='orange'>**对于以太网帧格式，有两种常见的格式：IEEE802.3帧和以太网II帧**</font>



- **IEEE 802.3帧的别称是以太网帧**（Ethernet Frame）。这是因为IEEE 802.3标准规定了以太网的帧结构和传输方式，因此在讨论网络数据传输时，IEEE 802.3帧通常直接称为以太网帧。IEEE 802.3最初使用长度字段（Length）来指示数据部分的长度，但后续版本也引入了类型字段。**IEEE 802.3帧，又包括802.3 MAC帧和802.3 SNAP帧**
- **以太网V2（Ethernet Version 2）即以太网II帧，用于区分vlan也被称为未标记帧**，以太网V2使用类型字段（Type）来指明数据部分所使用的协议。
- **802.1Q帧，用于区分vlan也被称为标记帧/vlan帧,**相对于以太网II帧添加了Vlan标签(包含TPID,PRI,CFI,VID)，用于支持VLAN

​	<font color='pink'>**这三种帧格式都是在局域网中广泛使用的封装方法，各自有其特定的应用场景和兼容性要求。Ethernet II帧由于其简单和有效性，已经成为当前以太网的主流帧格式。而IEEE 802.1Q帧则被广泛用于需要支持VLAN的网络环境中。**</font>









### 3.1封装成帧

**<font color='orange'>详细拆解一下封装成帧</font>**

```
举例
 【7B    1B 前导码部分】【以太网II头部包括6B的目的MAC，6B的源MAC，2B的类型/长度；一般作为帧首】
【前同步码 帧开始定界符】【EthernetII头部】【DATA】【FCS】
               【数据就是上层交付的协议】         【FCS是帧检验序列，4B，一般作为帧尾】                           
```



- 含义：数据链路层将上层交付的协议数据单元添加帧头和帧尾，使之成为帧
  - 帧头和帧尾中包含重要的控制信息
  - 帧头帧尾的作用之一就是帧定界

​					**//PPP帧：**

![image-20240312120412227](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312120412227.png)



**//以太网V2的MAC帧**

![image-20240312120457875](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312120457875.png)

//其中前导码 前七个字节为前同步码，作用是使接收方的时钟同步；后面一个字节是帧开始定界符，表明紧跟着的就是MAC帧



//另外，以太网的MAC帧不需要帧结束定界符，因为有帧间间隔

![image-20240312120747027](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312120747027.png)





- **透明传输**
  - 含义：将数据链路层对上层交付的传输数据没有任何限制，就好像数据链路层不存在一样
  - 提问：若在数据中恰好含有 和帧开始结束定界符一样 的字节 该怎么办？
    - ![image-20240312121505883](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312121505883.png)

​		



### 3.2 差错检测



- **奇偶检测（漏洞多，一般不会采用该方法）**

![image-20240312121626716](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312121626716.png)





- **循环冗余检验CRC(Cyclic Redundancy Check)**

![image-20240312124952968](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312124952968.png)

![image-20240312125012554](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312125012554.png)

![image-20240312125056495](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312125056495.png)



![image-20240312125111487](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312125111487.png)

### 3.3可靠传输

#### 3.3.1  一些基本概念

![image-20240312125358854](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312125358854.png)



![image-20240312125407375](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312125407375.png)



#### 3.3.2  停止-等待协议SW(stop-and-Wait)



![image-20240312125956484](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312125956484.png)



#### 3.3.3 回退N帧协议GBN

![image-20240312130048735](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312130048735.png)



![image-20240312130212292](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312130212292.png)

  



#### 3.3.4 选择重传协议SR



总体流程也是滑动窗口那样，只不过接收窗口的接收数量不再是1。

![image-20240312131438514](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312131438514.png)



![image-20240312131503952](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312131503952.png)





### 3.4 点对点协议PPP

**//特点：PPP报文没有序号，不需要ACK确认，只对检验码出错的数据进行丢弃。**





#### 3.4.1 帧格式

![image-20240312132511372](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312132511372.png)



#### 3.4.2 透明传输

![image-20240312132734084](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312132734084.png)



![image-20240312132952660](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312132952660.png)



![image-20240312133719483](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312133719483.png)







#### 3.4.3 差错检测

//采用前面学过的CRC 进行计算

![image-20240312133943995](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312133943995.png)



#### 3.4.4 工作状态



![image-20240312134425041](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240312134425041.png)







### 3.5 媒体接入控制



#### 3.5.1 媒体接入控制的基本概念



![image-20240313130000993](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313130000993.png)





#### 3.5.2 静态划分信道



- **频分复用FDM**

![image-20240313130124945](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313130124945.png)

- **时分复用TDM**

![image-20240313130219510](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313130219510.png)



- **波分复用WDM**

![image-20240313130159167](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313130159167.png)

- **⭐码分复用CDM**



![image-20240313130305618](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313130305618.png)



![image-20240313130335927](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313130335927.png)



![image-20240313130349151](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313130349151.png)



![image-20240313130410158](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313130410158.png)







#### 3.5.3	动态接入控制--随机接入---CSMD/CD协议



##### 1.**CSMA/CD协议--概念**

**//CSMA/CD协议适用于 有线网络，CSMA/CA协议适用于无线网络**

![image-20240313131246643](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313131246643.png)




##### 2.**CSMA/CD协议--碰撞检测的流程**

![image-20240313131452352](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313131452352.png)

##### 3.**CSMA/CD协议--争用期（碰撞窗口）**

![image-20240313132008824](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313132008824.png)

##### 4.**CSMA/CD协议--最小帧长和最大帧长**

最小帧长 = 争用期 * 数据传输速率

![image-20240313132610509](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313132610509.png)

![image-20240313133043076](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313133043076.png)



##### 5. **CSMA/CD协议--截断二进制指数退避算法**

![image-20240313133359241](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313133359241.png)



##### 6.**CSMA/CD协议--信道利用率**

S = T/T+t =  1/1+t/T 

![image-20240313133626688](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313133626688.png)

##### 7.**CSMA/CD协议--帧接收和发送流程**

​		![image-20240313133919741](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313133919741.png)



![image-20240313134154261](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313134154261.png)





##### 8.总结

**//CSMA/CD协议曾经用于各种总线结构以太网和双绞线以太网的早期版本中，现在的以太网基于减缓及和全双工连接，不会有碰撞，因此没必要使用CSMA/CD协议**

![image-20240313140346274](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313140346274.png)











#### 3.5.4	动态接入控制--随机接入---CSMA/CA协议

**//CSMD/CA协议  适用于  无线局域网**



##### 1.    CSMA 依然可用  , CD 不可用



![image-20240313174909038](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313174909038.png)

![image-20240313175011566](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313175011566.png)



##### 2.   注意:  802.11标准  使用了	SW

![image-20240313175256965](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313175256965.png)







##### 3.帧间间隔(IFS)   SIFS DIFS

![image-20240313175422690](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313175422690.png)



##### 4.退避算法

![image-20240313175643190](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313175643190.png)

![image-20240313175725469](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313175725469.png)





##### 5.具体工作流程	

![image-20240313175950154](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313175950154.png)





##### 6.信道预约



![image-20240313180031024](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313180031024.png)



​	![image-20240313180334354](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313180334354.png)



##### 7.虚拟载波监听 



![image-20240313180415857](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240313180415857.png)





### 3.5 MAC地址、IP地址、ARP协议







#### 3.5.1 MAC地址



- 总览

![image-20240318133316442](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318133316442.png)









- MAC地址的四种分类

**//全F  就是 广播地址**

![image-20240318132511261](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318132511261.png)



- 广播帧、单播帧、多播帧

**//广播帧   是目的地址为全F；  当其他主机接收到广播帧就会接收**

**//单播帧 就是地址匹配就接收，不匹配就丢弃,easy**

![image-20240318132814159](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318132814159.png)

**//多播帧**

![image-20240318133239410](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318133239410.png)







#### 3.5.2 IP地址







- 总览




![image-20240318134343003](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318134343003.png)





- 数据包转发过程中IP地址与MAC地址的变化情况	

**//哇哦，这样就无法直接定位发送信息的主机真实信息，更加安全！！！**

![image-20240318134040958](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318134040958.png)





#### 3.5.3 ARP协议

**//详细内容移步下面的网络协议分析**



### 3.6  交换机

#### ①工作流程

![image-20240607221321886](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240607221321886.png)

![image-20240607221341063](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240607221341063.png)



#### 与集线器的区别

**//区别就是，交换机能自己判断，集线器只是传播工具;交换机工作在数据链路层也包括部分物理层，集线器只包含物理层**

![image-20240318141542441](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318141542441.png)







### 3.8 以太网交换机的生成树协议STP（了解）





![image-20240318161832766](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318161832766.png)

- STP  
  - BID(桥ID)  由桥优先级 和 桥MAC 组成，缺省为32768
  - PID(端口ID) 由端口优先级 和 端口号 组成 ，缺省128
  - RB（根桥）确定依据：























### 3.9 虚拟网VLAN

#### ① vlan的作用

**//解决巨大广播域中广播风暴之类难以管理和维护的问题，用路由器来分割广播域，这一块块的小网络就是VLAN**

**<font color='orange'>作用就是分割广播域!!</font>**

**如下图：我们只想要通过广播通知财务部，该如何实现呢?**

![image-20240607223645147](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240607223645147.png)

#### ② 特点与解惑

<font color='orange'>**设备划分与物理位置无关**</font>

<font color='red'>**为什么不用路由器实现分割广播域? 答：路由器实现分割的费用比较贵，且有一些局限**</font>

#### ③ 虚拟局域网VLAN的实现机制



- IEEE 802.1Q帧

![image-20240318164412552](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240318164412552.png)



#### **④交换机的三大端口类型**

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609115433717.png)

- **<font color='orange'>Access端口类型 ：连接用户的端口为access端口</font>**

1. **定义**：Access端口用于连接终端设备，如计算机、打印机、服务器等。
2. **VLAN**：一个Access端口只能属于一个VLAN。它接收到的所有流量都被打上该VLAN的标签，并且发送出去的流量也是无标签的。
3. **使用场景**：常用于需要将单个VLAN流量发送到终端设备的场景。比如，办公室中的PC连接到交换机的Access端口。

- **<font color='orange'>trunk端口类型 : 交换机内部的端口为trunk端口</font>**

1. **定义**：Trunk端口用于连接交换机之间或交换机与路由器之间，以便多VLAN之间的通信。
2. **VLAN**：一个Trunk端口可以携带多个VLAN的流量。Trunk端口上的帧被打上VLAN标签，以便接收端知道该帧属于哪个VLAN。
3. **使用场景**：常用于需要在交换机之间传输多个VLAN流量的场景。比如，在大型网络中，主干链路（Trunk链路）通常用于连接核心交换机和接入交换机。

- <font color='orange'>**hybird端口类型**</font>
  不用了解
  
  混合端口











## 四.网络层





### 4.1网络层概述



![image-20240417122652968](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417122652968.png)

![image-20240417123009043](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417123009043.png)





### 4.2网络层提供的两种服务



![image-20240417123509727](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417123509727.png)



![image-20240417123521920](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417123521920.png)









### 4.3 IPv4地址

#### 1.初步了解ipv4

- IPv4地址的概念：就是给因特网提供上的每一个主机/路由器的每一个接口分配一个**在全世界范围内唯一的32比特的标识符**
- IP地址是谁分配的？：因特网名字和数字分配机构**ICANN**进行分配，我国可以向亚太网络信息中心APNIC申请IP地址，需要缴费，一般不接受个人申请，2011年，互联网号码分配管理局宣布，IPv4地址已经全部分配完毕！我国也在2014年后逐步停止向新用户分配ipv4地址，同时全面开展商用部署ipv6.



#### 2.ipv4地址概述



- 由于32比特的ipv4地址不方便阅读，记录等，因此ipv4地址采用**点分十进制表示方法**，便于用户使用
  - ![image-20240417124449251](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417124449251.png)

#### 3.ipv4地址经历的三种分配方式之分类地址

**技巧:**

**128（1-127）  64（128-191）32（192-223）



**<font color='orange'>224-239用于多播，240-247保留</font>**

![image-20240417125138865](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417125138865.png)


![image-20240417125759744](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417125759744.png)



![image-20240417130234084](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417130234084.png)



![image-20240417130708643](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417130708643.png)





![image-20240417131501645](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417131501645.png)

![image-20240417131858903](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417131858903.png)









#### 4.ipv4地址经历的三种分配方式之划分子网(子网掩码)



**引出子网掩码**

![image-20240417132147522](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417132147522.png)



**//子网掩码就是从主机号中借用几个比特作为子网号**

![image-20240417132403638](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417132403638.png)

**//划分案例**

![image-20240417132645730](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417132645730.png)

**//默认子网掩码**

![image-20240417134843766](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417134843766.png)





**//三道练习题**

![image-20240417133223148](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417133223148.png)

![image-20240417133407827](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417133407827.png)

![image-20240417134706356](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417134706356.png)



####  5.ipv4地址经历的三种分配方式之无分类编址



**//为什么使用无分类编址?**

![image-20240417140229106](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417140229106.png)

**//具体使用**

![image-20240417140217783](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417140217783.png)





**//路由器中如何构造路由表**



![image-20240417140112860](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417140112860.png)



**//习题**

![image-20240417140700591](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417140700591.png)





#### 6.网关

- 一般情况下网关都设置成254，因为255是广播，后面就没有了
- 软件网关：比如你使用的jwt











### 4.4ipv4地址的应用规划

#### 1.定长的子网掩码FLSM

![image-20240417191139698](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417191139698.png)







#### 2.边长的子网掩码VLSM

![image-20240417191724673](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417191724673.png)







### 4.5 IP数据报的发送和转发过程

**//主机A  ->  主机D**

**//网络地址 = 目的地址 ^ 子网掩码**

```
1.根据主机A与D的ip地址与A的子网掩码 得出A与D的网络地址，进行比较若相同则在同一网络可直接交付，若不在同一网络则间接交付

2.间接交付，为了使不同网络的主机进行通信，必须给主机指定一个路由器，该路由器负责帮忙转发，所指定的路由器也称为默认网关！对于本例我们可以将路由器R的接口0的ip地址作为默认网关。  

3.到达路由器，将IP数据报中目的地址^路由表中的地址掩码，若目的网络相同则根据表中信息转发
```

![image-20240418110745322](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418110745322.png)



**//主机A本网络的广播**



![image-20240418110722031](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418110722031.png)



**//练习题**

![image-20240418112617883](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418112617883.png)





### 4.6静态路由选择



就是人工配置



![image-20240418120231132](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418120231132.png)

### 4.6动态路由选择

#### 4.6.1路由选择协议概述

路由选择协议概述



![image-20240418120251919](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418120251919.png)





![image-20240418120441145](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418120441145.png)

 



![image-20240418120950149](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418120950149.png)











#### 4.6.2路由信息协议RIP

**//Router Information Protocol RIP**

**一些概念**

- 路由信息协议RIP是内部网关协议/内部路由协议IGP中最先得到广泛使用的协议之一
- RIP要求自治系统AS中每一个路由器都维护一个从它自己到AS内其他每一个网络的距离记录，这些距离称为，距离向量D-V
  - RIP使用跳数作为度量
  - 路由器到直连网络的距离为1
  - 路由器到非直连网络的距离为中间经过的路由器数量+1
  - 一条路径最多只能包含十五个路由器，当距离 == 16 意思是不可达，因此RIP只适用于小型互联网
  - ![image-20240418124658267](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418124658267.png)

- RIP 认为 好的路由是 距离短的路由
- 当到达同一目的网络有多条距离相等的路由时，可以进行等价负载均衡
- RIP 包含三个要点
  - 和谁交换信息       仅和自己相邻的路由交换信息
  - 交换什么信息      自己的路由表
  - 何时交换信息       周期性交换（例如每三十秒）

**基本工作过程**

![image-20240418124126922](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418124126922.png)



**更新规则**

**//到达目的网络，相同下一跳，如果是新消息则更新**

![image-20240418124144953](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418124144953.png)



**坏消息传得慢**



![image-20240418125852876](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418125852876.png)

![image-20240418125918708](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418125918708.png)











#### 4.6.3开放最短路径优先OSPF

**//Open Shortest Path First OSPF**

**一些概念**

- 开放最短路径优先OSPF是为了克服RIP的许多缺点在1989年开发出来的
  - “开放” 表明OSPF协议不是受某家公司控制，而是公开发表的
  - 最短路径优先，是指使用了迪结特斯拉发明的spf最短路径算法

- OSPF是基于**链路状态**的，而不是像RIP那样是基于距离向量
- OSPF的优点
  - OSPF采用SPF算法，从算法上保证了不会产生路由环路  
  - OPF**不限制网络规模** ，更新效率高，收敛速度块

- 链路状态**是指本路由器都和那些路由器相邻**，以及相应链路的**“代价**”
  - 代价用来表示费用，距离，时延，带宽，等等。这些是由网络管理人员来决定的.
  - ![image-20240418134405019](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418134405019.png)



**OPSF的五个分组类型**

- 问候(Hello)分组
  - ![image-20240418134558549](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418134558549.png)

- 数据库描述分组
- 链路状态请求分组
- 链路状态更新分组
- 链路状态确认分组 







- 链路状态通告LSA
  - ![image-20240418135644588](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418135644588.png)
- 使用OSPF的每个路由器都有一个链路状态数据库LSDB，用于存储LSA
- 通过各路由器洪范发送封装有自己LSA的LSU分组，各路由器的LSDB最终达到一致
  - ![image-20240418140251730](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418140251730.png)





**OSPF的基本工作流程**

1. 通过问候分组创建邻居表，链路状态通告LSA的洪范使各个路由器的链路状态数据库达到一致
2. 使用OSPF的各路由器基于链路状态数据库LSDB，进行最短路径SPF算法计算，构建出各自到达其他路由器的最短路径

![image-20240418140614579](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418140614579.png)



![image-20240418141311367](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418141311367.png)





#### 4.6.4边界网关协议BGP

不再深入讨论



![image-20240418152335546](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240418152335546.png)







### 4.7 IP数据报

#### ①IP数据报

![image-20240525120525578](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525120525578.png)

- **IP数据报的报头，通常称之为IP首部，即图中IP数据上面的全部属于IP首部，由20字节固定部分和40字节可变长度构成**

- **IP首部的组成**

  - **版本**：(4字节) 对于IPv4来说，这个值总是4

  - **首部长度**：按照32位(4字节)计算IP首部的长度，包括任何选项字节数，取值范围5-15。
                        普通IP首部没有任何选项字节时，该字段为5，4*5=20，即20字节
                         IP首部最长为15 * 4  = 60，该字段为15 即60字节长，这时可选字段中有数据

  - **区分服务/服务类型(**type of service:TOS)：设置分类和优先级

  - **总长度**：整个IP数据报以字节为单位的长度，占16位，因此IP数据报最长可达65535字节。由于链路层MTU
                   的限制，较长的IP数据报会被分片。当数据报被分片时，该字段也会随着变化，因为该字段表示当前
                   IP数据报总长度。**IP数据报中没有数据的长度，但是数据长度=  总长度 - 首部长度**

  - **标识符/标识**：唯一标识主机发送的每份数据报，占16位。主机为自己发送的IP报文设置一个报文计数器，发送一次，其报文标识符就+1。不同分片表示同一个IP数据报，其标识应当一致

  - **标志**：说明IP报文是否允许被分片，占3位，目前只有后两位有意义。标志字段的最低位是MF(more fragment),MF=1表示后面还    

    ​           有分片，为0表示本报文就是最后一个分片，标志字段的中间位是DF(don`t fragment) DF=0才允许分片。字段首位无意义

  - **片偏移**：片偏移以8字节为偏移单位。指示出数据报被分片后，当前数据报在原分组的相对位置.

  - 生存时间(time-to-live,TTL):用来设置数据报可以经过的最多路由器数，占8位。TTL的初始值由主机设置，推荐的TTL初始值为64
                                        一旦经过一个处理报文的路由器，TTL就减少1，当TTL为0时，数据报就被丢弃，并发送ICMP报文通知主机

  - **类型/协议字段**：也叫协议字段，表示向IP传送数据的上层协议。指的是IP数据的格式，可以说是属于传输层范畴。
                                    当协议字段=6，表明数据部分是TCP报文段

  - **首部检验和**：根据首部数据的二进制反码求和，主要用于对首部进行检验，接收方根据此进行计算，判断该IP数据报是否       

       ​                         有错误，若有错误则丢弃。

  - **源IP地址和目标地址**：每份IP数据报都含有源IP地址和目标地址

  - **选项**：实际上选项用的不多。

- **IP数据：**通常包含一个完整的TCP端或者UDP数据报，也可以包含其协议的报文，如ICMP报文。



#### **例题1**

![image-20240525125803516](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525125803516.png)



#### **考研真题**



![image-20240525131226811](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525131226811.png)



![image-20240525131310354](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525131310354.png)





#### 例题2

![image-20240525132231378](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525132231378.png)







### 4.8 ICMP网络控制报文协议



#### ①什么是ICMP

![image-20240525133644113](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525133644113.png)

![image-20240525133702249](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525133702249.png)





#### ②不发送的情况

![image-20240525134022055](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525134022055.png)



#### ③ICMP询问报文

![image-20240525140029642](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525140029642.png)





#### ③ICMP询问报文典型应用之分组网间探测PING

Ping : **P**acket **I**nter**N**et **G**roup

用来测试目的站是否可达及了解有关状态

在windows命令中为 ping ip地址





#### ④ICMP询问报文典型应用之跟踪路由trace route

用来测试IP数据报从源主机到目标主机要经过哪些路由器

在windows中命令为 tracert ip地址





































### 4.9 虚拟专用网VPN

![image-20240525134823142](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525134823142.png)





![image-20240525134904570](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525134904570.png)

















### 4.10网络地址转换NAT

#### ①引出NAT

![image-20240525135109231](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525135109231.png)



#### ②NAT工作流程

![image-20240525135439875](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525135439875.png)





#### ③NAPT的工作流程

![image-20240525135417041](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525135417041.png)



#### ④NAT的局限和解决方法

解决：可以购买一个公网IP，或者使用内网穿透

![image-20240525135647837](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525135647837.png)







## 五.运输层



### 5.1 运输层概述

![image-20240525205555095](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525205555095.png)



### 5.2 运输层端口号，复用与分用的概念



#### ①端口号

![image-20240525210500409](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525210500409.png)







#### ②复用与分用

![image-20240525210742048](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525210742048.png)



![image-20240525211153027](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525211153027.png)









### 5.3 TCP与UDP对比

#### ①面向不同

**TCP面向字节流，这是TCP实现可靠传输，流量控制等功能的基石**

**UDP面向应用报文的，对应用层报文不合并也不拆分**

![image-20240525212130612](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525212130612.png)



#### ②一对多 一对一

![image-20240525212529100](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525212529100.png)

#### ③数据传输时机不同

**UDP随时可以传输数据**

**TCP必须通过三报文握手建立连接后才能传输数据，通过四报文挥手释放连接**

![image-20240525212615982](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525212615982.png)



#### ④可靠or不可靠

![image-20240525212855983](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240525212855983.png)







### 5.4 TCP报文段

**//Transmission Control Prototcol   传输控制协议**

![image-20240526164002552](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526164002552.png)

- **TCP段首部格式**

  - 源端口和目的端口：每一个TCP段都包含对应的源端口和目的端口

  - 序号：用来标识从TCP发送端到接收端发送的数据字节流，指出本TCP报文段数据载荷的第一个字节的序号，
                 取值范围[0,2^32-1],达到最大后又回到0开始

  - 确认号：指出期望收到对方下一个TCP报文段的数据载荷的第一个字节的序号，同时也是对之前收到的所有数据的确认

    ​			   若 确认号=n  表示到序号n-1之前的数据都已正确接收，期望接收序号为n的数据		
    ​				只有ACK = 1时，确认号才有效，取值为0时，确认号失效。
    ​				TCP规定，在建立连接后所有传送的TCP报文段的ACK都要置1

    ​					取值范围[0,2^32-1],达到最大后又回到0开始

  - 数据偏移/HLEN：用来指出TCP报文段的数据载荷部分的起始处距离TCP报文段的起始处有多远
                       这个字段实际上指出了TCP报文段的首部长度
                       最小长度20字节，最大60字节
  - 窗口：以接收方的接受能力来控制发送方的发送能力，也就是`流量控制`
  - 六个标志位
    - URG:	紧急指针有效
    - ACK：  确认序号有效
    - PSH：  接收方应该尽快将这个报文段交给应用层，不必等到接收缓存都填满后再向上交付
    - PST：  =1时，表明TCP连接出现异常，必须释放连接再重新连接
    - SYN：   同步序号，用来发起一个连接 ; SYN=1 本报文段不能携带数据，普通TCP报文段为0，可携带数据
    - FIN ：   发送端完成发送任务，可以断开连接
  - 检验和：用来检测整个TCP报文段在传输过程中是否出现误码。计算时要加上12字节形成一个伪首部。
  - 紧急指针：当发送发有紧急数据，可插队到发送缓存的最前面，并立刻封装TCP段发送。
                        紧急指针会指出本报文段数据载荷部分包含了多长的紧急数据，紧急数据之后是普通数据

     









### 5.5 UDP

**//User Datagram Protocol，用户数据报协议**

**//UDP也会搞一个UDP伪头部**

```
伪头部
在执行校验和算法之前，还会产生一个虚拟的伪头部出来（也不会真的被传输出去），以用于校验和算法。它是12字节（IPv4则是40字节），满足了偶数字节的要求。它比较奇怪的地方在于，这个作为存在于传输层的伪头部，它居然拥有网络层的信息（即拥有下一层的信息）：

来自IP头部的源ip地址。
来自IP头部的目的ip地址。
来自IP头部的协议号，这个协议号用来指明IP的数据里，装的到底哪个传输层协议的分组。比如装的是UDP的话，就是17。
UDP长度。
伪头部的目的是，让UDP层验证数据是否已经到达了正确的目的地。
```

![image-20240528145744051](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240528145744051.png)



### 5.6 TCP的流量控制



**根据接收方缓存剩余量，对发送方进行流量控制，调整接收窗口.当接收方缓存已满，将接收窗口调整为0。**

**此时，发送方发送零窗口探测报文，若接收方缓存有了存储空间则调整接收窗口，若没有则依然为0。**

![image-20240526134456130](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526134456130.png)

![image-20240526134907108](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526134907108.png)





### 5.7 TCP的拥塞控制

![image-20240526140007382](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526140007382.png)



**慢开始和拥塞避免是1988年提出的TCP拥塞控制算法(TCP Tahoe版本)**

以下是慢开始与要塞避免的演示过程:

```jav
刚开始cwnd<sstresh使用慢开始算法，即指数增长；
当超过ssthresh使用拥塞避免算法，即每次只+1；当出现报文丢失等错误时，将ssthresh调整为当前cwnd的1/2,并设置cwnd=1.
```

![image-20240526145419387](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526145419387.png)



**1990年又增加了快重传和快恢复算法，用来改进TCP的性能，比如报文丢失但没有发生网络拥塞会导致发送发超时重传，误认为拥塞，将cwnd重置为1，使效率降低很多。**

![image-20240526150306003](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526150306003.png)

![image-20240526150417228](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526150417228.png)









### 5.8 TCP的超时重传时间的选择（了解）





### 5.9 TCP可靠传输的实现

**TCP基于以<font color=red>字节为单位的滑动窗口</font>来实现可靠传输**

**感觉就是普通的滑动窗口机制	**

![image-20240526154148110](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526154148110.png)



![image-20240526154944252](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526154944252.png)





![image-20240526155210710](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526155210710.png)

**//easy**

![image-20240526155443690](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526155443690.png)





### 5.10 TCP建立连接⭐

**//<font color=red>比较专业的版本</font>**

![image-20240526163420660](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240526163420660.png)



**//<font color =red>便于理解的版本</font>**

![img](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/202008271630393.png)



### 5.11 TCP释放连接

**//<font color=red>正常的TCP释放连接</font>**

![image-20240527163151399](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527163151399.png)



**//<font color=red>为什么要客户端需要等待2MSL后才关闭呢？答：防止最后一次确认报文丢失导致TCP服务器无法关闭，且此期间可以清除以前的数据</font>**

![image-20240527163359432](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527163359432.png)



**<font color=red>如果TCP客户端出现故障，TCP服务器该如何发现并处理呢？答：TCP保活计时器</font> 	**

![image-20240527163641841](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527163641841.png)





## 六.应用层





### 6.1 C/S与P2P对等方式



![image-20240527164648731](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527164648731.png)

​	



### 6.2 动态主机配置协议DHCP



<font color=red>**DHCP的作用：可以为局域网中各主机自动配置IP地址，子网掩码，默认网关，DNS服务器等信息**</font>

![image-20240527170500609](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527170500609.png)

**<font color=red>DHCP工作流程(了解一下就可以了)</font>**

![image-20240527170303370](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527170303370.png)



<font color=red>**DHCP中继代理:让主机可以访问不在同一局域网的DHCP服务器，从而获取网络配置信息**</font>

![image-20240527171231388](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527171231388.png)





### 6.3 域名系统DNS

#### ①域名组成及其分类

![image-20240527190801227](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527190801227.png)

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527191117417.png)

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527191336696.png)



#### ②域名服务器分类

![image-20240527191620604](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527191620604.png)



#### ③域名解析

![image-20240527193709695](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527193709695.png)

![image-20240527193800604](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527193800604.png)





#### ④DNS报文格式

![image-20240610210140553](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610210140553.png)

​																					**<font color='orange'>八个标志</font>**

![image-20240610210123667](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610210123667.png)

**<font color='red'>真实抓包结果:</font>**

![image-20240610214448296](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610214448296.png)







#### ⑤抓包

**//注意：1.有的字段没有显示，因为抓包工具认为不重要；**

​				**2.zero(零域)：现在新规则应该是1bit**

![image-20240610211423793](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610211423793.png)















### 6.4 文件传送协议FTP	

![image-20240527195156859](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527195156859.png)

**//用于传送控制命令的TCP连接在整个过程都打开，传送数据的TCP连接则在数据传输完毕后关闭**

![image-20240527195656555](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527195656555.png)

























### 6.5 电子邮件

#### ①发送过程总览

![image-20240527202035881](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527202035881.png)







#### ②SMTP(Simple Mail Transfer Protocol)工作原理(了解)



![image-20240527202308186](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527202308186.png)



#### ③ 电子邮件格式

![image-20240527202514238](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527202514238.png)



![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527202631630.png)



#### ④ 邮件读取协议

![image-20240527202824587](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527202824587.png)

#### ⑤基于万维网的电子邮件

![image-20240527203025938](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527203025938.png)





### 6.6万维网WWW





#### ①万维网相关概念

![image-20240527203518104](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527203518104.png)



![image-20240527203539841](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527203539841.png)

#### ② HTTP两种连接方式

![image-20240527203803987](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527203803987.png)

![image-20240527204014615](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527204014615.png)





#### ③HTTP请求/响应报文格式

![image-20240527204238353](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527204238353.png)



![image-20240527204337797](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527204337797.png)



#### ④万维网缓存

![image-20240527204609798](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527204609798.png)

#### ⑤真题

![image-20240527204944209](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240527204944209.png)







## 网络协议分析



### 1.简介







### 2.格式

#### ①两种以太网帧+802.1Q帧

![image-20240609112218426](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609112218426.png)



![image-20240609114519844](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609114519844.png)



​																									**主要是802.3MAC帧和802.2 LLC**

![image-20240609111455584](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609111455584.png)

![image-20240609112944400](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609112944400.png)

![image-20240609114936969](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609114936969.png)













### 3.详解ARP协议



#### 3.1同网段ARP

![image-20240608185348060](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240608185348060.png)



![image-20240608185649515](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240608185649515.png)

#### 3.2跨网段ARP

![image-20240608185926690](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240608185926690.png)



![image-20240608190253205](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240608190253205.png)



#### 3.3 ARP格式

- <font color='orange'>**ARP报文格式**</font>

​                                                                     **帧首:**

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609110308893.png)

![image-20240609110140668](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609110140668.png)

​																	**总览**

![image-20240609113603118](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609113603118.png)





- **<font color='orange'>同网段ARP格式</font>**
  - 略

- **<font color='orange'>跨网段ARP格式</font>**

  **第一个ARP请求**

![image-20240609113913647](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609113913647.png)

**第一个ARP应答**

![image-20240609113924884](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609113924884.png)

**第二个ARP请求**

![image-20240609114140327](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609114140327.png)



**第二个ARP应答**

![image-20240609114202083](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609114202083.png)







#### 3.4 跨网段ARP流程图

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609114035171.png)





​	

#### 3.5 特殊ARP之免费ARP



##### ①四种原因

**这三种情况都可以归结为  IP地址要生效**

![image-20240609122209213](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609122209213.png)

**此外，就是修改mac地址，可以归结为 刷新ARP缓存记录**





##### ② 流程

<font color='orange'>开机，重启，修改的原理</font>：想要当前IP生效，就去询问本网段中该IP的mac地址，若有则说明被占用，系统会随机分配(这里也会发免费ARP检验)；没有就可以使用

- 1.发送ARP请求

![image-20240609123239598](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609123239598.png)







#### 3.6 特殊ARP之ARP代理

<font color='orange'>**arp代理：就是路由器帮你去问，没有arp代理,pc3会先问3.254的mac，但有arp代理pc3可以直接问1.1的mac地址**</font>

![image-20240609150731743](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609150731743.png)







#### 3.7 arp欺骗







### 4. ICMP协议分析



#### 4.1 ICMP报文类型



![image-20240609222153588](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609222153588.png)

![image-20240609222650660](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609222650660.png)





#### 4.2 不产生差错报文的情况

![image-20240609222544711](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609222544711.png)



#### 4.3 路由跟踪

**利用时间超时差错报告报文  实现 路由跟踪**

![image-20240609223650543](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240609223650543.png)



### 5.IP选路协议基础

#### 5.0 路由基础

- 主机路由     /32
- 网络路由
- 黑洞路由
- 缺省路由



#### 5.1 路由表项与转发表项

![image-20240610160748277](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610160748277.png)

- Proto
  - ![image-20240610160717920](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610160717920.png)

- Pre
  - ![image-20240610160738940](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610160738940.png)



- Cost :   16表示不可达
- Flags: 
  - D  ： 下发到FIB表  ， 一般用于 直连
  - RD：  迭代路由    一般用于 非直连
  - R : 备份路由， 如果RIB有个路由出问题，刚好该路由有备份路由，备份路由就会立刻替代

**<font color='orange'>转发表 表项解读(只解读不同的):</font>**

![image-20240610162229310](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610162229310.png)

![image-20240610162445372](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610162445372.png)

![image-20240610162453117](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610162453117.png)

- Flags:
  - G : Gateway Route 网关路由,类似上面的RD
  - H Host Route 主机路由
  - U  Up Route  可用路由
  - S Static Route 静态路由
  - D Dynamic Route 动态路由
  - B Black Hole Route 黑洞路由
  - L Vlink Route   Vlink的虚拟链路路由
- TimeStap:表项已存在时间
- TunnelID:隧道ID    
  - =0    不通过隧道转发
  - ≠0    通过隧道转发







#### 5.2 路由选择基础



![image-20240610155737997](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610155737997.png)

**平时我们说的查路由表查路由表，实际上主要指的就是本地核心路由表**

![image-20240610155754489](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610155754489.png)



![image-20240610160232061](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610160232456.png)







### 6. 动态路由协议RIP



#### 6.1 工作原理

**//简单一句话：就是靠人传人的原理**

![image-20240610175356460](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610175356460.png)





#### 6.2 计时器



- <font color='orange'>更新计时器：</font>路由器定期将路由表发给相邻路由器
- <font color='orange'>失效计时器：</font>
  - 为每一条RIP路由表项建立一个定时器
  - 时间内未收到更新，将该路由度量设置无穷大，标注删除
- <font color='orange'>垃圾收集计时器:</font>标注为删除后生存时间，到期后将彻底删除

![image-20240610180453365](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610180453365.png)











#### 6.3 格式



#### 6.4 静默端口

**像以下四个端口，不需要发送rip，就可以设置成静默端口**

![image-20240610182212621](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240610182212621.png)

















### 7.DNS











































































































































































































