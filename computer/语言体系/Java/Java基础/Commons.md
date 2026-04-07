# 1. IO流

### 一.IO流

#### 1.文件的操作

(1)File类

注意：File类可以表示一个文件，还可以表示一个目录（Directory），所以我们可以在程序中用File 类的对象可以表示一个文件 或者 目录
当创建了 File 对象之后，我们可以利用该对象来对文件或者目录进行书属性修改：例如：文件的名称，修改日期的日期等等
File 类的对象 还不能直接对文件进行读写操作，只能修改文件的属性等静态操作

File类的一些基本操作：

- `boolean`  `createNewFile()`  当且仅当具有此名称的文件尚不存在时，以原子方式创建由此抽象路径名命名的新空文件。
- `boolean`  `delete()`                 删除此抽象路径名表示的文件或目录。
- `boolean`  `exists()`                 测试此抽象路径名表示的文件或目录是否存在
- `boolean` `mkdir()`                    创建单个目录   
- `boolean` `mikdirs()`                创建多级目录

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







#### 



















































































































































# 2. 反射





# 3. 泛型	

```
1、泛型的本质
	本质：java泛型本质上就是用编译期类型约束，换取运行期安全+代码复用
	注意：java泛型是伪泛型，通过类型擦除实现。C++、C#、kotlin、go等等很多语言都有泛型
	
2、基础使用
① 泛型类: T只是占位符，这样实现代码复用
public class Box<T> {
	private T value;
	public void Box(T value){
		this.value = value;
	}
}
② 泛型方法: 依然是为了代码复用
  注意语法 <T>在前 T在后
pubilc static <T> T getFirst(List<T> list){
	return list.get(0);
}
③ 泛型接口
public interface Repository<T,ID> {
	T findByID(ID id);
}

3、运行期安全是什么意思？
比如说 List<String> list = new ArrayList<>(); list.add(123) 这在编译器直接报错，防止运行期报错
```



# 4. 注解

```java
1、注解的本质
    本质：java中的注解本质上就是一种“结构化的元数据”，供给程序、框架看的信息，本身不执行任何逻辑。
	作用：程序和框架读取注解之后就可以做很多事情，比如配合AOP实现自定义注解，当AOP代理检测到这个方法有我们设置的自定义注解
    	 就会执行一些预先设计好的行为，比如日志打印之类的。所以注解需要被读取才能发挥作用。

2、一些基础，以下面的自定义注解作为演示
@Target：注解用在哪里？比如ElementType.METHOD，就是用在方法上
@Retention:注解的生命周期 ，比如RetenionPolicy.RUNTIME，只在运行时可反射获取
@Documented：一般情况用不到，加了就可以在java自带命令生成的输出文档中看到该自定义注解，感觉作用不大
    
3、注解合并
注解在SpringBoot是可以合并的，比如我们常用的RestController,就是通过以下方式得到的：
@RestController = @Controller + @ResponseBody
    具体代码如下：
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Controller
@ResponseBody
public @interface RestController {}

4、AOP+自定义注解
① 自定义注解
@Target(ElementType.METHOD)
@Retention(RetenionPolicy.RUNTIME)
@Ducumented
public @interfeca LogTime {
	String value() default "";
}
② AOP
@Aspect
@Comment
public class LogTimeAspect {
	@Aroud("@annotation(logTime)")
	public Object logMethodTime(ProceedingJoinPoint joinPoint, LogTime logTime) throws Throwable {
		// 方法信息
		MethodSignature signature = (MethodSignature) joinPoint.getSignature();
        String className = signature.getDeclaringTypeName();
        String methodName = signature.getName();
        // 打印start
        long startTime = System.currentTimeMillis();
        log.info("【开始】{}.{}() 开始执行，时间：{}，描述：{}",
        className,
        methodName,
        startTime,
        logTime.value()
        );
        // 打印end
        Object result;
        try {
        	result = joinPoint.proceed(); // 执行原方法
        } finally {
        	long endTime = System.currentTimeMillis();
            log.info("【结束】{}.{}() 执行结束，时间：{}，耗时：{} ms",
                    className,
                    methodName,
                    endTime,
                    endTime - startTime
            );
        }
        // 返回结果
        return result;
	}
}
```



# 5、接口与抽象类

```
接口主要是 制定规范 + 代码解耦
抽象类主要是 指定模板 + 代码复用
```



# 6.线程池

## ① 最佳实践

使用阿里巴巴推荐的ThreadPoolExecutor构造函数自定义参数的方式来创建线程池

