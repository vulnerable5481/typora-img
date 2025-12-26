# NULL

```

由于第一次实习的时候，在杭州就用过python开发过爬虫、脚本，所以对python有了一点兴趣(好吧，只是太简单了，随手学一下就ok了)

学习python，只打算速通一下基础知识，简单学一下相关的类库使用，需要使用python编写脚本就用AI搞完事了，自己能看懂修缮即可。
```



# 一、基础



## 1、差异

```
0、虚拟环境
	产生背景：默认情况python引入第三方库是全局的，每个python项目都会使用一套，这肯定不行，想想java开发项目之间库使用一个不炸了
	虚拟环境：假设本地只有一个python，虚拟环境可以帮助我们模拟出多个python环境，这样就实现项目之间依赖的隔离性。

1、for循环
   如果不需要索引下标：
   		for _ in range():
   如果需要索引下标：
   	    number = 100
   	    # 这里的index,value可以随便取名字，格式就是(下标，元素)
   	    for index,value in enumerate(number):
   	    	print(index,value)

2、运算符号
	可以使用in /  not in 判断是否在集合里面
	if x in list/dict/tuple/set

3、函数定义、return、解包
	def get_user():
		return 1,"Tom",18  # 等价于 return (1,"Tom",18)
	# 注意这里返回的不是三个值，而是一个user对象的元组，不允许修改
	# return user对象 这样才会返回一个字典，允许修改
	# id,name,age = get_user()  pt支持解包

4、模块管理
	project/
    ├── main.py
    └── utils/
        ├── __init__.py
        └── test.py
	# 类似import，感觉第一种方式更不错
	① from utils.test import hello ，使用：hello()
	② import utils.test, 使用：utils.test.hello()

5、main函数
	注意如果import引入一个py文件，这个py文件可以直接当作脚本跑，import不会自动指向main里的代码
	
	def main():
		print("程序exe")
	
	if __name__ == "__main__":    #这一句是写死固定的
		main()
    【千万注意这里的__name__ 和 __main__，左右都是双下划线！】

6、魔法变量
	前后都是双下划线，是 Python 解释器约定好的特殊变量
	比如__name__ __file__ 之类的
   	    	
   	    	
   	    	
   	    	
【注意事项】   	    	
1、i++是不存在的，+对于py只是一个自增符
2、__name__ 和 __main__，左右都是双下划线！	
3、注意缩进
4、不要使用set、tuple、list等关键词汇进行命名！
```

## 2、数据结构

```
【获取数据结构长度，统一使用len()函数】
【获取数据的类型，统一使用type()函数】

1、列表（list）： 和Java中的ArrayList差不多，就是一个动态数组
	① py中有正向索引与反向索引，0~N-1 或者 -1~-N
	arr = [1，2，3]
	arr.append(4) # 尾插法
	arr.insert(1,123) # 指定插入
	arr[0] = 1
	arr.pop() # 尾删

2、元组(tuple): 只读列表，不可修改
	t = (1,2,3)

3、set：去重集合
	set = {1,2,3,3} # 会自动去重，保留一个3
	if x in s:
		print(x,'存在')
		
4、字典(dict): hashMap
	user = {
		"id":1,
		"name":"Tom",
		"age":18
	}
	user.get("age")
	user["age"] = 20

5、字符串
	没有String和char的区别，统一都是字符串， 使用"" 还是 '' 都可以
```

## 3、类与对象

```
class Person:
	
	#类属性
	birthPlace = "earth"
	
	#静态方法
	@staticmethod
	def test_static():
		print("静态方法")
	
	def _init_(self,name,age):
		self._name = name
		self._age = age
	
	def say_hello():
		print("hello!")
		
zlc = Person("zlc",12)

1、 _init_函数就是构造器
2、self 就是 this
3、类可以有属性、类属性、函数，注意一下对象属性与类属性的区别
4、静态方法，加装饰器@staticmethod
	【这里讲一下python的装饰器，看起来很像注解的东西：
		def my_decorator(func):
            def wrapper():
                print("Before")
                func()
                print("After")
            return wrapper

        @my_decorator
        def say_hello():
            print("Hello")

        say_hello()	】
5、python是一门动态语言，可以动态为对象添加属性，zlc.sex = male


1、继承
class Student(Person):
	def _init_(self,name,age):
		super._init_(name,age)
如果要重写的话，直接重写即可
```

