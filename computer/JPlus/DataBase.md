[TOC]



![image-20240402151727157](C:\Users\赵联城\Ap我是障碍物pData\Roaming\Typora\typora-user-images\image-20240402151727157.png)

# Mysql基础篇



## 一.基础回顾



### 1.知识回顾

![image-20240330185847058](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240330185847058.png)



1.别名  使用单引号 '' 括起来，别用双引号！！字符串都用单引号?

2.去重   select distinct emp_id   加入 distinct

3.列的别名只能在 order by 之后使用，不能where 中使用

4.(not )bettwen and      (not) in

5.select中出现的非组函数字段必须声明在group by中，反之group by中声明的字段不一定出现在select中





### 2.单行函数

**//注意:在mysql中 单行函数可以嵌套使用，但是聚合函数不可以嵌套使用  (oracle是可以嵌套使用的)**





#### 2.1数值函数



| 个人感觉常用的函数 | 用法           |
| ------------------ | -------------- |
| ABS(x)             | 返回X的绝对值  |
| MOD(x,y)           | 返回X除以Y的值 |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |
|                    |                |



| 函数                    | 用法                                       |
| ----------------------- | ------------------------------------------ |
|                         |                                            |
| SIGN(x)                 | 返回X的符号。正数返回1，负数返回-1，0返回0 |
| PI()                    | 返回圆周率的值                             |
| CEIL(x), CEILNG(x)      | 返回大于或等于某个值的最小整数             |
| FLOOR(e1,e2,e3...)      | 返回列表中的最小值                         |
| GREATEST（e1,e2,e3...） | 返回列表中的最大值                         |
|                         |                                            |
|                         |                                            |
|                         |                                            |









### 3.聚合函数

**什么是聚合函数**
聚合函数作用于一组数据，并对一组数据返回一个值。

**常见的五大聚合函数**

- **AVG()** ：只适用于数值类型的字段或变量。不包含NULL值
- **SUM()** ：只适用于数值类型的字段或变量。不包含NULL值
- **MAX()** ：适用于数值类型、字符串类型、日期时间类型的字段（或变量）不包含NULL值
- **MIN()** ：适用于数值类型、字符串类型、日期时间类型的字段（或变量）不包含NULL值
- **COUNT()** ：计算指定字段在查询结构中出现的个数（不包含NULL值）







### 4.HAVING



**1.如果过滤条件中出现了聚合函数，就不能使用where,必须使用having来替换where,否则报错**

**2.having必须声明在group by 后面**

**3.实际开发中，使用having的前提:使用了group by**

**4.having和where可以一起使用,若过滤条件没有聚合函数用哪个都可以，但是推荐写在where中，因为效率高**



例子:查询部门id=10，20，30，40中最高工资大于一万的部门信息

方式一:    having 和 where 一起使用   (**推荐使用方式一，reason:效率高**)

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





### **5.sql执行语句顺序**



sql92:

```
SELECT .......
FROM ... , ... ,... , ...
WHERE 外连接条件  AND 不包含聚合函数的过滤条件
GROUP BY...,...,..
HAVING 包含聚合函数的过滤条件
ORDER BY ... (ASC/DESC)
LIMIT ...,...
```

sql99:

```
SELECT .......
FROM ... (LEFT / RIGHT)JOIN ... ON 外连接条件 JOIN ... ON 外连接条件
WHERE 不包含聚合函数的过滤条件
GROUP BY...,...,..
HAVING 包含聚合函数的过滤条件
ORDER BY ... (ASC/DESC)
LIMIT ...,...
```



**执行顺序**

- FROM ...   -> ON  ->  (LEFT / RIGHT) ->	  where -> group by  -> having  -> select  -> distinct  ->order by -> limit 

**//解惑:为什么where 的效率 高于 having ？**

**//因为:where 先过滤 然后再 分组  ,  但是having 会先分组(可能会有一些无意义的分组)**



![image-20240330200725613](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240330200725613.png)



### 6.子查询

**//注意:子查询  效率比较低，能用别的就用别的(比如使用自连接)，实在不行再用子查询**

![image-20240401201359936](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240401201359936.png)

#### 6.1 单行子查询

easy



#### 6.2 多行子查询

![image-20240401183115984](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240401183115984.png)



x = ANY (…)	c列中的值必须与集合中的一个或多个值匹配，以评估为true。
x != ANY (…)	c列中的值不能与集合中的一个或多个值匹配以评估为true。
x > ANY (…)	c列中的值必须大于要评估为true的集合中的最小值。
x < ANY (…)	c列中的值必须小于要评估为true的集合中的最大值。
x >= ANY (…)	c列中的值必须大于或等于要评估为true的集合中的最小值。
x <= ANY (…)	c列中的值必须小于或等于要评估为true的集合中的最大值。
———————————————

条件	描述
c > ALL(…)	c列中的值必须大于要评估为true的集合中的最大值。
c >= ALL(…)	c列中的值必须大于或等于要评估为true的集合中的最大值。
c < ALL(…)	c列中的值必须小于要评估为true的集合中的最小值。
c <= ALL(…)	c列中的值必须小于或等于要评估为true的集合中的最小值。
c <> ALL(…)	c列中的值不得等于要评估为true的集合中的任何值。
c = ALL(…)	c列中的值必须等于要评估为true的集合中的任何值。
———————————————















**//注意  在from中使用子查询 ，则必须给它起别名**

```
查询 平均工资最低的部门Id及其最低工资 (如果只要求查询部门id则需要最下面的两种方法)  
//题外话：如果是Oracle 直接秒了，因为Oracle允许聚合函数嵌套使用，可以直接 MIN(AVG(salary)),还得是付费！！！！！
select department_id,MIN(avg_sal)
from (
		select AVG(salary) avg_sal
        from employees
        group by department_id
	)   dept_avg_salary
	
查询 平均工资最低的部门id  
方法一
select department_id
from employees
group by department_id
having AVG(salary) = (
					select MIN(avg_sal)
                    from (
                            select AVG(salary) avg_sal
                            from employees
                            group by department_id
                          ) dept_avg_salary
					  )

方法二
select department_id
from employees
group by department_id
having AVG(salary) <= all (
		select AVG(salary) avg_sal
        from employees
        group by department_id
	)  
```



**空值问题**

```
select last_name
from employees
where employees_id not in (
							select manager_id
							from employees
							#where manager_id is not null  //如果里面有一个Null值就会导致整体查出来的为空！！！
							)							   //所以有的时候需要 注意空值问题

```

















#### 6.3 相关子查询

select * from emp where salary  

##### 6.3.1 一个案例

```
查询 工资大于等于 本部门平均工资 的员工信息
方式一:
select *
from employees e1
where salary >= (
				select AVG(salary)
				from employees e2
				group by department_id
				where e2.employees_id = e1.employees_id
				)
				
方式二(更常用??):
seelct *
from employees e join (
                        select department_id,AVG(salary)
                        from employees
                        group by department_id
						) t_emp_avg_sal.department_id
on e.department_id = t_emp_avg_sal.department_id
where e.salary >= xx.salary;
```





##### 6.3.2 EXISTS，NOT EXISTS



![image-20240401195603390](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240401195603390.png)



```
查询公司管理者的信息
方式一:自连接
select * 
from employees emp join employees mgr
on emp.employees_id = mgr.employees_id

方式二:子查询 (效率低)
select *
from employees
where employees_id in (
						select manager_id
						from employees
						)
						
方式三:EXISTS   (效率比较高)
select * 
from employees e1
where  EXISTS(
			select *
			from employees e2
			where e1.employees_id = e2.employees_id
			  ) 
			  
			  
一个别的案例
select department_id,department_name 
from employees e
WHERE NOT EXISTS(
								select *
								from department d
								where e.department_id = d.department_id 
								);

```





##### 6.3.3 相关更新

**//使用相关子查询依据一个表的数据来更新另外一个表的数据**



```
在employees中增加一个字段department_name，利用department表来填充数据

update employees e
set department_name = (
						select department_name
						from department d
						where e.department_id = department_id
						)

```



##### 6.3.4 相关删除

**//和相关更新差不多**

```
删除表employees中 与emp_history两者都有的数据
delete from employees e1
where employees_id in(
					select employees_id 
					from emp_history e2
					where e1.employees_id = e2.employees_id
						)
```

























##### 6.3.5 一些不错的案例



```sql
查询  平均工资最低的部门信息及其平均工资

SELECT d.* , (SELECT AVG(salary) FROM employees WHERE department_id = d.department_id) avg_sal
FROM department d
WHERE department_id = (
												SELECT department_id
												from employees
												GROUP BY department_id
												HAVING AVG(salary) <= ALL (
																			SELECT  AVG(salary)
																			from employees
																			GROUP BY department_id
																		 )
											);
											
			//其实还可以使用Limit								
SELECT d.* , (SELECT AVG(salary) FROM employees WHERE department_id = d.department_id) avg_sal
FROM department d
WHERE department_id = (
												SELECT department_id
												from employees
												GROUP BY department_id
												HAVING AVG(salary) <= ALL (
																			SELECT  AVG(salary) a_sal
																			from employees
																			GROUP BY department_id
                                                    						ORDER BY a_sal
                                                    						LIMIT 0,1
																		 )
											);

```







### 7.视图

**//大项目用的多，小项目用的少**

**本质就是存储起来的sql语句,视图不是表，不直接存储数据，是一张虚拟的表；**



**创建视图**	CREATE VIEW 视图名(列1，列2...) AS SELECT (列1，列2...) FROM ...;
**使用视图**	当成表使用就好
**修改视图**	CREATE OR REPLACE VIEW 视图名 AS SELECT [...] FROM [...];
查看数据库已有视图	>SHOW TABLES [like...];（可以使用模糊查找）
查看视图详情	DESC 视图名或者SHOW FIELDS FROM 视图名
视图条件限制	[WITH CHECK OPTION]





### 8.GLOBAL与SESSION系统变量的使用



#### 8.1什么是系统变量？

系统变量分为全局系统变量(需要添加global关键字)和会话系统变量(需要添加session关键字)，有时把全局系统变量称为全局变量，会话变量称为Local变量。**如果不指定，默认会话级别。**

每一个Mysql客户端成功连接Mysql服务器之后，都会产生与之对应的会话。会话期间，Mysql服务实例会在Mysql服务器内存中生成与该会话对应的会话系统变量，这些会话系统变量的初始值是全局系统变量的复制。



![image-20240424125223015](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240424125223015.png)



- 全局系统变量针对所有会话(连接)有效，**但不能跨重启**,一旦重启就全部失效
- 会话系统变量只针对当前会话(连接)有效，连接期间修改也只改变当前会话

#### 8.2查看系统变量



查看系统变量

```mysql
//1.查询全部系统变量
SHOW SESSION/GLOBAL VARIABLES; 
//2.查询部分系统变量
SHOW @@session/global VARIABLES LIKE '%XXX%' --@@XXX 表示系统变量   @XX表示用户自定义变量

//3.查询指定系统变量
SELECT @@global.max_connections;

```



#### 8.3永久修改系统变量

**//方法一：去这里面修改配置文件(此方法需要重启mysql服务，在实际生产代价比较大)**

![image-20240424131315891](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240424131315891.png)

**//方法二：在mysql运行期间，使用‘set'指令重新设置系统变量的值,（重启mysql服务就会失效）**

```
SET @@global.max_connections = 111; // SET GLOBAL max_connections = 111;

```





### 9.用户自定义变量



#### 9.1什么是用户自定义变量?

用户变量是用户自定义的，作为mysql编码规范，Mysql中的用户变量以一个@开头，根据作用范围不同，又可以分为会话用户变量，和局部变量

- 会话用户变量，只对当前会话有效
- 局部变量，只在BEGIN和END语句有效。**局部变量只能在存储函数和函数中使用**







### 10.类型





#### 1.整数

