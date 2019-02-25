---
title: CMake 以及衍生
date: 2019-02-24 21:40:28
tags: tool
categories: tool
---
CMake
*****

![cmake](../../../../asset/Snip20190226_3.png "cmake 代码架构")

CMakeLists.txt /*.cmake 都是构建的配置文件

CMake[cross platform make]是一个跨平台的安装（编译）工具，
* 1）可以用简单的语句来描述所有平台的安装(编译过程)。
* 2）输出各种各样的makefile或者project文件，能测试编译器所支持的C++特性,类似UNIX下的automake。只是 CMake 的组态档取名为 CMakeLists.txt。
* 3）Cmake 并不直接建构出最终的软件，而是产生标准的建构档（如 Unix 的 Makefile 或 Windows Visual C++ 的 projects/workspaces），然后再依一般的建构方式使用。  这使得熟悉某个集成开发环境（IDE）的开发者可以用标准的方式建构他的软件，这种可以使用各平台的原生建构系统的能力是 CMake 和 SCons 等其他类似系统的区别之处。

功能：
CMake 可以编译源代码、制作程序库、产生适配器（wrapper）、还可以用任意的顺序建构执行档。CMake 支持 in-place 建构（二进档和源代码在同一个目录树中）和 out-of-place 建构（二进档在别的目录里），因此可以很容易从同一个源代码目录树中建构出多个二进档。CMake 也支持静态与动态程式库的建构。
“CMake”这个名字是“cross platform make”的缩写。虽然名字中含有“make”，但是CMake和Unix上常见的“make”系统是分开的，而且更为高阶。


```
make 和cmake有什么区别？
*1、GCC是多种语言的编译器；（括C、C++、Objective-C、Fortran、Java等等）【如果你的源文件只有一个的时候，直接用gcc命令编译它； 多个源文件时，用gcc命令逐个去编译时，工作量大且混乱】
*2、多个源文件如果编译？ ———>make
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

cmake的源码应该怎么样子去看，我这里还不是很懂， 先看cmake里面的CMakeLists.txt文件吧；



2、Doxygen是一种开源跨平台的，以类似JavaDoc风格描述的文档系统，完全支持C、C++、Java、Objective-C和IDL语言，部分支持PHP、C#。注释的语法与Qt-Doc、KDoc和JavaDoc兼容。Doxygen可以从一套归档源文件开始，生成HTML格式的在线类浏览器，或离线的LATEX、RTF参考手册。

Doxygen 是一个程序的文件产生工具，可将程序中的特定注释转换成为说明文件。通常我们在写程序时，或多或少都会写上注释，但是对于其它人而言，要直接探索程序里的注释，与打捞泰坦尼克号同样的辛苦。大部分有用的注释都是属于针对函数、类型等等的说明。所以，如果能依据程序本身的结构，将注释经过处理重新整理成为一个纯粹的参考手册，对于后面利用您的程序代码的人而言将会减少许多的负担。不过，反过来说，整理文件的工作对于您来说，就是沉重的负担。

[xcode上配置Doxygen](https://www.cnblogs.com/1-434/p/8086435.html)

知道cmake里面使用了doxygen 来生成开发文档， 这里暂时先不管了； 到时候再去研究？？？？

3、cmake项目的源代码以及配置的了解
DartConfig.cmake 文件的内容
[Dart 语言链接，dart就是D语言](https://www.dartlang.org/guides/language/language-tour)
[Dart github地址](https://github.com/dart-atom)
[dart 语言应用在flutter项目中](https://flutterchina.club/using-packages/)

```
Dareconfig.cmake 文件的内容：
set(CTEST_PROJECT_NAME "CMake") // 设置测试的项目名字
set(CTEST_NIGHTLY_START_TIME "21:00:00 EDT") //每天晚上9点钟执行

set(CTEST_DROP_METHOD "http")  // 方法使用http
set(CTEST_DROP_SITE "open.cdash.org") // 测试地址
set(CTEST_DROP_LOCATION "/submit.php?project=CMake") // 位置
set(CTEST_DROP_SITE_CDASH TRUE) // 地址为真
```
上面的代码块中可以查找网址:<a href="https://cmake.org/cmake/help/v3.12/manual/ctest.1.html">CTest的内容</a>
```
set(CTEST_PROJECT_NAME "CMake") // 设置测试的项目名字
文档里面没有给出project name, 但是我们知道这个指定测试项目的名字了 【不过里面有个build name（也许可以替换）】

set(CTEST_NIGHTLY_START_TIME "21:00:00 EDT") //每天晚上9点钟执行
>  NightlyStartTime
在夜间仪表盘模式，指定“夜间开始时间（nightly start time）”，带有确定的控制系统版本（cvs、svn），更新步骤检查软件的版本在这个时候所以，多客户端会选择一个共同的版本测试。 对于分布式版本控制不是很好定义，所以设置被忽略掉；
CTest脚本变量: CTEST_NIGHTLY_START_TIME
如果模块变量设置，则为NIGHTLY_START_TIME ，其他的是CTEST_NIGHTLY_START_TIME ；
【符合ctest的定义和书写格式】 【一会其他特殊的才会标出来】

set(CTEST_DROP_METHOD "http")  // 方法使用http
> 	DropMethod
指定提交到dashboard服务器的方法，值可以是：cp, ftp, http, https, scp, or xmlrpc（如果cmake支持它）
同样也有脚本变量和模块变量以及其他的方式 和上面一样；
CTEST_DROP_METHOD DROP_METHOD   CTEST_DROP_METHOD

set(CTEST_DROP_SITE "open.cdash.org") // 测试地址
DropSite （网址： 域名）
dashboard server的名字（ftp, http, and https, scp, and xmlrpc 的目标服务器）
CTEST_DROP_SITE   DROP_SITE

set(CTEST_DROP_LOCATION "/submit.php?project=CMake") // 位置
DropLocation （位置）
服务器上面的路径 

set(CTEST_DROP_SITE_CDASH TRUE)
IsCDash
判断dashboard server 是否是一个CDash 或者一个老的dashboard server  实现需求TriggerSite。
scripte 变量： CTEST_DROP_SITE_CDASH
module 变量： CTEST_DROP_SITE_CDASH
[CDash 一个测试服务器，集成了CMake， CTest,CPack](https://www.cdash.org/overview/) 
这个东西怎么使用？ 以后需要使用的时候再进行使用吧？
```
>cmake 没有指定，应该是讲所有的CMakeLists.txt /*.cmake 的文件进行建立；


CTestCustom.cmake.in 和CTestConfig.cmake 是什么关系？
in文件：是对文件进行统一的管理
CTestCustom.cmake.in  这个文件应该是对文件的同一管理的内容，也就是公共部分；

```
CTestCustom.cmake.in

list(APPEND CTEST_CUSTOM_ERROR_MATCH "ERROR:") 
// 匹配对应的错误（文档中没有找到） 

列出app 结束的时候的警告异常：
list(APPEND CTEST_CUSTOM_WARNING_EXCEPTION
  "warning: cast from 'char\\*' to 'cmCursesWidget\\*' increases required alignment of target type" # Occurs when using Solaris's system libform
  "xtree.[0-9]+. : warning C4702: unreachable code"
  "warning LNK4221"
  "warning LNK4204" # Occurs by race condition with objects in small libs
  "variable .var_args[2]*. is used before its value is set"
  "jobserver unavailable"
  "warning: \\(Long double usage is reported only once for each file"
  "warning: To disable this warning use"
  "could not be inlined"
  "libcmcurl.*has no symbols"
  "not sorted slower link editing will result"
  "stl_deque.h:479"
  "Utilities.cmzlib."
  "Utilities.cmbzip2."
  "Source.CTest.Curl"
  "Source.CursesDialog.form"
  "Utilities.cmcurl"
  "Utilities.cmexpat."
  "Utilities.cmlibarchive"
  "warning: declaration of .single. shadows a global declaration"
  "/usr/include.*(warning|note).*shadowed declaration is here"
  "/usr/bin/ld.*warning.*-..*directory.name.*bin.*does not exist"
  "Redeclaration of .send..... with a different storage class specifier"
  "is not used for resolving any symbol"
  "Clock skew detected"
  "remark\\(1209"
  "remark: .*LOOP WAS VECTORIZED"
  "warning .980: wrong number of actual arguments to intrinsic function .std::basic_"
  "LINK : warning LNK4089: all references to.*ADVAPI32.dll.*discarded by /OPT:REF"
  "LINK : warning LNK4089: all references to.*CRYPT32.dll.*discarded by /OPT:REF"
  "LINK : warning LNK4089: all references to.*PSAPI.DLL.*discarded by /OPT:REF"
  "LINK : warning LNK4089: all references to.*RPCRT4.dll.*discarded by /OPT:REF"
  "LINK : warning LNK4089: all references to.*SHELL32.dll.*discarded by /OPT:REF"
  "LINK : warning LNK4089: all references to.*USER32.dll.*discarded by /OPT:REF"
  "LINK : warning LNK4089: all references to.*ole32.dll.*discarded by /OPT:REF"
  "Warning.*: .*/Utilities/KWIML/test/test_int_format.h.* # Redundant preprocessing concatenation"
  "Warning: library was too large for page size.*"
  "Warning: public.*_archive_.*in module.*archive_*clashes with prior module.*archive_.*"
  "Warning: public.*BZ2_bz.*in module.*bzlib.*clashes with prior module.*bzlib.*"
  "Warning: public.*_archive.*clashes with prior module.*"
  "Warning: LINN32: Last line.*is less.*"
  "Warning: Olimit was exceeded on function.*"
  "Warning: To override Olimit for all functions in file.*"
  "Warning: Function .* can throw only the exceptions thrown by the function .* it overrides\\."
  "WarningMessagesDialog\\.cxx"
  "warning.*directory name.*CMake-Xcode.*/bin/.*does not exist.*"
  "stl_deque.h:1051"
  "(Lexer|Parser).*warning.*conversion.*may (alter its value|change the sign)"
  "(Lexer|Parser).*warning.*(statement is unreachable|will never be executed)"
  "(Lexer|Parser).*warning.*variable.*was set but never used"
  "PGC-W-0095-Type cast required for this conversion.*ProcessUNIX.c"
  "[Qq]t([Cc]ore|[Gg]ui|[Ww]idgets).*warning.*conversion.*may alter its value"
  "warning:.*is.*very unsafe.*consider using.*"
  "warning:.*is.*misused, please use.*"
  "cmake.version.manifest.*manifest authoring warning.*Unrecognized Element"
  "cc-3968 CC: WARNING File.*" # "implicit" truncation by static_cast
  "ld: warning: directory not found for option .-(F|L)"
  "ld: warning .*/libgcc.a archive's cputype"
  "ld: warning: ignoring file .*/libgcc.a, file was built for archive which is not the architecture being linked"
  "ld: warning: in .*/libgcc.a, file is not of required architecture"
  "warning.*This version of Mac OS X is unsupported"
  "clang.*: warning: argument unused during compilation: .-g"
  "note: in expansion of macro" # diagnostic context note
  "note: expanded from macro" # diagnostic context note
  "cm(StringCommand|CTestTestHandler)\\.cxx.*warning.*rand.*may return deterministic values"
  "cm(StringCommand|CTestTestHandler)\\.cxx.*warning.*rand.*isn.*t random" # we do not do crypto
  "cm(StringCommand|CTestTestHandler)\\.cxx.*warning.*srand.*seed choices are.*poor" # we do not do crypto
  "IPA warning: function.*multiply defined in"

  # Ignore compiler summary warning, assuming prior text has matched some
  # other warning expression:
  "[0-9,]+ warnings? generated." # Clang
  "compilation completed with warnings" # PGI
  "[0-9]+ Warning\\(s\\) detected" # SunPro

