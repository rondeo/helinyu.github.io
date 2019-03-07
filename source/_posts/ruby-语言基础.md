---
title: ruby 语言基础
date: 2019-03-03 03:43:27
tags: ruby
categories: 编程语言
---




【基本的语法复习完成即可(对于web的项目也可以去实现看接下来的安排)】

<h2> 一、ruby语言基础复习 </h2>
[教程的地址【H看】](http://www.runoob.com/ruby/ruby-tutorial.html)

1、略过  ruby安装不同的平台等环境以及步骤。
2、中文编码问题,（有可能有些安装环境并没有支持中文编码）
>可能出现的问题： invalid multibyte char (US-ASCII) 

PS： 
>1）设置utf-8解析源码
2）设置文件编码为utf-8 保存
```
#!/usr/bin/ruby -w
# -*- coding: UTF-8 -*- #  多了上面这一行
puts "你好，世界！ssss";
```
3、ruby命令行 【也就是指定ruby脚本可以添加的一些参数】 
其实和其他命令没有什么差别， 
>ruby [ options ] [.] [ programfile ] [ arguments ... ]

> man ruby  || ruby -h

下面是对应的饿命令参数：
>-w              turn warnings on for your script [显示出警告的内容]

4、环境变量 env
> 含义： 环境变量是用来控制ruby解释器来控制它的行为。

终端上输入： env 即可查看当前编译器设置的环境变量列表

5、基本语法（基本约定）：
1）
1、1） 空白字符（空格、制表符）【同般】
1、2）有时用来解释模棱两可的语句 ，启用 -w 会出现警告
>eg：
a + b 被解释为 a+b （这是一个局部变量）
a  +b 被解释为 a(+b) （这是一个方法调用）

2） ruby 行尾
2、1）分号和换行 【同般】
2、2）运算符；eg：+、- 、反斜杠 表示语句延续

3）标示符
3.1）【同般】 （同一班的语言）大小写敏感

4）保留字
BEGIN	do		next		then
END		else		nil		true
alias	elsif		not		undef
and		end		or		unless
begin	ensure	redo	until
break	false	rescuse	when
case	for		retry	while
class	if		return	while
def		in 		self		__FILE__
defined? module	super	__LINE__	

5)ruby 中here document（以前没有的概念） ——> 建立多行字符串
```
print <<EOF
    这是第一种方式创建here document 。
    多行字符串。
EOF
```
<< 之后，可以制定一个字符串或者标示符来终止， 上面； EOF， 
EOF所有行的字符串就是我们要的值。
请注意<< 和终止符之间必须没有空格。

6) BEGIN、END 语句
BEGIN：程序在运行之前被调用
END：程序在运行结尾调用
```
#!/usr/bin/ruby
puts "这是主 Ruby 程序"
BEGIN {
   puts "初始化 Ruby 程序"
}

#!/usr/bin/ruby
 
puts "这是主 Ruby 程序"
 
END {
   puts "停止 Ruby 程序"
}
BEGIN {
   puts "初始化 Ruby 程序"
}
```

8)ruby注释
【同般】 #开头

6、数据类型 （略过）

7、类和对象 以及类案例   
ruby是完美的面向对象语言
特征：
* 数据封装
* 数据抽象
* 多态性
* 继承


1)类定义： （同般）
```
class Customer
.......

end
```

2）类中变量 （4种）
2.1）局部变量： 方法中定义的变量，局部变量以小写字母或 _ 开始。（同般）
2.2）实例变量： 实例变量可以跨任何特定的实例或对象中的方法使用。这意味着，实例变量可以从对象到对象的改变。实例变量在变量名之前放置符号（@）。 【这个不是很理解】
2.3）类变量：  可以跨不同的对象，(同般) 类变量在变量名之前放置符号（@@）。
2.4）全局变量：类变量不可以跨类使用， 全局变量可以，全局变量总是以美元符号（$）开始。