![在这里插入图片描述](https://gitee.com/vulnerable5481/typora-img/raw/master/img/641cba90fbb146a383d8ccc273b25791.png)

 应用场景

（1）TINYINT ：一般用于枚举数据，比如系统设定取值范围很小且固定的场景。
（2）SMALLINT ：可以用于较小范围的统计数据，比如统计工厂的固定资产库存数量等。
（3）MEDIUMINT ：用于较大整数的计算，比如车站每日的客流量等。
（4）INT、INTEGER ：取值范围足够大，一般情况下不用考虑超限问题，用得最多。比如商品编号。
（5）BIGINT ：只有当你处理特别巨大的整数时才会用到。比如双十一的交易量、大型门户网站点击量、证券公司衍生产品持仓等。





#### 2.定点类型

**定点类型已经取代浮点类型**

只使用 decimal   

decimal(M,D):		其中，M被称为精度，D被称为标度。0<=M<=65， 0<=D<=30，D<M。
例如，定义DECIMAL（5,2）的类型，表示该列取值范围是-999.99~999.99。





#### 3.位类型

**//用的比较少**



#### 4.**日期与时间类型**

只使用datatime就可以了

DATETIME 类型通常用来表示年、月、日、时、分、秒

![image-20240501143739014](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501143739014.png)



**但是在实际项目中，尽量用 DATETIME 类型**。因为这个数据类型包括了完整的日期和时间信息，取值范围也最大，使用起来比较方便。毕竟，如果日期时间信息分散在好几个字段，很不容易记，而且查询的时候，SQL 语句也会更加复杂。



此外，**一般存注册时间、商品发布时间等，不建议使用DATETIME存储，而是使用时间戳** ，因为DATETIME虽然直观，但不便于计算。





#### 5.文本类型

MySQL中，文本字符串总体上分为 CHAR 、VARCHAR 、 TINYTEXT 、 TEXT 、 MEDIUMTEXT 、LONGTEXT 、 ENUM 、 SET 等类型。

- **char(M) , varchar(M)** 就没什么可以说的了,M就是几个字节,**如果不指定(M)，则表示长度默认是1个字符**。

- ![image-20240501144226209](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501144226209.png)
- 
- **总结：**
  TEXT文本类型，可以存比较大的文本段，搜索速度稍慢，**因此如果不是特别大的内容，建议使用CHAR， VARCHAR来代替。**还有TEXT类型不用加默认值，加了也没用。而且text和blob类型的数据删除后容易导致“空洞”，使得文件碎片比较多，**所以频繁使用的表不建议包含TEXT类型字段，建议单独分出去，单独用一个表。**





#### 6.**JSON类型**



#### 7.还有一些不怎么用的懒得列举





# Mysql高级篇





## 1.linux下安装mysql8.0



**//挺麻烦的，直接去看视频，有空自己总结下来，还是很有帮助的!**









## 2.mysql8.0与5.7的一些区别和一些小知识





### 2.1字符集

**结论:mysql8.0很多重要的表默认字符集是utf8 , mysql5.7很多重要的表默认是latin**

​		**这就导致5.7如果不做修改直接添加中文会失败，而8.0则不会**

**//表的默认字符集关键就是character_set_server和character_set_database的字符集是什么,而character_set_server是数据库级别，会影响character_set_database，所以只需要修改character_set_server**



**//8.0**

![image-20240423214210994](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240423214210994.png)



**//5.7**

![image-20240423213853913](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240423213853913.png)





**在基础篇我们已经修改过，但是在linux环境下如何修改呢？**

只需要修改5.7的/etc/my.cnf,在随便位置(建议直接写在最后面)添加 character_set_server=utf8

//但是已创建的数据库(表默认跟随数据库的字符集)还是不变 

//如图所示

![image-20240423214932139](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240423214932139.png)







关于字符集的一些知识:

各级别的字符集

- 服务器级别
- 数据库级别
- 表级别
- 列级别

如果不想跟随上级的字符集，可以自己单独去修改字段之类的去操作.





### 2.2sql规范

window不区分大小写,linux表名，别名，字段名，数据库名等等一些名字会区分大小写

**//企业规范：凡是关键字;函数名称都大写，名字别名都小写;sql语句必须以分号结尾**





### 2.3sql_mode

宽松模式VS严格模式



最经典的问题

SELECT name,dep,age,MAX(salary)

FROM emp

GROUP BY dep

**select中的非聚合字段必须出现在 group by 中，还记得吗！**



**//开发中我们使用的是严格模式**





### 2.4文件系统中的表示

**//关于文件系统中的表示windows和linux都是一样的**





#### 2.4.1 InnoDB存储引擎下的5.7与8.0的区别

**5.7**

**//db.opt存放字符集和比较规则**

![image-20240424134421597](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240424134421597.png)

![image-20240424134540571](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240424134540571.png)







**//8.0**

**//.ibd和.frm合二为一成.ibd   	**

![image-20240424134811271](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240424134811271.png)













#### 2.4.2MyISAM存储引擎模式

**//MyISAM存储引擎下5.7和8.0区别不是很大**





**//5.7**

![image-20240424135327392](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240424135327392.png)



**//8.0**

**/.sdi 就是 .frm**

![image-20240424135341730](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240424135341730.png)





#### 2.4.3总结



```
//InnoDB 5.7
产生一个db.opt:保存数据库的相关配置，比如字符集，比较规则等 (5.7提供，8.0也不再提供)
产生一个.frm:存放表结构
产生一个.ibd:存放表数据(采用独立表结构才会生成)
如果使用系统表空间存储模式，则数据信息和索引信息都存储在idata1(默认12MB，会跟随数据变大而变大)中
如果使用独立表空间存储模式，则会表数据存放到.ibd
！！！！5.7之前默认是系统表空间存储模式！！！5.7及其之后默认采用独立表空间存储模式!!!!

//InnoDB 8.0
产生一个.ibd:表结构，表数据，数据库相关配置都存放在此!!!三合一！！

//MyISAM 5.7 与 8.0 区别不是很大！
//MyISAM 5.7  
产生一个.frm
产生一个.MYD   存放表数据(如果采用独立表空间模式)
产生一个.MYI   存放索引信息文件


//MyISAM 8.0
产生一个.sdi   //这个就是.frm 放表结构的
产生一个.MYD   存放表数据(如果采用独立表空间模式)
产生一个.MYI   存放索引信息文件
```







## 3.用户管理与权限

**//下文中 用户都默认是 'username'@'%',简单使用 用户 两个字 替代**





### 3.1用户管理相关操作



```
//1.登录用户
mysql -u username -h localhost -P 3306 -p

//2.创建用户
若用户已存在则报错，username和host共同作为联合主键，即使username一样,host不一样也算两个用户
CREATE USER 'username'@'host' IDENTIFIED BY '密码'

//3.修改用户
若已经use mysql 就可以直接update user set xxx;
UPDATE mysql.user SET USER = 'username' (and host = 'host' ) //默认host为 %
FLUSH PRIVILEGES 

//4.删除用户
DROP USER username1,username2.....//默认host为%,建议加上@'host'

//5.修改用户密码

```



### 3.2权限相关操作



```
//1.授予权限
grant select,update on 数据库名字.*/表名 to 'zlc'@'%';

//2.授予用户zlc所有权限
注意唯独一个权限with grant option 没有给，那就是赋权限给其他用户，也就是说zlc不能控制别人的权限
grant all privileges on *.* to 'zlc'@'%' identified by '密码';

//3.查看权限
show grants; //查看当前用户权限
show grants for 'username'@'host';//root下查看用户权限

//4.收回权限
revoke 权限1，权限2.... on 数据库名.*/表名 from 'username'@'host';
revoke all privileges om *.* from xxx;
```









### 3.3权限表

**//本章节是对前面两节底层实现的讲解**

mysql服务器通过**权限表**来控制用户对数据库的访问，**权限表存放在初始四个数据库中的mysql库中**.mysql数据库系统会根据这些权限表的内容为每个用户赋予权限。这些权限表中最重要的是user表，db表。此外还有table_priv表(表权限)，colimn_priv表（列权限)和proc_priv表（过程权限表）。msyql启动时，服务器会将这些数据表中的权限信息读入内存中。 











### 3.4角色管理

**//mysql8.0引入的新功能，人家oracle早就有了  !  ! **



**角色管理相关操作**

```
//1.创建角色
create role '角色名字';

//2.给角色赋予权限 
//3.查看角色权限
除了 show grants for xxx  还可以直接查看当前角色是什么 select current_role();
//4.回收角色权限
没什么区别
	

```



**赋予用户角色相关操作**

```
//1.赋予用户角色
grant '角色'@‘%’ to 'xxx'@'xxx';

//2.激活角色
赋予完用户角色，不会生效，必须激活,然后重新登录才能生效!
set default role '角色名'@'%' to ’xx'@'xxx';


//3.撤销角色
revoke '角色'@'XX' from 'xx'@'xx';

//4.设置强制角色(这个和我这种配角没什么关系把)
强制角色是给每个创建账户的默认角色，不需要手动设置。强制角色无法被revoke或drop;
//4.1 方式1：服务启动前设置
[mysqlId]
//4.2 方式2：启动时设置

```



## 4.逻辑架构





### 4.1 逻辑架构总览

![image-20240424202922949](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240424202922949.png)





**//非常经典的Mysql5.7 流程分析图，8.0略有区别，好像是缓存相关没了，因为实际中缓存命中率很低且占用多**

![image-20240425125103233](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425125103233.png)



**//三层：连接层，服务层，引擎层**

![image-20240425125252818](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425125252818.png)











### 4.2 SQL执行流程



![image-20240425125848180](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425125848180.png)

![image-20240425130710081](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425130710081.png)



### 4.3查询执行流程相关操作(弃用)

**//使用EXPLAIN替代**

```
//1.查看profiling
select @@profiling;

//2.设置profiling
set @@profiling = 1;

//3.查看所有执行流程
show profiles;

//4.根据所有执行流程表的序号来查看指定流程
show profile [type 比如cpu什么的] for query 序号;
例子
show profile cpu for query 5;
```







## 5.存储引擎



### 5.1什么是存储引擎？

为了管理方便，人们将<font color="red">连接管理，查询缓存，语法解析，查询优化</font>,这些并不涉及真实数据的功能划分为<font color="red">Mysql server</font>功能，把真实存取数据的功能划分为**存储引擎**的功能。所以在Mysql server完成了查询优化后，只需要按照生成的**执行计划**调用底层**存储引擎提供的API**，获取到数据返回给客户端就好了。

简而言之，存储引擎就是表的类型，它的功能就是接收上层传下来的命令，然后对表中数据进行提取/写入操作。



### 5.2 InnoDB存储引擎

**//直接上结论：没特别情况优先使用InnoDB**



**特点** ：

- **支持事务**
- 性能优势,专门处理巨大数据量





### 5.3 MYISAM存储引擎



**特点**：

- 不支持事务，崩溃无法恢复
- 只适合处理数据量小的表





### 5.4 对比

![image-20240425135427309](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425135427309.png)





## 6.索引⭐



### 6.1 索引概述及其优缺点



- ​	<font color="red">索引的概述</font>
  -  索引的**定义**是**帮助Mysql高效获取数据的数据结构**，可以根据这些数据结构的基础实现高级查找算法
    **索引是在存储引擎中实现的**，因此每种存储引擎的索引不一定完全相同。
- <font color="red">索引的优点</font>:
  - **降低数据库IO成本**，这也是创建索引的最主要原因
  - 通过创建唯一索引，**保证每一数据的唯一性**
  - **加速表与表之间的连接**。（对于有依赖关系的子表和父表联合查询时，可以提高查询速度）
  - 使用分组和排序子句进行查询时，可以**显著减少查询中分组和排序的时间**
- <font color="red">索引的缺点</font>
  - 创建和维护索引要耗费时间
  - 索引需要占用磁盘空间
  - 索引虽然大大提高查询速度，但是会降低增删改的速度





### 6.2设计索引



#### **1.一个简单索引**

![image-20240425143837410](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425143837410.png)

 



#### **2.迭代一次：目录项记录的页**

![image-20240425150058248](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425150058248.png)





#### **3.迭代两次：多个目录项记录的页**



略



#### **4.迭代三次：向外又拓展了一个级别**



![image-20240425150645141](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425150645141.png)







#### 5.B+Tree



![](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425151042504.png)

![image-20240425151117613](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425151117613.png)



