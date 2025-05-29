

# P;目的



- 阅读本书的目的
  - 深入内核，阅读源码，提高自己对MySQL及INNODB引擎的理解
  - 书中有一些基础知识，用来补全操作系统等其他方面的不足之处
- 对于源码，浅尝辄止，不追求太深入，辅助理解某些知识点，也没有进行断点调试，因为vscode2003没找到版本
- 前五章简单看一下就Ok了，重点是第六章开始的内容！













# 一、share



## 1. 语言差异



- **内联函数**

  - C语言中有内联函数的关键字，即不是函数跳转调用（压栈、跳转、返回），而是直接原地复制展开，适合短小函数，减少开销
  - **Java 有内联函数的机制**，只是由 **JVM 自动决定**，而不是程序员手动控制。由JIT即时编译器对代码进行优化，就包括函数内联

- **volatitle**

  - 让系统总是从该变量所在的内存处获取数据，保证数据一定是最新的。

- **值传递**

  - C系语言方法只有值传递，但可以通过传一级指针，然后通过一级指针获取对应的值，做到真正的修改。
    引用类型也可以通过二级指针做到修改，**即使引用类型，也可以通过修改指针，达到真正修改！【java做不到】**

    - ```
      通过单向链表删除目标元素，举一个二级指针的例子
      正常思路：需要区分是不是第一个节点和其他节点
      ListNode *find_and_delete(ListNode *head,int target)
      {
          ListNode *pre = NULL;
          ListNode *entry;
      
          for (entry = head; entry != NULL; entry = entry->next) 
          {
              if (entry->data == target)
              {
                  /* 判断删除的结点是否是第一个结点*/
                  if (entry == head) 
                      head = entry->next;
                  else
                      pre->next = entry->next;
      
                  free(entry);
                  break;
              }
              pre = entry;
          }
          return head;
      }
      二级指针思路：不需要考虑是不是第一个节点了
      void find_and_delete2(ListNode **head,int target)
      {
          for (; *head != NULL; head = &(*head)->next)
          {
              if ((*head)->data == target)
              {
                  (*head) = (*head)->next;
                  break;
              }   
          }   
      }
      ```

  - java中只有值传递，基本类型只修改副本，引用可以修改部分，但是修改整个引用不行

    【比如我要实现将数组[3]的地址换成数组[4]的地址，这样利用二级指针实现删除数组[3]的值，java做不到！】





## 2. 盲点



- mutex与读写锁
  - mutex就是互斥锁，不分读写，只能一个线程有
  - 读写锁，区分读写，按理说可以直接替代mutex，但是实际上读写锁适用于读多写少的情况。





































# 二、内存管理·算法

// 本章介绍InnoDB存储引擎的内存管理系统实现，基本数据结构



## 1.内存管理系统



### ① 需要注意

P8





### ② 内存分配



- <font color='blue'>InnoDB到底是如何管理内存的？</font>

```
答：InnoDB存储引擎没有直接使用系统提供的malloc和free方法。
	on the Solaris + GCCsystem（50 MHz Sparc,1993） the pair takes 3 microseconds,
	on Win NT + 100MHz Pentium, 2.5 microseconds.
	基于上述原因，InnoDB选择采用内存堆（memory heap）一次性获取大块的内存，之后的内存分配在InnoDB内部进行，
	减少了调用系统API的开销，同时增加了拓展性。
	此外，InnoDB还允许从缓冲池分配内存建立内存堆，这样可以更快速请求整个内存页(16KB)。
```

- **缓冲池分配**
  - InnoDB允许从缓冲池中分配内存，建立内存堆，可以更快速请求整个内存页(16kb)
- **动态分配**
  - 从操作系统中分配内存





- **层次结构**
  - 最顶层为一系列各种用途的**内存堆对象**
  - 中间是**通用内存池、缓冲池**。
  - 最下层是系统内存，也是InnoDB内存空间的最终来源
  - ![img](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/37af6024115359ac76a53ba9b994712b_720.jpg)







