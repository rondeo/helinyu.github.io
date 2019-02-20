---
title: C语言标准库等
date: 2019-02-17 19:57:42
tags: C
categories: C
---

1、C语言的基本内容暂时就先不看了， 可以参考这里的基本内容：
[C语言的内容参考链接](http://www.runoob.com/cprogramming/c-standard-library.html)
[C语言学习资源](https://github.com/jobbole/awesome-c-cn)

2、系统函数
 &&&&
系统库里面的内容；
usr/include 开发环境下提供对应的系统库[开发对应系统上面的应用都是有这个系统库的]
&&& 有时间也要熟悉一下系统常用的函数内容
>了解:ANSI C
ANSI C是由美国国家标准协会（ANSI）及国际标准化组织（ISO）推出的关于C语言的标准。ANSI C 主要标准化了现存的实践， 同时增加了一些来自 C++ 的内容 （主要是函数原型） 并支持多国字符集 （包括备受争议的三字符序列）。 ANSI C 标准同时规定了 C 运行期库例程的标准。

&&&

3、下面会对C语言中系统的一些标准库的了解：
1）<assert.h>
C 标准库的 assert.h头文件提供了一个名为 assert 的宏，它可用于验证程序做出的假设，并在假设为假时输出诊断消息。
```
void assert(int expression);
expression： 一个变量或任何C表达式；true， assert不执行任何动作。否则，assert（）会在标准错误stderr上显示错误消息，并且终止程序。
[可以查看一下里面的几个内部的使用方法，上面的这个方法最常用]
```

2)<ctype.h> /<_ctype.h>文件
1>提供一些函数用于测试和映射字符。
2>函数接受 int 作为参数，它的值必须是 EOF 或表示为一个无符号字符。
3> 如果参数 c 满足描述的条件，则这些函数返回非零（true）。如果参数 c 不满足描述的条件，则这些函数返回零。
```
1	int isalnum(int c)
该函数检查所传的字符是否是字母和数字。
2	int isalpha(int c)
该函数检查所传的字符是否是字母。
3	int iscntrl(int c)
该函数检查所传的字符是否是控制字符。
4	int isdigit(int c)
该函数检查所传的字符是否是十进制数字。
5	int isgraph(int c)
该函数检查所传的字符是否有图形表示法。
6	int islower(int c)
该函数检查所传的字符是否是小写字母。
7	int isprint(int c)
该函数检查所传的字符是否是可打印的。
8	int ispunct(int c)
该函数检查所传的字符是否是标点符号字符。
9	int isspace(int c)
该函数检查所传的字符是否是空白字符。
10	int isupper(int c)
该函数检查所传的字符是否是大写字母。
11	int isxdigit(int c)
该函数检查所传的字符是否是十六进制数字。
标准库还包含了两个转换函数，它们接受并返回一个 "int"
13 int tolower(int c)
该函数把大写字母转换为小写字母。
14 int toupper(int c)
该函数把小写字母转换为大写字母。
```

3)<errno.h> 文件
1>定义了整数变量 errno，它是通过系统调用设置的，在错误事件中的某些库函数表明了什么发生了错误。该宏扩展为类型为 int 的可更改的左值，因此它可以被一个程序读取和修改。
2>在程序启动时，errno 设置为零，C 标准库中的特定函数修改它的值为一些非零值以表示某些类型的错误。您也可以在适当的时候修改它的值或重置为零。
3>errno.h 头文件定义了一系列表示不同错误代码的宏，这些宏应扩展为类型为 int 的整数常量表达式。
```
1	extern int errno
这是通过系统调用设置的宏，在错误事件中的某些库函数表明了什么发生了错误。
2	EDOM Domain Error
这个宏表示一个域错误，它在输入参数超出数学函数定义的域时发生，errno 被设置为 EDOM。
3	ERANGE Range Error
这个宏表示一个范围错误，它在输入参数超出数学函数定义的范围时发生，errno 被设置为 ERANGE。
4、在对应的头文件中看到了对应的1~106的错误码。
```