# scanbuild exceptions
  "char_traits.h:.*: warning: Null pointer argument in call to string length function"
  "stl_construct.h:.*: warning: Forming reference to null pointer"
  ".*stl_uninitialized.h:75:19: warning: Forming reference to null pointer.*"
  ".*stl_vector.h:.*: warning: Returning null reference.*"
  "warning: Value stored to 'yymsg' is never read"
  "warning: Value stored to 'yytoken' is never read"
  "index_encoder.c.241.2. warning: Value stored to .out_start. is never read"
  "index.c.*warning: Access to field.*results in a dereference of a null pointer.*loaded from variable.*"
  "cmCommandArgumentLexer.cxx:[0-9]+:[0-9]+: warning: Call to 'realloc' has an allocation size of 0 bytes"
  "cmDependsJavaLexer.cxx:[0-9]+:[0-9]+: warning: Call to 'realloc' has an allocation size of 0 bytes"
  "cmExprLexer.cxx:[0-9]+:[0-9]+: warning: Call to 'realloc' has an allocation size of 0 bytes"
  "cmListFileLexer.c:[0-9]+:[0-9]+: warning: Call to 'realloc' has an allocation size of 0 bytes"
  "cmFortranLexer.cxx:[0-9]+:[0-9]+: warning: Call to 'realloc' has an allocation size of 0 bytes"
  "testProcess.*warning: Dereference of null pointer .loaded from variable .invalidAddress.."
  "liblzma/simple/x86.c:[0-9]+:[0-9]+: warning: The result of the '<<' expression is undefined"
  "liblzma/common/index_encoder.c:[0-9]+:[0-9]+: warning: Value stored to .* during its initialization is never read"
  "libuv/src/.*:[0-9]+:[0-9]+: warning: Dereference of null pointer"
  "libuv/src/.*:[0-9]+:[0-9]+: warning: The left operand of '==' is a garbage value"
  )

