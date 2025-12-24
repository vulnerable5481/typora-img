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
		return 1,"Tom",18
	# 注意这里返回的不是三个值，而是一个user对象的元组，不允许修改
	# return 1,2,3 这样就是返回一个字典，允许修改
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
	
	if _name_ == "_main_":
		main()
   	    	
   	    	
   	    	
   	    	
【注意事项】   	    	
1、i++是不存在的，+对于py只是一个自增符
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
		
4、字典(dict): 不就是对象吗
	user = {
		"id":1,
		"name":"Tom",
		"age":18
	}
	user.get("age")
	user["age"] = 20
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
		super.
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

























































































