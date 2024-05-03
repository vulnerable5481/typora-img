# Linux



## 学习git需要的基础命令







## 一.初始Linux

### 1.1 软件安装



- vmware    : 虚拟机
- Xshell7  ： 远程登录
- XFTP7  : UNIX/LINUX 和 windows PC之间传输文件











### 1.2文件目录



/bin        二进制文件，系统常规命令
/boot       系统启动分区，系统启动时读取的文件
/dev        设备文件
**/etc        大多数配置文件**
**/home       普通用户的家目录**
/lib        32位函数库
/lib64      64位库
/media      手动临时挂载点
/mnt        手动临时挂载点
**/opt        第三方软件安装位置**
/proc       进程信息及硬件信息
/root       临时设备的默认挂载点
/sbin       系统管理命令
/srv        数据
/var        数据
/sys        内核相关信息
/tmp        临时文件
**/usr        类似于windows的program files目录**





![image-20240321121230376](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321121230376.png)

![image-20240321121500094](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321121500094.png)



![image-20240321121719487](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321121719487.png)





![image-20240321122023626](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321122023626.png)







### 1.3 vm  vim

**//自带的一个文本编译器**



**//三种模式的切换**

![image-20240321125955986](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321125955986.png)

![image-20240321130024745](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321130024745.png)



​	



**//vim快捷键**

![image-20240321130841676](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321130841676.png)







### 1.4指令操作