3）Ruby 类中的成员函数，函数被称为方法。每个方法是以关键字 def 开始，后跟方法名。
```
class Sample
   def function
      statement 1
      statement 2
   end
end
```
不错的例子：
```
#!/usr/bin/ruby

class Customer
   @@no_of_customers=0
   def initialize(id, name, addr)
      @cust_id=id
      @cust_name=name
      @cust_addr=addr
   end
   def display_details()
      puts "Customer id #@cust_id"
      puts "Customer name #@cust_name"
      puts "Customer address #@cust_addr"
   end
   def total_no_of_customers()
      @@no_of_customers += 1
      puts "Total number of customers: #@@no_of_customers"
   end
end

# 创建对象
cust1=Customer.new("1", "John", "Wisdom Apartments, Ludhiya")
cust2=Customer.new("2", "Poul", "New Empire road, Khandala")

# 调用方法
cust1.display_details()
cust1.total_no_of_customers()
cust2.display_details()
cust2.total_no_of_customers()
```


>变量、运算符、注释、条件判断、循环、方法（略） 【这些都是略过的内容】

8、ruby中的 块
* 块由大量的代码组成。
* 您需要给块取个名称。
* 块中的代码总是包含在大括号 {} 内。
* 块总是从与其具有相同名称的函数调用。<font color=red>这意味着如果您的块名称为 test，那么您要使用函数 test 来调用这个块。</font>
* 您可以使用 yield 语句来调用块。

```
block_name{
   statement1
   statement2
   ..........
}
```

1)
```
这样的一个例子：
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-

def test
   puts "在 test 方法内"
   yield
   puts "你又回到了 test 方法内"
   yield
end
test {puts "块内代码执行"}

|| 上面这个例子，如果将类名字改为test1 ，将会出现错误，或者同时将块的名字test改为test1.

```
2)
```
带有参数：
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-

def test
   yield 5
   puts "在 test 方法内"
   yield 100
end
test {|i| puts "你在块 #{i} 内"}
|| yield 语句后跟着参数。您甚至可以传递多个参数。在块中，您可以在两个竖线之间放置一个变量来接受参数。
|| yield a, b   # 多个参数传递的方式
   test {|a, b| statement}
```
3)块和方法 ：通常使用 yield 语句从与其具有相同名称的方法调用块
* 如果方法的最后一个参数前带有 &，将向该方法传递一个块，且这个块可被赋给最后一个参数。如果 * 和 & 同时出现在参数列表中，& 应放在后面。

```
#!/usr/bin/ruby

def test(&block)
   block.call
end
test { puts "Hello World!"}
```

ps: 块的概念 ——> 代码块(函数的方式调用) ———>  无参数、参数、取地址的方式

9、字符串（略）有关查询可以到菜鸟教程里面

10、数组、哈希、日期、范围（略)

11、迭代器

12、文件的输入和输出

13、file类和方法

14、Dir类和方法

15、异常

<h3>高级内容</h3>

16、面向对象 （基本上看了，但是还没有所有的都理解执行了，明天回来再看一遍）
> 纯粹的面向对象语言； 一切哦都市对象到的形式纯在； 每个值都是一个对象（包括原始的 字符串、数字、true、false）；类本身也是一个对象（类是class类的一个实例）

1)ruby类定义
>定义了类的对象的蓝图：定义了类的对象将由什么组成，以及在该对象上能执行什么操作。【属性和方法】
```
class Box
   code
end

```
2)定义对象
> 由类创建，用 new 关键字声明类的对象。
```
box1 = Box.new
box2 = Box.new
```
3)initialize 方法 构造方法 （类比其他方法的：constructor
```
class Box
   def initialize(w,h)
      @width, @height = w, h
   end
end
```
上面：可以重写带有参数；

4）实例变量
就是ruby中定义的变量；
```
@ 	开头 ： 实例变量
@@	开头： 类变量
```
实例变量，外面不可以直接访问，可以通过下面说的访问器（setter、getter方法）和外部方法；


