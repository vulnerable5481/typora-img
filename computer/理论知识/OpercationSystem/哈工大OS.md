#   一.初识OS



## 1.从os启动开始

- **<font color='blue'>接下来，我们将从计算机开机后出现windos Logo 加载时的第一行代码讲起</font>**



### ① 打开电源

- **<font color='blue'>0磁道0扇区，是磁盘上的第一块扇区，也被称为引导扇区</font>**

![image-20241221223126588](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241221223126588.png)



### ② 引导扇区

- **<font color='blue'>0x07c0:0</font>**  将0x07c0:0处的256个字copy到0x9000:0处，也就是从BOOTSEG拷贝到INITSEG
- 然后修改cs和ip，跳转到0x9000:0处（INITSEG）

![image-20241221223248510](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241221223248510.png)



### ③ jmi go,INITSEG

- **<font color='blue'>0x9000:0</font>**    执行load_setup,从第二个扇区往后读取4个扇区（即setup的四个扇）,实现载入setup模块
- **<font color='blue'>载入的setup模块在哪里呢？</font>**答案：es:bx，即 0x9020:0处

![image-20241221224351826](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241221224351826.png)



### ④ ok_load_setup

- **这里做两件事，一是 打印字符串‘Loading system...’ ，二是 调用call read_it //开始读入system模块**

![image-20241221224706498](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241221224706498.png)



### ⑤ read_it

![image-20241221225639118](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241221225639118.png)



## 2.setup模块





### ① 移动sys

- **<font color='blue'>取出光标位置(包括其他硬件数据)到 0x90000处</font>**
- **<font color='red'>同时，将system模块向前移动。其实是把10000~90000之间的数据全部往前平移了10000位，就是移动到了0~80000的位置。</font>**

![image-20241221230426656](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241221230426656.png)





### ② end_move

- <font color='blue'>**临时创建并初始化gdt,为进入保护模式做准备**</font>

![image-20241222205405074](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241222205405074.png)





### ③ 进入保护模式

**<font color='red'>steup中间还做了很多事情，但不是重点，此处我们省略，直接跳到setup最后也是最关键的地方：进入保护模式</font>**



- **cr0是一个32位寄存器，其第一位是PG，最后一位是PE。若PE=1,则开启保护模式;若PG=0,则启动分页**

![image-20241222205932457](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241222205932457.png)





## 3. system模块

**<font color='blue'>system模块的第一部分代码，就是head.s</font>**



### ① head.s

- <font color='blue'>**end_move中建立的只是临时gdt，方便在保护模式下跳转到0:0处，这里会真正建立gdt**</font>

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241222212945008.png)



### ② 汇编->C

**<font color='red'>执行完head.s后，下一部分代码为main.c，注意不再是汇编，而是C语言</font>**



### ③after_page_tables

- **<font color='blue'>设置页表之后，调用main函数，然后进入死循环，因为操作系统就是一个永不停止的程序</font>**

![image-20241222213639946](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241222213639946.png)



### ④ main.c

![image-20241222213933795](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241222213933795.png)



### ⑤ mem_init

- **<font color='red'>此处我们只以 mem_init()，内存初始化为例子，其他的都是一个道理</font>**



- **start_mem、end_mem就是mem_map占用的内存空间，这两个参数从哪里来？** 答：很简单，90002处的内存单元。
- **代码如何初始化内存？**  答：将mem_map已经使用的内存置为100,没用过的地方设置为0

![image-20241222214704228](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241222214704228.png)







## 4. 补充:保护与实







## 5. 操作系统接口

- **操作系统接口，就是暴露给外面的调用的一些函数，平时我们说调用函数，那这里就是调用系统函数，即system_call**

- **<font color='red'>system_call是什么？</font>**，就是操作系统给我们提供的可以访问被保护的内核的函数

- **<font color='red'>为什么需要操作系统接口？</font>**  比如 100:0 放着当前用户的名字和ID，直接jmp或者mov取出来不就行了？不就在那块内存放着，我直接取出来不就行了？很显然，这样是不安全的，是不被操作系统允许的，**你怎么能随意访问操作系统所占据的内存呢？**

- **<font color='red'>你既然说不能跳进操作系统使用的内存，那为什么不能直接访问，这是如何实现的？</font>**

  - 内核态，用户态
  - 这种机制是通过一种处理器“硬件设计”，也只有硬件才能做到
  - 特权级（Privilege Levels）：OS用于控制不同级别的访问权限
  - 具体体现在：如果你要访问访问/跳到一段内存，会比较特权级！如果当前特权级CPL > 目标特权级DPL，才允许访问
  - ![image-20241225222104475](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241225222104475.png)

- **<font color='red'>如何才能进入内核？</font>**   表面是系统函数的调用，实际上是中断指令int !  (至少x86是这样的)

