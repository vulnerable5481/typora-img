

# JAVA与GO

```
下面我总结以下java转go的一些比较难受的点：

1、GO没有隐式转换，必须强转
2、函数可以有多个返回值
3、GO函数的参数永远是值拷贝，都会在内存老老实实copy一份，除非使用指针 or 接收函数返回值
4、不支持重载、嵌套，一个包不能有两个名字一样的函数
5、通过字母首大写来进行区分pubilc private protected，感觉很不直观

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
type xx struct/interface {} 声明结构体/接口
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

3、变量的初始化/类型的零值
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

4、字符与字符串
	""就是string，自带一些API
	''就是单个的字符,也就是char类型

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
	注意interface类型，只有当其值和类型都为nil的情况下，interface == nil
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
	感觉有点奇怪，但其实和其他语言的多维数组是没有区别的，就是根据语法怪怪的
	
5、可以通过内置函数len()、cap()计算长度
	len()计算的是集合当前元素的大小；
	cap()计算的是集合最大容量的大小；

【切片slice】
1、定义：切片是数组的引用，长度是动态的，依然值拷贝传递；其实和java中的arrayList、c++的vector比较相似
2、声明：var arrayList []int   
		var arrayList = make([]int,10)
3、切片表达式：
	slice[start:end]，左闭右开 [start,end)
	slice[:end]、slice[start:]，这两种都是省略写法，表示从0或者取到Len-1

4、一些API
	① 添加数据
	arrayList = append(arrayList,1) // append是一个全局函数，其次一定要接收，因为可能扩容，切片地址就变了所以要接收
	② 删除数据：强迫你意识到正在删除意味着内存的拷贝，需要谨慎，其他语言都用优雅的API掩盖，但是go会赤裸裸揭示
	// 第一种利用append拼接删除某个元素： [0,index) , [index+1,len)/[index+1,len-1]
	slice = append(slice[:index],slice[index+1:])
	// 第二种快速删除头节点、尾节点
	slice = slice[1:]
	slice = slice[:len(slice)-1]
	③ 标准库
	貌似go1.21版本之后引入了slices标准库，可以更优雅地删除
	## 说实话这跟之前区别也不大啊，一样难用
	slice = slices.Delete(slice,1,2) // 删除索引[1,2)之间的元素，也就是和删除索引1

5、含有中文字符串：
	str := "你好世界，hello"
	strArr := []rune(str)
```



### 1.4.3 指针

```
1、与C、C++指针的区别：
	区别于C、C++的指针，GO中的指针是安全指针，不能进行偏移和运算。
	
2、GO语言为什么会有指针？
	因为GO语言的函数传参永远都是值拷贝！不需要跟C++那样纠结参数是啥，因为函数的参数永远都是值拷贝，除非使用指针。所以在Go，指针操作很简单就是 &取地址、*根据地址取值，没别的了~~

3、空指针
	GO的指针被定义后没有被分配任何变量时， == nil
```



### 1.4.4 map

```
1、语法: var a = map[key_type]value_type
		var strMap = make(map[string]string,20)
	
2、判断map是否存在某个键
	value,is_contain := scoureMap["赵联城"]
	if is_contain {
		print(value)
	} else {
		print("查无此人")
	}

3、遍历统一使用for
	// 遍历map
	for key,value := range scoreMap {
		print(k,v)
	}
	// 只想遍历key
	for key := raneg scoreMap{
		print(key)
	}
	// 只想遍历value
	for _,value := range scoureMap{
		print(value)
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
	方法就是一个类内部的函数；方法有值接收者
	函数就是函数，不属于任何类型；函数没有值接收者

4、值接收者（有点接近self、this）
	语法：
		func(接收者变量 接收者类型) 方法名(参数列表) 返回参数 {}
		只有方法才有值接收者
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



### 1.4.6 make、new

```
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
	
	语法: make([]type,len) len可省略
	
	// 下面为b分配内存空间
	var b map[string]int = make(map[string]int , 10)
	b["age"] = 22
```



### 1.4.7 :与:=

```
1、区别：
	本质区别 : 就是 赋值 ， 而 := 是声明+赋值
	        : 如果没有声明就直接赋值是不允许的，会报错，除非你早就已经声明好了

2、问题的起因：
	for key,value = range hashMap {}
	for key,value := range hashMap {}
	我很好奇为什么这里要加:，因为外面没有声明key,value所以需要 先声明在赋值，需要使用 :=
	如果你确实想要使用第一种直接用=，那么必须先在外部声明key,value

