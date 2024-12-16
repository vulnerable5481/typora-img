# NIO基础



## 1.三大组件

### 简介

```
NIO主要有三大核心部分：Channel(通道)，Buffer(缓冲区), Selector。传统IO基于字节流和字符流进行操作，而NIO基于Channel和Buffer(缓冲区)进行操作，数据总是从通道读取到缓冲区中，或者从缓冲区写入到通道中。Selector(选择区)用于监听多个通道的事件（比如：连接打开，数据到达）。因此，单个线程可以监听多个数据通道。

NIO和传统IO（一下简称IO）之间第一个最大的区别是，IO是面向流的，NIO是面向缓冲区的。 Java IO面向流意味着每次从流中读一个或多个字节，直至读取所有字节，它们没有被缓存在任何地方。此外，它不能前后移动流中的数据。如果需要前后移动从流中读取的数据，需要先将它缓存到一个缓冲区。NIO的缓冲导向方法略有不同。数据读取到一个它稍后处理的缓冲区，需要时可在缓冲区中前后移动。这就增加了处理过程中的灵活性。但是，还需要检查是否该缓冲区中包含所有您需要处理的数据。而且，需确保当更多的数据读入缓冲区时，不要覆盖缓冲区里尚未处理的数据。

IO的各种流是阻塞的。这意味着，当一个线程调用read() 或 write()时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。该线程在此期间不能再干任何事情了。 NIO的非阻塞模式，使一个线程从某通道发送请求读取数据，但是它仅能得到目前可用的数据，如果目前没有数据可用时，就什么都不会获取。而不是保持线程阻塞，所以直至数据变得可以读取之前，该线程可以继续做其他的事情。 非阻塞写也是如此。一个线程请求写入一些数据到某通道，但不需要等待它完全写入，这个线程同时可以去做别的事情。 线程通常将非阻塞IO的空闲时间用于在其它通道上执行IO操作，所以一个单独的线程现在可以管理多个输入和输出通道（channel）。
```



### ① Channel

- **简介**

```
Channel和IO中的Stream(流)是差不多一个等级的。只不过Stream是单向的，譬如：InputStream, OutputStream.而Channel是双向的，既可以用来进行读操作，又可以用来进行写操作。
```

NIO中的Channel的主要实现有：

- FileChannel   :  用于读取、写入、映射和操作文件的通道。
- DatagramChannel：   通过 UDP 读写网络中的数据通道。
- SocketChannel：         通过 TCP 读写网络中的数据。
- ServerSocketChannel： 可以监听新进来的 TCP 连接，对每一个新进来的连接都会创建一个 SocketChannel。



- 如下图所示，操作系统中：通道是一种通过执行通道程序管理 I/O 操作的控制器，它使主机（CPU 和内存）与 I/O 操作之间达到更高的并行程度。需要进行 I/O 操作时，CPU 只需启动通道，然后可以继续执行自身程序，通道则执行通道程序，管理与实现 I/O 操作。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b43216d1bbbe4c529d781f30fb3f9a2c~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp)



### ② Buffer

```
NIO中的关键Buffer实现有：ByteBuffer, CharBuffer, DoubleBuffer, FloatBuffer, IntBuffer, LongBuffer, ShortBuffer，分别对应基本数据类型: byte, char, double, float, int, long, short。当然NIO中还有MappedByteBuffer, HeapByteBuffer, DirectByteBuffer等这里先不进行陈述。
```



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



<img src="C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20241210125447644.png" alt="image-20241210125447644" style="zoom: 80%;" />

- **创建分配空间**

  - ```
    BufferByte buf = BufferByte.allocate(1024)
    BufferByte buf = BufferByte.allocateDirect(1024)
     * 非直接缓冲区：通过allocate()方法分配缓冲区，将缓冲区建立在JVM的内存中。
     *
     * 直接缓冲区：通过allocateDirect()方法分配直接缓冲区，将缓冲区建立在物理内存中。可以提高效率
     *          此方法返回的 缓冲区进行分配和取消分配所需成本通常高于非直接缓冲区 。
     *          直接缓冲区的内容可以驻留在常规的垃圾回收堆之外.
     *          将直接缓冲区主要分配给那些易受基础系统的本机 I/O 操作影响的大型、持久的缓冲区。
     *          最好仅在直接缓冲区能在程序性能方面带来明显好处时分配它们。
     *          直接字节缓冲区还可以过 通过FileChannel 的 map() 方法 将文件区域直接映射到内存中来创建 。该方法返回
    ```

- **滚动:  准备开始-读操作**

  - 将position指针移到0，limit移到数据尾端

    ```
    buf.flip(); 
    ```