CTEST_CUSTOM_WARNING_EXCEPTION 这个是警告的异常

 这里是xcode结束的
if(NOT "@CMAKE_GENERATOR@" MATCHES "Xcode")
  list(APPEND CTEST_CUSTOM_COVERAGE_EXCLUDE "XCode")
endif ()

 覆盖率
list(APPEND CTEST_CUSTOM_COVERAGE_EXCLUDE
  # Exclude kwsys files from coverage results. They are reported
  # (with better coverage results) on kwsys dashboards...
  "/Source/(cm|kw)sys/"

  # Exclude try_compile sources from coverage results:
  "/CMakeFiles/CMakeTmp/"

  # Exclude Qt source files from coverage results:
  "[A-Za-z]./[Qq]t/qt-.+-opensource-src"
  )

内存检查忽略
list(APPEND CTEST_CUSTOM_MEMCHECK_IGNORE
  kwsys.testProcess-10 # See Source/kwsys/CTestCustom.cmake.in
  )

PS : 从上面可以看出，列出了很对对应的列表内容；
```

```
set(CTEST_PROJECT_NAME "CMake") // 项目名字
set(CTEST_NIGHTLY_START_TIME "1:00:00 UTC") // 执行时间

set(CTEST_DROP_METHOD "http") // 方式
set(CTEST_DROP_SITE "open.cdash.org") // 网址
set(CTEST_DROP_LOCATION "/submit.php?project=CMake") // 存放位置
set(CTEST_DROP_SITE_CDASH TRUE) // 是否使用CDash ，所以这个是CDash上面使用的
set(CTEST_CDASH_VERSION "1.6") // CDash版本
set(CTEST_CDASH_QUERY_VERSION TRUE)// CDash 请求版本