3、作用域不同/变量屏蔽
	var key,value string
	for key,value = range hashMap {}
	----------
	for key,value := range hashMap {}
	可以看到第一种=，key和value的作用域放大了，可以在外部，但是如果是第二种key value都只能用在循环内部
	还有第三种，外部声明了key,value,但是依然使用了:=,这时候就出现了变量屏蔽，循环内部的key,value与外部的key value指向的的内     存地址不同
```



### 1.4.8 接口

```
1、基本使用
	① 定义：接口(interface)是一种类型，interface是一组method的集合
	② 签名：type 接口名 interface {
		test1()
		test2(string) int
		......
	}
	③ 注意事项、建议：
	 1.接口名：使用type将接口定义为自定义的类型名。Go语言的接口在命名时，一般会在单词后面添加er，如有写操作的接口叫                   Writer，有字符串功能的接口叫Stringer等。接口名最好要能突出该接口的类型含义。
     2.方法名：当方法名首字母是大写且这个接口类型名首字母也是大写时，这个方法可以被接口所在的包（package）之外的代码访问。
     3.参数列表、返回值列表：参数列表和返回值列表中的参数变量名可以省略。

2、例子：
	// 定义接口
    type Sayer interface {
        say()
    }
    // 实现接口
    type Dog struct {}
    func (d *Dog) say(){
    	print("wwww")
    }
    type Car struct {}
    func (c *Cat) say(){
    	print("mmmm")
    }
    // 多态的体现
    func main() {
    var x Sayer // 声明一个Sayer类型的变量x
    a := cat{}  // 实例化一个cat
    b := dog{}  // 实例化一个dog
    x = a       // 可以把cat实例直接赋值给x
    x.say()     // 喵喵喵
    x = b       // 可以把dog实例直接赋值给x
    x.say()     // 汪汪汪
}

3、空接口
	① 定义：空接口是指没有定义任何方法的接口。因此任何类型都实现了空接口。
		   空接口类型的变量可以存储任意类型的变量。
	② 语法： interface{} 或者 any
	③ 应用：
		// 空接口作为函数参数，可以接收任意类型的函数参数
		func show(a any) {}
		// 空接口作为map的值，实现保存任意值的字典
		var studentInfo = make(map[string]any,100)

4、类型断言
	① 作用：
		any空接口类型将不同的东西模糊化，类型断言将东西具体化
	② 语法：
		value,ok := x.(type)
		value就是x转化为type后的值，ok就是布尔值，表示断言成功还是失败
	③ 实际使用：
		假如有一个Animal接口，我们需要判断只有Bird类才会飞,这时候就需要类型断言
		if v,ok := adws.(Bird); ok {
			bird.fly() // 只有确认是鸟才能调用鸟类特有的方法
		}
```



## 1.5 流程控制

```
1、IF
	① 可以省略条件表达式的括号
	② 左边大括号必须和条件表达式在一行
	③ 自带初始化的条件表达式
	// 这在其他语言其实比较少见的
	比如  if err := recover(); err != nil {}

2、switch
	① 可以省略括号
	② 不需要显式地声明break！
	③ 支持类型判断，java17才支持这一功能
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