5）访问器(getter) & 设置器(setter)方法
```
由于两种方法非常常用，Ruby 定义了 attr_accessor :variable_name、attr_reader :variable_name、attr_writer :variable_name 三种属性声明方法。其中：accessor=reader+writer。

同时注意：变量名前一定要带 : ，变量名之间要用 , 分割。
```

6）实例方法
就是对象来进行呢调用的方法 （同般）

7）类方法 & 类变量
>类变量是在类的所有实例中共享的变量(类变量的实例可以被所有的对象实例访问);类变量（@@）作为前缀，类变量必须在类定义中被初始化.
<font color=red>
类方法使用 def self.methodname() 定义，类方法以 end 分隔符结尾。类方法可使用带有类名称的 classname.methodname 形式调用</font>

8) to_s
任何类都有一个 to_s 实例方法来返回对象的字符串表示形式;

9) 访问控制 。。。 后续处理
```
Public 方法： Public 方法可被任意对象调用。默认情况下，方法都是 public 的，除了 initialize 方法总是 private 的。
Private 方法： Private 方法不能从类外部访问或查看。只有类方法可以访问私有成员。
Protected 方法： Protected 方法只能被类及其子类的对象调用。访问也只能在类及其子类内部进行。
```

10）类的继承
Ruby 不支持多继承，但是 Ruby 支持 mixins。mixin 就像是多继承的一个特定实现，在多继承中，只有接口部分是可继承的。

11）方法重载
改变已经在父类中定义的方法的行为，这时您可以保持方法名称不变，重载方法的功能；

12） 运算符重载
 + 运算符执行两个 Box 对象的向量加法，使用 * 运算符来把 Box 的 width 和 height 相乘，使用一元运算符 - 对 Box 的 width 和 height 求反。


13) 冻结对象
防止对象被改变,它能有效地把一个对象变成一个常量。
任何对象都可以通过调用 Object.freeze 进行冻结。冻结对象不能被修改，也就是说，您不能改变它的实例变量。

14) 类常量
14.1）在类内部定义常量 （通过把一个直接的数值或字符串值赋给一个变量来定义的，常量的定义不需要使用 @ 或 @@）
14.2）常量的名称使用大写。在类的外部访问常量，那么您必须使用 classname::constant

15）使用 allocate 创建对象
15.1）想要在不调用对象构造器 initialize 的情况下创建对象，即，使用 new 方法创建对象；1
15.2） 使用allocate创建一个未初始化的对象


16) 类信息
>Ruby的代码逐行执行，所以在不同的上下文(context)self就有了不同的含义


17、ruby的正则表达式 （暂时略过）


18、Ruby 数据库访问  以及 Ruby 连接 Mysql （暂时略过）


19、 CGI编程 以及 CGI方法 [（通用网关接口）]
1）CGI 是Web 服务器运行时外部程序的规范,按CGI 编写的程序可以扩展服务器功能。
2）CGI 应用程序能与浏览器进行交互,还可通过数据库API 与数据库服务器等外部数据源进行通信,从数据库服务器中获取数据。
格式化为HTML文档后，发送给浏览器，也可以将从浏览器获得的数据放到数据库中。几乎所有服务器都支持CGI,可用任何语言编写CGI,包括流行的C、C ++、VB 和Delphi 等。
3）CGI 分为标准CGI 和间接CGI两种。
	* 标准CGI 使用命令行参数或环境变量表示服务器的详细请求，服务器与浏览器通信采用标准输入输出方式。
	* 间接CGI 又称缓冲CGI,在CGI 程序和CGI 接口之间插入一个缓冲程序，缓冲程序与CGI 接口间用标准输入输出进行通信

20、 ruby的cookie和session

21、 Ruby 发送邮件 - SMATp实现了发邮件的功能

22、Ruby Socket 编程


23、Ruby XML, XSLT 和 XPath 教程


24、SOAP

25、ruby上面多线程的使用过程

26、Ruby JSON （json数据解析）

27、RubyGems（ruby包管理器）















