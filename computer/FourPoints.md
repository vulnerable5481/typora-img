# 计算机网络



## 一,计算机网络概述



### 1.1 三种交换方式



#### (1) 分组交换⭐

​	![image-20240228103558021](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228103558021.png)





#### (2)电路交换

简单来说，就是用电路直接去连接x台设备

#### (3)报文交换

了解一下即可





### 1.2计算机网络的定义和分类



计算机网络的定义比较复杂，简单来说就是 一些互相连接的，自治的计算机集合   (此处的计算机也包括智能手机之类)



分类：![image-20240228103855408](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228103855408.png)







### 1.3计算机网络的性能指标



- 速率
  ![image-20240228104138303](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228104138303.png)
- 带宽：最大速率
- 吞吐量 :  单位时间总传输的数据量
- 时延 : 通常包括  发送时延，传输时延 ，接收时延，排队时延(可能没有可能有)
- 时延带宽积
- 往返时间
- 利用率
- 丢包率



### 1.4计算机网络体系结构⭐



#### (1)常见的计算机网络体系结构

![image-20240228104408856](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228104408856.png)

**TCP/IP协议的展开**



![image-20240228113407353](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228113407353.png)

#### (2)计算机网络分层的必要性

![image-20240228105019240](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228105019240.png)







#### (3)分层的例子一http请求与响应

//注意：此处假设N1，N2是以太网

**//注意：这些各种层只是我们为了理解和应用而进行的分层，实际上其实是一个整体过程，只是我们分层剖析**





##### 1 主机H1中的浏览器发出一个Http请求到路由器的过程

1.第一步：在应用层  (具体就是在谷歌浏览器)  根据http协议创建一个htpp报文

![image-20240228105757745](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228105757745.png)

2.第二步：在运输层  添加一个TCP首段 使之成为 TCP报文段（该首部的作用主要是为了区分应用进程，以及实现可靠传输）



![image-20240228105925915](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228105925915.png)



3.第三步，在网络层  添加一个IP首部 ，使之成为 IP数据报(该首部含有目的地址，其主要作用是可以被路由器转发(因为在这里可以得到目的地址))

![image-20240228110040252](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228110040252.png)



4.第四步，在数据链路层 添加一个首部和一个尾部，使之成为一个帧 (首部作用是为了让帧能在一段链路上或一个网络上传输，被相应的目的主机接收； 尾部作用是为了让目的主机检查所接收到的帧是否有误码)



​	![image-20240228110949276](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228110949276.png)





5.第五步，在物理层，将帧看作比特流，由于网络N1是以太网，还会加入前导码(其作用是让目的主机做好接收帧的准备，比如使接收方的时钟同步)

物理层将添加有前导码的比特流转换为响应的信号发送到传输媒体，信号通过传输媒体到达路由器。



![image-20240228111441553](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240228111441553.png)







##### 2，路由器处理比特流的过程



1.去掉前导码，将其转交给数据链路层(实际上交付的是帧)

2.数据链路层将帧的首部尾部去掉后，交付给网络层(实际上交付的是IP数据报)

3.网络层解析IP数据报的首部，得到目的地址，然后查找自身路由表，确定转发端口以便转发，网络层将IP数据报转交给数据链路层

4.数据链路层给IP数据报添加一个首部和一个尾部使之成为一个帧，然后交给物理层。

5.物理层将帧看作比特流，由于N2是以太网，物理层还会加入前导码,转化为相应的信号发送到传输媒体,信号通过传输媒体到达web服务器。



##### 3.从路由器到目的主机(web服务器)的过程

层层剥皮，最后在应用层得到http请求报文，解析数据,然后给h1主机返回http响应



##### 4.从目的主机(web服务器)返回http响应到主机h1的过程

和前面差不多，也是层层剥皮，层层套皮。









## 二.物理层

**//简单学习一下即可，重点是掌握基本概念**







### 2.1 物理层的基本概念

![image-20240305123648466](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240305123648466.png)





### 2.2 物理层之下的传输媒体(了解)

**//知道传输媒体大概有这几个就Ok 了**