```go
函数的定义
func 函数名(参数列表) 返回值 {}

1、几个注意事项，或不同之处
	① 函数本身作为一个参数被使用
		func test(move() func){
			move()
		}
	② 参数名在前，类型在后，多个参数类型相同可叠在一起只用一个类型标识
	③ 函数可有多个返回值
	④ 默认情况全部是值传递，即使是引用类型，除非使用指针

2、闭包
	题外话：闭包的概念我很久之前在javascript了解过，但是遗忘了，而且也没感觉到有啥用，Go也支持闭包
	用到再说吧

3、defer 延迟返回
	① 定义、应用场景
	最实用的场景就是关闭文件句柄、锁资源的释放、数据库连接释放等等，主要就是资源管理
	其实defer有点类似于 finally，但是finally在最后，你try了几百行，可能都忘记上面都开了哪些资源
	如果使用defer，逻辑就是拿到资源先交代后事，打开资源的那一刻就反手一个defer，然后放心大胆地操作资源，反正已经defer兜底关闭
	② 语法
		// 第一种直接调用一个函数
        defer file.close()
        // 第二种匿名函数,注意末尾要加()，表示立即执行该函数，不然就写错了，相当于错写为defer file.close,你看得加()吧！
        defer func(){
            print("xx")
        }()
	③ 例子：
	f, err := os.Open("test.txt")
    if err != nil {
        return // 如果打开失败，f 是空的，你不需要也不应该去 Close 它
    }

    // 只有到了这一行，说明 f 成功拿到了，这时候赶紧注册“后事”
    defer f.Close()
    
    // 接下来你就可以放心地写业务逻辑了，不用再管关闭的事
    buf := make([]byte, 1024)
    f.Read(buf)
    fmt.Println(string(buf))
    }

4、异常处理
	① 异常分类：
	error:GO认为error是业务的一部分，是意料之中的错误，比如文件找不到、网络异常，应该在程序中显式处理
	panic:GO认为panic是程序的致命崩溃，是意料之外的错误，比如数组越界、内存溢出、空指针

	② 如何捕获异常？（defer+recover）
		defer预设后事 + recover拦截恐慌
		func main() {
    fmt.Println("程序开始...")
            
    ③ panic内置函数
      专门用来抛出异常
      panic("我是一个异常")
    
    ④ recover内置函数
      专门捕获panic，一般都会与defer一起使用
            defer func(){
                if err:=recover(); err != nil {
                    print("我捕获到了一个异常:",err.(string))
                }
            }
            
	③ 例子：
    // 1. 必须在 defer 闭包里调用 recover
    defer func() {
        if r := recover(); r != nil {
            // 如果 r 不为 nil，说明发生了 panic
            fmt.Printf("【捕获成功】拦截到致命异常: %v\n", r)
        }
    }()
    // 2. 模拟一个触发异常的操作
    doSomethingDangerous()
    fmt.Println("这行代码在 panic 之后，永远不会被执行")
}
func doSomethingDangerous() {
    // 第一种模拟手动抛出异常
    panic("牛魔，系统炸了！") 
    // 第二种模拟
    a := 2
    c := a/0
}
```



## 1.7 方法

```
1、方法定义、与函数的区别
	① 定义：方法就是一个包含接收者的函数，Golang里面的方法总是绑定对象实例，并隐式地将实例作为第一实参（接收者）
	② 区别：方法会由接收者，函数没有

2、方法的函数签名
	func (recevier type) 方法名(参数列表) 返回值 {}
	// 官方建议使用接收者类型名的第一个小写字母，而不是self、this之类的命名
	例如：
	func (p *Person) setName(name string) {
		p.name = name
	}

3、方法比函数更聪明
	普通的函数参数要求指针就必须传指针，参数要求值就必须传递值
	方法的参数要求指针/值，你可以传指针/值，Go底层会自动帮你转化
```



## 1.8 面向对象

```go
1、封装
	go没有private、public等关键字，它的封装就是通过首字母大小写控制
	
	① 类型名的大小写
	// 小写别的包进都进不去dog结构体内部，更别说获取里面的属性与方法了
    type dog struct {xx}
	// 大写可以进去，能否使用里面的东西取决于变量名的大小写
	type Dog struct {xx}

	② 变量名的大小写
	type Dog struct {
		// 大写相当于public
		Name string
		// 小写相当于private
		age int
	}
	// 可以通过get方法获取private字段
	func (d *Dog) getAge() int{
		return d.age
	}

2、继承
	① 匿名字段/嵌入字段
	// 这里只写类型Animal就可以直接使用父类Animal的字段，如果有同名字段可以区分
	type Dog struct {
		Animal
		habbit string
	}
	dog := Dog{Animal:Animal{Name:"醒醒"},habbit:"eat"}
	② 方法也自然被继承

3、多态
	【多态体现在接口类型变量】
		// 定义接口
    type Sayer interface {
        say()
    }
    // 实现接口
    type Dog struct {}
    func (d *Dog) say(){
    	print("wwww")
    }
    type Car struct {}
    func (c *Cat) say(){
    	print("mmmm")
    }
    // 多态的体现
    func main() {
    var x Sayer // 声明一个Sayer类型的变量x
    a := cat{}  // 实例化一个cat
    b := dog{}  // 实例化一个dog
    x = a       // 可以把cat实例直接赋值给x
    x.say()     // 喵喵喵
    x = b       // 可以把dog实例直接赋值给x
    x.say()     // 汪汪汪
}
```



# 2、并发编程



## 2.1 Go并发