[Linux 常用操作命令大全（最后更新时间：2024年1月）_linux常用命令-CSDN博客](https://blog.csdn.net/m0_46422300/article/details/104645072)

/bin        二进制文件，系统常规命令
/boot       系统启动分区，系统启动时读取的文件
/dev        设备文件
/etc        大多数配置文件
/home       普通用户的家目录
/lib        32位函数库
/lib64      64位库
/media      手动临时挂载点
/mnt        手动临时挂载点
/opt        第三方软件安装位置
/proc       进程信息及硬件信息
/root       临时设备的默认挂载点
/sbin       系统管理命令
/srv        数据
/var        数据
/sys        内核相关信息
/tmp        临时文件
/usr        用户相关设定





#### (1) 关机重启操作

```
- shutdown -h now  立刻关机
- shutdown -h -2    两分钟之后关机
- shutdown -r now 立刻重新启动计算机
- shutdown -r 2   两分钟后重新启动计算机

关机重启之前，建议使用  sync   把内存的数据同步到磁盘，以防万一
```



#### (2)用户管理操作

```
用户管理操作：
useradd xx   /  useradd -d /home/xxx  这个可以指定名字
userdel xx  /userdel -r xx  后者是完全删除，前者会保留家目录,一般建议保留家目录
useradd -g 用户组名 用户名  /增加一个用户，并分配到xx组
usermod -g 新组名 用户名
passwd xx  给用户密码
su - xx   /切换用户    切换到root可以直接su   
exit 退出当前用户

id xx  /查询用户信息
who am i  /简写whoami   查询当前用户是谁在什么时候登录的


用户组管理操作:  系统可以对有共性/相同权限的组进行管理,专门用来区分不同的组拥有不同的权限
groupadd xx	
groupdel xx



```



![image-20240321135604894](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321135604894.png)



#### (3)目录操作

```
切换目录：
  cd /                 //切换到根目录
  cd /bin              //切换到根目录下的bin目录
  cd ../               //切换到上一级目录 或者使用命令：cd ..
  cd ~                 //切换到home目录
  cd -                 //切换到上次访问的目录
  cd xx(文件夹名)       //切换到本目录下的名为xx的文件目录，如果目录不存在报错
  cd /xxx/xx/x         //可以输入完整的路径，直接切换到目标目录，输入过程中可以使用tab键快速补全


查看目录：
  ll   
  ls                   //查看当前目录下的所有目录和文件
  ls -a                //查看当前目录下的所有目录和文件（包括隐藏的文件）
  ls -l                //列表查看当前目录下的所有目录和文件（列表查看，显示更多信息），与命令"ll"效果一样
  ls /bin              //查看指定目录下的所有目录和文件 


创建目录:
  mkdir xxx				创建单一目录
  mkdir -p /xx/x/x/x/x/x  创建多级目录


删除目录：
  rm 文件名              //删除当前目录下的文件
  rm -f 文件名           //删除当前目录的的文件（不询问）
  rm -r 文件夹名         //递归删除当前目录下此名的目录
  rm -rf 文件夹名        //递归删除当前目录下此名的目录（不询问）
  rm -rf *              //将当前目录下的所有目录和文件全部删除
  rm -rf /*             //将根目录下的所有文件全部删除【慎用！相当于格式化系统】

修改目录：
  mv 当前目录名 新目录名        //修改目录名，同样适用与文件操作
  mv /usr/tmp/tool /opt       //将/usr/tmp目录下的tool目录剪切到 /opt目录下面
  mv -r /usr/tmp/tool /opt    //递归剪切目录中所有文件和文件夹

拷贝目录:
  cp /usr/tmp/tool /opt       //将/usr/tmp目录下的tool目录复制到 /opt目录下面
  cp -r /usr/tmp/tool /opt    //递归剪复制目录中所有文件和文件夹


```



#### (4)文件操作

```
创建文件:
  touch  a.txt 
  vim  xx.txt 

删除文件：
  rm 文件名              //删除当前目录下的文件
  rm -f 文件名           //删除当前目录的的文件（不询问）

修改文件：
  vim xx    //上节详细讲解
 
  echo “你好” > wd.txt     >就是重定向，可以以此来文本写入信息 //重定向会覆盖原有文本的内容！！
  echo "xx" > xx.txt  >>就是追加 而不覆盖原有内容

查看文件
  cat a.txt          //查看文件最后一屏内容
  less a.txt         //PgUp向上翻页，PgDn向下翻页，"q"退出查看   当文件大的时候推荐less  动态查看文件，资源消耗少
  more a.txt         //显示百分比，回车查看下一行，空格查看下一页，"q"退出查看 当文件小的时候可以直接more
  tail -100 a.txt    //查看文件的后100行,默认是10行，"Ctrl+C"退出查看,用于查看日志？？

```





#### (5)查找操作

```
find:
	find 目录 -name/user/size 文件名   :例子 find /home -user zlc 查询/home目录下面 user为zlc的文件
										   find /home -size +/-/n200M/K/G   查询/home目录下面文件><=xx的文件
locate:
	updatedb
	locate hello.txt

grep:
	cat a.txt | grep "yes"    //起到一个过滤的作用
			  | grep sshd




```

![image-20240324123323078](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240324123323078.png)





#### (6)解压打包文件

**//说明:**

  .zip、.rar        //windows系统中压缩文件的扩展名
  .tar              //Linux中打包文件的扩展名
  .gz               //Linux中压缩文件的扩展名
  .tar.gz           //Linux中打包并压缩文件的扩展名





```
 最常用:::::::tar指令
 tar -zcvf 打包压缩后的文件名 要打包的文件
  参数说明：z：调用gzip压缩命令进行压缩; c：打包文件; v：显示运行过程; f：指定文件名;
  示例：
  tar -zcvf a.tar file1 file2,...      //多个文件压缩打包
  									   //该指令既可以压缩也可以解压
  

zip:
	zip xxxx
	zip -r /home/* -r 递归压缩，连带着目录及其下面的内容都压缩
	
unzip:
	unzip xxx
	unzip -d /opt/tem /home/myhome.zip    -d 指定目录  将myhome.zip解压到/opt/tem



```

![image-20240324125736115](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240324125736115.png)







#### (7)其他操作



```




```















### 1.5运行级别

![image-20240321140505190](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321140505190.png)

![image-20240321140856663](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240321140856663.png)





### 1.6找回root密码



//自己搜







### 1.7权限



#### 1.7.1权限的概念



![image-20240324133939740](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240324133939740.png)









![image-20240324133951953](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240324133951953.png)



![image-20240324134146904](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240324134146904.png)



#### 1.7.2修改权限



![image-20240324134840934](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240324134840934.png)



![image-20240324150304789](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240324150304789.png)















### 1.8修改文件所有者/所在组



```
修改文件所有者:
			chown tom /home/abc.txt  
            chown -R tom /home/test  递归修改test下面所有文件的所有者
            
修改文件所在组:            
			chown group3 /home/abc.txt 
			chown -R group4 /home/abc.txt 递归修改
```









### 1.9两个任务制度



#### 1.9.1crond任务调度



**// crond任务 是周而复始的， 到时间就会自动执行一次**

**//作用: 用于一些重要且需要经常使用的行动，比如病毒检测 ，对重要文件的备份**



```
crontab:
		crontab -e  进入编辑模式，编辑 cront定时周期任务
		crontab -l  查询crontab定时任务
		crontab -r  删除当前用户所有的crontab任务


cront任务时间规则  就是 cront表达式
cront任务 经常是 执行shell脚本
```

**//简单例子 ：每一分钟将当前日期写入 /home/test.txt  文件中**



​	

#### 1.9.2at定时任务



**//只会到达指定时间执行一次，不会重复执行**



用到在学吧







### 1.10磁盘分区和挂载



![image-20240324172850057](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240324172850057.png)



用到再学吧









### 1.11网络代理



- 原理：就是通过代理，linux虚拟机->vmnet -> 无线网卡 -> baidu.com

![image-20240325102051446](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325102051446.png)







- 实操：如何将linux虚拟机的ip固定，而不是自动分配




![image-20240325104558805](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325104558805.png)



然后别忘了这里也要修改哦！       比如你打算设置Ip:192.168.150.15  ,这里子网就要修改为192.168.150.0

![image-20240325104757536](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325104757536.png)







### 1.12设置主机名和hosts映射



**//有的时候我们 ping ip 会感觉有点麻烦，所以我们也可以选择ping 主机名,所以接下来要学习主机名相关的配置**





- 修改linux主机名


vim   /etc/hostname

修改后重启生效 ~ ~ 



![image-20240325110235216](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325110235216.png)





![image-20240325111531924](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325111531924.png)





​											**更加专业的主机名解析机制分析::::**

![image-20240325111645795](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240325111645795.png)







### 1.13进程管理





#### 1.13.1 进程基本操作

- 查看进程
  - 例子 : ps -aux | grep sshd **（静态） **  //-a 显示当前终端的所有进程消息  -u 以用户格式显示进程信息  -x显示后台进程运行参数
  - 查看进程树pstree -p    ：  -p显示 进程号  **（静态）** 
  - ![image-20240328124346843](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240328124346843.png)

​           ![image-20240328124638214](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240328124638214.png)





- 杀死进程
  - kill 1234  /   killall 1234  /  kill - 9 getid      :    -9强制杀死  killall杀死包括子线程在内的线程









#### 1.13.2 服务管理



##### （1）service 操作

【Centos7.0后面，很多服务使用systemctl管理服务！！故此处不细研究】



setup  //用来查看服务名



##### (2)运行级别

![image-20240327210019193](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240327210019193.png)









**//运行级别的设置与管理，一般我们在实际开发中为了节约空间都是使用级别3，这里使用5只是方便学习**

![image-20240327205901026](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240327205901026.png)







##### （3chkconfig查看设置服务自启动

**//一句话：用于设置各个服务在不同运行级别是自启动还是关闭**





```
查看服务运行级别下的自启动状况: chkconfig --list | grep network   //后面的过滤也可以不加

修改服务运行级别下的自启动状况: chkconfig --level 5 服务名 on/off  //设置服务在运行级别X下是自启动还是关闭

修改2，3，4，5级别下自启动状况:chkconfig network on/off  //这个指令只会修改2,3,4,5四个级别下的自启动状态

```



##### （4)systemctl指令⭐



```
查看所有服务: ll /usr/lib/systemd/system    
systemctl [start|stop|restart|status] 服务名   //临时关闭打开服务，若永久关闭需要使用下面的设置服务关闭指令

//关于自启动
查看服务自启动状态: systemctl list-unit-files | grep xxx    //可以查看服务自启动状态
查看某个服务是否自启动: systemctl is-enable 服务名  
设置服务开机启动:systemctl enable 服务名    
设置服务开机关闭:systemctl disable 服务名	//这三个指令和上面chkconfig的区别就是该指令只会修改级别3和5

```











##### （5)firewall指令⭐

```
打开指定端口:firewall-cmd --permanent --add-port=端口号/协议
关闭指定端口:firewall-cmd --permanent --remove-port=端口号/协议
重新载入，才能生效:firewall-cmd --reload
查询端口是否开放:firewall-cmd --query-port=端口号/协议

```









#### 1.13.3监控网络状态



```
查看系统网络状态:netstat -anp | grep xxx   //-an 按照一定顺序排列输出  -p显示哪个进程在调用

检测主机连接命令：ping ip/配置过后的主机名  //这个我们比较熟悉了
```









### 1.14软件包管理rpm



```
查询已安装的所有软件列表: rpm -qa | grep xx

比如查询是否安装火狐浏览器：
				  rpm -qa | grep firefox
			返回 :firefox-68.10.0-1.el7.centos.x86_64
				名称:firefox
				版本号: 68.10.0-1
				适用操作系统:el7.centos.x86_64,如果是i686,i386表示32位系统，noarch表示通用
```

```
查询所有安装的rpm软件包列表:rpm -qa 
查询单个软件是否安装:rpm -q 软件包名


查询软件包信息: rpm -qi 软件包名
查询软件包中的文件:rpm -ql 软件包名
查询当前文件属于哪个软件包: rpm -qf 文件全路径名
```

```
删除rpm包:rpm -e rpm包全路径名称(可以直接简写包名)  //比如删除火狐  rpm -e firefox

安装rpm包:rpm -ivh rpm包全路径名称   -i install安装  -v verbose提示 -h hash进度条
当你需要下载rpm包时，需要先去光盘中packs中寻找对应的rpm包，拷贝到本地才能安装
```

**//强制删除的参数（不过出现这个依赖错误，我们不建议强行删除）**

![image-20240328134642012](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240328134642012.png)





**//更加便捷的rpm软件包下载--yum**

![image-20240328141545253](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240328141545253.png)

















## 二.环境搭配

**//如果我们需要在linux下进行JavaEE的开发，我们需要安装如下软件:**

![image-20240328142306749](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240328142306749.png)



### 2.1安装jdk

```
=====安装jdk============
1.mkdir /opt/jdk
2.如果xftp7 上传jdk的包到 /opt/jdk下
3.cd /opt/jdk
4.解压 tar -zxvf jdk-8u261-linux-x64.tar.gz
5.mkdir /usr/local/java
6.mv /opt/jdk/jdk-8u261 /usr/local/java
=====配置环境变量========
7.vim /etc/profile
8.在配置文件最后加上 export JAVA_HOME=/usr/local/java/jdk1.8.0_401
				  export PATH=$JAVA_HOME/bin/:$PATH
9.source /etc/profile  【让文件生效】
10.写一个hello.java/java -version 测试一下安装是否成功


```



### 2.2安装tomcat



```
1.mkdir /opt/tomcat
2.tar -zxvf tomcatxxxxxx.tar.gz
3.cd tomcatxxxx/bin
4../startup.sh
5.firewall-cmd --permanent --add-port=8080/tcp
6.测试一下是否可以在windows/linux 192.168.200.130:8080看见tomcat页面
```







### 2.3安装Idea

**//一般不会在linux环境下写代码，所以这个不用下**







### 2.4安装mysql5.7



**//这个有空回去补**



### 2.5安装mysql8.0

**//详看mysql数据库那节！！**





## 三.Shell编程



### 3.1 第一个shell脚本

![image-20240328174201895](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240328174201895.png)



![image-20240328174732557](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240328174732557.png)







### 3.2shell变量

**//shell变量包括 系统变量  和  用户自定义变量	**

**//规范:变量最好都大写**

**//注释: #   多行注释 :<<!      !    两者都必须新起一行!!!**

```
#!/bin/bash
#1.定义变量
A=100     #注意不要加空格，必须紧挨着
echo A=$    #注意：加不加""一点都不影响输出内容，但是加''就是将其当成字符串直接输出，$符可以显示变量值

#2.撤销变量
unset A
echo A=$A  #撤销变量后会输出 "A="

#3.静态变量    #1.静态变量只会被初始化一次，占用资源少2.静态变量不能被撤销，如果强制撤销就会报错
readonly B=2
echo B=$B

#4.将命令赋值给变量
C=`date`			//两者作用一致
D=$(date)
echo C=$C			//输出 C=当前时间
echo D=$D			//输出 D=当前时间

```



**//     设置全局变量/环境变量**

```
export 变量名=值	//在配置文件中设置环境变量
source 配置文件     //如果不刷新是不能立刻生效的 ! ! !
echo $变量名       //查询环境变量

```





**//传参**

```
./myshell.sh 100 200 300

$1---$9 意思是第i个参数
$* 意思是所有的参数    //此处将所有参数看成一个
$@ 意思也是所有的参数   //此处将每个参数单独对待
$# 意思是所有参数的length
```





**//预定义变量**

//就是shell设计者事先已经定义好的变量，可以直接在shell脚本中使用

```
$$: 当前进程号(PID)
$!: 后台运行的最后一个进程的进程号(PID)
$?: 最后一次执行的命令的返回状态 ， 0 表示 上个命令正确执行，如果非0（具体哪个数字自己决定）  则表示上个命令执行失败



```









### 3.3运算符



有三种方式，我个人只推荐第二种

```
xx=$[(2+3)*5]

```







### 3.4条件判断



![image-20240331121432423](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331121432423.png)



shell里面的if - else if -else if长这样   



![image-20240331123644539](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331123644539.png)

shell里面的 if - else if -else 长这样

![image-20240331123710912](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331123710912.png)



[ 条件 ] && 操作  ：意思是满足前面的条件就执行后面的语句

例如:  [ ! -d "${BACKUP}/{DATETIME}" ] && mkdir "${BACKUP}/{DATETIME}"









### 3.5shell版本的swich



![image-20240331125649727](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331125649727.png)









### 3.6shell版本的for循环



![image-20240331130028167](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331130028167.png)





![image-20240331130745437](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331130745437.png)







### 3.7while



![image-20240331130934041](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331130934041.png)











### 3.8read



​	![image-20240331132418496](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240331132418496.png)





### 3.9系统函数,自定义函数



几个常用的**系统函数** (可以直接用在终端也可以直接用在shell脚本中):

```
语法  basename 文件路径 [.后缀]

basename /home/aaa/test.txt
返回  test.txt


basename /home/aaa/test.txt .txt
返回  test
```



```
语法  dirname 文件绝对路径

dirname /home/aaa/test.txt
返回 /home/aaa

```





**自定义函数**

```
[function] funname()
{
	xxxxx;
	return xxx;   //如果需要返回值
}


```

















### 3.10自动备份数据库

作为普通开发者 ，能写出类似这样的shell脚本来帮助我们自动完成一些功能就可以了



![image-20240401162655704](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240401162655704.png)



```
最后利用crond 实现每天两点半自动备份即可！
```









































