![image-20240305123811825](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240305123811825.png)





### 2.3 传输方式



![image-20240305124256236](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240305124256236.png)





### 2.4编码与调制(⭐)

![image-20240305134336274](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240305134336274.png)





### 2.5 信道的极限容量

![image-20240305142453179](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240305142453179.png)







## 三.数据链路层





### 3.1封装成帧



- 含义：数据链路层将上层交付的协议数据单元添加帧头和帧尾，使之成为帧
  - 帧头和帧尾中包含重要的控制信息
  - 帧头帧尾的作用之一就是帧定界

​					**//PPP帧：**

![image-20240312120412227](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312120412227.png)



**//以太网V2的MAC帧**

![image-20240312120457875](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312120457875.png)

//其中前导码 前七个字节为前同步码，作用是使接收方的时钟同步；后面一个字节是帧开始定界符，表明紧跟着的就是MAC帧



//另外，以太网的MAC帧不需要帧结束定界符，因为有帧间间隔（后面会详细讲解）

![image-20240312120747027](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312120747027.png)





- **透明传输**
  - 含义：将数据链路层对上层交付的传输数据没有任何限制，就好像数据链路层不存在一样
  - 提问：若在数据中恰好含有 和帧开始结束定界符一样 的字节 该怎么办？
    - ![image-20240312121505883](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312121505883.png)

​		



### 3.2 差错检测



- **奇偶检测（漏洞多，一般不会采用该方法）**

![image-20240312121626716](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312121626716.png)





- **循环冗余检验CRC(Cyclic Redundancy Check)**

![image-20240312124952968](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312124952968.png)

![image-20240312125012554](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312125012554.png)

![image-20240312125056495](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312125056495.png)



![image-20240312125111487](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312125111487.png)

### 3.3可靠传输

#### 3.3.1  一些基本概念

![image-20240312125358854](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312125358854.png)



![image-20240312125407375](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312125407375.png)



#### 3.3.2  停止-等待协议SW(stop-and-Wait)



![image-20240312125956484](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312125956484.png)



#### 3.3.3 回退N帧协议GBN

![image-20240312130048735](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312130048735.png)



![image-20240312130212292](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312130212292.png)

  



#### 3.3.4 选择重传协议SR



总体流程也是滑动窗口那样，只不过接收窗口的接收数量不再是1。

![image-20240312131438514](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312131438514.png)



![image-20240312131503952](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312131503952.png)





### 3.4 点对点协议PPP



#### 3.4.1 帧格式

![image-20240312132511372](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312132511372.png)



#### 3.4.2 透明传输

![image-20240312132734084](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312132734084.png)



![image-20240312132952660](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312132952660.png)



![image-20240312133719483](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312133719483.png)







#### 3.4.3 差错检测

//采用前面学过的CRC 进行计算

![image-20240312133943995](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312133943995.png)



#### 3.4.4 工作状态



![image-20240312134425041](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240312134425041.png)







### 3.5 媒体接入控制



#### 3.5.1 媒体接入控制的基本概念



![image-20240313130000993](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313130000993.png)





#### 3.5.2 静态划分信道



- **频分复用FDM**

![image-20240313130124945](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313130124945.png)

- **时分复用TDM**

![image-20240313130219510](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313130219510.png)



- **波分复用WDM**

![image-20240313130159167](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313130159167.png)

- **⭐码分复用CDM**



![image-20240313130305618](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313130305618.png)



![image-20240313130335927](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313130335927.png)



![image-20240313130349151](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313130349151.png)



![image-20240313130410158](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313130410158.png)







#### 3.5.3	动态接入控制--随机接入---CSMD/CD协议



##### 1.**CSMA/CD协议--概念**

**//CSMA/CD协议适用于 有线网络，CSMA/CA协议适用于无线网络**

![image-20240313131246643](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313131246643.png)




##### 2.**CSMA/CD协议--碰撞检测的流程**

![image-20240313131452352](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313131452352.png)

##### 3.**CSMA/CD协议--争用期（碰撞窗口）**

![image-20240313132008824](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313132008824.png)

