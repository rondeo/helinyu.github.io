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

16、面向对象















