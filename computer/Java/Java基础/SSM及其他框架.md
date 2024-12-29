







# JavaSe-Review

### 一.IO流

#### 1.文件的操作

(1)File类

注意：File类可以表示一个文件，还可以表示一个目录（Directory），所以我们可以在程序中用File 类的对象可以表示一个文件 或者 目录
当创建了 File 对象之后，我们可以利用该对象来对文件或者目录进行书属性修改：例如：文件的名称，修改日期的日期等等
File 类的对象 还不能直接对文件进行读写操作，只能修改文件的属性等静态操作

File类的一些基本操作：

- `boolean`  `createNewFile()`  当且仅当具有此名称的文件尚不存在时，以原子方式创建由此抽象路径名命名的新空文件。
- `boolean`  `delete()`  删除此抽象路径名表示的文件或目录。
- `boolean`  `exists()`  测试此抽象路径名表示的文件或目录是否存在
- boolean mkdir() 创建单个目录   
- boolean mikdirs() 创建多级目录

​    //注意  ：  这里的file只是一个Java对象，只有使用了createNewFile()方法之后才会真正地在磁盘中创建一个文件

例子:

```
public static void createNewFile(){
    File f1=new File("E:/PR/zlc.txt");
    //如果是相对路径，如果没有前面的src，就在当前目录创建文件
    //如果是绝对路径，那中间推荐使用 / 而不是\\
    //注意  ：  这里的file只是一个Java对象，只有使用了createNewFile()方法之后才会真正地在磁盘中创建一个文件
    if(f1.exists()) {
        System.out.println("文件已经存在");
    }else {
        try {
            f1.createNewFile();
                //注意  ：  这里的file只是一个Java对象，只有使用了createNewFile()方法之后才会真正地在磁盘中创建一个文件
            System.out.println("文件创建成功");
            //注意:创建文件的路径必须存在否则会抛出异常，比如  new File("E:/")
        } catch (Exception e) {
            // TODO: handle exception
        }
        System.out.println("文件的绝对路径" + file.getAbsolutePath());
        System.out.println("文件的父级目录" + file.getParentFile());
        System.out.println("文件的大小" + file.length());
        System.out.println("是不是一个文件" + file.isFile());
        System.out.println("是不是一个目录" + file.isDirectory());
    }
}
```

(2)  一些概念

目录也是文件，是一种特殊文件，叫目录文件，简称目录。
目录是文件系统对象，属于文件系统的概念
术语目录指的是文档文件和文件夹的结构化列表存储在计算机上的方式。它与包含姓名、号码和地址列表的电话簿相当，并且不包含实际文件本身
目录并不是真的把文件放在里面。目录是一个“特殊的文件”，它知道文件的存储位置（通过 inode）。这就说明了为什么它被称为目录。目录用来保存文件项目的索引，而不用保存文件项目本身。Linux 和 UNIX 中的目录并不保存它里面的文件。它们只是记录文件位置的信息

文件夹不一定是磁盘上的物理目录，例如，它可以是Windows中的打印机文件夹或控制面板文件夹
文件夹是图形用户界面对文档容器的隐喻
文件夹是GUI对象
文件夹通常用图标描绘，视觉上类似于物理文件夹

文件就是目录文件以外的普通文件，简称文件。

总结：大部分情况下文件夹与目录的含义相同。

(3) 关于同时创建目录和文件