```
1、goroutine（协程并发）
    ● 协程：coroutine。相当于轻量级线程或者用户级线程,goroutine是go语言发明的进化版协程
    ● 与传统的系统级线程和进程相比，协程最大的优势在于“轻量级”。可以轻松创建上万个而不会导致系统资源衰竭。而线程和进程通常很难超       过1万个。这也是协程别称“轻量级线程”的原因。
 	● 多数语言在语法层面并不直接支持协程，而是通过库的方式支持，但用库的方式支持的功能也并不完整，效率也没有很高
 
2、协程
	● goroutine从量级上看很像协程，可以简单说goroutine就是协程，或者说是协程一种进化版本
      一个线程中可以有任意多个协程，但同一时刻只跑一个协程，多个协程分享该线程分配到的计算机资源。
	● 执行goroutine只需要4~5kb，其栈内存不是固定的，可以按需变大变小，很灵活。也正因为如此，可同时运行成千上万个并发任务。
	● goroutine比thread更易用、更高效、更轻便。一个普通计算机跑几十个线程就有点负载过大，但是同样的机器却轻松跑成百上千协程
	
3、GPM
	● GPM是Go语言自己实现的一套调度系统，是运行时层面实现的。区别于操作系统调度OS线程。
	● ① G就是goroutine
	  ② P就是管理goruntie的队列，会保存当前goruntine的上下文（函数指针、堆栈空间、地址边界），会进行一些调度（比如暂停占用cpu         太长时间的goroutine），如果当前队列没有goroutine就去全局队列获取，如果全局队列也没有就去别的P队列抢任务。
	  ③ M（machine），指Go运行时对OS内核线程的虚拟，M与内核线程一般是一一映射的，一个goroutine最终还是要交给OS执行
	● P与M的关系也是一一对应的，总结来说，P管理着一组G，将其挂载到M上执行
	● P的个数是通过runtime.GOMAXPROCS设定（最大256），Go1.5版本之后默认为物理线程数。
	
4、Go并发的优势：
	① 除了上面一直强调的协程很轻量级
	② 还有一点Go是通过自己的一套调度系统GPM管理协程的，而非直接让OS调度。这个调度器会使用一个称为m:n调度的技术，调度m个goroutine到n个OS线程，这样的好处就是go的调度是在用户态完成的，不需要频繁切换内核态，内存分配与释放都是在用户态维护着一大块内存池，不直接调用OS的malloc函数，成本低很多。
	③ 另一方面充分利用了多核的硬件资源，近似的把若干goroutine均分在物理线程上

5、Go并发的实现
	① go关键字
	② channel类型
```



## 2.2 go关键字

```
在java/c++中我们要实现并发编程的时候，我们通常需要自己维护一个线程池，并且需要自己去包装一个又一个的任务，同时需要自己去调度线程执行任务并维护上下文切换，但是在Go，只需要将任务封装到一个函数，开启一个goroutine去执行即可。

1、使用goroutine
	非常简单，只需要在调用函数前加上go关键字即可，就相当于创建一个goroutine去执行该函数/任务
	func main(){
		// 对，就是如此简单粗暴
		go test()
	}

2、main自带一个默认的goruotine
	在程序启动时，Go程序就会为main()函数创建一个默认的goroutine。当main函数返回时该goroutine就结束了，所有在main函数的协程都会一同结束。
	主协程如果退出了，子协程当然会被杀死
```



## 2.3 channel

```
1、为什么需要channel？
	● 首先函数单纯并发执行是没有意义的，并发函数与函数之间进行数据交换才有意义。
	  如果涉及到数据交换，我们可以使用共享内存，但是这就涉及到加锁来避免竞争，开销会变大
	● Go语言的并发模型是CSP，提倡通过通信共享内存，而不是通过共享内存通信
	● 根据CSP的理念，Go采取了channel，channel是连接着goroutine之间的通道，让一个go协程发送数据给另一个go协程的通信机制。

2、语法: (channel是引用类型，零值是nil)
	① var 通道名 chan type 
	② 通道名 := = make(chan int,len)
	比如 test_chan := make(chan int,10) 创建了一个传输int类型的通道，缓冲大小为10个int

3、API
	① 发送和接收数据
		ch:=make(chan int)
		ch <- 10 // 把10发送到ch中
		x := <- ch // 从ch中接收数据
		<- ch // 从ch取数据但不接收

	② 关闭
		close(ch)
		关闭之后通道里的数据依然存在，文件不一样，通道不关闭GC自己能回收，不过一般情况都要手动close，不然会出现阻塞死锁问题
		● 对一个关闭的通道发送数据会panic
		● 对关闭一个已经关闭的通道会panic
		● 对一个关闭的通道依然可以获取数据，直到通道为空
		● 对一个关闭的且为空的通道进行接收操作会得到对于类型的零值

4、
```





























































