



# 一、路由与交换技术

- 应用 
  - 端口隔离的两种方法接口单向隔离、端口隔离组，二层三层
    - 为什么不同组可以ping通？ 默认情况下，二层隔离三层互通。比如PC2发送的数据包，首先通过vlanif2,vlanif2发送给vlanif3,再发送给PC3，中间没有经过物理接口，所以能ping通。
  - 混合链路 hybrid 
- 填空
  - 镜像，我们要怎么做。【远二层镜像我们需要什么东西】
    - 远二层镜像，我们需要关闭目标交换机的mac地址学习能力   mac-address leaning disable
  - **逻辑接口**:  vlanif接口 ， loopback接口，inloopback接口 ，子接口  ,  链路聚合中的Eth-trunk【聚合接口】，Null空口【做黑洞路由的】       **【vlanif接口,loopback接口都是可以删除可以创建的 】**
- 分类
  - LACP的两种模式  手工模式和LACP模式
  - vlan:  mux vlan ,  sub vlan , super vlan 
- 快捷键
  - ctrl + c : 中断提示
  - ctrl + a :  光标移动到最左
  - ctrl + e :  光标移动到最右
  - ctrl + x： 删除左边全部字符
  - ctrl + y： 删除当前及左边全部字符
  - quit       返回上一级
  - rertun /  ctrl + Z 返回
  - ？  和  tab   :  帮助








## 1、vlan



### 1.1Vlan标签

<img src="C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20241104135205569.png" alt="image-20241104135205569" style="zoom:50%;" />

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104135531131.png" alt="image-20241104135531131" style="zoom:50%;" />

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104135544416.png" alt="image-20241104135544416" style="zoom:50%;" />



<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104135555478.png" alt="image-20241104135555478" style="zoom:50%;" />



### 1.2 混合链路

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104141949253.png" alt="image-20241104141949253" style="zoom:50%;" />

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241104142002205.png" alt="image-20241104142002205" style="zoom:50%;" />







## 4. s、m



smart link 

```
1. stp disable
2. 创建组，指定端口
3. 发送flush
4. 接收flush
5. 设置回切
6.smart-link enable
```

monitor link

```
1.配置monitor 上行组 、 下行组
2.配置回切
```



## 6.DHCP

```
1.dhcp enable
2.创建vlanif
3.配置地址池相关属性：计算IP划分->分配网络地址、租约期
4.配置路由器接口基于接口的服务方式 
```







# 二 OS





## 1.知识点



![image-20241229154622498](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229154622498.png)

![image-20241229160840542](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229160840542.png)



## 2. SPF

![image-20241229161558920](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229161558920.png)















































