### 6.3常见索引概念

索引按照物理实现方式，可以分为两种：聚簇索引（聚集索引）和非聚簇索引（非聚集索引）。我们也把非聚集索引称为二级索引/辅助索引。





#### 1.聚簇索引

**//聚簇索引中，索引即数据，数据即索引。**

**//特点：**

- 使用主键值进行记录和页的排序

  - 页内的记录是按照主键的大小顺序排成一个**单向链表**

  - 各个存放用户记录的页也是根据页中用户记录的主键大小顺序排成一个**双向链表**

  - 存放目录项记录的页也分为不同的层次，在同一层次页是根据页内主键大小排成一个**双向链表**

- B+树的**叶子节点**存放的是**完整的用户记录**

**//优点：**

- **自动根据主键生成**，不需要手动创建。
- **数据访问速度快**。因为索引和数据放在同一个B+树
- **查询速度快**。节省了大量的IO操作



**//限制：**

- MYSQL只对InnoDB支持聚簇索引，MYISAM不支持
- **每个MYSQL的表只能由一个聚簇索引，一般情况就是该表的主键。**
- 如果没有主键，InnoDB会选择非空的唯一索引 替代。如果也没有这样的索引，innoDB会隐式地定义一个主键作为聚簇索
- 聚簇索引不建议选择无法自增且有序的字段，不要随意修改聚簇索引(一般是主键)的值，让其自增。







#### 2.二级索引/辅助索引

**//非主键的索引就是二级索引**

**二级索引演示**：加入以c2作为二级索引，再建造一颗以c2为key，c1为value的B+树。

​							此时我们需要select c1,c2,c3 from table_test where c2 = 4;

​							我们根据这棵树找到c2=4，为了查到c3还需要回表，即以c1为key建造的B+树去查完整的数据

​							这时我们就能快速得到我们想要的数据了！

**总结:**  	当我们select * from xxx where 字段1 = xxx;

​				如果字段不是主键，那就不能使用聚簇索引了，这时候我们构造二级索引--->通过再建造一颗以xx字段为Key,主键为value的				B+树 ，  然后通过‘回表’的操作再通过 聚簇索引 查到完整的数据即可！

![image-20240425155911736](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425155911736.png)



![image-20240425160456065](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425160456065.png)









#### 3.联合索引

很多场景中，我们会以多个字段组成一个联合字段来当key 创建B+树，本质也是一个二级索引，只不过二级索引当中页里面的数据是按照联合字段来构建的！

比如 alter table xxx index idx_age_classId_name(age,classId,name),B+树中就首先按照age建立树，然后age一样的按照classId排序,classId一样的按照name排序，最后存放的是主键。







### 6.4 InnoDB中B+树注意事项



#### 1.根页面位置万年不动



**//解释：最开始B+树只有一个空的根页面，当数据进来就放到根页面，直到根页面满了之后又来了一条数据，此时复制根页面中所有数据到另一个地方，此时根页面充当目录项页，记录第一个空间的最小key；数据不断进入，很快根页面保存的目录项页也满了，这时复制根页面中数据到另一个地方，此时根页面充当更高一级的目录项页，新生成的地方就用于存放目录项页,此时B+树就有了三层结构。**



![image-20240425161930456](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425161930456.png)





#### 2.内节点中目录项记录的唯一性

这才是创建二级索引后的B+树的正确样子，前面省略了主键值!!!!!!!!!!

![image-20240425162721472](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425162721472.png)





#### 3.一个页面最少存储2条记录	









### 6.5 Mysql数据结构选择的合理性







#### 1.全表遍历



略。



#### 2.Hash结构



虽然查询速度比B+树还快，达到了常量级，但是缺点太多了，比如存储没有顺序，重复值多效率很低之类的；

Hash索引存在很多限制，相比之下B+树的应用场景更广，不过也有一些场景采用Hash索引效率更高，比如键值型数据库中，Redis存储的核心就是Hash表

![image-20240425164951610](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425164951610.png)







#### 3.二叉搜索树



二叉搜索树分层太多了，每一层都需要磁盘IO读写操作，容易产生二叉搜索树分层太多导致退化成链表的问题。



#### 4.平衡二叉树/AVL树

为了解决二叉搜索树分层太多退化成链表的问题，AVL树诞生了



虽然平衡二叉树的效率比二叉搜索树高很多，但是依然需要不少的磁盘IO操作！



#### 5.多路平衡查找树/B-树

AVL树的进化，进化在哪了？不止是二叉，而是可以分很多分叉



**B树和B+树的区别：B树非叶子节点也保存数据，B+树非叶子节点保存的是目录项，而非数据本身，需要根据目录项再去二分查找出真数据。**



![image-20240425165653903](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425165653903.png)





#### 6.B+树

基于B树的改进，B+树更适合文件索引系统。

**B树和B+树的区别：B树非叶子节点也保存数据，B+树非叶子节点保存的是目录项，而非数据本身，需要根据目录项再去二分查找出真数据。**





#### 7.R树

只支持geometry类型

用于解决查找20英里内的所有餐厅之类的





### 6.6 InnoDB数据存储结构





#### 1. 页概述

- 概述
  - 磁盘与内存交互**基本单位**：页
  - 不同数据库管理系统的页大小不同,InnoDB默认是16KB
  - ![image-20240425171519158](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425171519158.png)





#### 2.页的上层结构

![image-20240425172608527](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425172608527.png)



![image-20240425172651255](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425172651255.png)





#### 3.页的内部结构



![image-20240425174708631](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425174708631.png)





















#### 4.InnoDB行格式(行记录格式)

![image-20240425180134048](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240425180134048.png)









### 6.7 索引的创建与设计原则 



#### 1.索引分类

略



#### 2.索引相关操作



创建

``` 
//1.1创建表时，隐式创建索引
primary key / unique /外键   这三个约束都会隐式的创建索引

//1.2创建表时，显示创建索引   //关键字可以是index 也可以是key，推荐使用index
//普通索引
create table test_table(id int,name varchar(255),INDEX/KEY 索引名字(字段名字));
//唯一索引
xxxxxxxxxxxxxxxxxxxxxxx(xxxxxxxxxxxxxxxxxx,unique index/key 索引名字(字段名字));
//联合索引
xxxxxxxxxxxxxxxxxxxxxxx(xxxxxxxxxxxxxxxxxx,index/key 索引名字(字段名字1,字段名字2));

//2创建表后，添加索引

ALTER TABLE 表名 ADD INDEX 索引名字(字段)；
CREATE TABLE 表名 ON INDEX 索引名字(字段)；

//3.使用字符串前缀作为索引
//如果使用过长的字符串作为索引会很浪费效率，所以我们采用字符串的一部分作为索引
//那到底取多长呢？ 按照公式计算 count(distinct left(列名，索引长度))/count(*)
//一般取长度为20作为前缀 都可以达到90以上的区分度
//如果出现相同前缀，那就回表通过详细数据具体区分。
//但是使用字符串前缀作为索引，就不能排序了。
alter table xxx add index xxx(xxx(20));
```

查看

```
//1.show create table xxxx;

//2.show index from xxxx;
```



删除

```
//1.ALTER TABLE 表名 DROP INDEX 索引名字；
//2.DROP INDEX 索引名 ON 表名;

//注意  添加auto_increment约束的唯一索引是不能删除的！！！ 
```



#### 3.Mysql8.0索引新特性

**//用到再说吧！**

##### 1.降序索引

创建联合索引时可以给予第二个字段desc选择降序



##### 2.隐藏索引





#### 4.适合添加索引的十一种常见情况



- 字段的数值有唯一性的约束 ； 添加主键/unique	
- 频繁作为where 条件 的字段； 创建普通索引就可以大大提高效率
- distinct
- 经常group by 和 order by 的字段：可以创建索引，如果既有分组又有排序/单个分组或排序有多个字段都可以建立联合索引
- **最左前缀原则：最频繁的字段放在最左边，比如联合索引**
- 多个字段都要创建索引，联合索引>单个索引





#### 5.注意事项



- 单表的索引不建议超过6个
- 数据量小的表(小于一千)不建议创建索引
- 避免对频繁更新的字段创建索引
- 频繁更新的表也少创建索引











### 6.8 EXPLAIN性能分析





#### 1.查询系统性能参数(了解)



![image-20240426122338719](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240426122338719.png)









#### 2.查询sql性能（了解）



##### 2.1 查询上一条sql成本

```
//1.查询上一条sql的性能
show stauts like 'last_query_cost'
```



##### 2.2 查询所有/某个sql成本

```
//1.查看profiling
select @@profiling;

//2.设置profiling
set @@profiling = 1;

//3.查看所有执行流程
show profiles;

//4.根据所有执行流程表的序号来查看指定流程
show profile [type 比如cpu什么的] for query 序号;
例子
show profile cpu for query 5;
```





##### 2.3慢查询

**//默认是关闭的，非调优需要，一般是不需要开启的，会浪费部分性能**



```
//1.查询慢查询日志参数
show variables like 'slow_query_log';
set @@global.slow_query_log='on';

//2.查询慢查询的时间阈值
show variables like 'long_query_time';
set @@global.long_query_time=xx;  //单位秒

//3.释放慢查询日志
手动删除，一般该日志文件都在 /var/lib/mysql下面  一个xxx.log的文件，将其删除即可

//4.初始化慢查询日志文件
mysqladmin -uroot -p flush-logs slow; //如果不加slow就会将所有日志文件都初始化
```







#### 3.EXPLAIN⭐



**//explain是干什么的？一句话，就是查看优化器的优化方案，比如sql的执行顺序，哪些索引被使用,多表连接的顺序**





#### 3.1基本语法



explain SQL语句;

**//该sql不会真正执行**



#### 3.2EXPLAIN各列作用

![image-20240426165954067](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240426165954067.png)







//一个细节  如果Key1 是 varchar类型  ，但是 xxx where key1 = 10005 ,没有加单引号，此时10005是int类型，底层会应用函数隐式转换，**应用函数后就不再使用索引.**



- table
  -   不止是用到的表，还可能存在临时表和中间表
- id
  - id就是为不同的select语句分序，如果ID相同就说明优化器将子查询优化成多表查询
- select_type            (查询类型，挺多的用到再说吧)
  - 查询类型，挺多的用到再说吧
- type⭐
  - system(只有一条数据) 
  - const(根据主键/一二级索引   与    常数进行等值匹配),xxxx where id = 1;
  - eq_ref (根据主键/一二级索引   与  主键/索引等值匹配) xxx where s1.id = s2.id;
  - ref （根据二级索引      与     常量/ 二级索引）
  - ref or null (二级索引     与      常量/二级索引/null)  多了个Null
  - index_merge  (使用了union,intersection,sort-union这三种索引合并的场景)
  - unique_subquery (针对包含IN子查询的语句，如果查询优化器将IN子查询 优化 成EXISTS子查询，而且子查询可以使用到主键进行等值判断，那么该select_tyupe就是unique_subquery)
  - range    （范围级别）  where key1 > 3   /   key1 in (  x,x,x,x );
  - //////////////////////////////////////////////////////////////////////////////////////////////////////////////
  - index  (当我们可以使用索引覆盖，但需要扫描全部的索引记录时)
  - all
  - 

![image-20240428132359612](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240428132359612.png)

- key_len 的计算  比如索引 idx_age(age) 
  ![image-20240501151129832](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501151129832.png)
- extra ： 里面也会包含很多重要信息！





### 6.9索引优化与查询优化

**//直接结论：下面所有的索引失效情况都可以根据B+树推演出来**







#### 1.索引失效的情况



- 全局索引我最爱
  - 索引1: index(age) 索引2:index(age,classId),索引3:index(age,classId,name),如果查询很明显索引3优先级最高，2和1会失效。

- 最左前缀原则,违反则失效
- 计算，函数(自动/手动)都将导致索引失效
- 类型转换
  - 如果Key1 是 varchar类型  ，但是 xxx where key1 = 10005 ,没有加单引号，此时10005是int类型，底层会应用函数隐式转换，**应用函数后就不再使用索引.**
