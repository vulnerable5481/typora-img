

```
重新整理一遍Mysql相关的知识，之前那份笔记过于随意了
```



# 一、基础篇





## 1、概念与规定

关系型数据库 VS  非关系型数据库

```
关系型数据库：
	就是最经典的二元关系，行与列组成一张表，一张张表又组成了库，关系型数据库可以看做是二维表格，且表与表之间有关系的，
	比如可以进行联查操作，redis就没法做到这样
	【综合全能数据库，啥都能干】
非关系型数据库：
	比如mangodb就是文档型数据库，存储的是json数据，redis就是KV，ES就是针对复杂查询做聚合的
	【阉割版，通过去掉一些复杂的功能比如事务什么的，以此让某几个功能变得异常强大】
```

一些规约

```
1、列的别名，最好是用as + 双引号""   xxx as "xxx"
2、字符串和日期类型的数据可以使用单引号''表示  
3、windows下不分大小写，linux下区分大小写
4、mysql不允许嵌套使用聚合函数，比如MIN(AVG(salary)),但是oracle允许使用，还得是付费！
```



① **DDL** 数据定义语言

- create  

- alert    修改

- drop    删除

② **DML**  数据操作语言   

- insert

- delete

- update

- select

③ **DCL**   数据控制语言

- commit 

- rollback





## 2、执行顺序

**sql92:**

```
SQL语句的执行顺序
select ... 
from ...
where 外连接条件 and 不包含聚合函数的过滤条件
group by ...
having 包含聚合函数的过滤条件
order by ...(asc/desc)
limit ...

```

**sql99**:

```
SELECT .......
FROM ... (LEFT / RIGHT)JOIN ... ON 外连接条件 JOIN ... ON 外连接条件
WHERE 不包含聚合函数的过滤条件
GROUP BY...,...,..
HAVING 包含聚合函数的过滤条件
ORDER BY ... (ASC/DESC)
LIMIT ...,...
```

```
 from->on->(left/right join) -> where -> group by -> having -> select -> order by -> limit

```









## 3、DML

### ① 常见操作

- **DISTINCT** 

  ```
  可以实现去重效果，但是group by在一些场景下可以实现去重
  distinct的底层原理是如何实现去重的呢？
  	第一种：排序去重（性能差一点）
  		myhsq对结果集进行排序，排序后相同的值就会在一起，只取每个相同值的第一个，这样就实现了去重
  	第二种：哈希临时表去重(空间换时间)
  		mysql8.0优化器引入hash-based distinct，在某些场景下会临时选择哈希表存储已见过的值，每次新行过来的时候，先算哈希
  		if hash_code is same -> discard
  		if hash_code is new  -> save/insert
  		通过这张临时表就实现了去重
  	第三张：如果有索引就走索引，只需要顺序扫描索引，重复值自然聚在一起
  ```

- **运算符**

  ```
  1、+ -  * /或DIV %或MOD
  2、or或|| and或&&  =  !=   
  3、is null  is not null
  4、  in ,  not in  ， like
  // 下面是我不怎么熟悉的运算符
  5、least 最小  greatest 最大 比如: where a least(b,c)
  6、(not)between and 判断一个值是否在两个值之间  where 10 between 5 and 15
  ```

  

### ② 排序与分页

- **order by**

  ```
  1、默认是asc  由低到高 上面是低的
  2、列的别名可以在order by中使用
  3、二级排序，万一按照年龄排序，但是年龄same如何排序？可以Order by age asc,salary asc 多加一层排序
  	其实默认情况是会按照字典排序，就是abc的顺序 ； 或者按照物理存储顺序，主键存储顺序等等
  ```

- **limit**

  ```
  1、limit 0,20  加载从0开始的后二十条数据
  2、需要注意的点，下标从零开始，第32个数据，下标就是31
  ```

  

### ③ 多表查询

```
sql92的语法： 区分左右连接用(+),但是mysql不支持，oracle支持
select xx
from user u,user_desc u_d
where u.id = u_d.id(+)


sql99的语法  区分左右连接用left/right/in：join on
select xx
from user u
join user_desc u_d on u.id = u_d.id
where ...
```



**总结：一张图就知道各种连接了**

![image-20250920113709451](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20250920113709451.png)



**UNION 与 UNION ALL**

```
union 		就是将两个集合合并，会去除两者中重复的元素
union all   就是合并但不去除
【由于union有去重，所以性能很差，数据量大了不建议使用！！！！！】
【你可以用union all 去合并 左连接+右外连接 ，这样就避免去重了！】

例子
SELECT id, name FROM student_2024
UNION ALL
SELECT id, name FROM student_2025;

```



### ④ 单行函数

`mysql中有很多丰富的内置函数辅助我们的开发`

**我只列举自己遇到过的，其他用到自己去搜吧**

| 数值函数               | 作用               |
| ---------------------- | ------------------ |
| least(a1,a2,a3, ...)   | 返回列表中最小的值 |
| greatest(s1,s2,s3,...) | 返回列表中最大的值 |
| 用到自己去搜           |                    |
|                        |                    |
|                        |                    |

| 字符串函数       | 作用                       |
| ---------------- | -------------------------- |
| concat(s1,s2,..) | 拼接字符串                 |
| trim(s)          | 去掉字符串开头与结尾的空格 |
|                  |                            |

