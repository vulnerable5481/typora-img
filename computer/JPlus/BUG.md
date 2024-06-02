# 一.世界未解之谜





## 1.reids篇





### 1.redis与lutter

```
<!--        redis-依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
            <version>2.7.3</version>
        </dependency>
<!--        lettue 缓存连接池-->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
            <version>2.7.3</version>
        </dependency>
```

按理说一般都是同时引入这两个依赖，但是我同时引入却一直报错

attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'redisConnectionFactory' defined in class path resource [org/springframework/boot/autoconfigure/data/redis/LettuceConnectionConfiguration.class]: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory]: Factory method 'redisConnectionFactory' threw ex





### 2.redis中的""



从Java端存到reids的""  并不等于 java中的 ""

而且 " " 也同样不相等

这是为什么呢？？？？？





