- 范围条件右边的列索引失效
  - alter table xxx index idx_age_classId_name(age,classId,name)
    select * from student  where student.age = 30 and **student.classId > 20** and student.name like 'a%';
    此时中间是范围条件，所以右边的列索引就失效了，只有age和classId起到索引的效果 
  - **将范围查询条件放在联合索引中的最后**
  - 像实际开发中金额，创建时间什么的都经常要范围搜索，应该为了看起来规整，最好将其放到where语句的最后

- 不等于(!= / <>)索引失效
  - 动脑子想一想，联想一下B+树，等于很简单可以直接搜索找到，但是不等于你怎么快速找到？所以此时索引就没什么用了
- 同理 is null 可以索引，is not null 不可以索引
- like以通配符%开头 索引失效
  - 只要联想一下B+树就明白了，你开头都不知道，还这么查B+树？
  - 阿里巴巴开发手册严禁左模糊或者全模糊
- or前后存在非索引的列，索引失效
  - 联想B+树 ， easy
- 









#### 2.关联查询优化



例子 select * from s1 join s2 on s1.id = s2.id  还是 select * from s2 join s1 on xxx = xxx;

直接上结论：谁有索引谁是被驱动表，都有索引则**小表驱动大表**。 （稍微模拟一下过程即可退出)







#### 3.子查询优化

尽量不要使用 not in  / not exists  而是用 left join xxx on  xxx where xx is null 替代



**//尽量使用关联查询  替代  子查询， 因为子查询可能会涉及到临时表，临时表可没有索引，效率就很低**







#### 4.排序优化

在mysql中排序有两种，filesort和index

- index排序，索引可以保证数据的有序性，不需要在进行排序，效率更高。
- filesort排序，一般在内存中进行排序，占用CPU较多，如果待排结果较大,会产生临时文件I/O到磁盘进行排序，效率较低。
  - 算法一：双路排序(慢)       mysql4.1之前默认是这个算法
    比如order by age 没有索引就fielsort , 第一次将age读取到内存进行排序，然后根据排序后的age去第二次读取完整列数据到内存
  - 算法二:   单路排序(快,但占用更多内存,总体优于双路排序)       后面版本默认单路排序，除非无法使用单路排序才使用双路排序
    比如order by age 没有索引就firesort.第一次就直接将所有列读取到内存进行排序


**所以尽量使用index排序，如果使用filesort排序，也得对其进行优化**



**//排序过滤失效的原因**

- ![image-20240428201928162](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240428201928162.png)
  想一想B+树结构
  不一定，没有过滤排序也可能使用索引，这就是后面要学的覆盖索引
  
- order by时 不Limit 索引失效
  - index idx_age_classid_name(x,x,x);
    select * from xx order by age,classid   ,此时会使用索引吗？？
    答案是否定的,因为你使用索引排序还要回表什么的，数据量一大就很麻烦，优化器认为还不如直接filesort方便
    那为什么加上Limit 索引就有效了呢？因为加了Limit 一次性排序的数据量有限制了，虽然要回表，但是应该会比filesort快

- order by 规则不一致 索引失效
  - order by age desc ,name asc 这样就是错误的,优化器认为这样逆着来还不如直接filesort

**//总结：没有过滤条件 一律不索引！  没有limit 联合索引无效**

**//视频结论与实际结论相冲突！！！！！**







#### 5.group by优化

- 和order by 差不多，**group by 即使没有过滤条件也能 使用索引**

- **where 效率高于 having，能写在where的限定数据就不要写在having中**
- 包含order by , group by , distinct的这些查询语句，where过滤的条件尽可能保持在一千以内，否则sql会很慢



#### 6.分页查询优化

一般分页查询时，通过创建覆盖索引能够比较友好地提高性能。一个常见的问题：select x  from x limit 200000 10

为了查询第二十万之后的十条数据，需要白白浪费查询二十万的性能，这绝对不能接受！！！！



优化思路一:    在索引上完成排序分页操作，最后根据主键关联回表查询出需要的数据

​					select x,x,x,(select id from x) as 'a'   from xyz where xyz.id = a.id 

优化思路二：  

​					该方案适用于主键自增的表，可以把limit查询换成某个位置的查询

​					select * from xx where id > 200000 limit 10





#### 7.优先考虑覆盖索引



什么是覆盖索引?

答：就是直接返回二级索引，要查询的东西直接就在二级索引可以全部找到，就没必要回表，可以直接返回，这就是覆盖索引



**//覆盖索引可能导致前面的一些结论被推翻！！！！比如order by 无过滤不索引，和 != /is not null 不使用索引**





覆盖索引的利：

​							利：显著提高性能





#### 8.索引下推(ICP)

查完一个索引紧接着查询下一个索引











#### 9.其他优化策略



- exists 和 in 的区别
  - 直接结论：小表驱动大表
  - 例子： a表数据量 < b表数据量  ----> select *  from id  exsits (select id from b where a.id = b.id)
                a表数据量 > b表数据量   ---->  select * from id in (select id from b)



- 确定只有一条数据时，可以加上Limit 1 这样找到第一条数据后就会停下来，提高效率。
- 结束一个业务时，多commit，能释放资源，释放锁，提高效率







### 6.10 全局主键Id







## 7.数据库设计





### 7.1范式



#### 1什么是范式？



- **概念**：关于数据表设计的基本原则，规则就称为范式。英文简称 normal form 即 NF





#### 2范式都包括哪些

- ![image-20240430202956661](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240430202956661.png)





#### 3键和相关属性的概念



- **超键**  ： 能唯一标识元组的属性集就叫超键  ,  比如 学生Id + name 就可以唯一标识某一个学生，这样的组合就是超键
- **候选键**： 一句话，如果超键中不包括多余的属性，那么这个超键盘就是候选键。比如 学生Id可以是候选键，身份证也可以是候选键。但是两者组合不是，因为都可以唯一标识就有一个是多余的 ，加个 age classId 什么的也是多余属性
- **主键**： 从候选键中选一个当作主键，主键只能有一个，候选键可以有多个
- **外键**：如果一个表R1中的某属性不是R1的主键，但却是R2的主键，那么这个属性就是外键
- **主属性**：包含任一候选键 就是 主属性
- **非主属性**：不包含任一候选键

通常我们也将候选键称之为**“码”**，把主键称之为**“主码”**。



#### 4 第一范式(1st NF)

**第一范式的要求：字段必须具有原子性，即字段x 不能被 拆分成 x1 ,x2**



反例1：此处的员工手机号可能有两个，不应该存在同一条数据中，应该按照手机号分成两条数据

![image-20240430204511335](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240430204511335.png)



反例3：也不是一定要拆分，有的就没必要拆

![image-20240430204752892](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240430204752892.png)







#### 5第二范式

**除了满足第一范式，每一条数据都要唯一标识，而且所有非主键字段，都必须完全依赖主键，不能只依赖主键的一部分**



例子:  表属性有 球员id , name , age ,比赛编号，比赛时间，比赛场地，球员编号，比赛编号，得分。

​			上述并不符合第二范式，可以进行将其变成三张表

​			

| 球员表             | 球员编号，姓名，年龄等个人信息             |
| ------------------ | ------------------------------------------ |
| **比赛表**         | **比赛编号，比赛时间，比赛场地等比赛信息** |
| **球员比赛关系表** | **比赛编号，球员编号，得分等信息**         |



![image-20240430212114786](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240430212114786.png)







#### 6第三范式	

**要求数据表中的所有非主键字段不能依赖其他非主键字段**

比如，有一张员工表，有员工id , name , age ,dress ,部门id 

​			以上是满足第三范式的，但是如果继续添加部门相关信息，如部门name就违反了第三范式





#### 7 实战演练

**//请对下面进口信息设计数据库**

![image-20240430214109322](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240430214109322.png)





**//第一范式**

![image-20240430213342626](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240430213342626.png)

**//第二范式:**

![image-20240430213408088](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240430213408088.png)







#### 8拓展之反范式化

业务优先，很好理解。并不一定要遵循范式的规则





#### 9拓展之其他范式





### 7.2 ER模型





#### 1.什么是ER模型？

数据库设计是牵一发而动全身的。那有没有什么办法提前看到数据库的全貌呢?比如需要哪些数据表、数据表中应该有哪些字段，数据表与数据表之间有什么关系、通过什么字段进行连接，等等。这样我们才能进行整体的梳理和设计。
其实，ER 模型就是一个这样的工具。**ER 模型也叫作 实体关系模型** ，是用来描述现实生活中客观存在的事物、事物的属性，以及事物之间关系的一种数据模型。**在开发基于数据库的信息系统的设计阶段，通常使用 ER 模型来描述信息需求和信息特性，帮助我们理清业务逻辑，从而设计出优秀的数据库。**



#### 2.ER模型包含那些要素？

ER 模型中有三个要素，分别是实体、属性和关系,
**实体** ，可以看做是数据对象，往往对应于现实生活中的真实存在的个体。在 ER 模型中，用 **矩形** 来表示。实体分为两类，分别是 强实体 和 弱实体 。强实体是指不依赖于其他实体的实体;弱实体是指对另一个实体有很强的依赖关系的实体。
**属性**，则是指实体的特性。比如超市的地址、联系电话、员工数等。在 ER 模型中用 **椭圆形** 来表示。

**关系**，则是指实体之间的联系。比如超市把商品卖给顾客，就是一种超市与顾客之间的联系。在 ER 模型中用 **菱形** 来表示。

**注意**:实体和属性不容易区分。这里提供一个原则:我们要从系统整体的角度出发去看，可以独立存在的是实体，不可再分的是属性。也就是说，属性不能包含其他属性。







#### 3.建模分析

![image-20240501122953845](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501122953845.png)

在这个图中，地址和用户之间的添加关系，是一对多的关系，而商品和商品详情示一对1的关系，商品和订单是多对多的关系。 这个 ER 模型，包括了 8个实体之间的 8种关系。
(1)用户可以在电商平台添加多个地址;
(2)用户只能拥有一个购物车;
(3)用户可以生成多个订单;
(4)用户可以发表多条评论;
(5)一件商品可以有多条评论;
(6)每一个商品分类包含多种商品
(7)一个订单可以包含多个商品，一个商品可以在多个订单里。
(8)订单中又包含多个订单详情，因为一个订单中可能包含不同种类的商品



#### 4.ER模型建模的细化

有了这个 ER 模型，我们就可以从整体上 理解 电商的业务了。刚刚的 ER 模型展示了电商业务的框架，但是只包括了订单，地址，用户，购物车，评论，商品，商品分类和订单详情这八个实体，以及它们之间的关系，**还不能对应到具体的表，以及表与表之间的关联。我们需要把 属性加上 ，用 椭圆 来表示，这样我们得到的 ER 模型就更加完整了**
因此，我们需要进一步去设计一下这个 ER 模型的各个局部，也就是细化下电商的具体业务流程，然后把它们综合到一起，形成一个完整的 ER 模型。这样可以帮助我们理清数据库的设计思路。
接下来，我们再分析一下各个实体都有哪些属性，如下所示。
(1)地址实体 包括用户编号、省、市、地区、收件人、联系电话、是否是默认地址。
(2)用户实体 包括用户编号、用户名称、昵称、用户密码、手机号、邮箱、头像、用户级别。
(3)购物车实体 包括购物车编号、用户编号、商品编号、商品数量、图片文件url。
(4)订单实体 包括订单编号、收货人、收件人电话、总金额、用户编号、付款方式、送货地址、下单时间。
(5)订单详情实体 包括订单详情编号、订单编号、商品名称、商品编号、商品数量。
(6)商品实体 包括商品编号、价格、商品名称、分类编号、是否销售，规格、颜色。(7)评论实体 包括评论id、评论内容、评论时间、用户编号、商品编号(8)商品分类实体 包括类别编号、类别名称、父类别编号





![image-20240501123221030](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501123221030.png)





#### 5.小结



ER模型的创建过程就是：

1.先确定实体有那些，如一个经典电商为例，有用户，商品，订单，购物车，地址，评论，这些属性可以通过ER建模的过程逐步分析得出

2.确定属性 ：    如用户 就有name age phone 等等信息，使用椭圆表示

