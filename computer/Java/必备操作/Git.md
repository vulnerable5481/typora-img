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

// todo 凑空需要重新整理一份



## 2.常用命令

- **邮箱操作【如果第一次下载git使用，必须配置】**

```
git config --global user.name xxx
git config --global email xxx  //注意此处可以是一个虚拟的邮箱，即不存在的邮箱，也可以一个真实的邮箱
上面命令用于设置用户签名和邮箱，如果第一次下载git使用，必须配置，否则无法使用，可以在git.config文件中查看配置信息
//签名信息主要是确认本次提交是谁做的
```

- **基本操作**

```
1.初始化
	git init //会生成一个.git隐藏文件

2.基础命令：
  git clone url   // 默认主分支
  git clone -b [拉取指定的分支] url
  git status
  git add [file]  
  git add *	   【删除操作不会】
  git add .   【推荐，所有操作都会上传】
  git commit -m '信息' master
  git commit -m "xxx" fileName -a     //add commit 一块进行
  git pull 
  git pull github master
  git pull origin master --allow-unrelated-histories   //两个独立的 Git 历史尝试合并
  git push origin master
  
  git stash              # 保存当前修改
  git stash pop          # 恢复并删除 stash
  git stash apply        # 恢复但不删除 stash
  git stash list         # 查看 stash 列表
  git stash drop         # 删除某个 stash
  
  git log --oneline   //简单查看资源库文件
  git log             //详细查看资源库文件
  
  git branch -v     //查看分支
  git branch xxx //新建一个分支
  git checkout  xxx   //切换到xxx分支
  
	
3. 操作远程仓库
	git remote add xxx  url     添加一个新的远程仓库,并命名。
    git remote -v 显示所有远程仓库的详细信息。
    git remote show 显示某个远程仓库的详细信息。
    git remote rename 重命名远程仓库。
    git remote remove 删除远程仓库。
 
4.其他操作
	git reflog // 查看所有执行过的命令
	git checkout . // 这样可以快速放弃当前工作目录和暂存区的更改，将它们还原到最新一次提交的状态
```

- **更多操作**