### ③ 内存堆

<font color='blue'>**内存堆，InnoDB最基本也是最重要的内存管理对象**</font>

- what？
  - **从概念上看**，内存堆 = 一个栈stack。 
    通过不断增加内存块对象来增长空间，如果要释放内存堆中某个内存块，只能从栈顶开始释放，或者全部释放，这可不就是栈
  - **从本质上看**，内存堆 = 一系列连续的内存块
    每个内存块头部都包含mem_block_info_t用来存储元数据信息

- 类型划分
  - 你简单了解一下，知道有三种类型就可以了，比如从缓冲池获取的内存堆，操作系统获取的内存堆等



### ④ 通用内存池

```
InnoDB存储引擎启动后，内存实例会有一个mem_comm_pool对象，即通用内存池
通过调用函数mem_pool_create创建，大小通过参数innodb_additionnal_mem_pool进行定义
通用内存池服务于前面介绍的内存堆对象，主要进行小块内存的分配，通常用于分配InnoDB内存数据结构对象
```







### ⑤ 伙伴系统

```
buddy system, 伙伴系统分配
与linux内核一样采用伙伴系统用来解决频繁申请内存，导致的内存碎片化问题
```







## 2. 数据结构·算法









# 三、同步机制





## 1. 基础知识



```
InnoDB没有直接使用操作系统自带的mutex和rw-lock(读写锁)，而是自己进行了封装。
并通过spin(自旋)以及wait array(等待队列)的设计提高了性能
```

**<font color='green'>便于后续理解，在基础知识小节中会对一些概念进行解释</font>**

### ① mutex对象

- **mutex对象**
  - mutex对象是进行Mutual Exclusio(互斥)操作，目的是多线程并发情况下保证共享数据的准确性
  - 在linux系统下，可以通过 spin lock , semephore , monitor , sequencer 进行互斥操作
  - InnoDB自己封装了mutex数据结构，与linux的spin lock类似，但是多了一些功能的扩充和优化









### ② 内存模型

- <font color='red'>**注意**：后面提到的内存模型，特指一致性内存模型</font>
  - 一致性内存模型，例如sequential/total/partial store memmory model，都是指硬件/语言层次的内存模型
  - 操作系统/内核内存模型，例如Linux的 Flat/discontiguours/sparse memory model，都是操作系统层次的内存模型

```
memory model , 即内存模型，决定了CPU怎样访问内存，以及并发情况下各CPU之间的影响。
```



### ③ 临界区/资源



- 临界区 （critical section)

  - ```
    每个进程访问临界资源的那段代码就叫临界区
    ```

- 临界资源 （critical resource）

  - ```
    临界资源就是一次仅允许一个进程使用的共享资源。各线程通过互斥的方法实现临界资源
    属于临界资源的软件：消息队列，数组，变量，缓冲区等
    属于临界资源的硬件：打印机，磁带机等
    ```

    

### ④ 原子操作



- **atomic read-modify-write operation**

  - 概念：

    ```
    atomic read-modify-write operation，即允许一个CPU读取一个值，修改它，最后写回到内存的三个操作作为一个原子总线操作
    ```

  - 具体实现：

    ```
    该操作在CPU里面有一个专门利用硬件实现的指令,具体为test-and-set指令，即TAS指令，每个操作系统具体实现标准不同
    【这不就是CAS那块常说的利用硬件实现的原子性操作吗】
    ```

  - 作用：

    ```
    一旦CPU执行TAS指令，其他任何CPU和I/O设备都无法使用总线，目的是为了保证同一时刻只允许一个CPU执行临界区
    ```

    

### ⑤ spin lock



- ```
  在TAS操作的基础上，可以实现很多互斥的数据结构。而spin lock就是最简单也是应用最广泛的一种互斥结构。
  spin lock专门用来锁 sort-term cirtical section，不适合过大的临界区
  ```

- 代码实现：

