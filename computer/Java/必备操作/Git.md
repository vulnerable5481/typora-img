# 一.Git理论篇



## 1、Git基本理论



### ① 四个区域

```
1、工作区（Working Directory）
	本地电脑用来写代码、修改的文件

2、暂存区（Staging Area/Index）
	一个临时区域，用来收集准备提交的改动。GIT会把你git add的文件放到暂存区，只有暂存区的内容会被commit到本地仓库

3、本地仓库（Local Repository/.git目录)
	存放commit提交的地方，你可以直接找到本地仓库，就是.git目录下面的内容，包含整个仓库的数据

4、远程仓库
```

### ② 工作流程

| 流程                                               | git管理的文件状态  |
| -------------------------------------------------- | ------------------ |
| 1、在工作目录中添加、修改文件；                    | 已修改（modified） |
| 2、将需要进行版本管理的文件放入暂存区域 -> git add | 已暂存（staged）   |
| 3、将暂存区域的文件提交到git仓库。                 | 已提交(committed)  |

### ③ 文件的具体存储

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240810090658982.png" alt="image-20240810090658982" style="zoom:50%;" />

- Directory：使用Git管理的一个目录，也就是一个仓库，包含我们的工作空间和Git的管理空间。

- WorkSpace：需要通过Git进行版本控制的目录和文件，这些目录和文件组成了工作空间。

- git：存放Git管理信息的目录，初始化仓库的时候自动创建。

- Index/Stage：暂存区，或者叫待提交更新区，在提交进入repo之前，我们可以把所有的更新放在暂存区。

- Local Repo：本地仓库，一个存放在本地的版本库；HEAD会只是当前的开发分支（branch）。

- Stash：隐藏，是一个工作状态保存栈，用于保存/恢复WorkSpace中的临时状态。

### ④ 文件状态

```
1、未跟踪（unmarked）红色      : 新建的文件尚未被GIT管理
2、已修改但未暂存（Modify）红色 :文件之前已经被 Git 管理，你修改了内容还没git add
3、已暂存（Staged）绿色        
4、已提交（Commited）不显示
```



## 2、GIT底层知识

### ① 四个对象

```
GIT的核心是对象数据库（Object database），所有内容最终都以对象的形式存储在.git/objects下
GIT的本质就是内容可寻址的文件系统

1、Blob(文件内容)
	只存储文件的原始内容，一般为二进制的数据文件，不包含文件名字等其他信息。
	Key是SHA-1哈希值，通过哈希值寻址
			
2、Tree(目录)    
	存储目录结构，主要记录子目录(tree)、文件列表(blob)，以及文件类型、文件名、权限等
	类似文件系统的索引表,大概长下面这样:
	权限    类型    SHA1哈希值                                  对象名
	100644 blob 36a982c504eb92330573aa901c7482f7e7c9d2e6    .cise.yml
    100644 blob c439a8da9e9cca4e7b29ee260aea008964a00e9a    .eslintignore
    ..............
	
3、Commit(提交) 
	是一次修改的所有内容的集合，也可以说是一批修改过的文件的一个快照
	核心是一个链表结构：commit1 → commit2 → commit3 （SHA-1哈希值也是 commit 的唯一标识）
	长下面这样：  
    tree bd31831c26409eac7a79609592919e9dcd1a76f2     // 本次commit包含的tree的SHA，指向一个tree对象
    parent d62cf8ef977082319d8d8a0cf5150dfa1573c2b7   // 本次commit的父节点，多个就用空格隔开
    author xxx  1502331401 +0800					  // 谁修改了内容
    committer xxx  1502331401 +0800                   // 谁提交了本次修改  这两个往往都是一个人
    fix(bug):补交SQL文件                               //  commit message

4、Tag(标签)
	对象的别名，通常指向commit对象，对象是可签名的
	这个不太熟悉，好像和版本发布有关系
```

### ② 存储模型

```
1、GIT存储模型的独特之处：
	SVN等其他VCS对文件版本的理念是以文件为水平维度，记录每个文件在每个版本下的改变
	GIT对文件版本的理解是以每一次提交为一次快照，提交时进行一次全量快照，没有改变的文件就存储一个指向源文件的引用，不会重复存储

2、检索模型：
	GIT的对象有两种，一种是松散对象，比如.git/objects 的文件夹 03 28 7f ce d0 d5 e6 f9 等，这些文件夹只有 2 个字符开头，其实就是每个文件 SHA-1 值的前 2 个字母，最多有 #OXFF 256 个文件夹。
	另一种是打包压缩文件，打包压缩之后的对象主要存在的是pack文件中，主要用于文件在网络传输，减少网络消耗。为了加快 pack 文件的检索效率，git 基于 pack 文件会生成相应的索引 idx 文件。
```

// todo 以后有兴趣可以继续了解更深层的知识





# 二.GIT实践篇



## 1.常用命令

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



## 2.代码冲突

- **IDEA 内置处理器**

```
1、IDEA合并过程中出现冲突，会出现三个选项，我们一般都是手动合并
			accept yours:代表以自己的为准
            accept theris:代表以更新下来的文件为准
            ✅merge:代表手动合并
2、会出现一个窗口，分为三个部分
			最左侧：本地当前的代码
			中间  ：合并后的结果
			最右侧： 远程仓库的代码
   【通过比较文件内容，合并需要的代码到中间的位置，最后点击Apply就完成了】
3、解决完之后，先pull，再push 
```

- **拉取代码冲突**

```
1、本地修改量比较大，冲突较多
	① git stash -> git pull -> git stash pop -> IDEA内置处理器解决冲突
2、本地有一个或多个commit但未push的提交，经过一段时间有别人提交出现git pull成功但出现一条没有信息的merge，明明别人的代码和自己没有冲突
	原因：遇到的现象其实非常典型：本地有未 push 的提交（commit），远端也有人提交了新 commit，这时你执行 git pull，Git 发现 两边分叉了，默认就会走“合并（merge）”路线，于是出现一个 merge commit。
	解决：使用git pull --rebase 将两条提交线汇合一条线，这样就不冲突了！
```



## 3.几个常见的错误

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



## 4、Git忽略文件

```
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
```









