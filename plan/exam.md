



# 一、路由与交换技术





## 1、vlan



### 1.1Vlan标签·上

<img src="C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20241104135205569.png" alt="image-20241104135205569" style="zoom:50%;" />

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104135531131.png" alt="image-20241104135531131" style="zoom:50%;" />

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104135544416.png" alt="image-20241104135544416" style="zoom:50%;" />



<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104135555478.png" alt="image-20241104135555478" style="zoom:50%;" />





### 1.2 Vlan标签·下

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104141949253.png" alt="image-20241104141949253" style="zoom:50%;" />

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104142002205.png" alt="image-20241104142002205" style="zoom:50%;" />

















### 1.3 Vlan转发示例

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104140552755.png" alt="image-20241104140552755" style="zoom: 33%;" />



<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104141246303.png" alt="image-20241104141246303" style="zoom: 33%;" />



### 1.4 Vlan间的通信(vlanif)

- vlanif 就是一个逻辑接口，功能和路由器非常类似

- vlanif使用的条件： vlan2的PC和vlan3的PC不允许在同一个网段，比如vlan2的pc都是192.168.1.xxx 

  ​								  vlan3的pc都是192.168.2.xxx

- 如果vlan2和3在同一个网段，但又想要实现vlan间的通信，可以通过vlan聚合实现



#### ① 二层口、三层口

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104142932731.png" alt="image-20241104142932731" style="zoom:33%;" />



#### ② 交换机、路由器、三层交换机



<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104143210767.png" alt="image-20241104143210767" style="zoom: 33%;" />







#### ③ 单播示例

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104143435470.png" alt="image-20241104143435470" style="zoom: 33%;" />



<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104143447617.png" alt="image-20241104143447617" style="zoom:50%;" />



- **<font color='orange'>PC1 ping PC6 (单播)</font>**
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104144940892.png" alt="image-20241104144940892" style="zoom:33%;" />



- **<font color='orange'>PC1 ping PC3 (单播)</font>**
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104145300302.png" alt="image-20241104145300302" style="zoom:33%;" />



#### ④ 广播示例

```
MAC 地址转发表主要用于数据帧的转发，ARP 转发表用于 IP 到 MAC 地址的解析。虽然它们都与 MAC 地址有关，但用途和管理方式是不同的
```



- ​              S3的ARP转发表里 这两个网关的arp 默认自动生成

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104145721162.png" alt="image-20241104145721162" style="zoom: 50%;" />







### 1.5 Vlan聚合



#### ① 两个概念

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104151947622.png" alt="image-20241104151947622" style="zoom:33%;" />

**图形方便理解**

<img src="C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20241104152038921.png" alt="image-20241104152038921" style="zoom:50%;" />







#### ② 命令

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104152959078.png" alt="image-20241104152959078" style="zoom: 33%;" />

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104153048882.png" alt="image-20241104153048882" style="zoom:33%;" />





## 2. STP





## 3.OSPF



### 3.1 邻居状态机

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104162403053.png" alt="image-20241104162403053" style="zoom:33%;" />







### 3.2 OSPF报文



- IP首部协议号：89
- OSPF首部类型=1、2、3、4、5，分别代表Hello,DD,LSR,LSU,LSAck五种类型数据报
-  OSPF首部格式：

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104162717285.png" alt="image-20241104162717285" style="zoom:33%;" />



- 五种报文格式
- type = 1 : Hello报文格式
  - hello报文主要用于确认邻居关系
  - router dead inerval: 邻居死亡时间，如40，即在40s没有收到邻居信息则邻居死亡
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104162803561.png" alt="image-20241104162803561" style="zoom:33%;" />

- type = 2  : DD报文格式
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104162924026.png" alt="image-20241104162924026" style="zoom:33%;" />





































































































