- **核心属性**

  - 

  - ```
    buf.position();  // 当前position指针的位置
    buf.limit();	// 界限，表示缓冲区中当前可操作数据的大小
    buf.capacity();  // 容量，表示缓冲区中最大存储数据的容量。一旦声明不能改变。  
    ```

    


- **从channel中读取数据，向buffer写入数据**

  - 1.调用channel的read方法 

    ```
    int readBytes = channel.raed(buf);
    ```

  - 2.调用buffer自己的put方法

  - ```
    String data = "abcde"
    buf.put(data.getBytes())
    ```

- **从buffer中读数据,向channel写入数据**

  - 1.channel的write

    ```
    int writeBytes = channel.write(buf);
    ```

  - 2.buffer自己的get方法

    ```
    byte b = buf.get(new byte[4]); // 每次读取四个字节的数据
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

- **获取FileChannel**：必须通过FileInputStream，FileOutputStream,RandomAccessFile获取FileChannel,它们都有getChannel方法
  
  - RandomAccessFile 与输入流和输出流不同之处就是RandomAccessFile可以访问文件的任意地方同时支持文件的读和写，并且它支持随机访问。
  - `RandomAccessFile` 是 Java 中一个用于随机访问文件的类，允许你在文件中的任意位置读写数据。这使得处理文件分片和合并变得更加高效，尤其是在需要随机读取或写入数据的场景下。
  
- **读取数据**

  - 会从channel中读取数据，并填充到ByteBuffer,返回值表示读到了多少字节，-1表示到了文件末尾

  - ```
    int readBytes = channel.read(buffer); 
    ```

- **写入数据**

  - ```
    channel.write(buffer)
    ```
  
- **channel之间传输数据**

  - 底层利用操作系统的**零拷贝**进行优化，比传统的读写效率要高很多！**<font color='red'>建议两个通道直接transferTo简单又高效</font>**

  - **<font color='red'>有一个注意点：transferTo方法一次性最多只能传输2G，如果大于2G就分多次传输</font>**

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

    

### ② Path,Paths

```
JDK7 引入了 Path和Paths类  ，  便捷且规范地操作路径
	Paths是为了创建Path类