```

```
configure 文件内容:

其实就是shell脚本配置bootstrap 的脚本 ，其实这里启动了bootstrap这个命令
#!/bin/sh
cmake_source_dir=`cd "\`dirname \"$0\"\`";pwd` 获取到当前的目录下面，这个cmake_source_dir值（具体什么原理得看shell）
exec "${cmake_source_dir}/bootstrap" "$@" //执行bootstrap


shell脚本内容:
eg:新建了一个shell脚本 Test.sh 文件，内容：
#!/bin/sh
echo "shell脚本本身的名字: $0"
echo "传给shell的第一个参数: $1"
echo "传给shell的第二个参数: $2"
在Test.sh所在的目录下输入 bash Test.sh 1 2
结果为:
shell脚本本身的名字: Test.sh
传给shell的第一个参数: 1
传给shell的第二个参数:  2

变量	含义
$0	当前脚本的文件名
$n	传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是$1，第二个参数是$2
$#	传递给脚本或函数的参数个数
$*	传递给脚本或函数的所有参数
$@	传递给脚本或函数的所有参数。被双引号(" ")包含时，与 $* 稍有不同
$?	上个命令的退出状态，或函数的返回值
$$	当前Shell进程ID。对于 Shell 脚本，就是这些脚本所在的进程ID
 
