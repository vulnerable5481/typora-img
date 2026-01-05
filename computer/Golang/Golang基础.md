

# JAVA与GO

```
下面我总结以下java转go的一些比较难受的点：

1、GO没有隐式转换，必须强转
2、函数可以有多个返回值
3、GO函数的参数永远是值拷贝，都会在内存老老实实copy一份，除非使用指针 or 接收函数返回值
4、不支持重载、嵌套，一个包不能有两个名字一样的函数

下面是一些优点：

1、for循环可以遍历集合，很方便，语法都很统一
2、GO的结构体指针，可以直接获取属性，而非C++那样指针和实例的操作符分得很死：实例用.  指针用 ->
3、Go语言有一套官方统一的格式化标准，很方便
```



# 0、发展史

```
  go语言（或 Golang）是Google开发的开源编程语言，诞生于2006年1月2日下午15点4分5秒，于2009年11月开源，2012年发布go稳定版。
  很多公司，特别是中国的互联网公司，即将或者已经完成了使用 Go 语言改造旧系统的过程。经过 Go 语言重构的系统能使用更少的硬件资源获得更高的并发和I/O吞吐表现。充分挖掘硬件设备的潜力也满足当前精细化运营的市场大环境。
  go语言简单，学习成本低，开发效率=python、java，性能却又几乎=C/C++，天生支持并发，完美契合当下高并发的互联网生态。
  
  个人认为如果go的生态环境逐渐发展起来，是可以替代java的，所以未来go或者另外一个go终将会替代java，保持自身竞争力！
```



# 1、基础语法



## 1.1 主要特性

```
1、自带gc，可以像java一样自动管理内存
2、简单的思想，没有继承、多态、类等，大道至简，甚至只有25个关键字，37个保留字
3、语法底层支持并发，和拥有同步并发的channel类型，使并发开发变得非常方便。
4、函数多返回值
5、反射
```



## 1.2 项目结构

```
1、GOPATH( go1.11之前 )：
	$GOPATH/
        ├─ bin/   # 编译后的可执行文件
        ├─ pkg/   # 编译缓存
        └─ src/   # 所有源码（你的 + 第三方）
当前要求所有的go项目都必须放在$GOPATH/src下面，IDE要打开src，不过这个时代已经结束了

2、GO MOUDLE( now ):
   你可以把项目放在任意目录下面，比如E:\Study\goproject\firstProject
   然后 cd E:\Study\goproject\firstProject 
        go mod init hello
	项目结构会变成，IDE只需要打开hello这个目录即可,当然上面创建项目的步骤你也可以直接使用GOland
	hello/
        ├─ go.mod
        ├─ main.go
        └─ (其他 .go 文件)
```



## 1.3 变量、常量

### 1.3.1 声明

```
var：  声明变量  
const：声明常量
type： 声明类型
func： 声明函数
```

### 1.3.2 变量

```go
1、标准声明
        // 第一种 标准声明
         var a int
        // 第二种 类型推导
         var a  = 1  
        // 第三种 语法糖，只能在函数内部使用
             func main() {
                n := 1
                m := "zlc"
             }
 
2、批量声明
// 这种方式一般用于声明全局变量
 var (
 	a string
 	b int
 	c bool
 	d float32
 )

3、变量的初始化
    比如 string 默认就是 空字符串，bool默认就是 false 等等
	如果是slice、指针默认就是nil

4、匿名变量（lua等语言中也叫哑元变量）
	go语言函数可以有多个返回值，但有的值不需要，就用匿名变量接收，使用下划线_接收
	【匿名变量即不占用命名空间，也不占用内存！但是匿名变量不能用在函数外】
	func test(){
		return 1,2,"zlc"
	}
	func main(){
		// 此处只使用ab接收1，2，但是“zlc"我不需要，所以就用匿名变量接收，这样即不占用命名空间，也不占用内存
		a,b,_ := test()
	}
```

### 1.3.3 常量

```
iota用做自增长
const (
	unknown = iota // iota=0
    female         // iota = 1
    male 	       // iota = 2
)
```



## 1.4 类型

### 1.4.1 基本类型