##### 4.**CSMA/CD协议--最小帧长和最大帧长**

最小帧长 = 争用期 * 数据传输速率

![image-20240313132610509](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313132610509.png)

![image-20240313133043076](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313133043076.png)



##### 5. **CSMA/CD协议--截断二进制指数退避算法**

![image-20240313133359241](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313133359241.png)



##### 6.**CSMA/CD协议--信道利用率**

S = T/T+t =  1/1+t/T 

![image-20240313133626688](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313133626688.png)

##### 7.**CSMA/CD协议--帧接收和发送流程**

​		![image-20240313133919741](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313133919741.png)



![image-20240313134154261](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313134154261.png)





##### 8.总结

**//CSMA/CD协议曾经用于各种总线结构以太网和双绞线以太网的早期版本中，现在的以太网基于减缓及和全双工连接，不会有碰撞，因此没必要使用CSMA/CD协议**

![image-20240313140346274](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313140346274.png)











#### 3.5.4	动态接入控制--随机接入---CSMA/CA协议

**//CSMD/CA协议  适用于  无线局域网**



##### 1.    CSMA 依然可用  , CD 不可用



![image-20240313174909038](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313174909038.png)

![image-20240313175011566](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313175011566.png)



##### 2.   注意:  802.11标准  使用了	SW

![image-20240313175256965](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313175256965.png)







##### 3.帧间间隔(IFS)   SIFS DIFS

![image-20240313175422690](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313175422690.png)



##### 4.退避算法

![image-20240313175643190](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313175643190.png)

![image-20240313175725469](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313175725469.png)





##### 5.具体工作流程	

![image-20240313175950154](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313175950154.png)





##### 6.信道预约



![image-20240313180031024](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313180031024.png)



​	![image-20240313180334354](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313180334354.png)



##### 7.虚拟载波监听 



![image-20240313180415857](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240313180415857.png)





### 3.5 MAC地址、IP地址、ARP协议







#### 3.5.1 MAC地址



- 总览

![image-20240318133316442](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318133316442.png)









- MAC地址的四种分类

**//全F  就是 广播地址**

![image-20240318132511261](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318132511261.png)



- 广播帧、单播帧、多播帧

**//广播帧   是目的地址为全F；  当其他主机接收到广播帧就会接收**

**//单播帧 就是地址匹配就接收，不匹配就丢弃,easy**

![image-20240318132814159](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318132814159.png)

**//多播帧**

![image-20240318133239410](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318133239410.png)







#### 3.5.2 IP地址







- 总览




![image-20240318134343003](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318134343003.png)





- 数据包转发过程中IP地址与MAC地址的变化情况	

**//哇哦，这样就无法定位发送信息的主机真实信息**

![image-20240318134040958](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318134040958.png)





#### 3.5.3 ARP协议



**//ARP协议工作流程**



1.在本机的ARP高速缓存中查找 Ip地址对应的MAC地址



![image-20240318135025426](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318135025426.png)



2.  查找成功就直接发送，查找失败就发送ARP请求	 (该请求是一个广播帧)



![image-20240318135107463](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318135107463.png)



3.找到后，另外那台主机就发送ARP响应，以告知自己的MAC地址，主机收到ARP响应后，将其添加到ARP高速缓存中,并发送



![image-20240318135331369](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318135331369.png)





4. ARP高速缓存的一些信息

![image-20240318135355770](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318135355770.png)





5.不可以通过ARP协议跨网络获取其他网络中主机的MAC地址，因为广播帧只能在本频道中传播



![image-20240318135427454](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318135427454.png)



### 3.6  集线器与交换机的区别

**//区别就是，交换机能自己判断，集线器只是传播工具**

![image-20240318141542441](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318141542441.png)





### 3.7以太网交换机自学习与转发帧的流程





![image-20240318143338935](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318143338935.png)







### 3.8 以太网交换机的生成树协议STP（了解）





![image-20240318161832766](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318161832766.png)

- STP  
  - BID(桥ID)  由桥优先级 和 桥MAC 组成，缺省为32768
  - PID(端口ID) 由端口优先级 和 端口号 组成 ，缺省128
  - RB（根桥）确定依据：