| 日期函数 | 作用 |
| -------- | ---- |
| NOW（）  |      |
|          |      |
|          |      |



### ⑤ 聚合函数

**什么是聚合函数**
聚合函数作用于一组数据，并对一组数据返回一个值。

**常见的五大聚合函数**

- **AVG()** ：只适用于数值类型的字段或变量。不包含NULL值

- **SUM()** ：只适用于数值类型的字段或变量。不包含NULL值

- **MAX()** ：适用于数值类型、字符串类型、日期时间类型的字段（或变量）不包含NULL值

- **MIN()** ：适用于数值类型、字符串类型、日期时间类型的字段（或变量）不包含NULL值

- **COUNT()** ：计算指定字段在查询结构中出现的个数（不包含NULL值）

  ```
  1、count(1)  count(*)   count(列名)可以计算记录总数；
  【count(1)=count(*)性能 > count(列名)】
  在innodb引擎是真的要数一遍，o(n)
  myisam是维护一个计数器
  之所以innodb要自己数而不是维护计数器，是因为要保证事务，如果有了计数器 ,可想而知，各种插入删除以及回滚操作，为了维护计数器反而开销很大！！！！！包括MVCC的机制可能每个事务看到的计数器也不一样，总之，开销以及实现就很复杂麻烦！
  ```



### ⑥ HAVING

1、如果过滤条件出现了聚合函数，不能使用where，必须使用having替换where，否则报错

2、having必须声明在group by的后面

3**、实际开发中，使用having的前提是：使用了group by**

4、having与where可以一起使用，若过滤条件没有用聚合条件用哪个都可以，但是推荐平时还是用where，因为效率高一点

```
为什么where的效率比having高？
想一想sql语句的执行顺序，因为where先过滤后分组，但是having是先分组在过滤，可能会有很多无意义的分组
```



```
(**推荐使用方式一，reason:效率高**)

方式一:    having 和 where 一起使用   
select department_id,MAX(salary)
from department
where department_id  in (10,20,30,40)
group by department_id
having  MAX(salary) > 10000;

方式二：只使用having
select department_id,MAX(salary)
from department
group by department_id
having  MAX(salary) > 10000 and department_id  in (10,20,30,40);
```



### ⑦ Group By

**一个歧义！**

```
重点：select中出现的普通字段必须声明在group by中，反之group by中声明的字段不一定出现在select

比如：
	SELECT dept_id, name, COUNT(*) 
    FROM employee
    GROUP BY dept_id;
   ❌ 问题：name 没有聚合函数，也没在 GROUP BY 里
   ✅ 正确写法：
   	SELECT dept_id, name, COUNT(*) 
    FROM employee
    GROUP BY dept_id,name;
    
why? 为什么一定要有这样的规定呢？
因为会产生歧义！
比如
dept_id  name     salary
   1      jerry   3000
   1      marry   4000
   2      jack    5000
这样就会导致分组时，有两个dept_id,数据库不知道该返回的是jerry or marry,这就导致出现了歧义

why? 为什么使用聚合函数就可以消除问题呢？
按照下面的例子，你这样就等于告诉数据库我只要每组的最大/小，这样就消除了歧义！
SELECT dept_id, MAX(name), MAX(salary)
FROM employee
GROUP BY dept_id;

IF 如果我的dept_id是主键不就不会产生歧义了吗？是的，所以在非严格模式下，你可以不遵守这个规定，你得自己确定分组会不会出现歧义！
	出现歧义会mysql会自己随机给你选一个；严格模式下会直接报错
```



**核心作用**

```
核心作用：将表中的行划分为若干组，然后对每组执行聚合或统计操作

为什么会产生之前说的歧义呢？因为我们误解了group by的作用，它分组是手段不是目的，真实目的是为了数据库搞清楚那些行属于哪一组才去分组，从而计算count,avg,sum等聚合值，也就是说计算聚合是真实目的，分组只是手段！！！
```





### ⑧ 子查询

`子查询如果嵌套多了，会比较影响性能，所以不建议你使用太多，尽可能别用吧！`



- **单行子查询**

  ```
  就是子查询返回的就是一行数据
  select *
  from employee
  where salary > (单行子查询，例如 select AVG(salary) from employee)
  ```

- **多行子查询、比较符**

  ```
  就是子查询返回的是多行数据，是一个集合
  多行子查询的比较符
  in、 any 、 all
  衍生出来了各种 >= any 、 != any 等等
  例如 
  select *
  from employee
  where salary > any (select AVG(salary) from employee group by department_id)
  ```

  

```
查询 平均工资最低的部门id 

// 先查出来平均工资
select AVG(salary) as avg_salary
from employees
group by d_id

// 查出来最低平均工资
select MIN(avg_salary)
from (
	AVG(salary) as avg_salary
    from employees
    group by d_id
) dept_avg_salary

// 查出来部门ID
select d_id
from employees e
group by d_id
having AVG(salary) = (
						select MIN(table.avg_salary)
                        from (
                            AVG(salary) as avg_salary
                            from employees
                            group by d_id
                        ) dept_avg_salary
         )
```



















































































































































































