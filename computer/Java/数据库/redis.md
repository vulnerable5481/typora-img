# Redis基础



## 1.常见类型



### ① 字符串

![image-20240402162348526](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240402162348526.png)

![image-20240402164344125](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240402164344125.png)



### ② Hash

**<font color='red'>适合存储对象</font>**

```
1.HSET:   hset student name jack age 12 skill study

2.HGET: hget student name 

3.MGET: mget user:student:1 name age skill

4.hgetall

5.hkeys

6.hvalues

7.hincrby

8.hsetnx
在 Redis 中可以通过 setex 或 expire 方式来设置 key 的过期时间。但是对于Hash 数据类型 Redis 是不支持的，所以我们需要使用“曲线救国”的方式去实现 Hash 数据类型的过期时间。

即，先对 Hash 数据类型赋值，然后再对 Hash 数据类型的 key 设置一个过期时间，这样就间接的实现了对 Hash 数据类型的过期时间操作。
```



### ③ List

**<font color='red'>查询速度快，比较适合朋友圈点赞列表，评论列表</font>**

![image-20240402170557754](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240402170557754.png)

```
1.LPUSH key element
  RPUSH key element

2.LPOP key  移除左侧第一个元素，若没有则返回nil
  RPOP key

3.LRANGE key star end 

4.BLPOP   和lpop rpop 的区别就是 blpop 不会直接返回nil 而是在没有元素时等待指定时间
  BRPOP

```



### ④ Set

**<font color='red'>不可重复，适合实现标签、好友列表等功能</font>**

![image-20240402180625576](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240402180625576.png)

```
1. SADD key element1 element2 ...

2.SREM key emlement1 element2 ...

3.SCARD key: 返回set中元素的个数

4.sismember key member: 判断存在

5.smembers key: 获取set中所有元素

6.sinter k1 k2 ：交集
  sdiff k1 k2 :差集
  sunion k1 k2:并集
```





### ⑤ SortedSet

![image-20240402181751599](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240402181751599.png)

```
1.ZADD key score1 member1 score2 member2 ...

2.ZREM key member1

3.ZSCORE key member1

4.zrank key member   //注意是从0开始计算的

5.zcard key  返回sortedset中元素的个数

6.zcount key score_min score_max   查询min - max 区间 元素个数

7.zrange key index_min index_max   正序查询 min - max 的元素信息
  zrevrange key index_min index_max 倒序查询 min - max 的元素信息

8.zrangebyscore key score_min score_max  注意两边是开区间
 
9.zincrby key 整数 member

10. zdiff zinter zunion
**sortedset 默认是升序**
```



## 2.客户端



### ①常见客户端

**如果你导入的依赖是spring-boot-start-redis,默认是lettuce**

![image-20240402213101169](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240402213101169.png)







## 3.SpringDataRedis

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240402220350324.png" alt="image-20240402220350324" style="zoom:50%;" />



### ①依赖

**<font color='red'>第二个依赖用于与redis通信，第三个使用缓存连接池提高效率,由于第一个依赖会自动将lettue当做redis的客户端，所以可以简写，只写第一个和第三个依赖</font>**

```
<!--        redis-依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
<!--      与 Redis 进行通信
        <dependency>
            <groupId>io.lettuce.core</groupId>
            <artifactId>lettuce-core</artifactId>
            <version>6.1.5</version> <!-- 请根据需要选择版本 -->
        </dependency>
<!--        管理lettue 缓存连接池-->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
        </dependency>
```





### ② 序列化问题

- **<font color='orange'>因为redis底层都是将Java传过来的对象进行字节处理，序列化，这就导致数据库那边变成乱码</font>**

<img src="https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240403134306803.png" alt="image-20240403134306803" style="zoom:50%;" />

#### a.自定义RedisTemplate

- 下面是配置序列化工具，可是解决序列化问题

```
@Configuration
public class RedisConfig {
    @Bean
    public RedisTemplate<String,Object> redisTemplate(RedisConnectionFactory redisConnectionFactory){
        //创建RedisTemplate对象
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        //设置连接工厂
        template.setConnectionFactory(redisConnectionFactory);
        //创建json序列化工具
        GenericJackson2JsonRedisSerializer jsonRedisSerializer = new GenericJackson2JsonRedisSerializer();
        //设置Key的序列化
        template.setKeySerializer(RedisSerializer.string());
        template.setHashKeySerializer(RedisSerializer.string());
        //设置value的序列化
        template.setValueSerializer(jsonRedisSerializer);
        template.setHashValueSerializer(jsonRedisSerializer);
        //返回
        return template;
    }
}
```

#### b.StringRedisTemplate

- **<font color='red'>最佳实践：直接使用StringRedisTemplate类</font>**
  - ![image-20240403132348437](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240403132348437.png)

### ③ 配置文件

```
spring:
    redis:
      host: 127.0.0.1 # Redis服务器地址
      port: 6379      # Redis服务器连接端口
      password:    # Redis服务器连接密码（默认为空）
      database: 0  # Redis数据库索引（默认为0）
      jedis:
        pool:
          max-active: 8   # 连接池最大连接数（使用负值表示没有限制）
          max-wait: -1ms  # 连接池最大阻塞等待时间（使用负值表示没有限制）
          max-idle: 500   # 连接池中的最大空闲连接
          min-idle: 0      # 连接池中的最小空闲连接
      lettuce:
        shutdown-timeout: 0ms
      timeout: 1000 # 连接超时时间（毫秒）

```



