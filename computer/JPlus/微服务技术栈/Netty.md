# NIO基础

**<font color='red'>以前的IO是面向流的【尽管也有buffer缓存】，而NIO是面向缓存，且可以做到异步操作</font>**

## 1.三大组件

### ① Channel

//IO流的各种Stream都是单向的，而channel是双向的，通过**RandomRandomAccessFile 既可以输入也可以输出**

//**最关键的就是channel底层会使用零拷贝，性能有不错的提升！！！！！**



### ② Buffer

比较常用的就是下面要介绍的ByteBuffer



### ③Selector

**<font color='red'>文件编程中依然是阻塞的【未使用Selector】，在网络编程才会使用</font>**

- 传统设计的弊端
  - 多线程：内存占用高吃CPU，线程切换成本高，只适合连接数少的场景
  - 线程池：阻塞模式下，线程池一次只能处理一个socket连接,若单个连接占用时间长导致利用率低，只适合短连接的场景
- Selector的优点
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241019130620592.png" alt="image-20241019130620592" style="zoom:50%;" />





## 2.ByteBuffer



### ① 结构

- 从ByteBuffer的结构我们可以直观地认识到，为什么需要切换到读模式才能正确读取数据，实际上就是移动指针到正确位置
- <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241019153424665.png" alt="image-20241019153424665" style="zoom: 45%;" />





### ② 常见API





- **创建分配空间**

  - ```
    BufferByte buf = BufferByte.allocate(16)
    ```

- **翻动！我自认为叫翻动模式**

  - 实际上就是将position指针移到0，limit移到数据尾端

    ```
    buf.flip(); 
    ```

- **从channel中读取数据，向buffer写入数据**

  - 1.调用channel的read方法 

    ```
    int readBytes = channel.raed(buf);
    ```

  - 2.调用buffer自己的put方法

  - ```
    buf.put((byte)127)
    ```

- **从buffer中读数据,向channel写入数据**

  - 1.channel的write

    ```
    int writeBytes = channel.write(buf);
    ```

  - 2.buffer自己的get方法

    ```
    byte b = buf.get(new byte[4]);
    ```

- **检查是否有剩余数据**

  - ```
    while(buf.hasRemaining()){...}
    ```

- **limit**

  - ```
    buf.limit();  //获取limit指针的索引,也就是获取buf的长度-1
    ```

- **清除**

  - ```
    buf.clear()//会重置指针，让一切回到最开始
    ```

  - ```
    buf.compact()//也会重置指针，但会将剩余没读完的数据保存，position指在当前数据的下一个位置
    ```

- **重置与标记**

  - get方法会让position读向后走，如果想重复读取数据，可以调用rewind()将position重置为零

    或者调用get(int i)方法获取索引i的内容，它不会移动读指针

  - mark()方法会记录当前的position位置，reset()方法会回到mark标记位置





- **字符串转bytebuffer**
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241019155732848.png" alt="image-20241019155732848" style="zoom: 67%;" />





## 3.文件编程

### ① FileChannel

**<font color='red'>FileChannel只能工作在阻塞模式下,只有和网络编程相关的才会使用到Selector</font>**

- **获取FileChannel**：必须通过FileInputStream，FileOutputStream,RandomAccessFile获取FileChannel,它们都有getChannel方法
  
  - 注意FileInputStream和FileOutputStream只能单向写or读
  - RandomAccessFile是否能读写根据构造RandomAccessFile的**读写模式**决定
  - `RandomAccessFile` 是 Java 中一个用于随机访问文件的类，允许你在文件中的任意位置读写数据。这使得处理文件分片和合并变得更加高效，尤其是在需要随机读取或写入数据的场景下。
  
- **读取数据**

  - 会从channel中读取数据填充ByteBuffer,返回值表示读到了多少字节，-1表示到了文件末尾

  - ```
    int readBytes = channel.read(buffer); 
    ```

- **写入数据**

  - ```
    channel.write(buffer)
    ```
  
- **channel之间传输数据**

  - 底层利用操作系统的**零拷贝**进行优化，比传统的读写效率要高很多！**<font color='red'>建议以后直接transferTo简单又高效</font>**

  - channel1 给 channel2 传输数据

    ```
    FileChannel channel1 = new FileInputStream("from.txt").getChannel;
    FileChannel channel2 = new FileOutputStream("to.txt").getChannel;
    channel1.transferTo(0,channel1.size(),channel2)
    //起始位置0，大小为channel1的大小，传输对象为channel2
    ```

- **关闭**

  - ```
    channel.close() 或者 生成channel的流的close
    ```

- **一些无关紧要的API**

  - ```
    channel.position();//获取当前位置
    channel.position(long 新位置);//设置新位置
    channel.size()//获取文件大小
    ```

    

### ② Path







### ③ Files













## 4.网络编程

























































































































































































































































































