## 4、IO操作、异常

```
1、基础写法：
	# 例如当前py文件在D:/project/python/main.py
	
	# 读操作
	from pathlib import Path
	base_dir  = Path(__file__).parent
	file_path = base_dir / "test.txt"
	file = open(file_path,"r",encoding="utf-8")
	print(file.read())
	file.close()
	
	# 写操作
	file = open('致橡树.txt', 'a', encoding='utf-8')
    file.write('\n标题：《致橡树》')
    file.write('\n作者：舒婷')
    file.close()

2、open函数解析
	① 第一个字段就是文件名字，默认会直接在当前py脚本所在的目录寻找，也可以自己设置文件路径
	② 第二个字段就是操作模式，  'r'	读取 （默认）
                            'w'	写入（覆盖之前的内容）
                            'x'	写入，如果文件已经存在会产生异常
                            'a'	追加，将内容写入到已有文件的末尾
                            'b'	二进制模式
                            't'	文本模式（默认）
                            '+'	更新（既可以读又可以写）
	③ 第三个字段就是编码

3、如何往文件中写入py中的对象呢？
	序列化与反序列化：通过引入json的dumps方法将字典、对象转化-> json对象
	import json 
	my_dict = {
		"name":"test",
		"age": 12
	}
	api用到再说吧
	

4、进阶写法:with
	# 自动管理IO资源，自动管理，比较方便
	try:
        with oepn("test.txt","a") as file1:
            print(file1.read())
    except FileNotFoundError:
    print('指定的文件无法打开.')
    except IOError:
    print('读写文件时出现错误.')
	
5、异常处理机制
	try:
		file = open('致橡树.txt', 'a', encoding='utf-8')
        file.write('\n标题：《致橡树》')
    except Exception as err:
    	print(err)
    finally:
    	if file is not None:
            file.close()
```



## 5、PIP

```
通过pip可以下载第三方库，非常常用

比如我要下载requests
terminal: pip install requests

import requests
resp = requests.get('http://api.tianapi.com/guonei/?key=APIKey&num=10')
if resp.status_code == 200:
    data_model = resp.json()
    for news in data_model['newslist']:
        print(news['title'])
        print(news['url'])
        print('-' * 60)

【通过下面几个案例，你就知道了python可以利用第三方库做很多事情】
1、拓展：python读写CSV文件、Excel文件、PDF文件
	AI去写即可。

2、拓展：用Pillow处理图像
	Pillow 是由从著名的 Python 图像处理库 PIL 发展出来的一个分支，通过 Pillow 可以实现图像压缩和图像处理等各种操作。可以使用下面的命令来安装 Pillow  ：   pip install pillow
	Pillow 中最为重要的是Image类，可以通过Image模块的open函数来读取图像并获得Image类型的对象。
	AI去写即可。
```

## 6、多线程、异步

```
1、基本案例
import threading
import time
def task(name):
	print(f"{name} start")
	time.sleep(5)
	print(f"{name} end")
	
t1 = threading.Thread(target=task,args=("A",))
t2 = threading.Thread(target=task,args=("B",))

t1.start()
t2.start()

t1.join()
t2.join()

print("main end")

2、核心API
	① 创建线程 threading.Thread(target=线程要执行的函数,args=("线程名字",)) #只有一个参数也要写逗号
	② 执行线程 start
	③ 阻塞线程 join 阻塞线程，直到当前线程执行完

3、python多线程的真相:GIL （Global Interpreter Lock）
	【python的多线程相比java、C++差距很大，python多线程其实是假的多线程！伪多线程！】
	
	GIL：CPython解释器中，只有一个GIL，同一时刻只允许一个线程执行python字节码
	结果：即使你开 8 个线程，Python 只能一个线程在执行 CPU 密集型代码
	适合场景：IO场景，比如文件读写、网络请求阻塞、数据库操作
	缺点：完全不适合CPU密集型操作，比如你做大量计算，可能还不如单线程速度快
	
	如何真正多线程？依靠第三方库吧，感觉都使用python了，也别指望使用多线程了

4、我们还可以通过线程池的方式将任务放到多个线程中去执行，通过线程池来使用线程应该是多线程编程最理想的选择
5、python还可以直接多进程，这样就可以打破python解释器只有一个GIL导致多线程利用率不高的问题。

4、异步
import asyncio

async def task(name):
    print(f"{name} start")
    await asyncio.sleep(1)  # 非阻塞 I/O
    print(f"{name} end")

# 事件循环运行协程
asyncio.run(task("A"))
```

