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