$* 和 $@ 的区别
$* 和 $@ 都表示传递给函数或脚本的所有参数，不被双引号(" ")包含时，都以"$1" "$2" … "$n" 的形式输出所有参数。但是当它们被双引号(" ")包含时，"$*" 会将所有的参数作为一个整体，以"$1 $2 … $n"的形式输出所有参数；"$@" 会将各个参数分开，以"$1" "$2" … "$n" 的形式输出所有参数。
参考链接：https://www.cnblogs.com/zhaohuiazl/p/7423779.html

dirname (man dirname)
脚本中获取 脚本文件所在的绝对路径
shellPath=$(cd "$(dirname "$0")"; pwd)
echo $shellPaht

[shell 命令大全](http://www.runoob.com/linux/linux-command-manual.html)
```

```
bootstrap： 是shell脚本，这个有时间再去看一下 【很多项目构建都会写一个引导程序来处理编译打包的逻辑】

```
```
CompileFlags.cmake : 编译的配置
主要根据平台来设置一些标识，用于接下来的编译，所以做到了跨平台
里面每个字段的定义，可以再一次去看看！
```

```
CMakeLists.txt 真正构建cmake项目的文件 （详情细看）

```

```
CMakeGraphVizOptions.cmake 图像的选择

```
```
CMakeCPackOptions.cmake.in 打包选项的配置

```
```
CMakeCPack.cmake 打包的cmake
```
```
cmake_uninstall.cmake.in 卸载的cmake
```
```
.hooks-config ： 这个不知道是配置什么来的 ，不知道这个是什么 [应该是属于git的内容]
```
```
.gitignore git忽略的文件
```
```
.gitattributes 这个配置git的属性
```
```
.clang-tidy  clang tidy 是一个静态代码分析框架 https://www.jianshu.com/p/d6e12fc51294
```
```
.clang-format 格式样式
```
```
Auxiliary 辅助文件夹
Bootstrap.cmk 启动配置
Help 帮助文档
Licenses 
Modules 模块
Packaging 打包
source 存放文件源代码
Templates 模板
Tests 测试代码
Utilities 集合
```

[关于c/c++的后缀名](https://blog.csdn.net/u012662731/article/details/78531497?locationNum=5&fps=1)
[.rst文件介绍](https://blog.csdn.net/grllery/article/details/80426875)

—————————————————————————————————————————————
这个项目无法再接着继续看了，因为太多东西了； 有一天写C项目的时候，在仔细去研究研究
<font size=2 color=red>暂时先到这里</font>