```

- **Paths类是为了创建Path类**        

  - 相对路径，是相对项目工程目录**user.dir**, 即 从整个项目开始，比如咕噜项目，C:\Users\赵联城\Desktop\GuluGulu\gulugulu-back

  - ```
    // 相对路径              C:\Users\赵联城\Desktop\GuluGulu\gulugulu-back\test/t.txt
    1.Path source = Paths.get("test/t.txt");
    // 绝对路径
    2.Path source = Paths.get("d:/test/t.txt");    都一样，
      Path source = Paths.get("d:\\test/t.txt");
    ```

- 常用API

  - Path类里面有一些API帮助我们快速判断/操作路径，用到自己去看源码，或者搜索吧

  



### ③ Files

```
java.nio.file.Files 用于操作文件或目录的工具类。
```

里面封装了丰富的方法，比如文件的复制，创建/删除，移动一个文件/目录； 判断文件是否存在，判断是否是目录，判断是否是隐藏文件
判断文件是否可读， 判断文件是否可写，获取与 path 指定的文件相关联的属性等等一系列API









## 4.网络编程



### 4.1 阻塞与非阻塞

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211142227713.png" alt="image-20241211142227713" style="zoom: 67%;" />

- 如上图所示，ssc.configureBlocking(false) 开启非阻塞模式，本来ssc.accept()，如果没有连接会阻塞在此处，非阻塞模式则不会，如果有连接则继续，没有则返回null，不会一直阻塞等待连接

- 如上图所示，sc.configureBlocking(false);开启非阻塞模式， 本来sc .accept()， 如果没有数据读会阻塞在此处，非阻塞模式则不会，

  如果有数据就读，没有read就返回0，不会一直阻塞等待数据



### 4.2 Selector代码演示

```

        Selector selector = null;
        ServerSocketChannel ssc = null;
        try{
        // 1. 创建服务器、selector
            selector = Selector.open();
            ssc= ServerSocketChannel.open();
            ssc.socket().bind(new InetSocketAddress(PORT));
            ssc.configureBlocking(false); // 设置服务器为非阻塞模式
       //  2. 将服务器注册到selector中     
            ssc.register(selector, SelectionKey.OP_ACCEPT);	
            while(true){
	  //  3. select()方法，没有事件发生，线程阻塞；有事件发生，线程恢复运行
	  			selector在事件未处理时，不会阻塞，事件要么处理，要么取消，不能置之不理！
	  			selector.select();
	  //   4. 处理事件，selectedKeys 内部包含了所有发生的事件
                Iterator<SelectionKey> iter = selector.selectedKeys().iterator();
                while(iter.hasNext()){
                    SelectionKey key = iter.next();
      //   5. 区分事件类型
      				// 处理连接事件
                    if(key.isAcceptable()){
                        handleAccept(key);
                    }
                    // 处理读事件
                    else if(key.isReadable()){
                        handleRead(key);
                    }
                    // 处理写事件
                    else if(key.isWritable() && key.isValid()){
                        handleWrite(key);
                    }
                    // 处理接收事件
                    else if(key.isConnectable()){
                        System.out.println("isConnectable = true");
                    }
                    else {
                    // 专门用来取消事件的
                    	key.cancle();
                    }
       // 6. key使用完毕后，需要remove !              
                    iter.remove();
                }
            }
        }catch(IOException e){
       // 7. 处理客户端断开强制断开错误
            e.printStackTrace();
            key.cancel();   // 通过cancel(),从集合中删去
        }finally{
            try{
                if(selector!=null){
                    selector.close();
                }
                if(ssc!=null){
                    ssc.close();
                }
            }catch(IOException e){
                e.printStackTrace();
            }

```











### 4.3selecto解析

- **SelectionKey的四种常量，表示类型**

```
当调用 register(Selector sel, int ops) 将通道注册选择器时，选择器对通道的监听事件，需要通过第二个参数 ops 指定。
可以监听的事件类型（用 可使用 SelectionKey 的四个常量表示，常量类型是 int 型）：

读事件：SelectionKey.OP\_READ，值是 1
写事件：SelectionKey.OP\_WRITE，值是 4
连接事件：SelectionKey.OP\_CONNECT，值是 8
接收事件：SelectionKey.OP\_ACCEPT，值是 16
```

- **SelectionKey**

  - ![image-20241211152836808](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211152836808.png)

    



### 4.4为什么需要及时删除key?

- 当你从Selector获取一个selected key集合并处理这些keys时，一旦完成对某个key的处理，应该立即从selected set中移除它。这是因为Selector不会自动从已选择的键集中移除已处理的键。

- 总之，你至少得知道要及时清理Key,原理最好掌握。

<font color='red'>具体流程自己去网上找资源分析,大概就是事件已经被处理过了，如果不清理，拿到null就会报错！</font>





### 4.5 处理客户端断开错误

**如果客户端因为某些原因，强制断开，会报错，需要key.cancel()处理错误**

```
catch(IOException e){
       // 7. 处理客户端断开的一个错误
            e.printStackTrace();
            key.cancel();
        }
```





**如果客户端正常断开，也要处理**

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211173924695.png" alt="image-20241211173924695" style="zoom:67%;" />







### 4.6消息边界问题

- **什么是消息边界问题？**
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211185507297.png" alt="image-20241211185507297" style="zoom: 50%;" />
  - 如上图所示，第一种情况，服务器预留的byteBuffer大小<消息的长度，就需要读取两次消息，如果
    byteBuffer为4，消息为"你好", 这样就会导致半包，出现乱码。
  - 第二种情况，出现半包，即 一个大消息"HelloWorldTCPMessage"，被分割[Hello] [World] [TCPMessage]多个数据包，这样，接收端收到的就不是一个完整的消息，而是多个数据包，接收端需要重新拼接这些包才能得到原始的完整消息。
  - 第三种情况，出现黏包



- **如何解决？**

  - ```
    1.定长消息：每个数据包的大小固定，接收端可以根据固定的长度进行解析。
    	【缺点是浪费带宽，消息可能很小】
    
    2.分隔符法：应用层协议使用特定的分隔符（如 \n 或其他特殊字符）来标识消息的结束，接收端根据分隔符分割数据包。
    	【缺点是效率低，每个字符都要检查】
    
    3.消息头方式：在每个消息前面添加一个固定长度的消息头，消息头中包含消息的长度信息，接收端可以根据消息头的长度确定每个数据包的边界。
    	【推荐！HTTP协议也是采取该方式】
    	【拓展小知识，HTTP1.1采用的是TLV格式，HTTP2.0采用的是LTV格式	】
    ```

    



### 4.7 写入过多内容问题

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211204213639.png" alt="image-20241211204213639" style="zoom:67%;" />

- 问题：如果一次性写入大量数据，会导致性能比较低，而且还会阻塞，肯定是不可取的
- 解决：通过把未写完的数据挂载到scKey上，同时关注可写事件，通过多次写





### 4.8 多线程优化

自己去看视频之类的吧



## 5.概念剖析



### 5.1 IO模型 

- **<font color='blue'>同步阻塞</font>**
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211215607747.png" alt="image-20241211215607747" style="zoom: 67%;" />

- **<font color='blue'>非阻塞IO</font>**
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211215816062.png" alt="image-20241211215816062" style="zoom:67%;" />

- <font color='blue'>**多路复用**</font>
  - 可以看出，**阻塞 I/O** 每执行一个操作时都会阻塞，必须等待底层数据操作完成才释放，因此每次只能完成一个操作。
    而 **多路复用** 则不同，执行一个操作时，只需事件本身（如数据准备好、连接可读写等）完成即可，因此一个循环可以处理多个事件，从而在同一时间内完成多个操作，提高了并发处理能力。
  - <img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211215921846.png" alt="image-20241211215921846" style="zoom:50%;" />





### 5.2 零拷贝

#### ①解析正常拷贝流程



![image-20241211221246484](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241211221246484.png)

1. java本身不具备IO读写能力，因此，read方法调用后，会从java程序的用户态切换到内核态，去调用操作系统的读写能力，将数据读入内核缓冲区。这期间用户线程阻塞，操作系统使用DMA（Direct Memory Access）来实现文件读，期间也不会使用CPU。

   > **DMA 也可以理解为硬件单元，用来解放 CPU 完成文件 IO。**
   > DMA（直接内存访问）是一种允许外设直接与系统内存交换数据的技术，而无需经过CPU。这能显著减轻CPU负担，提高数据传输效率。在大多数情况下，DMA在数据传输方面比CPU更高效，因为它避免了CPU的干预，从而减少了延迟并释放了CPU进行其他任务。然而，DMA的性能提升主要体现在大量数据的传输，CPU在处理复杂计算时仍然具有优势。

	2.从内核态切换回用户态，将数据从内核缓冲区读入用户缓冲区（即byte[] buf）,这期间cpu会参与拷贝，无法利用DMA
	
	3.调用write()方法，这时数据从用户缓冲区(byte[] buf)读取数据到socket缓冲区，cpu参与拷贝
	
	4.接下来向网卡写数据，这项能力java也不具备，因此又得从用户态切换至内核态，调用操作系统的写能力，使用DMA将scoket缓冲区的数据写入网卡，不会使用cpu

- 用户态与内核态切换了3次，这个操作比较重量级
- 数据拷贝了4次



#### ② NIO优化

**<font color='blue'>通过DirectByteBuf</font>**

- 间接访问：ByteBuffer.allocate(1024)   即常规的HeapByteBuffer  使用的是java内存 。

  > Java 堆内存是 JVM 管理的内存区域，用于存储对象。数据存取过程需要通过 JVM 堆内存到物理内存的转换，存在一定的性能开销。

- 直接访问：ByteBuffer.allocateDirect(1024) , 使用的是操作系统内存，这块内存java用户程序和操作系统都可以访问

  > 直接内存不属于 JVM 堆的一部分，而是直接通过操作系统的系统调用来分配的内存。它绕过了 JVM 堆，直接与操作系统的内存进行交互，减少了垃圾回收和堆内存管理的负担。

- 大部分操作和之前一样，唯有一点：java通过内存映射，可以操作内核缓冲区的数据
- **用户态和内核态的切换没有减少，但是数据拷贝减少了一次；**
- 个人感觉正常情况下用不到，因为小数据就减少一次拷贝没必要，除非数据量比较大减少一次拷贝就很不错，但是有了后面更优秀的优化方案，所以你知道有这个东西即可
- <img src="C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20241212121526624.png" alt="image-20241212121526624" style="zoom: 67%;" />





**<font color='blue'>进一步优化(linux2.1后提供 sendFile方法)，java中对应着两个channle调用transferTo/TransferFrom方法拷贝数据</font>**

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241212122803852.png" alt="image-20241212122803852" style="zoom: 67%;" />

- java调用transferTo方法后，要从java用户态切换到内核态，使用DMA将数据读入内核缓存区，不会使用cpu
- 数据从内核缓冲区 ---> socket缓冲区
- 最后使用DMA将socket缓冲区的数据写入网卡，不会使用cpu
- **可以看到，只有一次切换：只需要用户态切换到内核态，调用一次sendFile()就直接发送到socket缓冲区了**







**<font color='blue'>再一次优化（linux 2.4）</font>**

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20241212125115038.png" alt="image-20241212125115038" style="zoom:67%;" />

- 和linux2.1差不多，但是对sendFile()方法进行了优化，只会将一些offset和length拷贝到sokect缓冲区，






#### ③ 零拷贝

从NIO优化的演变，我们可以认识到，零拷贝不是真正的无拷贝，而是不会拷贝**重复数据到jvm内存中**

优点：

- 更少的用户态和内核态的切换
- 不利于cpu的计算，减少cpu缓存伪共享
- 零拷贝适合小文件传输 		























































































































































