## 7、Mysql

```
1、python如何接入mysql？
	在 Python3 中，我们可以使用mysqlclient或者pymysql三方库来接入 MySQL，二者的用法完全相同，只是导入的模块名不一样。我们推荐大家使用纯 Python 的三方库pymysql，因为它更容易安装成功。
	① 下载
	pip install pymysql cryptography
	② 实战：【最好用实习当时的python脚本】
	# 1. 创建连接（Connection）
conn = pymysql.connect(host='127.0.0.1', port=3306,
                       user='guest', password='Guest.618',
                       database='hrs', charset='utf8mb4')
try:
    # 2. 获取游标对象（Cursor）
    with conn.cursor() as cursor:
        # 3. 通过游标对象向数据库服务器发出SQL语句
        affected_rows = cursor.execute(
            'insert into `tb_dept` values (%s, %s, %s)',
            (no, name, location)
        )
        if affected_rows == 1:
            print('新增部门成功!!!')
    # 4. 提交事务（transaction）
    conn.commit()
except pymysql.MySQLError as err:
    # 4. 回滚事务
    conn.rollback()
    print(type(err), err)
finally:
    # 5. 关闭连接释放资源
    conn.close()
	
```



## 二、大数据开发

## 1、了解一下

```
1、什么是大数据开发？
	python的话，本质就是利用python作为开发语言，完成对海量数据的采集、存储、分析、计算与服务化。
	适用场景：① 用户行为分析：用户点了什么，看了多久，哪一步流量流失最多
			② 视频网站数据分析：视频播放次数、弹幕密度、哪一秒最多人推出、完播率
			③ 业务指标统计/数据报表
			④ 日志分析 & 运维监控
			⑤ 推荐系统：推荐系统底层肯定依赖你账号的数据分析进行推荐，这也是根据海量数据推算出来的
			可以看到，大数据开发其实也有很重要的作用，都是基于海量数据采集+开发(分析)，

2、相关组件
	Hadoop：一整套生态：里面又包括HDFS、MapRedece(逐渐被Spark取代)
	
3、Hadoop:
	HDFS:分布式存储文件系统，负责存储数据。进行大数据开发，数据量肯定很大，可能有1TB的日志文件放到本地/常规数据库都不方便，
		 HDFS要做的就是把文件切成块，每个块存放到不同的服务器，每个块存放三份副本
	Spark:用来快速处理海量数据的分布式计算引擎
	举个例子：
		from pyspark.sql import SparkSession

        # 1. 创建 SparkSession（入口）
        spark = SparkSession.builder \
            .appName("demo") \
            .getOrCreate()

        # 2. 读取 HDFS 或本地数据
        df = spark.read.csv("hdfs://localhost:9000/data/logs/access.log")

        # 3. 做简单处理
        df.show()

        # 4. 统计
        df.groupBy("_c0").count().show()
```



# 三、Django

```
python中的web框架
```



# 四、爬虫

