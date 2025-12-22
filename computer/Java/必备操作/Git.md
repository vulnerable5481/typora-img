# 一.Git





## Git基本理论（核心）



### 三个区域

Git本地有三个工作区域：

- 工作目录（Working Directory）
- 暂存区(Stage/Index)
- 资源库(Repository或Git Directory)
- 远程的git仓库(Remote Directory)【第四个工作区域,不在本地】

![image-20240810090649096](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240810090649096.png)



- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换
- Repository仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本

- ndex / Stage：暂存区，用于临时存放你的改动，**事实上它只是一个文件**，保存即将提交到文件列表信息

- Workspace：工作区，就是你平时存放项目代码的地方

### **文件在这四个区域的具体存储**

![image-20240810090658982](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240810090658982.png)

- Directory：使用Git管理的一个目录，也就是一个仓库，包含我们的工作空间和Git的管理空间。

- WorkSpace：需要通过Git进行版本控制的目录和文件，这些目录和文件组成了工作空间。

- git：存放Git管理信息的目录，初始化仓库的时候自动创建。

- Index/Stage：暂存区，或者叫待提交更新区，在提交进入repo之前，我们可以把所有的更新放在暂存区。

- Local Repo：本地仓库，一个存放在本地的版本库；HEAD会只是当前的开发分支（branch）。

- Stash：隐藏，是一个工作状态保存栈，用于保存/恢复WorkSpace中的临时状态。
  

### **工作流程**

| 流程                                      | git管理的文件状态  |
| ----------------------------------------- | ------------------ |
| 1、在工作目录中添加、修改文件；           | 已修改（modified） |
| 2、将需要进行版本管理的文件放入暂存区域； | 已暂存（staged）   |
| 3、将暂存区域的文件提交到git仓库。        | 已提交(committed)  |







## 项目搭建







### 创建工作目录常用指令

![image-20240810090951999](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240810090951999.png)

`WorkSpace`（工作目录）：你希望Git帮助你管理的文件夹，可以是你项目的目录，也可以是一个空目录，建议不要有中文。



### 本地仓库搭建

> 方法一：创建全新的仓库

```php
# 在当前目录新建一个Git代码库
$ git init
12
```

执行后可以看到在项目目录多出了一个.git目录(**注意该文件是隐藏的**)，关于版本等的所有信息都在这个目录里面。





>
> 方法二：克隆远程仓库

- 将远程服务器上的仓库完全镜像一份至本地！

```php
# 克隆一个项目和它的整个代码历史(版本信息)
$ git clone [url]  # https://gitee.com/kuangstudy/openclass.git
```



## Git文件操作

要对文件进行修改、提交等操作，首先要知道文件当前在什么状态，不然可能会提交了现在还不想提交的文件，或者要提交的文件没提交上。



![img](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/f6d1d99b0ed7a5b02150016060b7a30d.png)



- ![在这里插入图片描述](https://img-blog.csdnimg.cn/20201113002948309.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaTE5ODYyMQ==,size_16,color_FFFFFF,t_70#pic_center)




`git add . `：添加所有文件到暂存区

`git commit -m "消息内容"`：提交暂存区中的内容到本地仓库 -m 提交信息

`git status `：查看所有文件状态

`git status [filename] `：查看指定文件状态



## Git忽略文件



有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等

在主目录下建立".gitignore"文件，此文件有如下规则：

1、忽略文件中的空行或以井号（#）开始的行将会被忽略。

2、可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{string1,string2,…}）代表可选的字符串等。

3、如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。

4、如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。

5、如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。

`#为注释
*.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
!lib.txt     #但lib.txt除外
/temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
build/       #忽略build/目录下的所有文件
doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt`



## IDEA集成使用Git





完整的流程：比如你想要在gitee上面部署一个项目gut-study。

1. 在Gitee新建一个本地仓库
2. 在本地新建一个仓库(git init)
3. 在该仓库下面建立一个目录，比如git-learn,然后将gitee仓库中的新建项目git clone 到 当前目录，将其里面的文件复制到git-learn，然后可以将它删掉了(万能法,其实直接重名就更加简单了)
4. Idea中的使用细节，自己去琢磨



别的方式：

还可以直接在idea生成本地仓库，Idea 里面有个VCS 可以直接生成.













# 一.Git(new)



## 1.git基本理论

详看上一章





## 2.常用命令



- **邮箱操作【如果第一次下载git使用，必须配置】**

```
git config --global user.name xxx
git config --global email xxx  //注意此处可以是一个虚拟的邮箱，即不存在的邮箱，也可以一个真实的邮箱
上面命令用于设置用户签名和邮箱，如果第一次下载git使用，必须配置，否则无法使用，可以在git.config文件中查看配置信息
//签名信息主要是确认本次提交是谁做的
```



- 基本操作

```
1.初始化
	git init //会生成一个.git隐藏文件

2.git status
  git add [file]  
  git add .   【推荐，所有操作都会上传】
  git add *	   【删除操作不会】
  git commit -m '信息' master
  git commit -m "xxx" fileName -a     //add commit 一块进行
  git clone url
  git push origin master
  git pull 
  git pull origin master --allow-unrelated-histories   //两个独立的 Git 历史尝试合并
 
3. 操作远程仓库
	git remote add xxx  url     添加一个新的远程仓库,并命名。
    git remote -v 显示所有远程仓库的详细信息。
    git remote show 显示某个远程仓库的详细信息。
    git remote rename 重命名远程仓库。
    git remote remove 删除远程仓库。
 
4.其他操作
	git relog   //简单查看资源库文件
	git log     //详细查看资源库文件
	git reset --hard 简化版本号     //用于回溯版本

5.分支
 git branch -v     //查看分支
 git branch xxx //新建一个分支
 git checkout  xxx   //切换到xxx分支
 git merge xxx     //将xxx 分支  合并到 --> 当前分支
  - 分支冲突，比如master对a.txt修改了,hot-fix也对a.txt修改了,（新版本不在同一行不会出现冲突，以前的版本会冲突），这时合并分支会发生冲突，解决方法: 会报错误，将冲突所在文件告诉你，由你手动去解决冲突
```



## 3.几个常见的错误

- github 2020年之后默认分支为 main 而非master

- github创建一个库，此时库中若有自带的readme ,  .gitnore之类的文件，需要先pull，再push

  - 但是经常性的会pull失败，需要借助下面的指令 

    ```
    git pull origin master --allow-unrelated-histories
    ```

    









## 4.GitHub	



团队协作：需要在远程库的setting中的管理成员 添加新成员 ，之后新成员就可以push了



**//直接clone和fork的区别，直接clone你在github上没有对应的库，而fork是将别人的库复制一份在github仓库中，然后clone就可以正常push，想修改人家的代码，需要pull request 对方审核同意才可以合并**

!(https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240417215058189.png)







## 5. 代理服务



```
如果git push 失败，但是网络是可靠的，那么大概率是开VPN导致端口不一致
1、git config --global -l  // 查看端口是否与代理端口一致
2、git config --global http.proxy 127.0.0.1:7890 // 比如我的端口是7890
   git config --global https.proxy 127.0.0.1:10809  // 如果是https
3、如果没有挂着VPN，但还是遇到了该报错，还是端口不一致导致的问题
	git config --global --unset http.proxy    // 取消代理
	git config --global --unset https.proxy
```