```
public static void createNewDirectory(){
    File file = new File("E:/PR/java/zlc/haha.txt");
    if(!file.exists()){
        try {
            file.getParentFile().mkdirs();
            file.createNewFile();
            System.out.println("目录创建成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

最后结果就是在E盘下面创建了一个    java/zlc/haha.txt

#### 2.stream流

**（1）** 

字节流
java.io.InputStream 字节输入流
java.io.OutputStream 字节输出流
字符流
java.io.Reader 字符输入流
java.io.Writer 字符输出流
注意：

四大家族的首领都是抽象类。(abstract class)
所有的流都实现了：
java.io.Closeable接口，都是可关闭的，都有 close() 方法。
流是一个管道，这个是内存和硬盘之间的通道，用完之后一定要关闭，不然会耗费(占用)很多资源。养成好习惯，用完流一定要关闭。
所有的 输出流 都实现了：
java.io.Flushable接口，都是可刷新的，都有 flush() 方法。
养成一个好习惯，输出流在最终输出之后，一定要记得flush()刷新一下。这个刷新表示将通道/管道当中剩余未输出的数据强行输出完（清空管道！）刷新的作用就是清空管道。
**ps**：**`如果没有flush()可能会导致丢失数据`**。

在java中只要“**类名**”以 **`Stream`** 结尾的都是**字节流**。以“ **`Reader/Writer`** ”结尾的都是**字符流**。

**(2)java 中 的十六个流**

文件专属：
java.io.FileInputStream（掌握）
java.io.FileOutputStream（掌握）
java.io.FileReader
java.io.FileWriter
转换流：（将字节流转换成字符流）
java.io.InputStreamReader
java.io.OutputStreamWriter
缓冲流专属：
java.io.BufferedReader
java.io.BufferedWriter
java.io.BufferedInputStream
java.io.BufferedOutputStream
数据流专属：
java.io.DataInputStream
java.io.DataOutputStream
标准输出流：
java.io.PrintWriter
java.io.PrintStream（掌握）
对象专属流：
java.io.ObjectInputStream（掌握）
java.io.ObjectOutputStream（掌握）
File文件类
java.io.File

**补充：Windows/Linux小知识点**

Windows：`D:\Soft\QQ\Plugin`
Linux：   `D:/Soft/QQ/Plugin`

#### **(3) IO四大家族之节点流**

##### 1.字节流

##### FileInputStream:

一般情况下，我们应该优先选取BufferedInputStream&BufferedOutputStream。

用途：文件字节输入流，万能的，任何类型的文件都可以采用这个流来读

实例:

```
public static void readTxt(){
    byte[] buf = new byte[1024];//意思是一次读取1024个字节
    int readData = 0;
    FileInputStream fileInputStream = null;
    try {
        fileInputStream = new FileInputStream("E:/zlc.txt");
        while((readData = fileInputStream.read(buf))!=-1){
            System.out.print(new String(buf,0,readData));

        }
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            fileInputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



##### **FileOutputStream**:

```
public static void putTxt(){
    FileOutputStream fileOutputStream = null;
    try {
        fileOutputStream = new FileOutputStream("e:/zlc.txt",true);
        //这个默认是false ，写true 意思就是不会覆盖之前的内容
        fileOutputStream.write("你好世界".getBytes());
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            fileOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


}
```

##### 图片copy :

```
    public static void copyPicture(){
        FileInputStream fileInputStream = null;
        FileOutputStream outputStream = null;
        byte[] bytes = new byte[1024];
        int readData = 0;
        try {
            fileInputStream = new FileInputStream("e:\\img.jpg");
            outputStream = new FileOutputStream("e:\\copyimg.jpg");
            while((readData = fileInputStream.read(bytes)) != -1){
                outputStream.write(bytes,0,readData);
                outputStream.flush();//良好的素质程序员就要学会自己去冲
            }
            System.out.println("Good copy img,my master!");
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                fileInputStream.close();
                outputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
    }
```



##### 2.**字符流**  

##### **FileReader**:

```
public static void test1(){
    FileReader fileReader  = null ;
    char[] data = new char[1024];
    int readLength = 0;
    try {
        fileReader = new FileReader("e:/zlc.txt");
        while((readLength = fileReader.read(data)) != -1){
            System.out.println(new String(data,0,readLength));
        }
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            fileReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

##### **FileWritter**:

```
public static void test1(){
    FileWriter fileWriter = null;
    try {
        fileWriter  = new FileWriter("e:/zlc.txt",true);
        fileWriter.write("我是你爹");
        fileWriter.flush();//良好的素质程序员就是要自己去冲
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

##### (3)字符流和字节流的区别：

字节流   可以用来操作二进制文件 如 图片  视频之类的,这个操作文本信息不太好用有很多弊端

字符流    不能处理二进制文件，但是用来处理文本信息十分快捷



#### (4)IO四大家族之处理流

**(优先使用处理流，是节点流的改良版，性能更好一点)**



##### **BufferdInputStream**:

 一般情况下，我们应该优先选取BufferedInputStream&BufferedOutputStream。   

```
public static void test1(){
    BufferedInputStream bufferedInputStream = null;
    byte[] bytes = new byte[1024];
    int readLine = 0;
    try {
        bufferedInputStream = new BufferedInputStream(new FileInputStream("e:/zlc.txt"));
        while((readLine = bufferedInputStream.read(bytes)) != -1){
            System.out.println(new String(bytes,0,readLine));
        }
    } catch (IOException e) {
        e.printStackTrace();
    }finally{
       // 忘了close()了
    }
}
```



##### **BufferdOutputStream**:

```
public static void test1(){
    BufferedOutputStream bufferedOutputStream = null;
    try {
        bufferedOutputStream = new BufferedOutputStream(new FileOutputStream("e:/zlc.txt",true));
        bufferedOutputStream.write("现在是晚上".getBytes());
        bufferedOutputStream.flush();
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            bufferedOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



##### **BufferdReader**

（优先选择BufferdReader而不是FileReader,因为BufferdReader自带缓冲区，不需要你自己new byte[]）

```
public static void test1(){
    BufferedReader bufferdReader = null;
    String readLine = "";
    try {
        bufferdReader = new BufferedReader(new FileReader("e:/zlc.txt"));
        while((readLine = bufferdReader.readLine()) != null){
        //注意    BufferdReader的readLine方法是直接读取一整行（一整行是指遇见换行符\n），回车符\r中的任何一个或者
        //   		随后的换行符都会终止,返回Null
        //同时BufferdReader也支持原先的read()方法
            System.out.println(readLine);
        }
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            bufferdReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

##### **BufferdWriter**

```
public static void test1(){
    BufferedWriter bufferedWriter = null;
    try {
        bufferedWriter = new BufferedWriter(new FileWriter("e:/zlc.txt",true));
        bufferedWriter.write("好，那么好");
        bufferedWriter.newLine();
        //newLine（）换行的作用
        //建议你写一句话，就换一次行，因为有时候不止一句话，好习惯
        bufferedWriter.write("空气中充满了快活的气息");
        bufferedWriter.newLine();
        bufferedWriter.flush();
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        try {
            bufferedWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



#### (5)四大家族之转换流



#### (6)四大家族之打印流









### 二.多线程



#### 1.基础知识





#### 2.线程池





#### 3.悲观锁与乐观锁



**悲观锁:** 悲观锁在操作数据的时候比较悲观，**认为别人会同时修改数据。**

​			因此操作数据时直接**把数据锁住**，直到操作完成后才会释放锁；上锁期间其他人不能修改数据。

**//实现方式**

```
数据库中的行锁，表锁，读锁（共享锁），写锁（排他锁），以及syncronized实现的锁均为悲观锁






```





**乐观锁**:乐观锁在操作数据的时候比较乐观，**认为别人不会同时修改数据。**

​			因此乐观锁**不会上锁**,只是在更新的时候判断一下在此期间别人是否修改了数据；如果别人修改了数据则放弃操作，否则执行操作

**//实现方式1:CAS（Compare And Swap）**

```
操作流程:
 	 1) 需要读写的内存位置(V)
     2) 进行比较的预期值(A)
     3) 拟写入的新值(B)
操作逻辑:
        涉及到三个操作数，数据所在的内存值，预期值，新值。当需要更新时，判断当前内存值与之前取到的值是否相等，若相等，则用新值更         新，若失败则重试，一般情况下是一个自旋操作，即不断的重试。
一个问题:
	许多CAS的操作是自旋的：如果操作不成功，会一直重试，直到操作成功为止。
    这里引出一个新的问题，既然CAS包含了Compare和Swap两个操作，它又如何保证原子性呢？
    答案是：CAS是由CPU支持的原子操作，其原子性是在硬件层面进行保证的。



```

**//实现方式2：版本号(比较常用)**

```
一般是在数据表中加上一个数据版本号version字段，表示数据被修改的次数，当数据被修改时，version值会加一。当线程A要更新数据值时，在读取数据的同时也会读取version值，在提交更新时，若刚才读取到的version值为当前数据库中的version值相等时才更新，否则重试更新操作，直到更新成功。
```



**//区别与应用场景**





















































































































