```
1、整型
	有符号：int8 int16 int32 int64
	无符号：uint8 uint16 uint32 uint64
	其中，uint8就是我们熟悉的byte类型，int16对应java中的short,int32 = int ,int64 = long
	如果只写int，一般会根据平台自动对应，32/64

2、浮点型
	float32 = 其他语言float
	float64 = 其他语言double
	【注意float32/64必须指明，不能模糊，而且两者之间居然不能隐式转换！必须显式地强转，主要是因为go没有隐式转换】

3、复数 （这个类型其他语言还真没有直接当成基本类型）
	复数有实部和虚部，complex64，实部32位虚部32位，complex128同理均分

4、string
	依然""没啥区别吧，自带一些API

5、uint8(也就是byte)、rune类型
	可以使用uint8和rune 当作char类型去获取字符串的每一个字符：
        ① uint8类型，或者叫 byte 型，代表了ASCII码的一个字符。
        ② rune类型，代表一个 UTF-8字符。
    为什么会存在rune类型呢?
    	因为当需要处理中文、日文或者其他符合字符时，需要使用rune类型，rune本质就是int32,go使用特殊rune类型处理Unicode编码，
    	使得unicode的文本处理更加方便，也可以使用uint8进行默认字符处理，性能和拓展性都有照顾

这里额外说一下编码问题，此前对这里有点小模糊：
	在早期的编程语言中，比如C语言诞生的年代，ASCII码是主流，一个字符就是一个字节，但到了互联网时代，为了兼容全球语言，unicode(为全世界每个字符都分配一个唯一的数字编号)，问题是unicode只是编号，它在计算机怎么存储呢？用的是UTF-8编码，而UTF-8是变长的，一个英文占1字节，一个汉字通常占用3个字节，如果只使用byte(uint8)去处理字符串，遇到汉字岂不是每次只能拿到汉字的三分之一，这就出现了乱码或截断。
	GO为什么详细拆分为uint8、rune?
	主要是为了两种目的，第一种是传输/存储需求，这里只关心数据占了多少空间，不关心内容，byte即可
				     第二种是文本逻辑需求，我需要解析字符串，如果是中文需要用rune不然就出现乱码，无法阅读

6、nil
	每个类型若没有被初始化就，就等于自己的零值，比如bool = false,int = 0之类的
	而对于指针、slice、map等类型的零值就是nil，nil的本质就是说你这个变量没有分配对应的内存空间
```



### 1.4.2 数组、切片

```
之所以把数组单独拿出来，是因为GO的数组和我们熟悉的数组不太一样。

【数组】
1、定义：是同一种类型的固定长度的序列
2、声明：var arr[10] int  
	   var arr [10]int = [10]int{1,2,3,4}
	   // 下面这种写法更简单一点
	   var arr = [10]int{1,2,3,4}
	   // 声明也可以指定对应下标的值
	   var arr = [10]int{1:1, 3:2, 7:123}
	   // 局部变量的语法糖
	   arr := [10]int{1,2,3}
3、注意如果把数组传给一个函数，是全量拷贝，会将数组完整复制一份给函数，所以不会影响外面的数组，但是java数组就会影响，因为java只是把指向数组的指针复制一份给函数，即使是List也如此，而C++原生数组更是将数组的头指针传给函数，这样就只有数组头指针，连数组大小都不知道，所以C++一般都用标准库，比如定长数组std::array,动态数组std::vector ，这两个都是值传递，会全量拷贝，不会影响外面数组
【原生数组，C++和java的数组会传递真正的数组地址啊，C++的vector是值传递，但是java的List是对象，是引用传递】
【GO的原生数组并不传递真正的数组地址，而是全量拷贝，是值传递】
4、多维数组
	var arr = [2][3]int{1,2,3},{3,2,1}
	这里你是不是可能感觉很奇怪，GO的数组定义了2个长度为3的数组，这个和其他语言定义的很不一样！
5、可以通过内置函数len()、cap()计算长度


【切片slice】
1、定义：切片是数组的引用，长度是动态的，依然值拷贝传递；其实和java中的arrayList、c++的vector比较相似
2、声明：var arrayList []int   
```



### 1.4.3 指针

```
1、与C、C++指针的区别：
	区别于C、C++的指针，GO中的指针是安全指针，不能进行偏移和运算。
	
2、GO语言为什么会有指针？
	因为GO语言的函数传参永远都是值拷贝！不需要跟C++那样纠结参数是啥，因为函数的参数永远都是值拷贝，除非使用指针。所以在Go，指针操作很简单就是 &取地址、*根据地址取值，没别的了~~

3、空指针
	GO的指针被定义后没有被分配任何变量时， = nil

4、new、make
	为什么需要new和make?
		如果是值类型会自动分配内存空间，会自动初始化，但是如果是引用类型，比如map、slice之类的，必须显式声明分配内存空间
		比如: 
			// 这就不对，因为map类型的零值是nil,压根没有被分配内存空间，你在向“虚无”添加一个键值对
			 var b = map[string]int
			 b["age"] = 22 
		   // 同理，因为指针的零值是nil，压根没有被分配内存空间，你在向"虚无"赋值，当然报错啊
		   	 var a *int
		   	 *a = 100

4.1 new
	首先内置函数new不常用！比如我们很少会孤零零地声明一个指向基础类型的指针。
	new的函数签名：  func new(Type) *Type
	// 下面为a分配一个int大小的内存空间
	var a *int = new(int)
	*a = 100
	
4.2 make
	make也是用于内存分配，它只为slice、map、以及chan分配内存，返回三个类型本身，因为三个都是引用类型，无需返回它们的指针
	make函数是很常用的，我们初始化slice map channal的时候，都需要进行make初始化，然后才可以对它们操作
	
	语法: make([]type,len)
	
	// 下面为b分配内存空间
	var b map[string]int = make(map[string]int , 10)
	b["age"] = 22
```