### ④.SRTemplate

**<font color='red'>关于StringRedisTemplate的一些基础API自己去熟悉即可</font>**





## 4.四个问题

**<font color='orange'>将以短信验证登录为例子，通过如何保存验证码，来学习如何解决四个难题</font>**

### ①缓存更新

```
最佳实践：
	1.低一致性需求：使用内存淘汰机制，你不用管，内存不够redis自己删除
	2.高一致性需求：
		读操作：缓存命中直接返回；未命中查询数据库，写入缓存，设置TTL过期时间
		写操作：先写数据库，然后删除缓存【确保数据库和缓存操作的原子性】
```

![image-20240410123641028](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410123641028.png)

![image-20240410125548090](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410125548090.png)

![image-20240410125525968](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410125525968.png)





### ②缓存穿透

![image-20240410132556671](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410132556671.png)

![image-20240410182015564](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410182015564.png)

![image-20240410181852339](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410181852339.png)

### ③缓存雪崩

**目前感觉给不同的key设置随机TTL即可！**

![image-20240410205400497](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410205400497.png)





### ④缓存击穿

![image-20240410210250457](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410210250457.png)

- **<font color='orange'>逻辑过期虽然性能不错，但是会返回旧数据，适合用户体验至关重要，且可以接受一定程度的旧数据</font>**
  - 比如：1.新闻推荐、社交媒体内容等 2.数据更新频率低而读取频繁的场景（如商品详情、用户资料等）
  - 3.数据过期不会影响核心业务逻辑和决策的场景 
  - 4.如果数据可以通过批量更新的方式来刷新（如每小时更新一次的统计数据），逻辑过期可以有效减少数据库请求。
- **互斥锁：一些对数据一致性要求很高的，比如支付这种，你必须使用互斥锁，尽管性能变低，但是很安全！**

![image-20240410210511769](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410210511769.png)

- 流程演示：

![image-20240410210223055](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240410210223055.png)

- 互斥锁的案例：  可以使用悲观锁，也可以使用乐观锁，如果是支付这种必须使用悲观锁，如果要求严但没有那么的严可以用乐观锁
  - 在金融系统中，常常需要读取用户账户信息（使用乐观锁），但在执行资金转账时则需要使用悲观锁来避免并发问题。
  - ![image-20240411122356869](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240411122356869.png)

- 逻辑过期的案例演示
  - ![image-20240411134514875](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240411134514875.png)





## 5.持久化

```
当服务器宕机或redis重启，保存的数据就会丢失，如何让redis中的数据持久化？  答案：RDB快照 /  AOF日志
```

**Redis 的持久化机制有两种，一种是快照（RDB），另一种是 AOF 日志。RDB是一次全量备份，AOF 日志是连续的增量备份。快照是内存数据的二进制序列化形式，在存储上非常紧凑，而 AOF 日志记录的是内存数据修改的指令记录文本。**

### ① RDB快照

- **RDB快照持久化是Redis默认开启的**
- 会根据配置策略将内存数据保存在一个名为dmp.rdb的二进制文件中。
- 在redis.conf配置文件中，可以配置RDB的持久化策略，系统默认是有三个保存策略(三个同时生效)，如下：
  - save 900 1       900秒内有1个键发生改变
  - save 300 10      30秒内有10个键发生改变
  - save 60 10000    60秒内有10000个键发生改变
- 如果我们要关闭RDB快照，直接将配置文件中上述三个save注释掉即可。



- 优点

  - Redis宕机后数据恢复快

  - 二进制文件体积小

- 缺点
  - 持久化策略可能会导致在宕机时数据丢失量较多



### ② AOF日志

- AOF持久化可以通过redis.conf文件中的appendonly参数控制是否开启。默认情况下是no
- 











### ③ redis.conf

```
nd 0.0.0.0

protected-mode no

port 6379

tcp-backlog 511

requirepass 1674472827

timeout 0

tcp-keepalive 300

daemonize no

supervised no

pidfile /var/run/redis_6379.pid

loglevel notice

logfile ""

databases 30

always-show-logo yes

save 900 1
save 300 10
save 60 10000

stop-writes-on-bgsave-error yes

rdbcompression yes

rdbchecksum yes

dbfilename dump.rdb

dir ./

replica-serve-stale-data yes

replica-read-only yes

repl-diskless-sync no

repl-disable-tcp-nodelay no

replica-priority 100

lazyfree-lazy-eviction no
lazyfree-lazy-expire no
lazyfree-lazy-server-del no
replica-lazy-flush no


aof-load-truncated yes

aof-use-rdb-preamble yes

lua-time-limit 5000

slowlog-max-len 128

notify-keyspace-events ""

hash-max-ziplist-entries 512
hash-max-ziplist-value 64

list-max-ziplist-size -2

list-compress-depth 0

set-max-intset-entries 512

zset-max-ziplist-entries 128
zset-max-ziplist-value 64

hll-sparse-max-bytes 3000

stream-node-max-bytes 4096
stream-node-max-entries 100

activerehashing yes

hz 10

dynamic-hz yes

aof-rewrite-incremental-fsync yes

rdb-save-incremental-fsync yes
```









































































































































































































































