```c
// 初始化spin lock
type int lock_k
void
initlock(volatitle lock_t *lock_status){
    *lock_status = 0;
}
// 使用TAS对一个spinlock对象上锁
void 
lock(volatitle lock_t* lock_status){
    while(test_and_set(lock_status) == 1)
        ;
}
// 释放锁
void
unlock(volatitle lock_t* lock_status){
    *lock_status = 0;
}
```











## 2.InnoDB的同步

```
InnoDB存储引擎没有直接使用操作系统的latch数据结构，而是自己封装并对其优化。
有两种同步机制：1、mutex，完全互斥的互斥操作
			 2、rw-lock，读写互斥，可以给临界资源加上s-latch（允许并发的读取操作） or x-latch（完全的互斥操作）
```







### ① mutex

- mutex_struct

  - ```
    前面我们提到了mutex对象，InnoDB自己实现了mutex对象，即mutex_struct
    和linux里面的spin lock类似，都是基于TAS操作实现的
    ```

- 核心区别：自旋

  - ```
    InnoDB实现的mutex对象有个显著改变，就是自旋操作。
    当tas操作返回的是1，那么会进行自旋操作，所谓的自旋操作就是让CPU短暂的等待一小会，然后再次执行tas操作，看看可以获取Mutex了吗。
    当tas操作返回1，首先进行自旋，而不是反复多次执行tas操作是有意义的。因为自旋时，判断lock_word的值是通过访问CPU的L1 cache和L2 cache得到的。减少对内存的访问，从而减少总线宽带的使用，
    ```

    

### ② rw-lock

- rw-lock

  - ```
    读写锁，也称为latch。 
    允许多个线程读，但是写操作只能一个线程使用。
    ```

- InnoDB也自己封装了rw-lock，并采用**FIFO的调度策略**

  - ```
    比如有一个临界资源object，第一次是读操作，即s-latch，第二次也是读操作，s-latch都没问题
    但第三次是写操作，即x-latch，如果前两次的s-latc没释放则x-latch需要等待
    这是FIFO的调度策略
    ```

    

### ③ 等待队列

比较简单，就是常见的等待队列





### ④ 死锁检测

```
InnoDB提供了死锁检测的机制，只有开启宏UNIV_SYNC_DEBUG才会进行死锁检测，其实正常情况下latch一般没有这个机制。
实现原理就是定义了锁的优先级，这样锁会按照顺序执行，不会出现AB-BA这种死锁情况。
```





# 四、重做日志







## 1. 相关概念





### ① redo log

```
重做日志，即redo log，用来实现事务的持久性。
由两个部分组成，redo log buffer(重做日志缓存)和redo log file(重做日志文件)
```



### ② 流程

```
1.当事务commit的时候，会先将redo log buffer中的日志写入到重做日志文件，进行持久化，持久化之后commit操作才算完成。
2.为了保证日志缓存一定写入到日志文件，需要InnoDB调用一次fsync操作。没有fsync重做日志->文件系统缓存->重做日志文件
  要是没有fsync操作，多了一步文件系统缓存，否则系统宕机，数据会丢失的
  【fsync是一个system call，可以强制将文件的所有修改（包括数据和元数据）从操作系统的缓存写入磁盘，确保持久化。】
3.参数innodb_flush_log_at_trx_commit可以控制刷盘策略。
	0：不要求一定要写入到重做日志文件，这样会失去持久性，但是效率大幅度提高，本来五十万数据插入要2分钟，设置0只需十来秒
	1：默认。强制要求写入重做日志文件。
	2：不强制使用fsync,会将日志保存在系统的文件缓存中，这样mysql宕机不会丢数据，但系统宕机会丢失，插入五十万数据，要二十多秒
	【一般情况还是要开启的，因为保证事务，很关键！！！！！】
4.redo log file在磁盘中是顺序写入的
5.innoDB引擎在启动时，无论上次正常关闭与否，都会先尝试进行恢复操作！
```



### ③ 日志类型



- **不同的数据库类型，使用的日志类型不同**
  - mysql innodb引擎：物理逻辑日志
  - oracle：redo log（物理） ， undo log（逻辑），组合使用