### 3.9 虚拟网VLAN



**//为解决巨大广播域中广播风暴之类难以管理和维护的问题，使用路由器来分割广播域，这一块块的小网络就是VLAN**



#### 3.9.1 虚拟局域网VLAN概述

![image-20240318162405855](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318162405855.png)



#### 3.9.2 虚拟局域网VLAN的实现机制



- IEEE 820.1Q帧

![image-20240318164412552](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318164412552.png)



**//交换机的三大端口类型**



- Access端口类型 ：连接用户的端口为access端口

![image-20240318164617630](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318164617630.png)

- trunk端口类型 : 交换机内部的端口为trunk端口

![image-20240318165152433](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240318165152433.png)

- hybrid端口
  不用了解











## 四.网络层



### 4.1网络层概述



![image-20240417122652968](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417122652968.png)

![image-20240417123009043](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417123009043.png)





### 4.2网络层提供的两种服务



![image-20240417123509727](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417123509727.png)



![image-20240417123521920](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417123521920.png)









### 4.3 IPv4地址

#### 1.初步了解ipv4

- IPv4地址的概念：就是给因特网提供上的每一个主机/路由器的每一个接口分配一个**在全世界范围内唯一的32比特的标识符**
- IP地址是谁分配的？：因特网名字和数字分配机构**ICANN**进行分配，我国可以向亚太网络信息中心APNIC申请IP地址，需要缴费，一般不接受个人申请，2011年，互联网号码分配管理局宣布，IPv4地址已经全部分配完毕！我国也在2014年后逐步停止向新用户分配ipv4地址，同时全面开展商用部署ipv6.



#### 2.ipv4地址概述



- 由于32比特的ipv4地址不方便阅读，记录等，因此ipv4地址采用**点分十进制表示方法**，便于用户使用
  - ![image-20240417124449251](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417124449251.png)

#### 3.ipv4地址经历的三种分配方式之分类地址

**技巧:**

**128（1-127）  64（128-191）32（192-223）



![image-20240417125138865](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417125138865.png)


![image-20240417125759744](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417125759744.png)



![image-20240417130234084](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417130234084.png)



![image-20240417130708643](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417130708643.png)





![image-20240417131501645](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417131501645.png)

![image-20240417131858903](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417131858903.png)









#### 4.ipv4地址经历的三种分配方式之划分子网(子网掩码)



**引出子网掩码**

![image-20240417132147522](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417132147522.png)



**//子网掩码就是从主机号中借用几个比特作为子网号**

![image-20240417132403638](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417132403638.png)

**//划分案例**

![image-20240417132645730](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417132645730.png)

**//默认子网掩码**

![image-20240417134843766](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417134843766.png)





**//三道练习题**

![image-20240417133223148](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417133223148.png)

![image-20240417133407827](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417133407827.png)

![image-20240417134706356](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417134706356.png)



####  5.ipv4地址经历的三种分配方式之无分类编址



**//为什么使用无分类编址?**

![image-20240417140229106](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417140229106.png)

**//具体使用**

![image-20240417140217783](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417140217783.png)





**//路由器中如何构造路由表**



![image-20240417140112860](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417140112860.png)



**//习题**

![image-20240417140700591](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417140700591.png)





### 4.4ipv4地址的应用规划

#### 1.定长的子网掩码FLSM

![image-20240417191139698](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417191139698.png)







#### 2.边长的子网掩码VLSM

![image-20240417191724673](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240417191724673.png)







### 4.5ip数据报的发送和转发过程

**//主机A  ->  主机D**

**//网络地址 = 目的地址 ^ 子网掩码**

```
1.根据主机A与D的ip地址与A的子网掩码 得出A与D的网络地址，进行比较若相同则在同一网络可直接交付，若不在同一网络则间接交付

2.间接交付，为了使不同网络的主机进行通信，必须给主机指定一个路由器，该路由器负责帮忙转发，所指定的路由器也称为默认网关！对于本例我们可以将路由器R的接口0的ip地址作为默认网关。  

3.到达路由器，将IP数据报中目的地址^路由表中的地址掩码，若目的网络相同则根据表中信息转发
```