3.关系：  一对一，一对多一般都不需要建立关系，通过理论外键即可，多对多需要建立关系。



ER模型 建造 数据库：

1.优先建立强实体







### 7.3 数据库设计原则



综合以上内容，总结出数据表设计的一般原则**:"三少一多"**
**1.数据表的个数越少越好**
RDBMS 的核心在于对实体和联系的定义，也就是E-R图(Entity Relationship Diagram)，数据表越少，证明实体和联系设计得越简洁，既方便理解又方便操作。
**2.数据表中的字段个数越少越好**
字段个数越多，数据冗余的可能性越大。设置字段个数少的前提是各个字段相互独立，而不是某个字段的取值可以由其他字段计算出来。当然字段个数少是相对的，我们通常会在 数据冗余 和 检索效率 中进行平衡。 
**3.数据表中联合主键的字段个数越少越好**
设置主键是为了确定唯一性，当一个字段无法确定唯一性的时候，就需要采用联合主键的方式(也就是用多个字段来定义一个主键)。联合主键中的字段越多，占用的索引空间越大，不仅会加大理解难度，还会增加运行时间和索引空间，因此联合主键的字段个数越少越好。
**4.使用主键和逻辑外键越多越好**
数据库的设计实际上就是定义各种表，以及各种字段之间的关系。这些关系越多，证明这些实体之间的冗余度越低，利用度越高。这样做的好处在于不仅保证了数据表之间的 独立性，还能提升相互之间的关联使用率。“三少一多”原则的核心就是 简单可复用 。简单指的是用更少的表、更少的字段、更少的联合主键字段来完成数据表的设计。可复用则是通过主键、外键的使用来增强数据表之间的复用率。因为一个主键可以理解是一张表的代表。键设计得越多，证明它们之间的利用率越高。





### 7.4 数据库对象编写建议

**10.1关于库**
【强制】库的名称必须控制在32个字符以内，只能使用英文字母、数字和下划线，建议以英文字母开头。
【强制】库名中英文 一律小写 ，不同单词采用 下划线 分割。须见名知意
<font color="red">【强制】库的名称格式:业务系统名称_子系统名。</font>
【强制】库名禁止使用关键字(如type,order等)
<font color="red">【强制】创建数据库时必须 显式指定字符集，并且字符集只能是utf8或者utf8mb4。</font>

建议】对于程序连接数据库账号，遵循 权限最小原则,使用数据库账号只能在一个DB下使用，不准跨库。程序使用的账号 原则上不准有drop权限。
【建议】临时库以 tmp为前缀，并以日期为后缀;
				备份库以 bak_为前缀，并以日期为后缀。



<font color="red"></font>

**10.2 关于表、列**
【强制】表和列的名称必须控制在32个字符以内，表名只能使用英文字母、数字和下划线，建议以 英文字母开头。
【强制】表名、列名一律小写，不同单词采用下划线分割。须见名知意。
<font color="red">【强制】表名要求有模块名强相关，同一模块的表名尽量使用 统一前缀。比如:crm_fund_item</font>
<font color="red">【强制】创建表时必须 显式指定字符集 为utf8或utf8mb4.</font>
【强制】表名、列名禁止使用关键字(如type,order等)
**【强制】创建表时必须 显式指定表存储引擎 类型。如无特殊需求，一律为InnaDB.**
**【强制】建表必须有comment。**
【强制】字段命名应尽可能使用表达实际含义的英文单词或 缩写。如:公司ID，不要使用corporation_id,而8.用corp_id 即可。

<font color="red">【强制】布尔值类型的字段命名为 is_描述。如member表上表示是否为enabled的会员的字段命名为is enabled.</font>//但是Java pojo类中不要以Is开头

【强制】禁止在数据库中存储图片、文件等大的二进制数据通常文件很大，短时间内造成数据量快速增长，数据库进行数据库读取时，通常会进行大量的随机0操作文件很大时，10操作很耗时。通常存储于文件服务器，数据库只存储文件地址信息。
【建议】建表时关于主键: 表必须有主键1.1
【强制】要求主键为id，类型为int或bigint，且为auto_increment 建议使用unsigned无符号型。(2)标识表里每一行主体的字段不要设为主键，建议设为其他字段如user_id，ordelid等，并建立unique key索引。因为如果设为主键日主键值为随机插入，则会导致innodb内部页分裂和大量随机I/0，性能下降。
【建议】核心表(如用户表)必须有行数据的 创建时间字段(create_time)和 最后更新时间字段(update_time)，便于查问题。
【建议】表中所有字段尽量都是 NOT NULL属性，业务可以根据需要定义 DEFAULT值。13因为使用NULL值会存在每一行都会占用额外存储空间、数据迁移容易出错、聚合函数计算结果偏差等问题,【建议】所有存储相同数据的 列名和列类型必须一致(一般作为关联列，如果査询时关联列类型不一致会自14动进行数据类型隐式转换，会造成列上的索引失效，导致查询效率降低)。

 

**10.3关于索引**
【强制】InnoDB表必须主键为id int/bigint auto_increment，且主键值禁止被更新。
【强制】InnoDB和MyISAM存储引擎表，索引类型必须为 BTREE。
【建议】主键的名称以 pk_开头，唯一键以 uni_或 uk_开头，普通索引以 idx_开头，一律使用小写3.
格式，以字段的名称或缩写作为后缀。
建议】多单词组成的&olumnname，取前几个单词首字母，加末单词组成column_name。如:sample表A.member id上的索引:idx sample mid.
建议】单个表上的索引个数 不能超过6个。
【建议】在建立索引时，多考虑建立 联合索引，并把区分度最高的字段放在最前面。6
【建议】在多表 JOIN 的SOL里，保证被驱动表的连接列上有索引，这样JOIN 执行效率最高
【建议】建表或加索引时，保证表里互相不存在 冗余索引。8比如:如果表里已经存在key(a,b)，则key(a)为冗余索引，需要删除。





### 7.5PowerDesigner



**/一个不错的开发数据库的软件**

**//用到再学吧**







## 8.事务





### 8.1 事务基础知识





#### 1.事务的ACID特性

- **原子性(atomicity)**
  即事务要么全部提交，要么全部回滚
- **一致性(consistency)**
  ![image-20240501155047671](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501155047671.png)

- **隔离性(isolation)**

  一个事务的执行**不能被其他事务影响**，即一个事务内部操作及使用的数据对**并发**的其他事务是隔离的 

- **持久性(durability)**
  一个事务一旦被提交，它对数据库中数据的改变就是**永久性的**，接下来其他操作和数据库故障不应该对其有任何影响



![image-20240501155510146](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501155510146.png)



#### 2. 事务的状态

- **活动的(active)** 
  事务对应的数据操作正在执行中

- **部分提交的(partially commited)**

  当事务的最后一个操作完成时，由于操作都在内存中执行，所造成的影响并没有刷新到磁盘中，这时处在部分提交状态

- **失败的(failed)**
  事务在active / partially commited 遇见了错误而无法继续执行 / 认为停止了当前事务的进行，我们就说该事务处在失败状态

- **中止的(aborted)**
  事务执行了一部分而变成失败状态，需要将进行回滚，当回滚到执行事务之前的状态，我们称之为中止状态

- **提交的(commited)**

  事务成功后，将修改过的数据都同步到磁盘之后，我们就可以称之为提交的





#### 3. 数据并发问题

两个事务Session A ,Session B   



##### 3.1**脏写(dirty write)**

if 事务A update了 未提交的事务B的数据 即 发生了脏写 
![image-20240501170531184](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501170531184.png)



##### 3.2 脏读(dirty read)

![image-20240501170710545](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501170710545.png)





##### 3.3不可重复读



![image-20240501171013680](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501171013680.png)







##### 3.4 幻读

![image-20240501171106621](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501171106621.png)



##### 3.5 小结



严重程度

```
脏写 > 脏读 > 不可重复读 > 幻读 
```







#### 4.事务隔离级别



脏写是绝对无法接受的，但有时候为了效率可以容忍部分问题,隔离级别应运而生。隔离级别越低，问题越多



**//下面是sql标准的规定，实际上各个数据库厂商对sql标准都不一样，比如MySQL在repeatable read就已经解决幻读了**

![image-20240501181001268](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501181001268.png)



seriablizable级别下如何解决幻读问题

![image-20240501181559105](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501181559105.png)



## 9.锁



### 9.1 概述



![image-20240501181929103](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501181929103.png)



### 9.2 Mysql并发事务访问相同记录



#### 1.写-写

即并发事务相继对相同的记录做出改动。

这种情况会出现脏写的情况，任何隔离级别都不允许出现。所以在多个未提交事务相继对同一条记录做出改动时，让它们排队执行，这个排队就是通过锁来实现的。

**这个所谓的锁其实是一个内存中的结构，在事务执行之前本来没有锁结构与记录进行关联的，当一个事务想对这条记录修改，首先会看看内存中有没有与这条记录关联的锁结构，当没有的时候，就会在内存中生成一个锁结构与之关联。**





#### 2.读-写/写-读

即一个事务正在读取操作，一个事务正在写操作。

这种情况可能出现脏读，不可重复读，幻读的问题



<font color="red">怎么解决脏读，不可重复读，幻读的问题呢？</font>

方案一： 读操作利用多版本并发控制(MVCC),写操作加锁

![image-20240501184420302](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501184420302.png)



方案二：读写都加锁



**//一般情况我们肯定更喜欢MVCC，而不是暴力加锁**









### 9.3 锁分类



![image-20240501184643584](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240501184643584.png)







#### 1.共享锁与排他锁

![image-20240503121151572](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503121151572.png)



加锁方法

```
5.7
select xxx  LOCK IN SHARE MODE;
8.0新增语法
select xxxx FOR SHARE/UPDATE;  share 共享锁，update排他锁




```

![image-20240503122207237](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503122207237.png)

![image-20240503122509549](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503122509549.png)



#### 2.表级锁，页级锁，行锁



**①表级锁**

- 优缺点：表级锁虽然开销很小，可以很好的避免死锁的问题，但是并发效率低下。

- **表级别的S锁X锁**，很少使用，了解

- **表级别的意向锁**

  ![](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503125418694.png)

  

  ![](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503125236755.png)

- **表级锁的自增锁**
  当我们给一个字段添加 auto_increment ，意味着该字段自增，其底层原理就是用自增锁
- **表级锁的元素锁(MDL锁)**
  ![image-20240503130422521](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503130422521.png)





**②InnoDB中的行锁**



- **记录锁**

  **行锁又称记录锁，即可以锁住某一行。需要注意的是Mysql服务没有实现行锁机制，行级锁只在存储引擎中实现**

  advantage:锁定力度小，发生锁冲突概率低，可以实现的并发度高

  disadvantage:对于锁的开销比较大，加锁比较慢，容易出现死锁
  记录锁也分为S型记录锁和X型记录锁，比如对id = 1的数据进行加锁



- **间隙锁**
  ![image-20240503132431851](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503132431851.png)



- **临键锁**
  ![image-20240503133955521](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503133955521.png)

- **插入意向锁**





**③页锁**

了解即可









#### 3.悲观锁与乐观锁

悲观锁与乐观锁是锁的设计思想，是看待数据并发的思维方式，并不是真正的锁结构 。



- **悲观锁**
  - 悲观锁总是假设最坏的情况，每次去拿数据都认为别人会修改，所以每次在拿数据的时候都上锁。	
    java中实现悲伤锁的方式synchronized 和 ReentranLock 
    例子，详见redis篇中的秒杀场景
- **乐观锁**
  - 乐观锁总是假设最好的情况，认为去拿数据别人会修改是小概率事件，不会每次都加锁，但是在更新的时候会判断一下在此期间别人有没有修改数据。
    只能程序中(如java)中实现乐观锁,实现方式



**乐观锁实现方式一：版本号机制**

​							数据库中记录每条数据更新的版本号，在更新某条数据时，先取出当前的版本号，然后将新的版本号加 1，并且与原版本号进行比较。如果两个版本号相同，则说明数据未被其他线程修改，可以执行更新操作；如果不同，则表示有其他线程已经修改过该数据，需要重新获取最新版本号再试一次。



**乐观锁实现方式二：时间戳充当版本号**

