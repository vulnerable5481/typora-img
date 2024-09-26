```

```

# 1.线程池



## ① 单线程基本使用

- 继承  Thread
- 实现 Runnable



```
1.开启线程
	Thread thread = new Thead(new MyRunnable());
	thread.start();
2.重写run方法
```



## ② 线程池DEMO

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

        for (int i = 0; i < 10; i++) {
            //创建WorkerThread对象（WorkerThread类实现了Runnable 接口）
            Runnable worker = new MyRunnable("" + i);
            //执行Runnable
            executor.execute(worker);
        }
        //终止线程池
        executor.shutdown();
    }
}

```

## ③ ThreadPoolExecutor

​	`ThreadPoolExecutor` 类中提供的四个构造方法

​	此处只介绍最长的

```java
    /**
     * 用给定的初始参数创建一个新的ThreadPoolExecutor。
     */
    public ThreadPoolExecutor(int corePoolSize,//线程池的核心线程数量
                              int maximumPoolSize,//线程池的最大线程数
                              long keepAliveTime,//当线程数大于核心线程数时，多余的空闲线程存活的最长时间
                              TimeUnit unit,//时间单位
                              BlockingQueue<Runnable> workQueue,//任务队列，用来储存等待执行任务的队列
                              ThreadFactory threadFactory,//线程工厂，用来创建线程，一般默认即可
                              RejectedExecutionHandler handler//拒绝策略，当提交的任务过多而不能及时处理时，我们可以定制策略来处理任务
                               ) {
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }

```

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



## ④ 深入理解线程池原理





## ⑤ 几种常见的对比



### execute() vs submit()

1. **`execute()`方法用于提交不需要返回值的任务，所以无法判断任务是否被线程池执行成功与否；**
2. **`submit()`方法用于提交需要返回值的任务。线程池会返回一个 `Future` 类型的对象，通过这个 `Future` 对象可以判断任务是否执行成功** ，并且可以通过 `Future` 的 `get()`方法来获取返回值，`get()`方法会阻塞当前线程直到任务完成，而使用 `get（long timeout，TimeUnit unit）`方法则会阻塞当前线程一段时间后立即返回，这时候有可能任务没有执行完。



### shutdown() vs shutdonwNow

- **`shutdown（）`** :关闭线程池，线程池的状态变为 `SHUTDOWN`。线程池不再接受新任务了，但是队列里的任务得执行完毕。
- **`shutdownNow（）`** :关闭线程池，线程的状态变为 `STOP`。线程池会终止当前正在运行的任务，并停止处理排队的任务并返回正在等待执行的 List。





### isTerminated() vs isShutDown

- **`isShutDown`** 当调用 `shutdown()` 方法后返回为 true。
- **`isTerminated`** 当调用 `shutdown()` 方法后，并且所有提交的任务完成后返回为 true







# 2.阿里云文件操作

看文档即可





# 3.验证码





# 4.JSR303

<font color='orange'>**数据校验的一大利器，常规简单数据校验可以使用JSR303, 剩余的复杂数据校验再由你自己来写**</font>

## 4.1 快速入门

1..引入依赖	

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

2.添加注解，并自定义错误信息message

3.controller层 添加@Valid   开启数据校验，注意必须要加这个不然就无效

4.controller层 可以添加一个数据 BindingResult result ， 意思是数据校验的结果



## 4.2 分组校验

- 1.设置空接口

![](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240922135412898.png)



- 2.   设置分组

  ```
  	@NotNull(message = "品牌id不存在",groups = {UpdateGroup.class})
  	@Null(message = "新增品牌不能指定id",groups = {AddGroup.class})
  	@TableId
  	private Long brandId;
  	/**
  	 * 品牌名
  	 */
  	@NotBlank(message = "品牌名不能为空",groups = {AddGroup.class,UpdateGroup.class})
  	private String name;
  	/**
  	 * 品牌logo地址
  	 */
  	@NotBlank(message = "品牌logo不能为空",groups = {AddGroup.class,UpdateGroup.class})
  	private String logo;
  	/**
  	 * 介绍
  	 */
  	 @NotBlank(message = "品牌介绍不能为空")
  	private String descript;
  ```

  

- 3. @Validated注解   标明分组

```
/**
 * 修改
 */
@RequestMapping("/update")
public R update(@Validated(UpdateGroup.class) @RequestBody BrandEntity brand) {
    brandService.updateById(brand);

    return R.ok();
}
```

- 4.注意点：如果使用在controller层使用@Validated(UpdateGroup.class)，那么 没有设置分组的属性，比如上面的品牌介绍，其@NotBlank就不会生效，使用普通的@Valid则依然起作用





## 4.3 最佳实践

<font color='orange'>**可以设置一个枚举类，来控制异常;**</font>****

```
package com.zlc.common.exception;

public enum BizCodeEnume {
    UNKONW_EXCEPTION(10000,"系统未知异常"),
    VALID_EXCEPTION(10001,"参数格式校验失败");


    private int code;
    private String message;

    BizCodeEnume(int code, String message) {
        this.code = code;
        this.message = message;
    }

    public int getCode() {
        return code;
    }

    public String getMessage() {
        return message;
    }
}

```

**<font color='orange'>为了让业务逻辑与数据校验分开，可以这么做,这样就不会污染controller层的代码</font>**

```
package com.zlc.gulimall.product.exception;

import com.zlc.common.exception.BizCodeEnume;
import com.zlc.common.utils.R;
import lombok.extern.slf4j.Slf4j;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.util.HashMap;


@Slf4j
@RestControllerAdvice
public class GulimallExceptionControllerAdvice {

    @ExceptionHandler
    public R handleValidException(MethodArgumentNotValidException e) {
        log.info("数据校验异常:{}", e.getMessage());
        //获取 BindingResult
        BindingResult result = e.getBindingResult();

        HashMap<String, String> map = new HashMap<>();
        //获取错误信息
        result.getFieldErrors().forEach((item) -> {
            //获取到错误信息
            String message = item.getDefaultMessage();
            //获取到错误字段
            String field = item.getField();
            map.put(field, message);
        });

        return R.error(BizCodeEnume.VALID_EXCEPTION.getCode(), BizCodeEnume.VALID_EXCEPTION.getMessage())
                .put("data", map);
    }

    @ExceptionHandler
    public R handleAll(Exception e){
        return R.error(e.getMessage());
    }
}

```





















