![image-20240418110745322](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418110745322.png)



**//主机A本网络的广播**



![image-20240418110722031](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418110722031.png)



**//练习题**

![image-20240418112617883](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418112617883.png)





### 4.6静态路由选择



就是人工配置



![image-20240418120231132](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418120231132.png)

### 4.6动态路由选择

#### 4.6.1路由选择协议概述

路由选择协议概述



![image-20240418120251919](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418120251919.png)





![image-20240418120441145](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418120441145.png)

 



![image-20240418120950149](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418120950149.png)











#### 4.6.2路由信息协议RIP的基本工作原理



**一些概念**

- 路由信息协议RIP是内部网关协议/内部路由协议IGP中最先得到广泛使用的协议之一
- RIP要求自治系统AS中每一个路由器都维护一个从它自己到AS内其他每一个网络的距离记录，这些距离称为，距离向量D-V
  - RIP使用跳数作为度量
  - 路由器到直连网络的距离为1
  - 路由器到非直连网络的距离为中间经过的路由器数量+1
  - 一条路径最多只能包含十五个路由器，当距离 == 16 意思是不可达，因此RIP只适用于小型互联网
  - ![image-20240418124658267](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418124658267.png)

- RIP 认为 好的路由是 距离短的路由
- 当到达同一目的网络有多条距离相等的路由时，可以进行等价负载均衡
- RIP 包含三个要点
  - 和谁交换信息       仅和自己相邻的路由交换信息
  - 交换什么信息      自己的路由表
  - 何时交换信息       周期性交换（例如每三十秒）

**基本工作过程**

![image-20240418124126922](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418124126922.png)



**更新规则**



![image-20240418124144953](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418124144953.png)



**坏消息传得慢**



![image-20240418125852876](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418125852876.png)

![image-20240418125918708](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418125918708.png)











#### 4.6.3开放最短路径优先OSPF基本工作原理



**一些概念**

- 开放最短路径优先OSPF是为了克服RIP的缺点在1989年开发出来的
  - “开放” 表明OSPF协议不是受某家公司控制，而是公开发表的
  - 最短路径优先，是指使用了迪结特斯拉发明的spf最短路径算法

- OSPF是基于**链路状态**的，而不是像RIP那样是基于距离向量
- OSPF的优点
  - OSPF采用SPF算法，从算法上保证了不会产生路由环路  
  - OPF**不限制网络规模** ，更新效率高，收敛速度块

- 链路状态**是指本路由器都和那些路由器相邻**，以及相应链路的**“代价**”
  - 代价用来表示费用，距离，时延，带宽，等等。这些是由网络管理人员来决定的.
  - ![image-20240418134405019](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418134405019.png)



**OPSF的五个分组类型**

- 问候(Hello)分组
  - ![image-20240418134558549](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418134558549.png)

- 数据库描述分组
- 链路状态请求分组
- 链路状态更新分组
- 链路状态确认分组 







- 链路状态通告LSA
  - ![image-20240418135644588](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418135644588.png)
- 使用OSPF的每个路由器都有一个链路状态数据库LSDB，用于存储LSA
- 通过各路由器洪范发送封装有自己LSA的LSU分组，各路由器的LSDB最终达到一致
  - ![image-20240418140251730](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418140251730.png)





**OSPF的基本工作流程**

1. 通过问候分组创建邻居表，链路状态通告LSA的洪范使各个路由器的链路状态数据库达到一致
2. 使用OSPF的各路由器基于链路状态数据库LSDB，进行最短路径SPF算法计算，构建出各自到达其他路由器的最短路径

![image-20240418140614579](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418140614579.png)



![image-20240418141311367](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418141311367.png)





#### 4.6.4边界网关协议BGP的基本工作原理

https://gitee.com/vulnerable5481/typora-img/raw/master/img/https://gitee.com/vulnerable5481/typora-img/raw/master/img/

不再深入讨论



![image-20240418152335546](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240418152335546.png)







### 4.7 IPv4数据报的首部格式















