数据库中记录每条数据修改的时间戳。当有线程要更新数据时，它会通过比较自己持有的时间戳和数据库中的时间戳来判断该数据是否被其他线程修改过。如果时间戳相同，则更新成功；如果不同，则需要重新获取最新时间戳并重试。



**乐观锁实现方式三：CAS**

​							







#### 4.显示锁与隐式锁

隐式锁主要有两种，**一个是在insert时，会有隐式锁，防止插入的数据在提交之前被其他事务访问到**，另外一个是在有间隙锁是进行insert操作，会有插入意向锁，也属于隐式锁。





#### 5.锁的内存结构与监控策略





![image-20240503150418533](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240503150418533.png)











### 9.2 多版本并发控制(MVCC)



**开发很少接触，但是面试高频知识点，以后再学**







## 10.日志

























# Redis基础篇

## 收获



### 1.线程池的应用

比如这个

```
private static final ExecutorService CACHE_REBUILD_EXEUTOR = Executors.newFixedThreadPool(10);
```

```
// 6.3获取成功，实现缓存重建
CACHE_REBUILD_EXEUTOR.submit(() ->{
   //重建缓存
   saveShop2Redis(id,20L);	
   //释放互斥锁
    unlock(lockKey);
});
```







### 2.给@Component传参



比如下面的代码，我以前都没想到还可以给组件传参，这样就省了很多东西，**提高复用性**

```
@Slf4j
@Component
public class CacheClient {

    private final StringRedisTemplate stringRedisTemplate;


    public CacheClient(StringRedisTemplate stringRedisTemplate) {
        this.stringRedisTemplate = stringRedisTemplate;
    }
```





### 3.自己将特定方法抽象成统一方法







### 4.位运算

​	

![image-20240412121400274](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240412121400274.png)



### 5.@Transactional



默认是只有遇见了runxxxxException才会报错







### 6.包装类与intern()



**直接上结论**：包装类型虽然值相同但是内存地址不同，所以比较的结果一定是false，如果将其.toString()也依然是不同的内存地址，但是使用.toString().intern()就可以实现值相同地址相同	(实现方式：去字符串池找如果找到一样的就直接返回)

```
@Test
void test() {
    Integer x = 1;
    Integer y = 1;
    String xx = x.toString().intern();
    String yy = y.toString().intern();
    if(xx == yy){
        System.out.println("相同");
    }else {
        System.out.println("不同");
    }
    System.out.println(1);
}
```



### 7.拆箱返回问题



    public boolean tryLock(long timeoutSec) {
        //获取线程id
        long id = Thread.currentThread().getId();
        //保存到redis
        Boolean success = stringRedisTemplate.opsForValue()
                .setIfAbsent(KEY_PREFIX + name, id + "", timeoutSec, TimeUnit.SECONDS);
    
        return Boolean.TRUE.equals(success);//注意，凡是拆箱都有可能出现空指针问题，因此建议不要直接返回拆箱结果
    }



### 8.UUID的生成时间



UUID是类初始化就已经生成好了!!!!!!!





### 9.提高效率的几个小技巧





### 10.hutool

一个万能的工具类

```
<!--hutool-->
<dependency>
    <groupId>cn.hutool</groupId>
    <artifactId>hutool-all</artifactId>
    <version>5.7.17</version>
```





### 11.lua脚本 



**//lua脚本专门解决  原子性问题**

在类路径下面编写lua脚本

```
//加载类路径下面的seckill.lua资源
private static final DefaultRedisScript SECKILL_SCRIPT;
static {
    SECKILL_SCRIPT = new DefaultRedisScript();
    SECKILL_SCRIPT.setLocation(new ClassPathResource("seckill.lua"));
    SECKILL_SCRIPT.setResultType(Long.class);
}
```

```
//2.使用lua脚本 判断用户是否具有购买资格
Long result = (Long) stringRedisTemplate.execute(
        SECKILL_SCRIPT,
        Collections.emptyList(),
        voucherId.toString(),
        userId.toString()
);
```







### 12.返回空集合

当你需要返回有个空List的时候就返回这个,同理其他空集合也各自有别的方法，直接返回Null一般是不合适的







### 13.stream流能将集合按类分组



​        Map<Long,List<Shop>> map = shops.stream().collect(Collectors.groupingBy(Shop::getTypeId));

```
    @Test
    void loadShopData() {
        //1.查询店铺信息
        List<Shop> shops = shopService.list();
        //2.将店铺按照类型分组
        Map<Long,List<Shop>> map = shops.stream().collect(Collectors.groupingBy(Shop::getTypeId));
        //3.将店铺坐标存入redis
        for(Map.Entry<Long,List<Shop>> entry : map.entrySet()) {
            //3.1获取类型Id
            Long typeId = entry.getKey();
            String key = "shop:geo:" + typeId;
            //3.2获取同类型的店铺的集合
            List<Shop> value = entry.getValue();
            //3.3写入redis GEO key 经度 纬度 member
            List<RedisGeoCommands.GeoLocation<String>> locations = new ArrayList<>(value.size());
            for(Shop shop : value) {
//                stringRedisTemplate.opsForGeo().add(key,new Point(shop.getX(),shop.getY()),shop.getId().toString());
//                这样一个一个存进去效率不高，所以我们选择另一种方法，也使我们之前的分组派上用场
                locations.add(new RedisGeoCommands.GeoLocation<>(
                        shop.getId().toString(),
                        new Point(shop.getX(),shop.getY())));
            }
            //这个重写版本的add，一次性添加一个集合，而不是之前那样一个一个添加，提高效率
            stringRedisTemplate.opsForGeo().add(key,locations);
        }

    }
```





### 14.日期格式化



```
LocalDateTime now = LocalDateTime.now(); // 2024-04-22T22:43:21.902337700
String result = now.format(DateTimeFormatter.ofPattern("自定义格式"));//比如 "yyyy-MMM-dd hh:mm:ss"或使用预定义的常数（如ISO_LOCAL_DATE_TIME）来格式化日期时间。   格式很自由，需要什么加什么，需要最前面加:就加，“:yyyyMM” 例子：:202404

```







## 0.初识redis







### 0.1  NoSql

**disadvantages:**	Nosql相比传统的mysql那种关系型数据库，数据结构比较松散不严格；数据无关联；语法比较松，不同的nosql数据库语法甚至都不一样；对于事务处理也只能做到一般处理

****

![image-20240320164740288](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240320164740288.png)

**advantages: **

​						查询性能高，一般都在内存中储存

​		





### 0.2linux下安装redis



```
1.下载redis-6.14xx版本  到 /usr/local/src 目录
2.下载相关依赖  yum install -y gcc tcl
3.tar -zxvf reids-6.xxxx
4.启动redis
    (1) 已经默认配置了全局变量，可以在任意位置 redis-server启动
    (2)修改配置文件: 首先备份一份redis.conf以防万一,cp redis.conf redis.conf.bck   (推荐)
    				然后   修改vim redis.conf   详情见下面
    				最后 启动时加上配置文件绝对路径(如果在reids目录下可不用加绝对路径)建议到目录下面运行
    				redis-server /usr/local/src/redis-6.xxx/redis.conf
    (3)开机自启动:
```





![image-20240402151727157](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402151727157.png)







### 0.3使用redis





```
1.命令行使用redis：进入cd /usr/local/bin
					redis-cli -h 当前ip/127.0.0.1 -p 6379 -a 密码 (这样是危险的)
			建议:    redis-cli -h 127.0.0.1 -p 6379
					AUTH 密码
					输入ping 
					回复pong 即成功！！
2.redis图形化操作:  https://github.com/lework/RedisDesktopManager-Windows/releases 下载
					要使用别忘了关闭防火墙



```



### 0.4  Redis是单线程的！！！！











## 1.redis基础



### 1.0 reids 通用操作

```
KEYS :  查看符合模板的所有key   keys a*  不建议在生产环境使用,效率可能比较低

DEL :   例子 DEL k1 k2 k3 k4   ,返回值为删除的数量 如果k4不存在，则返回3,表示删除了三个数据

EXISTS:  EXISTS K1  存在返回1，不存在返回0

expire: 给一个key设置有效期   expire key seconds           
 					-1 表示永久有效  -2 表示已经失效
TTL : 查看一个key的剩余有效期
```











### 1.1 redis的数据类型

![image-20240402162348526](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402162348526.png)



#### 1.1.1String类型



```
1.SET  :  会覆盖哦        //可以在后面加很多东西  set name jack ex 100(设置name有效期为100秒)
 											 set name jack nx == setnx name jack
2.GET

3.MSET :批量set   mset k1 v1 k2 v2 k3 v3

4.MGET :批量get   mget name age k1 k2 k3

5.INCR :自增长  set age 12; incr age ; get age /age = 13

6.INCRBY :自增长 by 整数   incrby age 3 ;

7.INCRBYFLOAT: 子增长 by 浮点数

8.DECR: 自减少

9.SETNX : 如果key不存在则生成，若存在则set失败  //底层是 set k v nx ，其实是set和nx两个组合使用，set 后面可以跟很多东西
```



![image-20240402164344125](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402164344125.png)







#### 1.1.2Hash类型



```
1.HSET:   hset student name jack age 12 skill study

2.HGET: hget student name 

3.MGET: mget user:student:1 name age skill

4.hgetall

5.hkeys

6.hvalues

7.hincrby

8.hsetnx
```

在 Redis 中可以通过 setex 或 expire 方式来设置 key 的过期时间。但是对于Hash 数据类型 Redis 是不支持的，所以我们需要使用“曲线救国”的方式去实现 Hash 数据类型的过期时间。

即，先对 Hash 数据类型赋值，然后再对 Hash 数据类型的 key 设置一个过期时间，这样就间接的实现了对 Hash 数据类型的过期时间操作。






#### 1.1.3List类型



![image-20240402170557754](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402170557754.png)q

```
1.LPUSH key element
  RPUSH key element

2.LPOP key  移除左侧第一个元素，若没有则返回nil
  RPOP key

3.LRANGE key star end 

4.BLPOP   和lpop rpop 的区别就是 blpop 不会直接返回nil 而是在没有元素时等待指定时间
  BRPOP

```







#### 1.1.4Set类型



![image-20240402180625576](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402180625576.png)



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







#### 1.1.5SortedSet类型



![image-20240402181751599](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402181751599.png)

**sortedset 默认是升序**

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
```









### 2.redis的Java客户端





#### 2.0 三种常用，一个整合

![image-20240402213101169](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402213101169.png)







#### 2.1 jedis



![image-20240402213619285](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402213619285.png)



**//如果真的要使用jedis，也得用jedis线程池，怎么写自己去搜**







####   2.2StringDataRedis







![image-20240402220350324](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240402220350324.png)



##### 2.2.1   依赖问题

引入依赖   lettue有问题，暂时别引入

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





##### 2.2.2 序列化问题



因为redis底层都是将Java传过来的对象进行字节处理，序列化，这就导致数据库那边变成乱码



![image-20240403122127294](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240403122127294.png)





//解决方法 :

**//注意  实际开发中，我们一般不需要查看value,所以一般都是只需要设置key的序列化工具即可**

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



**一个小疑问: RedisSerializer.String() 与 new StringSerializer()的区别**

解答;其实没有区别，你看源码，new StringSerializer()默认也是utf-8，直接RedisSerializer.String()也是返回utf-8的StringSerializer

```
static RedisSerializer<String> string() {
    return StringRedisSerializer.UTF_8;
}
```



**//小细节;ctrl + h 可以查看实现类**

![image-20240403130542313](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240403130542313.png)













##### 2.2.3 StringRedisTemplate



![image-20240403132307534](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240403132307534.png)

![image-20240403132324634](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240403132324634.png)



![image-20240403132348437](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240403132348437.png)







使用案例

**//没什么特别的，唯一需要注意的是需要你手动序列化，你可以使用jackson,gson,fastjson，随便，用哪个就去现学呗，都是api**



```java
@SpringBootTest
public class TestRedis {
    @Resource
    private RedisTemplate redisTemplate;

    @Resource
    private StringRedisTemplate stringRedisTemplate;

