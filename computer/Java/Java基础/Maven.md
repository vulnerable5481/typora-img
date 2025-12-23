# Maven

## 1. pom文件解读

**// 以谷粒商城的父工程的pom.xml文件 为例**

```java
//xml文件自带的，version="1.0" 声明用的xml版本是1.0，encoding="UTF-8使用utf8编码
<?xml version="1.0" encoding="UTF-8"?>
    
//maven项目--根标签
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	//默认自带的不用管， 使用4.0.0版本的标签结构
    <modelVersion>4.0.0</modelVersion>
	//maven坐标：由 g a v 三个组成
	//groupdId : 公司或团队的一个项目 
	//artifactId :  项目的某一个模块
	//version : 版本，-snapshop意思是快照
    <groupId>com.zlc.gulimall-ware</groupId>
    <artifactId>gulimall</artifactId>
    <version>0.0.1-SNAPSHOT</version>
	//name：当前模块的名字
    <name>gulimall</name>
	//描述一下该模块
    <description>聚合服务</description>
	//packaging：jar(java项目)，war(web项目)，pom（父模块）   默认是jar
    <packaging>pom</packaging>
             
    // 父工程 用来聚合子工程的标签
    <modules>
        <module>gulimall-coupon</module>
        <module>gulimall-member</module>
        <module>gulimall-order</module>
    </modules>
	
	//在MAVEN中定义属性值
    <properties>
		//java版本
        <java.version>1.8</java.version>
		//构建过程中读取源码时使用的字符集
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

	<dependencies>
		<denpendency>
             <grooupId></groudpid>
             <artifactId></artifactId>
             <version></version>
             //当前依赖的范围，test(只在测试环节)
             <scope>test</scope>
		</dependency>
	</dependencies>
</project>

如果当前的pom.xml可能不是最顶级目录下的，可能还会存在parent和build
<parent></parent>:就是父的坐标依然是g a v 组成
<build></build>  :设置打包相关操作，比如默认打包输出位置在target目录下，但是你可以在这里控制打包行为
    			   这也解决了我之前好奇的，为什么执行打包命令会将jar包都输出到指定的位置
```



## 2.底层指令

**<font color='orange'>以下指令皆为idea的面板操作，底层指令了解即可，图形化界面下面的本质就是这些指令</font>**

### ①clean

- 底层指令：mvn clean

- 效果：删除target目录

### ②compile

- 底层指令“：mvn compile(主程序编译)  ； mvn xxx-compile(xxx模块编译)
- 效果：编译，并将其放入target目录

### ③ 其他

还有其他操作 比如 mvn test(测试) ; mvn install(下载maven坐标)，Idea只是提供图形化界面，实际起作用的是这些底层的指令,

对于你来说 了解即可，不需深入理解



## 3.依赖范围

- <scope>标签可选范围 常用：compile,test,provided    ，了解：system,runtime,import
- ![image-20240909212226544](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240909212226544.png)
- ![image-20240909212851142](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240909212851142.png)



## 4. 依赖排除

如下图所示，如果A需要依赖B和C，B和C又需要依赖D，但是依赖传递引入的D是两个不同的版本，这就导致A同时有了两个不同版本的D

此时就会产生冲突！！！！

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240909213544079.png" alt="image-20240909213544079" style="zoom: 25%;" />

解决：让A排除B的依赖传递，这样既不影响B使用D也可以完成依赖排除     

![image-20240909213807356](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240909213807356.png)



## 5.继承

- **引子**：一个大项目通常进行模块拆分，一个project下面有多个moudle，每一个moudle都需要配置依赖信息
  			通过父工程统一管理项目中的依赖信息的版本 既保证项目使用准确的Jar包，也可以将类似项目的经验用在本项目中

- **parent标签**：

  ```
    	<parent>   
          <groupId>com.zlc.myapp</groupId>  
          <artifactId>app-parent</artifactId> 
          <version>1.0-SNAPSHOT</version>  
      </parent>  
      <modelVersion>4.0.0</modelVersion>  
      //因为通过parent标签实现了继承，而g a v中的g和v都继承了所以可以省略，只写一个artifactId即可
      <artifactId>app-child</artifactId>  
      
      
      <dependencies>  
          <dependency>  
              <groupId>commons-lang</groupId>  
              <artifactId>commons-lang</artifactId>  
              <version>2.4</version>  
          </dependency>  
      </dependencies>  
      
  ```

  

- **父工程管理子工程**
        <font color='red'>子工程在使用时，还是需要引入g,a但是不需要制定版本v</font>

  ![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240909221925527.png)                    



- **父工程动态管理版本号**:
                  ![image-20240909222649605](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240909222649605.png)

![image-20240909222714754](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240909222714754.png)



## 6.聚合

- 使用：父工程使用moudle标签聚合子工程
- 作用：还记得底层有个mvn install指令吗，聚合子工程直接就可以在父工程mvn install，会递归install子工程，
             如果没有聚合，那就需要一个一个去install麻烦
             此外，有了聚合，在父工程就形成一个列表可以直观的看到子模块都有哪些 



## 7.实际运用

1.一个父工程下面创建各个模块moudle
                                2.父工程的Pom.xml负责聚合下面的moudle
                                   如下所示，谷粒商城例子

```
    <modules>
        <module>gulimall-coupon</module>
        <module>gulimall-member</module>
        <module>gulimall-order</module>
        <module>gulimall-product</module>
        <module>gulimall-ware</module>
        <module>renren-fast</module>
        <module>renren-generator</module>
        <module>gulimall-common</module>
    </modules>
```

​                          3.专门用一个 xxxx-common的moudle来管理公共的依赖，比如gulimall-order需要mysql驱动，lombok

​						  就在gulimall-common下面引入maven坐标，然后让gulimall-order引入gulimall-common的坐标即可





# Maven实战

## 1.parant

**实际上parant，也可以这样使用，这样制定所有未分配版本的依赖，按照2.6.13 version，方便统一版本**

```
  在 Maven 中，parent 用于实现 POM 配置的继承。子项目可以继承父 POM 中定义的依赖管理、插件管理以及构建相关的默认配置，从而实现统一管理和简化配置。spring-boot-starter-parent 内部通过 dependencyManagement 统一管理了大量常用依赖的版本，因此子项目在引入依赖时可以省略版本号，从而保证整个项目依赖版本的一致性。

```



```
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.6.13</version>
        <relativePath></relativePath>
    </parent>
```

















































































































































































