- **物理日志**

  - ```
    保存的是页中发生变化的字节。
    这样重复多次执行该日志都不会导致问题，日志是幂等的
    ```

  - 优缺点：日志产生的量比较大，但是恢复数据比较快

- **逻辑日志**

  - ```
    记录的是对于表的操作。
    比如插入操作：<insert op,table name,recird value>
    ```

  - 优缺点：恢复数据比较慢，但是占用空间小

- **物理逻辑日志**

  - ```
    对页是物理的，页内部的操作是逻辑的，
    例如对于页进行重新整理的操作，只需要记录页的编号以及日志类型
    ```

    



### ④ 归档日志

```
InnoDB中，重做日志的大小是固定的，满了之后，旧日志会被新日志覆盖。
而归档日志就是InnoDB设计用来记录重做日志的。
```





## 2. 物理存储结构



### ① 日志结构



- **redo log group**：重做日志组
- **redo log file 1/2/3**：每个组包含多个重做日志文件，且内容都是一样的，是镜像关系
- **archive redo log**：归档日志

```
但是实际上只有一个redo log group，没有组的镜像，因为官方强制设置为1，关闭了日志组的镜像！
```

![img](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/f1744e68876264a2a3d4b77d19ab0125_720.jpg)





# 五、mini-transaction



## 1.介绍





- **什么是mini-transaction？**

  - ```
    mini-transaction模块，是InnoDB中的一个模块，专门用来实现物理逻辑日志的写入。
    第四章我们介绍了重做日志，但如何实现日志从redo log buffer -> redo log file并保证并发/异常情况下的页中数据一致性，
    就是mini-tranaction模块要做的事情。
    ```

- **与事务的区别**

  - ```
    mini-transaction仅仅保证了页的一致性
    正常的事务应该保证的是多个页操作数据的一致性和持久性，或者说正常事务的一致性与持久性的保证就是mini-transaction
    总结，mini-transaction是正常事务的一部分
    ```

- **三个协议**

  - ```
    为了保证mini-transaction，需要实现三种协议
    The FIX Rules
    Write-Ahead Log (WAL)
    Force-log-at-commit
    ```

    



## 2.三种协议



- **The FIX Rules**

  - ```
    修改一个页需要获得x-latch
    访问一个页需要获得r-latch or x-latch
    直到页操作完毕，释放对应latch
    ```

  - ```
    InnoDB对该协议进行了部分修改。
    todo // 在第十一章会有详细的例子
    ```

- **Write-Ahead Log（WAL）**

  - ```
    专业来说，页操作在写入持久存储设备之前，首先要将内存中的日志写入到持久设备
    [对于InnoDB,页的持久存储设备就是表空间；内存中的日志就是redo log buffer；持久设备自然是redo log file]
    简单来说，就是页操作在写入到表空间之前，首先要将redo log buffer中的日志写入到redo log file
    ```

- **Force-log-at-commit**

  - ```
    WAL规则要求先写日志后写页，但这不能保证数据的持久性。还需要Force-log-at-commit一起配合保证持久性。
    Force-log-at-commit： 要求一个事务被提交后，所有mini-transaction产生的日志都要刷新到redo log file
    ```

    

## 3. 全流程



- 结合第四章，重做日志的整个写入流程如下
  - ![img](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/047eabc082adf746cafede050fbd0f92_720.jpg)











# 六、存储管理



## 1. 物理存储

```
InnoDB存储引擎，没有直接使用OS的file system,而是在文件系统之上封装了自己对于存储设备的管理。
对于InnoDB，最小的存储单位是“页”，大小16KB。在页的基础上又划分了区(extent),段(segment)和表空间(tablespace)
```

- **页，文件系统的块、扇区之间的关系**
  - 页，就是InnoDB存储引擎的最小单位，大小：16KB，由file system的块构成。
  - 文件系统的块，机械硬盘512字节/固态硬盘4KB。
  - 文件系统的扇区，一般为4KB，扇区以0/1二进制方式存储数据，扇区被file system映射成块，方便file system 管理。
  - 其次，InnoDB一次性申请空间，是以区的方式，区的大小为1MB，总共64个页。