    private static final ObjectMapper mapper = new ObjectMapper();

    @Test
    void aa(){
        String json = null;
        //创建对象
        Student student = new Student("李元霸", 20, "举重");
        //手动序列化
        try {
            json = mapper.writeValueAsString(student);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
        }
        stringRedisTemplate.opsForValue().set("user:student:5",json);

        //取出数据
        String s = stringRedisTemplate.opsForValue().get("user:student:5");
        Student student1 = null;
        try {
            student1 = mapper.readValue(s, Student.class);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
        }
        System.out.println(student1);
    }
}
```





![image-20240403134306803](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240403134306803.png)

















## 2.redis实战篇之商户查询





### 2.1 hmdp之实现短信验证功能



![image-20240407175200237](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240407175200237.png)





- 隐藏用户敏感信息，不要直接将一个user存到threadlocal里面，可以存一个userDTO
- 一个问题:如何实现一个真实的短信发送功能呢?



### 2.2缓存更新



![image-20240410123641028](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410123641028.png)





**缓存更新策略的最佳实践方案:**

​											1.低一致性需求：使用redis自带的**内存淘汰**机制

​											2.高一致性需求："**主动更新**"(程序员自己在程序中添加更新/删除缓存的操作),并以"**超时剔除**"兜底

​												读操作：缓存命中直接返回；缓存未命中则查询数据库，写入缓存，设置TTL超时时间

​												写操作：先写数据库，然后删除缓存，确保数据库和缓存操作的原子性







![image-20240410125548090](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410125548090.png)

![image-20240410125525968](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410125525968.png)







### 2.3缓存穿透

![image-20240410132556671](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410132556671.png)



![image-20240410182015564](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410182015564.png)



![image-20240410181852339](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410181852339.png)







### 2.4缓存雪崩



![image-20240410205400497](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410205400497.png)









### 2.5缓存击穿



**//concept:**

![image-20240410210250457](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410210250457.png)

 

**//solution:**

![image-20240410210223055](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410210223055.png)



**//advantage and disadvantage**

![image-20240410210511769](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240410210511769.png)



互斥锁

![image-20240411122356869](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240411122356869.png)



逻辑过期

![image-20240411134514875](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240411134514875.png)









## 3.redis实战篇之优惠券秒杀





### 3.1 全局Id生成器（利用redis生成）





```
@Component
public class RedisIdWorker {

    /*
    * 开始时间
    * */
    private static final long BEGIN_TIMESTAMP = 1712923032L;
    /*
    * 序列号的位数
    * */
    private static final long COUNT_BITS = 32;

    private StringRedisTemplate stringRedisTemplate;

    public RedisIdWorker(StringRedisTemplate stringRedisTemplate) {
        this.stringRedisTemplate = stringRedisTemplate;
    }


    public long nextId(String keyPrefix) {
        //1.生成时间戳
        LocalDateTime now = LocalDateTime.now();
        long nowSecond = now.toEpochSecond(ZoneOffset.UTC);
        long timeStamp = nowSecond - BEGIN_TIMESTAMP;

        //2.生成序列号
        //2.1获取当前日期，精确到天       //这样有什么好处？解答：可以精确统计每一天/月/年的订单量； 也可以防止key一直增长到最大导致超出范围
        String date = now.format(DateTimeFormatter.ofPattern("yyyMMdd"));
        Long count = stringRedisTemplate.opsForValue().increment("icr:" + keyPrefix + ":" + date);

        //3.拼接并返回
        return timeStamp << COUNT_BITS | count;
    }

}
```



//这里巧妙利用 位运算

![image-20240412121325533](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240412121325533.png)





![image-20240412123239315](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240412123239315.png)









### 3.2 优惠券秒杀之单体应用版本的一人一单



![image-20240412204042917](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240412204042917.png)









![image-20240412210723107](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240412210723107.png) 	![image-20240412211423379](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240412211423379.png)





**//CAS乐观锁**



```
//4.扣除秒杀券
boolean success = seckillVoucherService.update()
        .setSql("stock = stock - 1")//set stock = stock - 1
        //cds实现乐观锁
        .eq("voucher_id", voucherId).gt("stock", 0)//where user_id=? and stock>0
        .update();
if(!success) {
    //扣减失败
    return Result.fail("VOUCHER_IS_OVER");
}
```





**//悲观锁**

没有选择直接将锁加在整个方法，是因为那样会串行执行，效率很低，将锁加在user_id，效率就高很多

注意一个地方，就是user_id是Long包装类型，即使传过来的值一样，但是底层仍然会new一个新对象，所以我们采取.toString方法将其变成String类型,再使用.instern()使其从字符串池中获取。



**//一些并发问题，这里我们将创建秒杀券抽出成一个方法，但是加上事务管理，使用悲观锁锁上user_id，但是依然无法解决并发问题,这是因为Spring管理的事务提交好像不是很块，在你执行完方法后，可能还没有提交事务,这时候已经释放锁了，导致并发问题**

```
/*
* 创建秒杀券
* */
    @Transactional
    public Result createVoucherOrder(Long voucherId,Long user_id) {
            //4.判断用户是否重复购买
            //查询订单
            Integer count = query().eq("user_id", user_id).eq("voucher_id", voucherId).count();
            if (count > 0) {
                //该用户重复购买，返回错误信息
                return Result.fail(VOUCHER_USER_IS_TWICE);
            }
            //5.扣除秒杀券
            boolean success = seckillVoucherService.update()
                    .setSql("stock = stock - 1")//set stock = stock - 1
                    //cds实现乐观锁
                    .eq("voucher_id", voucherId).gt("stock", 0)//where user_id=? and stock>0
                    .update();
            if(!success) {
                //扣减失败
                return Result.fail("VOUCHER_IS_OVER");
            }
            //6.下单
            VoucherOrder voucherOrder = new VoucherOrder();
            //订单Id
            long orderId = redisIdWorker.nextId("order");
            voucherOrder.setId(orderId);
            //代金券Id
            voucherOrder.setVoucherId(voucherId);
            //用户Id
            voucherOrder.setUserId(user_id);
            //生成订单
            save(voucherOrder);

            //7.返回订单Id
            return Result.ok(orderId);
    }
}
```



### 3.3优惠券秒杀之分布式锁



#### 问题的引出

**//由于开启了多个服务器，每个服务器的JVM都是独立的，导致之前锁上的user_id通过toString().intern()从字符串常量池获取来辨别的方式失效!!!**

![image-20240415145923311](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240415145923311.png)



#### 什么是分布式锁？

![image-20240415150651244](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240415150651244.png)

#### 分布式锁的多种实现

![image-20240415151258368](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240415151258368.png)







#### Redis实现分布式锁版本1

```
public class SimpleRedisLock {
    //不同业务 有不同的名称
    private String name;
    //前缀
    private static final String KEY_PREFIX = "lock:";
    private StringRedisTemplate stringRedisTemplate;

    public SimpleRedisLock(String name, StringRedisTemplate stringRedisTemplate) {
        this.name = name;
        this.stringRedisTemplate = stringRedisTemplate;
    }

    /*
    * 获取锁
    * */
    public boolean tryLock(long timeoutSec) {
        //获取线程id
        long id = Thread.currentThread().getId();
        //保存到redis
        Boolean success = stringRedisTemplate.opsForValue()
                .setIfAbsent(KEY_PREFIX + name, id + "", timeoutSec, TimeUnit.SECONDS);

        return Boolean.TRUE.equals(success);//注意，凡是拆箱都有可能出现空指针问题，因此建议不要直接返回拆箱结果
    }
    /*
    * 释放锁
    * */
    public void unLock() {
        stringRedisTemplate.delete(KEY_PREFIX + name);
    }
}
```



#### Redis实现分布式锁版本2

**解决极小概论事件：如果JVM1的线程1发送阻塞，超时删除锁，JVM2的线程2这时刚好获取锁，JVM1的线程1阻塞结束，就删除锁，这时就陷入到有线程还在继续业务，但是锁已经被释放！！（不过应该是比较小概率吧）**

**//UUID是类初始化就已经生成好了!!!!!!!**

**//uuid 是用来区分在不同JVM中的相同线程id的，如果是单服务器下直接用线程id区分，但是如果是集群那么还需要用uuid标识线程id是来自不同的集群**

```
public class SimpleRedisLock {
    //不同业务 有不同的名称
    private String name;
    //前缀
    private static final String KEY_PREFIX = "lock:";
    private static final String ID_PREFIX = UUID.randomUUID().toString(true) + "-";
    private StringRedisTemplate stringRedisTemplate;

    public SimpleRedisLock(String name, StringRedisTemplate stringRedisTemplate) {
        this.name = name;
        this.stringRedisTemplate = stringRedisTemplate;
    }

    /*
    * 获取锁
    * */
    public boolean tryLock(long timeoutSec) {
        //获取线程id
        String threadId = ID_PREFIX + Thread.currentThread().getId();
        //保存到redis
        Boolean success = stringRedisTemplate.opsForValue()
                .setIfAbsent(KEY_PREFIX + name, threadId, timeoutSec, TimeUnit.SECONDS);

        return Boolean.TRUE.equals(success);//注意，凡是拆箱都有可能出现空指针问题，因此建议不要直接返回拆箱结果
    }
    /*
    * 释放锁
    * */
    public void unLock() {
        // 获取线程标识
        String threadId = ID_PREFIX + Thread.currentThread().getId();
        // 获取锁中的标识
        String id = stringRedisTemplate.opsForValue().get(KEY_PREFIX + name);
        // 判读标识是否一致
        if(threadId.equals(id)) {
            //释放锁
            stringRedisTemplate.delete(KEY_PREFIX + name);
        }
    }
}
```





#### Redis实现分布式锁版本3

**//如何实现释放锁的原子性?**

**//这里我们使用lua脚本，因为lua脚本里面的代码是具有原子性的**

**//一个极端情况：在我们判断完锁标识之后，即将进行释放锁之前，阻塞了（比如因为JVM的垃圾回收机制）导致超时释放锁，此时刚好别的线程获取锁就会出问题**

![image-20240415185115809](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240415185115809.png)

**//解决方案：使用lua脚本**

```
public class SimpleRedisLock {
    //不同业务 有不同的名称
    private String name;
    //前缀
    private static final String KEY_PREFIX = "lock:";
    private static final String ID_PREFIX = UUID.randomUUID().toString(true) + "-";
    private static final DefaultRedisScript<Long> UNLOCK_SCRIPT;//ctrl+h 查看继承实现关系你就知道为什么了
    //之所以使用静态代码块，是因为需要在new 对象的时候添加逻辑(就是设置一些东西)
    static {
        UNLOCK_SCRIPT = new DefaultRedisScript<>();
        UNLOCK_SCRIPT.setLocation(new ClassPathResource("unlock.lua"));//todo new ClassPathResource
        UNLOCK_SCRIPT.setResultType(Long.class);
    }
    private StringRedisTemplate stringRedisTemplate;

    public SimpleRedisLock(String name, StringRedisTemplate stringRedisTemplate) {
        this.name = name;
        this.stringRedisTemplate = stringRedisTemplate;
    }

    /*
    * 获取锁
    * */
    public boolean tryLock(long timeoutSec) {
        //获取线程id
        String threadId = ID_PREFIX + Thread.currentThread().getId();
        //保存到redis
        Boolean success = stringRedisTemplate.opsForValue()
                .setIfAbsent(KEY_PREFIX + name, threadId, timeoutSec, TimeUnit.SECONDS);

        return Boolean.TRUE.equals(success);//注意，凡是拆箱都有可能出现空指针问题，因此建议不要直接返回拆箱结果
    }
    /*
    * 释放锁
    * */
    public void unLock() {
//        // 获取线程标识
//        String threadId = ID_PREFIX + Thread.currentThread().getId();
//        // 获取锁中的标识
//        String id = stringRedisTemplate.opsForValue().get(KEY_PREFIX + name);
//        // 判读标识是否一致
//        if (threadId.equals(id)) {
//            //释放锁
//            stringRedisTemplate.delete(KEY_PREFIX + name);
//        }
        ArrayList<String> keys = new ArrayList<>();
        keys.add(KEY_PREFIX + name);
        stringRedisTemplate.execute(
                UNLOCK_SCRIPT,//提前将要读取的文件整合到RedisScript类中，这样就不需要每次使用该方法都读取了！！！！
                keys,
                ID_PREFIX + Thread.currentThread().getId());
    }
}
```



"unlock.lua" 位置直接放在resource下面,关于lua编程感觉和linux的shell编程差不多，用到什么直接去查就完事了

```
-- 获取锁的线程标识
local id = redis.call('get',KEYS[1])
--判断两者是否一致
if(id == ARGV[1])
then
    --一致则释放锁
    return redis.call('del',KEYS[1])
