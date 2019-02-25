---
title: CMake 以及衍生
date: 2019-02-24 21:40:28
tags: tool
categories: tool
---
cmake：[源代码](https://github.com/Kitware/CMake.git) [官方网址](https://cmake.org/)  [3.12版本文档](https://cmake.org/cmake/help/v3.12/)

CMake[cross platform make]是一个跨平台的安装（编译）工具，
1）可以用简单的语句来描述所有平台的安装(编译过程)。
2）输出各种各样的makefile或者project文件，能测试编译器所支持的C++特性,类似UNIX下的automake。只是 CMake 的组态档取名为 CMakeLists.txt。
3）Cmake 并不直接建构出最终的软件，而是产生标准的建构档（如 Unix 的 Makefile 或 Windows Visual C++ 的 projects/workspaces），然后再依一般的建构方式使用。  这使得熟悉某个集成开发环境（IDE）的开发者可以用标准的方式建构他的软件，这种可以使用各平台的原生建构系统的能力是 CMake 和 SCons 等其他类似系统的区别之处。

功能：
CMake 可以编译源代码、制作程序库、产生适配器（wrapper）、还可以用任意的顺序建构执行档。CMake 支持 in-place 建构（二进档和源代码在同一个目录树中）和 out-of-place 建构（二进档在别的目录里），因此可以很容易从同一个源代码目录树中建构出多个二进档。CMake 也支持静态与动态程式库的建构。
“CMake”这个名字是“cross platform make”的缩写。虽然名字中含有“make”，但是CMake和Unix上常见的“make”系统是分开的，而且更为高阶。


```
make 和cmake有什么区别？
1、GCC是多种语言的编译器；（括C、C++、Objective-C、Fortran、Java等等）【如果你的源文件只有一个的时候，直接用gcc命令编译它； 多个源文件时，用gcc命令逐个去编译时，工作量大且混乱】
2、多个源文件如果编译？ ———>make
一个只能批处理的工具，【本身没有编译和链接的功能】，通过调用makefile文件中用户指定的命令来进行编译和链接的（可能make文件里面就写了gcc的编译命令）
3、makefile文件是什么? 上面： 存储编译命令，；比喻：简单的说就像一首歌的乐谱，make工具就像指挥家，指挥家根据乐谱指挥整个乐团怎么样演奏，make工具就根据makefile中的命令进行编译和链接的。(eg: makel命令中包含调用gcc编译某个源文件的命令)；make做一些简单的工程可以人手工在makefile文件里面添加编译等等命令；【（缺点）如果项目足够很大的时候，这样工作量也很大；如果换了平台，makefile又要重新修改】；
4、[跨平台]CMake工具解决makefile上手工添加命令的缺点；cmake就可以更加简单的生成makefile文件给上面那个make用； 同时扩平台【不用修改makefile文件】， 等等其他功能；
5、cmake如何生成makefile文件的？ —— CMakeLists.txt 文件（学名：组态档），通过它来生成makefile；所以，我们手工写CMakeLists.txt 这个文件即可【这个文件写入简单】
6、
cmake是用来生成Makefile文件的工具，生成Makefile文件的工具还有autotools，Qt环境下还有qmake
参考链接:
https://blog.csdn.net/jc_benben/article/details/78571728
https://www.cnblogs.com/sunsky303/p/7750299.html?utm_source=debugrun&utm_medium=referral

PS：cmake 不仅仅是make

```
>执行命令： cmake CMakeLists.txt 

看一下cmake的代码，里面写了什么， 建立系统、打包、创建测试环境；

&& ————————————————cmake的简单实用————————————
cmake_minimum_required(VERSION 3.12) // 这里的version要注意是当前系统的版本
[项目简单实践](https://www.jianshu.com/p/8df5b2aba316)
明天接着运行上面的例子；

CMakeList.txt 文件构建（写） 这里就是cmake的写法 【注意，写的时候不要有逗号在参数见】

好像SET这个命令有问题呀；??? 是不是我使用出现了错误还是在mac上不能够这样使用？
有关的书籍， 我们应该如何去存储？

[cmake实践](../../../../books/CMake Practice.pdf)
[实践参考链接](https://www.hahack.com/codes/cmake/)
set应该如何去使用？


https://cmake.org/cmake/help/v3.12/index.html 文档链接 内容如下
```
Command-Line Tools： 3个命令行
cmake 
ctest 
cpack

Interactive Dialogs： 交互的窗口（可视化界面）
cmake-gui(1)
ccmake(1)

Reference Manuals ： 参考手册
cmake-buildsystem(7) 主要介绍链接了系统的库内容
cmake-commands(7) 一些命令的设置
cmake-compile-features(7) 编译特色 【也就是编译指定的特点或者针对支持】
cmake-developer(7)
cmake-env-variables(7)
cmake-generator-expressions(7)
cmake-generators(7)
cmake-language(7)  语言，这个需要详细去查看
cmake-modules(7)
cmake-packages(7)
cmake-policies(7)
cmake-properties(7)
cmake-qt(7)
cmake-server(7)
cmake-toolchains(7)
cmake-variables(7)
```
总结： 这个项目主要是用cmake来构建代码编译打包等；有关内容，通过真实的项目来实现；

>几个关键字：CMakeLists.txt Makefile make cmake 