### ① 页

- 页，是InnoDB存储引擎访问的最小I/O单元，大小16KB。
- 页的头部存储表空间ID，表空间的偏移量，页类型等信息数据，尾部存储一个字段用来检验页完整性，剩下的部分存储真正的数据





### ② 区

- 区，是InnoDB存储引擎访问的最小单位，是申请空间最小单位，大小1MB，一个区有64个页。
- 区，由64个页构成，通过表空间的space header(空间头部)管理区的分配、管理。
             64个页是否全部使用，通过区描述符来控制，若一个区的页有区描述符，则为碎片区，不能分配给段。



### ③ 段

- 段，最多由32个页+若干个区组成。
- 段，用来保存特定对象的
  - 对于InnoDB，一张表就是最为常见的对象，所以段最经常用来保存一张表！
  - 同时，todo p82
- 段，是页+区混合组成的。
  - 刚开始的数据先保存在32个页中，如果页已经满了，就开始以区为单位申请空间。
  - 有的表或者对象很小，页为单位就够用了。有的却超过32个页，那么这张表的数据肯定不少，所以改用区为单位申请空间，
  - 这样保证空间使用率也兼顾空间分配率，节约空间，从你我做起。





### ④ 表空间

- 表空间，是一个逻辑概念，由页+区+段构成。表空间可以由多个文件组成。
- 表空间的组成。
  - space header, 前面提到过，仅存在于页(0,0)，固定112字节，用来保存区，段，已经使用的空间等信息，实际就是表空间的信息







# 七、记录



## 1. 概述



- **面向行**

  - ```
    InnoDB存储引擎是面向行的存储引擎，其他的例如sql server, oracle是可以自主选择面向行/列
    ```

  - ```
    行，通常可以理解为一条记录。多条记录就组成了一张表。
    ```

  - ```
    面向行的好处：
    		1.符合传统机械硬盘的访问方式
    		2.记录存放在一个页中，存储一条距离需要访问的页面较少
    		3.易于理解，数据的存取就像是对一张二维表进行访问。
    ```

    

- **物理记录**

  - ```
    物理记录，就是真实存在于磁盘中的一行数据，但是这里的数据是二进制字符串形式
    ```

- **逻辑记录**

  - ```
    逻辑记录，是物理记录在内存的表现形式，将二进制转化成可读数据，实际上不占用物理存储空间
    ```

- **记录之间的转换**

  - ```
    举一个例子你就明白了，当我们插入一条数据，此时该数据首先在内存创建逻辑记录，然后保存到外存，形成物理记录，之后才能进行各种数据库操作。
    同样的，物理记录从外存取出直接给用户，用户是看不懂的，需要将其转换成逻辑记录才行。
    ```

- **三个隐藏列**

  - 如果创建表没有指定主键索引，会自动生成一个隐藏列，作为主键索引
  - 回滚指针，实现MVCC的
  - 事务ID，判断当前记录对其他事务是否可见，实现事务隔离性以及MVCC





## 2.伪记录



- ```
  索引页存在伪记录，即Infimum记录和Supremum记录，这两个就是最小记录和最大记录，表示开头和结尾,起到“边界”作用
  Infimum | 行记录数据 | 行记录数据|.....|Supremum
  ```

  



## 3. 两者的比较



- 插入操作：插入操作由于物理记录不存在，先构造逻辑记录，将其保存成物理记录。
- 其他操作：查询，更新，删除，都需要SELECT定位物理记录，然后转化成逻辑记录。





## 4. 页中记录存储





- 页中记录的存储张什么样子
  - 下面的图片是理论上物理记录在索引页中的样子，这个顺序是按照主键顺序逻辑排序，实际上物理位置可能是乱序的。
  - ![image-20250525191504706](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20250525191504706.png)