4）<float.h> 头文件
1>包含了一组与浮点值相关的依赖于平台的常量。
```
浮点数是由下面四个元素组成的：
组件	组件描述
S	符号 ( +/- )
b	指数表示的基数，2 表示二进制，10 表示十进制，16 表示十六进制，等等...
e	指数，一个介于最小值 emin 和最大值 emax 之间的整数。
p	精度，基数 b 的有效位数
eg: 表示一个浮点数的值如下：
floating-point = ( S ) p x be
或
floating-point = (+/-) precision x baseexponent
```
2> 库宏：【注意，所有的实例 FLT 是指类型 float，DBL 是指类型 double，LDBL 是指类型 long double。】
```
FLT_ROUNDS	定义浮点加法的舍入模式，它可以是下列任何一个值：
-1 - 无法确定
0 - 趋向于零
1 - 去最近的值
2 - 趋向于正无穷
3 - 趋向于负无穷
FLT_RADIX 2	这个宏定义了指数表示的基数。基数 2 表示二进制，基数 10 表示十进制，基数 16 表示十六进制。

FLT_MANT_DIG
DBL_MANT_DIG
LDBL_MANT_DIG
这些宏定义了 FLT_RADIX 基数中的位数。

FLT_DIG 6
DBL_DIG 10
LDBL_DIG 10
这些宏定义了舍入后不会改变表示的十进制数字的最大值（基数 10）。

FLT_MIN_EXP
DBL_MIN_EXP
LDBL_MIN_EXP
这些宏定义了基数为 FLT_RADIX 时的指数的最小负整数值。

FLT_MIN_10_EXP -37
DBL_MIN_10_EXP -37
LDBL_MIN_10_EXP -37
这些宏定义了基数为 10 时的指数的最小负整数值。

FLT_MAX_EXP
DBL_MAX_EXP
LDBL_MAX_EXP
这些宏定义了基数为 FLT_RADIX 时的指数的最大整数值。

FLT_MAX_10_EXP +37
DBL_MAX_10_EXP +37
LDBL_MAX_10_EXP +37
这些宏定义了基数为 10 时的指数的最大整数值。

FLT_MAX 1E+37
DBL_MAX 1E+37
LDBL_MAX 1E+37
这些宏定义最大的有限浮点值。

FLT_EPSILON 1E-5
DBL_EPSILON 1E-9
LDBL_EPSILON 1E-9
这些宏定义了可表示的最小有效数字。

FLT_MIN 1E-37
DBL_MIN 1E-37
LDBL_MIN 1E-37
这些宏定义了最小的浮点值。
```

5) <limits.h>
limits.h 头文件决定了各种变量类型的各种属性。定义在该头文件中的宏限制了各种变量类型（比如 char、int 和 long）的值。
这些限制指定了变量不能存储任何超出这些限制的值，例如一个无符号可以存储的最大值是 255。
```
宏	  		值	描述
CHAR_BIT	8		定义一个字节的比特数。
SCHAR_MIN	-128	定义一个有符号字符的最小值。
SCHAR_MAX	127		定义一个有符号字符的最大值。
UCHAR_MAX	255		定义一个无符号字符的最大值。
CHAR_MIN	0		定义类型 char 的最小值，如果 char 表示负值，则它的值等于 SCHAR_MIN，否则等于 0。
CHAR_MAX	127		定义类型 char 的最大值，如果 char 表示负值，则它的值等于 SCHAR_MAX，否则等于 UCHAR_MAX。
MB_LEN_MAX	1		定义多字节字符中的最大字节数。
SHRT_MIN	-32768	定义一个短整型的最小值。
SHRT_MAX	+32767	定义一个短整型的最大值。
USHRT_MAX	65535	定义一个无符号短整型的最大值。
INT_MIN		-32768	定义一个整型的最小值。
INT_MAX		+32767	定义一个整型的最大值。
UINT_MAX	65535	定义一个无符号整型的最大值。
LONG_MIN	-2147483648	定义一个长整型的最小值。
LONG_MAX	+2147483647	定义一个长整型的最大值。
ULONG_MAX	4294967295	定义一个无符号长整型的最大值。
```

6) <locale.h>
locale.h 头文件定义了特定地域的设置，比如日期格式和货币符号。接下来我们将介绍一些宏，以及一个重要的结构 struct lconv 和两个重要的函数。
```
库函数
序号	函数 & 描述
1	char *setlocale(int category, const char *locale)
设置或读取地域化信息。
2	struct lconv *localeconv(void)
设置或读取地域化信息。

会使用到下面的宏：
序号	宏 & 描述
1	LC_ALL
设置下面的所有选项。
2	LC_COLLATE
影响 strcoll 和 strxfrm 函数。
3	LC_CTYPE
影响所有字符函数。
4	LC_MONETARY
影响 localeconv 函数提供的货币信息。
5	LC_NUMERIC
影响 localeconv 函数提供的小数点格式化和信息。
6	LC_TIME
影响 strftime 函数。
```