```
1、Robots协议：
	网络爬虫这个领域目前还属于拓荒阶段，虽然互联网世界已经通过自己的游戏规则建立起了一定的道德规范，即 Robots 协议（全称是“网络爬虫排除标准”），但法律部分还在建立和完善中，也就是说，现在这个领域暂时还是灰色地带。
	比如淘宝对爬虫的限制，从下面来看淘宝禁止百度爬取任何资源，你无法在百度上直接搜到淘宝的内部信息：
	User-agent: Baiduspider
    Disallow: /

2、往事回顾：我在杭州实习的时候就搞过python爬虫，虽然是比较简单的类型吧，也算一次不错体验

3、使用python爬取网络资源:
  ① 推荐requests库；
  ② 使用Selenium，会真正打开浏览器并执行页面，还记得杭州第一次就用的这个，虽然后面改成   了reuqests发送请求了
  ③ 当你写了很多个爬虫程序之后，你会发现每次写爬虫程序时，都需要将页面获取、页面解析、爬虫调度、异常处理、反爬应对这些代码从头至尾实现一遍，很多是重复劳动。利用爬虫框架可以提高效率，而在所有的爬虫框架中，Scrapy 应该是最流行、最强大的框架
  
4、使用IP代理，让爬虫程序隐蔽自己的身份是很重要的，很多网站对爬虫是比较反感的。
```





# 五、数据分析

```
而是结合公司的业务，完成监控数据、揪出异常、找到原因、探索趋势等工作。不管你是用 Python 语言、Excel、Tableau、SPSS或其他的商业智能工具，工具只是达成目标的手段，数据思维是核心技能，从实际业务问题出发到最终发现数据中的商业价值是终极目标。数据分析师在很多公司只是一个基础岗位，精于业务的数据分析师可以向数据分析经理或数据运营总监等管理岗位发展；对于熟悉机器学习算法的数据分析师来说，可以向数据挖掘工程师或算法专家方向发展，这些岗位除了需要相应的数学和统计学知识，在编程能力方面也比数据分析师有更高的要求，可能还需要有大数据存储和处理的相关经验。
【感觉和数学关联很大】
```



# 六、机器学习

```
1、what is machine learning ?
	机器学习是人工智能的一个子领域。
	人类通过记忆和归纳这两种方式进行学习，通过记忆可以积累单个事实，使用归纳可以从旧的事实推导出新的事实。机器学习是赋予机器从数据中学习知识的能力，这个过程并不需要人类的帮助（给出明确的规则）。
	机器学习算法和传统算法最根本的区别。传统的算法需要计算机被告知如何从复杂系统中找到答案，算法利用计算机的运算能力去寻找最佳结果。传统算法最大的缺点就是人类必须首先知道最佳的解决方案是什么，而机器学习算法并不需要人类告诉模型最佳解决方案，取而代之的是，我们提供和问题相关的示例数据。

2、机器学习已然广泛渗透生活
	① 图像识别与计算机视觉：（使机器能够理解和处理图像和视频数据）
		汽车可以识别障碍物自动驾驶、自动为图像打标签比如阿丘AI缺陷、人脸识别
	② 自然语言处理：（让计算机能够理解和生成自然语言）
		语音识别、机器翻译、文本生成、聊天、对话
	③ 金融领域：
		风险管理、预测和自动化交易等方面

3、机器模型主要分类：
这里简单列举按照学习方式进行分类，其他的就不多说了，有兴趣自己了解吧
① 监督学习（Supervised Learning）
    回归（Regression）：用于预测连续值的模型，例如线性回归、Ridge 回归、Lasso 回归等。
    分类（Classification）：用于预测离散类别的模型，例如逻辑回归、支持向量机、决策树、随机森林、k近邻、朴素贝叶斯等。
    
② 无监督学习（Unsupervised Learning）
    聚类（Clustering）：用于将数据分组的模型，例如K均值聚类、层次聚类、DBSCAN 等。
    降维（Dimensionality Reduction）：用于减少特征数量的模型，例如主成分分析（PCA）、线性判别分析（LDA）、t分布随机近邻嵌入（t-SNE）等。
    关联规则学习（Association Rule Learning）：用于发现数据集中项之间关系的模型，例如 Apriori 算法、Eclat 算法等。
    
③ 半监督学习（Semi-Supervised Learning）
	结合了监督学习和无监督学习的方法，使用大量未标记的数据和少量标记的数据来构建模型。
④ 强化学习（Reinforcement Learning）
	基于奖励机制的学习方法，例如Q-Learning、深度Q网络（DQN）、策略梯度方法等。

4、
```















