# 八、索引页





## 1. 存储结构



### ① Page Header

- Page Header保存了页中关于记录的存储信息

- ```
  当记录被删除时，page free会指向最近删除的记录空间，根据记录record header中的next record串联成一个根据删除记录得到的空闲空间链表。
  当有新记录申请页内可以空间时，首先判断page free指向的最近删除记录空间的大小是否满足，如果满足则使用，反之从page_heap_top
  （堆中空闲空间的位置(偏移量)）指向的空闲空间进行分配。
  ```



### ② Page Directory

- Page Directory用于记录的查询操作。B+树查询记录只能查询记录所在的页，要在该页中找到具体的记录需要page directory
- 可以简单理解为page directory就是一个数据结构，通过page directory中的槽，利用二分查找快速定位记录。





### ③ Page Cursor

- page cursor就是索引页的游标，简单来说就是一个用来指向记录所在位置的游标
- page cursor通过查询模式，进行顺序扫描，定位游标
- page cursor最重要的作用就是可以直接定位到一个记录，比如row id>=3 就会直接定位到row id=3的记录





## 2. 插入记录

先通过page cursor定位到记录，再通过插入记录







## 3. 删除记录

先通过page cursor定位到记录，再删除记录







# 九、锁



## 1. 隔离级别



- ISO和ANSI SQL标准规定了四个事务隔离级别
  - READ UNCOMMITED
  - READ COMMITTED
  - REPEATABLE READ
  - SERIALIZABLE
- 但实际上，数据库设计师处于性能的考虑，没有完全遵守这些规则，比如oracle只有read committed和 serializable
- 尽管InnoDB存储引擎默认隔离级别是REPEATABLE READ,但已经在该隔离级别下，通过next-key locking算法解决了幻读。
- 理论上，隔离级别越低事务请求的锁越少或者持有锁时间越短，性能越高，所以大多数人都会质疑SERIALIZABLE隔离级别带来的
  性能问题，但根据Jim Gray在Transaction Processing : Concepts and Techniques一书指出，两者开销几乎一致，甚至S的性能更优
  因此InnoDB选择REPEATABLE READ作为默认隔离级别，相对于其他数据库默认READ COMMITED,性能不会有什么损失。
- **幻读：**  同一事务，执行同一条sql语句的结果不一样。比如select得到的结果集，前后两次不一致
- **next-key locking算法**： 
  - 为了解决幻读，一种名为“谓词锁”的方法出现了，即锁住的不是单个记录而是一个范围。
  - 谓词锁有性能问题，改进后形成了key-range locking算法，根据锁的边界不同，又可以分为next-key locking和previous-key locking算法。
  - 例如，若有记录W,Y,Z根据next-key locking算法，则有(-无穷,W],(W,Y]，(Y,Z],(Z,+无穷)
    如果插入一条数据X，会锁住(W,Y]这个范围，插入后则有(-无穷,W],(W,X]，(X,Y],(Y,Z],(Z,+无穷), 





## 2.InnoDB中的锁



### ① 锁类型



- InnoDB存储引擎实现了两种标准锁，共享锁（S Lock）和排他锁（X Lock）
  - 共享锁：允许事务读一行数据
  - 排他锁：允许事务更新/删除一行数据
- InnoDB存储引擎，允许多粒度锁定，即允许在行记录级和表记录级同时加锁。同时为了更好的支持不同粒度上加锁操作，
  InnoDB存储引擎还提供了“意向锁”。
- **意向锁**：InnoDB存储引擎中的意向锁设计比较简练，就是表级别的锁。
  - 意向共享锁 IS LOCK：事务想要获取表中某几行的共享锁
  - 意向排他锁 IX LOCK：事务需要获取表中某几行的排他锁
- 锁的兼容性
  - IS和IX兼容的原因，就是获取表中的行不一样，所以是兼容的。
  - IS和X不兼容的原因，因为S和X是行级锁，所以这里IS和X肯定指的是同一行数据，就变成了S和X的关系了