```
1、 git cherry-pick hash值 // 一次提交合并到不同分支，比如合并报表的commit从feat-2.1.1也push到feat-2.1.2

2、 回退代码（只是回到某个版本看一看）+回到最新一次提交
  git log --oneline //查看历史版本，找到需要回退的版本
  git checkout hashCode    // 回退代码-老版本命令   git switch --detach hashCode //新版本命令	 
  git checkout master/main // 回到最新一次提交      git switch --detach master/main // 新版本命令

3、 回退代码（真的回退！会移动HEAD）
case 1:回退但保留修改内容
	git reset --soft hashCode
case 2:回退，修改放到工作区
	git reset --mixed hashCode
case 3:彻底回退，丢弃当前修改内容 ⚠危险
	git reset --head hashCode
	
4、 彻底回退代码，但依然可以补救
  git reflog // 查看所有操作，找到类似记录：a1b2c3d HEAD@{0}: reset: moving to e4f5g6h
  									   z9y8x7w HEAD@{1}: commit: 最新提交
  git reset --hard z9y8x7w  // 通过回退撤销回退

5、 合并代码，比如从mastr分支拉取一个feature分支，当我们开发一段时间后，需要合并master分支到我们当前feature分支
	      这时候我们一般都使用 git rebase 让分支变成一条直线，整洁历史
	      假如说在我们开发过程中，本地feature分支有三次提交，master也有两次提交，为避免冲突，肯定要在本地先合并代码
	      A --- B --- C   (master)
                 \
                  D --- E --- F   (feature)
		 ① git checkout feature // 确保在feature分支
		 ② git rebase master    // 把master的最新代码“变基”到feature上，这一步做了什么？
		 						 1.GIT暂时拿走feature上的DEF提交
		 						 2、把feature的基点移动到master的C
		 						 3、再把DEF提交一个一个重新应用
	   							 4、本地feature分支结果：A --- B --- C --- D' --- E' --- F' (feature) 
		 ③ git checkout master
		   git merge feature   // 因为 master 没有分叉，Git 会直接前移指针：
		                            本地master分支结果：A --- B --- C --- D' --- E' --- F'  (master)
		 ④ 如果出现了冲突，就去解决冲突,解决完就推送到master即可
		 	解决完冲突:          git rebase --continue
		 	解决失败放弃rebase:   git rebase --abort
		 ⑤ 【rebase的前提条件】
		   第一、永远不要对已经 push 到公共仓库、且被他人使用的分支做 rebase
		   情况1：git rebase origin/master，此时本地master有DEF未push的提交，远程有一个新的G提交，
		         D' E' F' 还没有 push 到远程，别人根本不知道 D' E' F'，当然可以rebase即使是master分支
		   情况2：本地feature分支，如果没人使用这个分支，自然可以随便rebase
		 ⑥ 在rebase之后会进行切换到master分支然后merge的操作，我的疑问就是这里merge会导致master分支提交时                          commit的提示语是“Merge branch 'master' of xxx ”吗？
             答： 
                不会，因为是Fast-Forward Merge（快进合并），rebase过程中已经解决了冲突，也就是没有merge的merge
                所谓的快进合并：当目标分支没有新提交，只需要往前移动Head指针，而不创建新的commit

6、git fetch
	git pull github master =  git fetch github master + git merge github master
	就是获取远程仓库最新状态，但不自动merge到本地仓库代码
	感觉这个命令实际上用处不大，尤其是在图形化界面+命令一块配合使用的时候，用的时候更少吧。
	
7、git revert
	   ① revert与reset的区别： reset用于本地回退，对本地修改影响取决于soft、hard等，会直接改变历史记录，所以能破坏公共历史
	   						 revert用于公共回退，不影响本地未提交修改，不会直接修改历史记录，所以不会破坏公共历史
                     简单理解：   						 
                         reset = “直接改掉过去的提交”
                         revert = “创建一个新提交，专门用来抵消过去的提交”
	   ② 应用场景：公共提交中某次提交有问题，需要回退，这时候需要使用git revert ,如果是本地回退用git reset
```



## 3.代码冲突

- **IDEA 内置处理器**

```
1、IDEA合并过程中出现冲突，会出现三个选项，我们一般都是手动合并
			accept yours:代表以自己的为准
            accept theris:代表以更新下来的文件为准
            ✅merge:代表手动合并
2、会出现一个窗口，分为三个部分
			最左侧：本地当前的代码
			中间  ：合并后的结果
			最左侧： 远程仓库的代码
   【通过比较文件内容，合并需要的代码到中间的位置，最后点击Apply就完成了】
3、解决完之后，先pull，再push 
```

- **拉取代码冲突**

```
1、本地修改量比较大，冲突较多
	① git stash -> git pull -> git stash pop -> IDEA内置处理器解决冲突
```



## 4.几个常见的错误

- github 2020年之后默认分支为 main 而非master

- github创建一个库，此时库中若有自带的readme ,  .gitnore之类的文件，需要先pull，再push

  - 但是经常性的会pull失败，需要借助下面的指令 

    ```
    git pull origin master --allow-unrelated-histories
    ```

- **端口不一致导致push失败**

```
如果git push 失败，但是网络是可靠的，那么大概率是开VPN导致端口不一致
1、git config --global -l  // 查看端口是否与代理端口一致
2、git config --global http.proxy 127.0.0.1:7890 // 比如我的端口是7890
   git config --global https.proxy 127.0.0.1:10809  // 如果是https
3、如果没有挂着VPN，但还是遇到了该报错，还是端口不一致导致的问题
	git config --global --unset http.proxy    // 取消代理
	git config --global --unset https.proxy
```