- **系统函数调用的核心：**   系统函数实际上展开，就是一段包含int指令的代码。而int指令才会真正进入操作系统内核，根据中断类型查询IDT（中断描述符表）,找出对应的程序入口，取指执行，执行完毕再跳回去，返回。

  

- **我们以 ptintf()为例子**
  - 第一，我们在应用程序中调用 printf("xx",xx);
  - 第二，printf又会调用C库函数printf(...),主要作用就是将参数转换为系统调用需要的参数
  - 第三，调用另一个库函数write,这个write展开就是包含int 0x80指令的代码  【这里的详细细节我们就省略了】
  - 第四，真正调用write()，这个write真正将东西取出来并写入显存，让你看见
  - ![image-20241225223205047](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241225223205047.png)

​	



# 二. 多进程





## 1. CPU管理

**<font color='blue'>通过研究CPU的计算与IO，引出进程！</font>**



**多进程的思想是管理CPU引出的，我们首先来看看<font color='red'>CPU是如何工作的，以及OS是如何管理CPU</font>**



- CPU如何工作？

  - ```
    不停地取指执行 取指执行 ...
    ```

- OS是如何管理CPU的？

  - ```
    最简单直接的方法就是，我们只需要设置好 PC的初值，然后CPU自己不停地取指执行即可
    ```

- 这样会有什么问题？

  - ```
    这样如何解决之前的问题：IO比较慢，在进行IO的时候让OS也同时执行其他比如计算之类的任务
    比如：我们在进行计算的时候，遇到一条IO，需要等一段时间，难道CPU光傻傻地等吗？显然CPU会利用这段时间去跳到别的地方执行程序
    ```

- **<font color='red'>并发</font>**

  - **并发的实质：CPU执行多道程序，交替执行**

  - ```
    多道程序，交替执行！
    提高CPU的利用率！让CPU忙碌起来！
    ```

- 如何实现并发？

  - ```
    修改寄存器PC,让其在等待时间去执行其他程序，那边等待就再取执行其他程序，以此反复
    ```

- 只需要修改PC就可以了吗？

  - 肯定不可以啊！切换进程，执行另外一个程序的时候，ax等等寄存器的值很有可能修改了！我们需要保存切换前那一刻的样子
  - 注意我这里的样子，是非常非常笼统的模糊的说法  ! 
  - **需要保存现场!**  :  比如通过堆栈保存现场，弹栈恢复现场。

- **<font color='blue'>进程</font>**

  - 注意我上面说的样子，这是一个很重要的概念，我们需要用一个词语去刻画这个概念，而这就是进程！
  - ![image-20241228222436579](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241228222436579.png)

- **现在我们来回答，OS是如何管理   <font color='red'>  好   </font>CPU的？**
  - 操作系统需要启动多个进程，CPU交替执行多个进程，CPU的利用率就提高了！
  
- **<font color='red'>误区： 我之前都搞混了！</font>**
  - **<font color='blue'>多进程 与 多线程</font>**
    - 概念：
      - **进程** 是操作系统执行管理的基本单位，拥有独立的资源，适用于任务之间需要较强隔离的场景。
      - **线程** 是执行的基本单位，线程之间共享进程资源，适用于任务之间需要共享数据和高效通信的场景。
    - 关系：
      -  **一个线程只能属于一个进程，而一个进程可以有多个线程**，但至少有一个线程。**线程依赖于进程而存在。**
      - 操作系统通过进程来管理执行中的程序。每个进程至少包含一个线程，通常称为主线程。
    - 异同：
      - 每一个进程都有独立的地址空间、代码、数据和资源； 每一个线程都使用同一块地址空间、代码、数据和资源
      - 进程切换的开销比较大；线程切换时仅需保存和恢复寄存器、栈等信息
    - **<font color='red'>线程的本质</font>**
      - **线程的本质就是解决一个问题：我们如何在一个进程中，从这里跳到别处执行，实现一个进程内也能切来切去，可能寄存器要变化，但是内存映射表不用变！这样切换的代价就小很多！**  说白了就是PC指针变但是映射表不变！
      - **线程既保留了并发的优点，又避免了进程切换那么大的代价**
  - **<font color='blue'>并发 与 并行</font>**
    - 并发：比如CPU执行多个程序，看起来是同时执行，其实是交替执行！哪个不 用等就执行哪个
    - 并行： 真正的同时执行！并行通常发生在具有多个 CPU 核心或多个处理单元的计算机上。在并行处理中，多个任务在同一时刻被同时执行，每个任务都在自己的处理器上独立运行。



## 2. 多进程图像

**<font color='red'>本节主要是引出问题，后面我们将围绕下面的问题，进入代码来深入学习</font>**

- **OS如何组织多个进程？**
  - 就是根据PCB，根据状态，放在不同的队列，放在不同的位置