**个人推荐以后就按照这个DEMO创建线程池**

```
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

public class ThreadPoolExecutorDemo {
	
    private static final int CORE_POOL_SIZE = 5;      //核心线程数
    private static final int MAX_POOL_SIZE = 10;	 //最大线程数
    private static final int QUEUE_CAPACITY = 100;	//队列容量
    private static final Long KEEP_ALIVE_TIME = 1L;  //等待时间
    public static void main(String[] args) {

        //使用阿里巴巴推荐的创建线程池的方式
        //通过ThreadPoolExecutor构造函数自定义参数创建
        ThreadPoolExecutor executor = new ThreadPoolExecutor(
                CORE_POOL_SIZE,		//核心线程数
                MAX_POOL_SIZE,		//最大线程数
                KEEP_ALIVE_TIME,	//指定等待时间
                TimeUnit.SECONDS,   //指定等待时间单位
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),//指定任务队列为ArrayBlockingQueue，并指定容量
                new ThreadPoolExecutor.CallerRunsPolicy()//饱和策略为 CallerRunsPolicy	
                );  

        //创建WorkerThread对象（WorkerThread类实现了Runnable 接口）
        Runnable worker = new MyRunnable("参数");
        //执行Runnable或者场景简单直接匿名类即可
        executor.execute(worker);          execeutor.execute(()=>{//do});
        //终止线程池
        executor.shutdown();
    }
}

```

## ② 参数详解

**三个最重要的参数**

```
corePoolSize : 核心线程数线程数定义了最小可以同时运行的线程数量。
maximumPoolSize : 当队列中存放的任务达到队列容量的时候，当前可以同时运行的线程数量变为最大线程数。
workQueue: 当新任务来的时候会先判断当前运行的线程数量是否达到核心线程数，如果达到的话，新任务就会被存放在队列中。
			推荐使用ArrayBlockingQueue一个由数组支持的有界阻塞队列。此队列按 FIFO（先进先出）原则对元素进行排序。一旦创建了             这样的缓存区，就不能再增加其容量。试图向已满队列中放入元素会导致操作受阻塞；试图从空队列中提取元素将导致类似阻塞。
```

**其他参数**

```
keepAliveTime:当线程池中的线程数量大于 corePoolSize 的时候，如果这时没有新的任务提交，核心线程外的线程不会立即销毁，而是会等待，直到等待的时间超过了 keepAliveTime才会被回收销毁；
unit : keepAliveTime 参数的时间单位。
threadFactory :executor 创建新线程的时候会用到。
handler :饱和策略。关于饱和策略下面单独介绍一下。
```

**饱和策略：默认为ThreadPoolExecutor.AbortPolicy**

```
ThreadPoolExecutor.AbortPolicy：抛出 RejectedExecutionException来拒绝新任务的处理。   
ThreadPoolExecutor.CallerRunsPolicy：调用执行自己的线程运行任务，也就是直接在调用execute方法的线程中运行(run)被拒绝的任务，如果执行程序已关闭，则会丢弃该任务。因此这种策略会降低对于新任务提交速度，影响程序的整体性能。如果您的应用程序可以承受此延迟并且你要求任何一个任务请求都要被执行的话，你可以选择这个策略。
ThreadPoolExecutor.DiscardPolicy： 不处理新任务，直接丢弃掉。
ThreadPoolExecutor.DiscardOldestPolicy： 此策略将丢弃最早的未处理的任务请求。
```

## ③ 函数的对比

```
1、execute() vs submit()
	execute():用于提交不需要返回值的任务，所以无法判断任务是否被线程池正确执行
	submit() :用于提交需要返回值的任务。线程池会返回一个Future对象，通过Future对象的get()可以拿到返回值，get()可能会阻塞线程直到任务完成才能拿到返回值，而使用get(lone timeout,TimeUnit unit)方法则会阻塞当前线程一段时间后立即返回，即使没有拿到结果

2、shutdown() vs shutdownNow()
	shutdown()：关闭线程池，线程池的状态变为SHUTDOWN。线程池不再接收新任务，但队列里的任务仍会执行
	shutdownNow：关闭线程池，线程池的状态变为STOP。线程池不再接收和执行队列里的任务，立即停止。
	
3、isTerminated`() vs isShutDown()
	isTerminated:当线程池状态变为terminated，返回true
	isShutDown  :当线程池状态变为shutdown  ，返回true      
	Shutdown状态：不再接收，但会处理队列里的任务
    Terminated状态：所有线程结束，线程池全部结束
```































































































































































































