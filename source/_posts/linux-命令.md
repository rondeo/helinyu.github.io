---
title: linux 命令
date: 2019-03-21 12:47:42
tags: linux
categories: linux
---


1、wc 用于计算数字
>wc指令我们可以计算文件的Byte数、字数、或是列数，若不指定文件名称、或是所给予的文件名为"-"，则wc指令会从标准输入设备读取数据。

> wc [-clw][--help][--version][文件...]
```
-c或--bytes或--chars 只显示Bytes数。
-l或--lines 只显示行数。
-w或--words 只显示字数。
--help 在线帮助。
--version 显示版本信息。
```
```
wc testfile           # testfile文件的统计信息  
3 92 598 testfile       # testfile文件的行数为3、单词数92、字节数598 
```