- **OS如何完成进程的切换？**
  - 调度
- **多进程如何分配各自的内存？**
  - 通过内存映射表，实现每个进程都有独立的资源 ! 
  - <img src="C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20241229151646724.png" alt="image-20241229151646724" style="zoom: 33%;" />

- **多进程之间的合作**
  - 要有进程的同步与合作



## 3. 用户级线程



### ① 引出多线程

- ​	1.CPU管理中，我详细讲解了进程与线程之间的区别，简单来说，切换线程就是不需要切换映射表的切换进程,so我们先看指令是如何切换，再看映射表怎么切换，两者合并，再加一点点细节就是进程的切换 ! 
- **多个执行序列（即多个线程）+ 一个地址空间是否实用？**
  - 比如此处一个网页浏览器的加载，文字、图片、动画的加载不是一次性，是通过多个线程来依次加载。
  - 为什么不用进程来加载？因为进程切换开销大！其次，进程的资源不共享，映射表不一样，所有的文本和图片都要显示在一个屏幕上，这样写入显存的时候，还要去不同的进程中copy，太麻烦了，线程则非常轻量级，且资源共享。
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229191652016.png" alt="image-20241229191652016" style="zoom: 33%;" />



- 如下图，刚开始我们通过TthraedCreate函数创建，通过Yield函数来回切换
- 也就是说，搞明白create和yield函数，我们就搞明白了线程级别的切换！
  - ![image-20241229192210194](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229192210194.png)





### ② 两个执行序列与一个栈

- **问题的产生：**:仔细分析下面的图，显然如果两个线程共用一个栈，会导致乱套，导致一个线程函数执行完,正常返回的时候直接跳到其他线程了。注意，在没有使用yiled的情况下，我们执行完函数后，返回的时候，由于使用同一个栈导致乱套了！
- **问题的理论解决：**   两个执行序列使用两个栈！
- **如何实现两个栈？：** 首先，什么时候需要切换栈？当然是切换线程的时候了，也就是调用yield的时候，在这个函数内部会切换栈
- **如何切换栈？代码说话！**： 看③
  - ![image-20241229192850473](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229192850473.png)



### ③ 两个执行序列与两个栈

**<font color='red'>代码的结构美！  通过 yield函数的右花括号 }，即可完美实现 线程的切换！</font>**

- 注意看，**问题并没有得到完美的解决**，因为两个栈虽然解决了不同线程间的乱跳，但是会导致一个线程内部的乱跳
- **为什么会在一个线程内部乱跳呢**？因为调用yield的时候把204压栈，如果将yield的jmp 204的204使用栈里的204不就完美解决了！！
- **如何使用栈的204，切回去？** ： 很简单，当使用yield，此时修改esp，再通过 } 也就是汇编中的ret ，弹栈即可！
  - 名词解释：**<font color='blue'>TCB</font>**：**Task Control Block**，任务控制块。是操作系统中用于管理和调度任务（或进程）的数据结构。它包含了与任务相关的所有必要信息，用于操作系统对任务的管理、调度和上下文切换。每个正在执行的任务（进程或线程）都有一个对应的 TCB。
  - 名词解释：**<font color='blue'> ESP</font> (Execution Stack Pointer)**, 是**堆栈指针寄存器**（**Stack Pointer**）的缩写，通常指向当前函数调用中栈的顶部。
  - ![image-20241229195856281](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229195856281.png)



### ④ yield

- **yield真的很简单  !  **  
  - 注意 x1是当前线程， x2是要切进去的线程
  - 最最核心的代码其实就是下面的形式，真实代码肯定比这复杂，但最核心的思想就是这么简单！
  - 切进去的yield:    { TCBx1.esp = esp;   esp = TCBx2.esp }
  - 切回去的yield:    { TCBx2.esp = esp;   esp = TCBx1.esp }



### ⑤ThreadCreate

- **前面说的create ,就是这个threadCreate**
- 其核心：就是用程序做出这三样东西   （哪三样？一个栈，一个TCB和栈关联，栈里面放着返回的地址）
- ![image-20241229201630551](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229201630551.png)



### ⑥why用户态

- **为什么说上面几节知识都是用户态？**
  - 还是网站加载为例子，连接URL发起请求，等待网卡IO，如果很卡的情况下，在内核态不就卡住了吗？即使用户态有很多线程，但是也没用啊，全都卡主了。
  - 在等待网卡IO的时间，会切换到别的进程，执行其他程序,  而这个切换才是内核态的切换，实际上用户态切换是它的子部分
  - ![image-20241229202511870](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229202511870.png)

​	

### ⑦ 预告

- 在用户态，线程的切换，调用的方法是yield ;  在内核态，进程的切换，调用的是schedule

![image-20241229202908090](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241229202908090.png)







































# 八个实验



## 一、操作系统的引导





































































































































































