|        | **IS** | **IX** | **S**  | **X**  |
| ------ | ------ | ------ | ------ | ------ |
| **IS** | 兼容   | 兼容   | 兼容   | 不兼容 |
| **IX** | 兼容   | 兼容   | 不兼容 | 不兼容 |
| **S**  | 兼容   | 不兼容 | 兼容   | 不兼容 |
| **X**  | 不兼容 | 不兼容 | 不兼容 | 不兼容 |











### ② 锁的内部实现





- **行锁的数据结构**

  - ```
    struct lock_rec_struct{
    	ulint space;      // 表空间ID
    	ulint page_no;	  // 页号
    	ulint n_bits;     // 位图中的位数，默认预分配64个记录的位图信息，即8字节
    }				    	 假如该页有250条记录，即250+64=314，1+314/8=40字节，该页的位图分配40字节空间用来管理
    ```

  - 其实还隐含lock bitmap的信息，因为位图是根据页中记录数量动态分配空间，所以不需要显示地对其定义。也就是说其实n_bits就是这张lock bitmap本身。

  - **InnoDB中的锁，没有锁升级，而是通过位图的方式来记录锁的持有情况**

  - lock bitmap根据页中记录来进行判断是否持有锁，页中的记录与位图上的索引是一一对应的，通过0/1来判断

  - 开销很小，因为每个页都有一张位图来记录锁，而位图占比空间非常小，只需要01就可以判断！

- **表锁的数据结构**

  - ```
    typedef struct lock_table_struct lock_table_t;
    struct lock_table_struct{
    	dict_table_t* table;  // daatbase table in dictionary cache 字典缓存中的数据库表
    	UT_LIST_NODE_T(lock_t)locks;  // list locks on the same table
    }
    ```





- **锁的真模样**

  - ```
    // 上面的行锁，表锁的数据结构都是单独的定义，实际产生的锁是在事务中，因此每个事务都有一个锁结构，如下：
    struct lock_struck{
    	trx_t* trx;   // transaction owning the lock
    	UT_LIST_NODE_T(lock_t)trx_locks;
    	dict_index_t* index; // index for a record lock
    	.... 省略一些无关紧要的字段
    }
    ```

  - 数据结构lock_struct是根据每个事务的每个页(或者每张表)进行定义的。但一个事务可能在不同的页上也有多个行锁，涉及不同的页，记录信息肯定要比单独记录一个页复杂。而字段trx_locks就专门将一个事务里面所有锁信息进行链接，这样就可以快速查询一个事务中所有锁的信息。
    【简单来说，trx_locks是一个链表，包含该事务所有锁的信息。查询该链表，可专门统计即使是不同页下的所有锁信息】

  - 此外，除了查询事务所有的锁信息，还需要根据某一行记录获取对应的锁信息。
    InnoDB的做法：有一张全局的哈希表，首先通过行所在的页进行哈希查询，在根据查询得到的行锁lock_rec_t，扫描行锁中的lock bitmap，判断是否有锁。
    当然你要是已经有trx_t对象，可以直接根据对象中的trx_locks遍历获取锁

  - ```
    上述根据页来进行对行锁的查询看似是效率低下的操作，其实开销很小。
    如果每一个行锁我们都去记录，那么开销是很大的，会占用很大的内存空间。如果是这种情况，正常设计师认为当一个事务占用太多资源，
    这时会进行锁升级，将行锁升级为更粗粒度的锁，如页锁/表锁。
    但InnoDB通过页和位图的方式，锁资源的消耗非常小，因此不支持也不需要锁升级操作。
    例子：假如一张表3000000个数据页，每个页100条记录，若一条sql对全表更新，则需要对所有记录加X-lock，那就是300000000个行锁进行管理，即使每个锁占用10字节也要3G的内存，即使有锁升级机制优化，但锁升级本身也难免有额外开销，何况优化后仍要几千MB；
    但是采用位图的方式，只需要300MB即可，还不需要操心锁升级机制。
    ```

    



























































































































































































































