### 1.4.4 map

```
1、语法： var a = map[key_type]value_type
	
2、判断map是否存在某个键
	value,is_contain := scoureMap["赵联城"]
	if is_contain {
		print(value)
	} else {
		print("查无此人")
	}

3、遍历统一使用for
	// 遍历map
	for key,value = range scoreMap {
		print(k,v)
	}
	// 只想遍历key
	for key := raneg scoreMap{
		print(key)
	}

4、删除
	delete(map,key)
```



### 1.4.5 结构体

```
1、类与结构体
	GO中没有传统面向对象中类、继承、多态等概念，GO通过结构体的内容再配合接口比面向对象具有更高的拓展性、灵活性
	简单来说就是GO中通过结构体来实现面向对象

2、结构体定义、实例化
	type 类型名 struct {
		字段名 字段类型
		字段名 字段类型
		 ...   ... 
	}
	例如：定义person类，并且实例化
	 type person struct {
	 	name string
	 	age  int
	 	city string
	 }
	 // 第一种实例化
	 var zlc person
	 zlc.name = "赵联城"
	 ....
	 // 第二种实例化
	 zlc := {
	 	name:"赵联城",
	 	age:22,
	 	city:"深圳"
	 }

3、方法与函数的区别
	方法就是一个类内部的函数
	函数就是函数，不属于任何类型

4、值接收者（有点接近self、this）
	语法：
		func(接收者变量 接收者类型) 方法名(参数列表) 返回参数 {}
		接收者变量：接收者中的参数变量名在命名时，官方建议使用接收者类型名的第一个小写字母，而不是self、this之类的命名
	例子：
		// person 结构体
		type person struct {
			name string
			age int
		}
		// sayHello
		func(p Person) sayHello() {
			fmt.Printf("hello,%s\n",p.name)
		}

5、指针类型的接收者（非常接近self、this）
	定义：
		指针类型的接收者就是一个结构体的指针，通过指针修改也能直接修改具体实例的成员变量，所以指针类型的接收者更加接近我们经常说         的java的this,python的self之类的
	例子：
        func (P *Person) setAge(age int) {
            p.age = age
        }
    区别：值接收者只是在修改副本，指针接收者修改的是原件
    使用范围：
    	① 需要使用指针修改接收者的值
    	② 接收的是一个拷贝代价高的大对象
    	③ 保证一致性，如果某个方法使用指针接收者，其他方法也应该使用指针接收者

6、嵌套结构体中的命名冲突
	指明是谁的哪个字段即可解决冲突
	user3.Address.createTime
	user3.Email.createTime
	
7、结构体的tag，标签
	就是结构体的元信息
```



## 1.5 流程控制

```
1、IF
	① 可以省略条件表达式的括号
	② 左边大括号必须和条件表达式在一行

2、switch
	① 可以省略括号
	② 不需要显式地声明break！
	③ 可以直接判断变量类型，java17才支持这一功能
	switch (a) {
		case 1:
			print(1)
		case 2:
			print(2)
		default:
			print("无事发生")
	}
	
3、for的三种用法
	// 第一种：最正常的一种
	s := "abcderfqaas"
	for (i,n:=0,len(s);i<n;i++) {
		print(s[i])
	}
	// 第二种：替代while
	for (n>2){
		xxx
	}
	// 第三种：替代while(true)  or  for(;;) 
	for {
		xxx
	}


4、循环语句for range
	① for range 可以做for能做的，也能做for不能做的
	② 专门用来循环集合（数组、map、slice、字符串），类似java中的迭代器
    
        for k,v := range oldMap {}
        for index,value := range s {}
        // 如果不需要某些值可以忽略
        for _,value := range s {}
        // 忽略全部，仅迭代
        for range s {}



5、select
	特性：
		你在别的语言都找不到，这是GO的特性之一，专门为并发而设计的！
	定义与区别：
		switch是在多个“值”之间选择，select是在多个“事件”之间选择
	典型用法の超时判断：

6、goto
	用到再说吧，感觉用不太到
		
```



## 1.6 函数

```
1、几个注意事项，或不同之处
	① 函数本身作为一个参数被使用
		func test(move() func){
			move()
		}
	② 参数名在前，类型在后，多个参数类型相同可写在一起只用一个类型
	③ 函数可有多个返回值
		return 1,2,"zlc",person
	④ 默认情况全部是值传递，即使是引用类型，除非使用指针

2、defer 延迟返回
	最实用的场景就是做一个最终的检测，给原本要崩溃的程序返回一个错误or默认值
	func test(a int b int ) (res int) {
		defer func(){
			if res < 10 {
				print("检测到结果过小,出现异常！")
				// 这里可以改变res，也可以不改变，不改变依然返回res原本的值
				// res = -1
			}
		}
		res := a + b
		return res
	}
```





















































































