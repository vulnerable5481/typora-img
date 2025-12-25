# NULL

```
学习python，只打算速通一下基础知识，简单学一下相关的类库使用，需要使用python编写脚本就用AI搞完事了，自己能看懂修缮即可。
```



# 一、基础语法



## 1、差异

```
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

## 二、大数据入门



































