end
--不一致就退出
return 0
```















### 3.4 Redisson

**//前面我们自己设计了一个SimpleRedisLock，用来解决分布式线程问题，但是自己实现有很多缺点而且比较麻烦，这里我们推荐使用redisson来直接获取锁**



#### 3.4.1 快速入门

1.引入依赖（好像这个依赖不好，以后使用到的时候自己去研究一下）：

```
<!--        redisson-->
        <dependency>
            <groupId>org.redisson</groupId>
            <artifactId>redisson</artifactId>
            <version>3.13.6</version>
        </dependency>
```

2.配置类/配置文件(配置文件还没有使用过)：

```
@Configuration
public class RedissonConfig {

    @Bean
    public RedissonClient redissonClient(){
        //配置类
        Config config = new Config();
        //配置单点对象,config.useClusterServers()是配置集群
        config.useSingleServer().setAddress("redis://192.168.200.130:6379").setPassword("1674472827");
        //返回
        return Redisson.create(config);
    }
}
```



3.使用redissonClient



```
Rlock lock = redissonClient.getLock(key);获取锁
boolean success = lock.trylock()//尝试获取锁,可以有参 lock.trylock(1,10,TIME.SECONDS)，1应该是表示启用吧
lock.unlock()//释放锁


```





#### 3.4.2 原理





![image-20240416133122091](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240416133122091.png)





#### 3.4.3 可重入的Redis分布式锁

**//同一个线程无法多次获取同一把锁，比如我们的购买秒杀券，确实需要同一个线程不能获取同一把锁，但是有的业务需要同一个线程多次获取同一把锁，来进行操作，这个我们自己设计锁的时候可以使用hash，存一个key,filed,value，其中key和filed不变依然是local:业务Name  +  uuid:id，维护一个value当作计数器，获取一次锁就++，结束一个业务就--，直到所有业务都结束，当value = 0就释放锁.**//以上操作可以使用lua脚本实现，确保原子性，实际上redisson底层就是使用lua脚本完成



![image-20240416133643515](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240416133643515.png)



![image-20240416133654249](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240416133654249.png)









![image-20240416155433658](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240416155433658.png)









### 3.5优惠券秒杀之异步优化



#### 3.5.0 老代码

```java
@Service
public class VoucherOrderServiceImpl extends ServiceImpl<VoucherOrderMapper, VoucherOrder> implements IVoucherOrderService {

    @Resource
    private ISeckillVoucherService seckillVoucherService;

    //全局id
    @Resource
    private RedisIdWorker redisIdWorker;

    @Resource
    private StringRedisTemplate stringRedisTemplate;

    /*
    * 购买秒杀券
    * */
    @Override
    public Result buySeckillVoucher(Long voucherId) {
        //1.根据Id查询秒杀券
        SeckillVoucher seckillVoucher = seckillVoucherService.getById(voucherId);
           //如果为空，返回错误
           return Result.fail(VOUCHER_IS_NULL);
        }
    	//2.判断当前时间是否允许购买
        LocalDateTime now = LocalDateTime.now();
        if(now.isBefore(seckillVoucher.getBeginTime()) || now.isAfter(seckillVoucher.getEndTime())) {
            return Result.fail(VOUCHER_IS_NOT_IN_TIME);
        }
        //3.判断秒杀券是否剩余
    	if(seckillVoucher.getStock() < 1) {
            return Result.fail(VOUCHER_IS_OVER);
        }

        Long userId = UserHolder.getUser().getId();
        if (userId == null) {
            userId = 1L;
        }

        //创建锁对象
        RLock lock = redissonClient.getLock("lock:order:" + userId);
        //获取锁
        boolean success = lock.tryLock();//无参，失败不等待
        if(!success) {
            //获取失败
            return Result.fail(VOUCHER_USER_IS_TWICE);
        }
        try {
            IVoucherOrderService proxy = (IVoucherOrderService) AopContext.currentProxy();
            return proxy.createVoucherOrder(voucherId,userId);
        } finally {
            //释放锁
            lock.unlock();
        }

    }

    /*
    * 创建秒杀券
    * */
    @Transactional
    public Result createVoucherOrder(Long voucherId,Long user_id) {
            //4.判断用户是否重复购买
            //查询订单
            Integer count = query().eq("user_id", user_id).eq("voucher_id", voucherId).count();
            if (count > 0) {
                //该用户重复购买，返回错误信息
                return Result.fail(VOUCHER_USER_IS_TWICE);
            }
            //5.扣除秒杀券
            boolean success = seckillVoucherService.update()
                    .setSql("stock = stock - 1")//set stock = stock - 1
                    //cds实现乐观锁
                    .eq("voucher_id", voucherId).gt("stock", 0)//where user_id=? and stock>0
                    .update();
            if(!success) {
                //扣减失败
                return Result.fail("VOUCHER_IS_OVER");
            }
            //6.下单
            VoucherOrder voucherOrder = new VoucherOrder();
            //订单Id
            long orderId = redisIdWorker.nextId("order");
            voucherOrder.setId(orderId);
            //代金券Id
            voucherOrder.setVoucherId(voucherId);
            //用户Id
            voucherOrder.setUserId(user_id);
            //生成订单
            save(voucherOrder);

            //7.返回订单Id
            return Result.ok(orderId);
    }
}
```









#### 3.5.1为什么需要优化以及优化思路

![image-20240419115723204](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240419115723204.png)

​	

![image-20240419122539513](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240419122539513.png)



#### 3.5.2 基于redis实现消息队列



**//消息队列还是有空专门学习redisMQ吧，这里就不学了，听得有点烦躁**



​	



## 4.基础功能实现





### 4.1发布博客

自己去看代码，这里图片是直接保存到了本地，也可以使用阿里云OSS





### 4.2点赞与点赞排行

利用redis中的sortedset





### 4.3共同关注

使用了redis的set中交集

```
Set<String> intersect = stringRedisTemplate.opsForSet().intersect(key1, key2);
```









## 5.Feed流(关注推送)





### 5.1什么是Feed流

![image-20240422155318827](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422155318827.png)



![image-20240422155345247](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422155345247.png)

### 5.2 实现TimeLine的三种模式

**这里我们学习简单的TimeLine模式，但是timeline也有三种实现模式**





![image-20240422155510503](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422155510503.png)



![image-20240422155522332](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422155522332.png)

![image-20240422160000539](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422160000539.png)

![image-20240422160011503](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422160011503.png)



  





## 6.GEO(附近店铺)





**//redis中提供了一个GEO数据结构，专门用来代表地理坐标，其实底层是用sortedset存储的**

![image-20240422195716182](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422195716182.png)



将数据库中的店铺的x,y存入到redis中

```
    @Test
    void loadShopData() {
        //1.查询店铺信息
        List<Shop> shops = shopService.list();
        //2.将店铺按照类型分组
        Map<Long,List<Shop>> map = shops.stream().collect(Collectors.groupingBy(Shop::getTypeId));
        //3.将店铺坐标存入redis
        for(Map.Entry<Long,List<Shop>> entry : map.entrySet()) {
            //3.1获取类型Id
            Long typeId = entry.getKey();
            String key = "shop:geo:" + typeId;
            //3.2获取同类型的店铺的集合
            List<Shop> value = entry.getValue();
            //3.3写入redis GEO key 经度 纬度 member
            List<RedisGeoCommands.GeoLocation<String>> locations = new ArrayList<>(value.size());
            for(Shop shop : value) {
//                stringRedisTemplate.opsForGeo().add(key,new Point(shop.getX(),shop.getY()),shop.getId().toString());
//                这样一个一个存进去效率不高，所以我们选择另一种方法，也使我们之前的分组派上用场
                locations.add(new RedisGeoCommands.GeoLocation<>(
                        shop.getId().toString(),
                        new Point(shop.getX(),shop.getY())));
            }
            //这个重写版本的add，一次性添加一个集合，而不是之前那样一个一个添加，提高效率
            stringRedisTemplate.opsForGeo().add(key,locations);
        }

    }
```









## 7.BitMap(用户签到)



### 7.1什么是BitMap?

**//重要思想：利用二进制中的0和1统计或计算或完成某些功能的思想，就是位图(BitMap)**

**//redis中使用String类型实现bitmap**

![image-20240422220640253](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422220640253.png)

![image-20240422221003372](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422221003372.png)



![](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422220853001.png)

```\
setbit group1 0 1
bitfiled group1 u2 0 //u2: u是无符号，2是查找几位，0是从下标0开始查,返回的是十进制，比如0011  返回的就是3 （8421法）
bitfiled group1 u4 0 //比如11011 返回的是13
u是无符号,i是有符号
```



![image-20240422222743602](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240422222743602.png)











### 7.2 实现签到



利用redis的bitmap实现签到

```
@Override
public Result sign() {
    //1.取出当前用户
    Long userId = UserHolder.getUser().getId();
    //2.获取日期
    LocalDateTime now = LocalDateTime.now();
    //3.拼接key
    String keySuffix = now.format(DateTimeFormatter.ofPattern(":yyyyMM"));
    String key = "sign:" + userId + keySuffix;
    //4.获取今天是第几天
    int dayOfMonth = now.getDayOfMonth();
    //5.写入redis
    //dayOfMonth因为下标从0开始要-1；true意思是用1占位，false用0占位
    stringRedisTemplate.opsForValue().setBit(key,dayOfMonth - 1,true);
    //6.返回
    return Result.ok();
}
```







### 7.3统计连续签到天数	



```
    // 1.获取当前登录用户
    Long userId = UserHolder.getUser().getId();
    // 2.获取日期
    LocalDateTime now = LocalDateTime.now();
    // 3.拼接key
    String keySuffix = now.format(DateTimeFormatter.ofPattern(":yyyyMM"));
    String key = USER_SIGN_KEY + userId + keySuffix;
    // 4.获取今天是本月的第几天
    int dayOfMonth = now.getDayOfMonth();
    // 5.获取本月截止今天为止的所有的签到记录，返回的是一个十进制的数字 BITFIELD sign:5:202203 GET u14 0
    List<Long> result = stringRedisTemplate.opsForValue().bitField(
            key,
            BitFieldSubCommands.create()
                    .get(BitFieldSubCommands.BitFieldType.unsigned(dayOfMonth)).valueAt(0)
    );
    if (result == null || result.isEmpty()) {
        // 没有任何签到结果
        return Result.ok(0);
    }
    Long num = result.get(0);
    if (num == null || num == 0) {
        return Result.ok(0);
    }
    // 6.循环遍历
    int count = 0;
    while (true) {
        // 6.1.让这个数字与1做与运算，得到数字的最后一个bit位  // 判断这个bit位是否为0
        if ((num & 1) == 0) {
            // 如果为0，说明未签到，结束
            break;
        }else {
            // 如果不为0，说明已签到，计数器+1
            count++;
        }
        // 把数字右移一位，抛弃最后一个bit位，继续下一个bit位
        num >>>= 1;
    }
    return Result.ok(count);
}
```









## 8.HyperLogLog



### 8.1什么是hyperloglog?

![image-20240423181817874](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240423181817874.png)	



**//HyperLogLog 非常适合用来计算 UV**

```
PFADD name e1 e2 e3 ....//添加  注意hyperloglog重复元素只会添加一次

PFCOUNT name //统计数量

```



**所以UV统计没什么难度，很简单!**







## 





# Redis高级篇





## 0.单点redis的问题

![image-20240423192315277](https://gitee.com/vulnerable5481/typora-img/raw/master/img/image-20240423192315277.png)