```
库结构
typedef struct {
   char *decimal_point; 用于非货币值的小数点字符.
   char *thousands_sep;  用于非货币值的千位分隔符。
   char *grouping;     一个表示非货币量中每组数字大小的字符串。每个字符代表一个整数值，每个整数指定当前组的位数。值为 0 意味着前一个值将应用于剩余的分组。
   char *int_curr_symbol; 国际货币符号使用的字符串。前三个字符是由 ISO 4217:1987 指定的，第四个字符用于分隔货币符号和货币量。
   char *currency_symbol;  用于货币的本地符号。
   char *mon_decimal_point;  用于货币值的小数点字符。
   char *mon_thousands_sep;  用于货币值的千位分隔符。
   char *mon_grouping;   一个表示货币值中每组数字大小的字符串。每个字符代表一个整数值，每个整数指定当前组的位数。值为 0 意味着前一个值将应用于剩余的分组。
   char *positive_sign;  用于正货币值的字符。
   char *negative_sign;  用于负货币值的字符。
   char int_frac_digits;  国际货币值中小数点后要显示的位数。
   char frac_digits;		货币值中小数点后要显示的位数。
   char p_cs_precedes;		如果等于 1，则 currency_symbol 出现在正货币值之前。如果等于 0，则 currency_symbol 出现在正货币值之后。
   char p_sep_by_space;		如果等于 1，则 currency_symbol 和正货币值之间使用空格分隔。如果等于 0，则 currency_symbol 和正货币值之间不使用空格分隔。
   char n_cs_precedes;		如果等于 1，则 currency_symbol 出现在负货币值之前。如果等于 0，则 currency_symbol 出现在负货币值之后。
   char n_sep_by_space;		如果等于 1，则 currency_symbol 和负货币值之间使用空格分隔。如果等于 0，则 currency_symbol 和负货币值之间不使用空格分隔。
   char p_sign_posn;	表示正货币值中正号的位置。
   char n_sign_posn;  表示负货币值中负号的位置。
} lconv

下面的值用于 p_sign_posn 和 n_sign_posn:
值	描述
0	封装值和 currency_symbol 的括号。
1	放置在值和 currency_symbol 之前的符号。
2	放置在值和 currency_symbol 之后的符号。
3	紧挨着放置在值和 currency_symbol 之前的符号。
4	紧挨着放置在值和 currency_symbol 之后的符号。

```
7) <math.h> 
math.h 头文件定义了各种数学函数和一个宏。在这个库中所有可用的功能都带有一个 double 类型的参数，且都返回 double 类型的结果。
>HUGE_VAL
当函数的结果不可以表示为浮点数时。如果是因为结果的幅度太大以致于无法表示，则函数会设置 errno 为 ERANGE 来表示范围错误，并返回一个由宏 HUGE_VAL 或者它的否定（- HUGE_VAL）命名的一个特定的很大的值。
如果结果的幅度太小，则会返回零值。在这种情况下，error 可能会被设置为 ERANGE，也有可能不会被设置为 ERANGE。
函数内容查看头文件。

8） <setjmp.h>
定义了宏 setjmp()、函数 longjmp() 和变量类型 jmp_buf，该变量类型会绕过正常的函数调用和返回规则。

jmp_buf 
这是一个用于存储宏 setjmp() 和函数 longjmp() 相关信息的数组类型。

> int setjmp(jmp_buf environment)
这个宏把当前环境保存在变量 environment 中，以便函数 longjmp() 后续使用。如果这个宏直接从宏调用中返回，则它会返回零，但是如果它从 longjmp() 函数调用中返回，则它会返回一个非零值。

> void longjmp(jmp_buf environment, int value)
该函数恢复最近一次调用 setjmp() 宏时保存的环境，jmp_buf 参数的设置是由之前调用 setjmp() 生成的。  || setjmp 中的唯一的一个函数

9）<signal.h>
signal.h 头文件定义了一个变量类型 sig_atomic_t、两个函数调用和一些宏来处理程序执行期间报告的不同信号。
|| 也就是处理系统信息的内容

10）  <stdarg.h>
stdarg.h 头文件定义了一个变量类型 va_list 和三个宏，这三个宏可用于在参数个数未知（即参数个数可变）时获取函数中的参数。
可变参数的函数通在参数列表的末尾是使用省略号(,...)定义的。

11）<stddef.h>
义了各种变量类型和宏。这些定义中的大部分也出现在其它头文件中。

12）stdio .h 
头文件定义了三个变量类型、一些宏和各种函数来执行输入和输出。

13） stdlib .h 
头文件定义了四个变量类型、一些宏和各种通用工具函数。

14）string .h
 头文件定义了一个变量类型、一个宏和各种操作字符数组的函数。

15）time.h 
头文件定义了四个变量类型、两个宏和各种操作日期和时间的函数。




