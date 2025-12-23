# 1. IO流





# 2. 反射





# 3. 泛型	





# 4. 注解



# 5.线程池

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































































































































































































