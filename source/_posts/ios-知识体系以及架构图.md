---
title: ios 知识体系以及架构图
date: 2019-02-20 16:51:29
tags: iOS
categories: iOS
---

<h2>ios 底层体系</h2>
<font size=4 color=red>第一部分： oc语法
</font>
1）oc对象本质
2）kvc/kvo
3）instance ,class , meta-class, isa, superclass
4)category, load , initialize ,关联对象

<font size=4 color=red>第二部分: block</font>
1）底层数据结构
2）变量捕获
3）内存管理
4）__block
5)循环引用

<font size=4 color=red>第三部分: runtime</font>
1）非指针isa
2）方法缓存
3）objc_msgSend
4) 消息发送、动态方法解析、消息转发
5）super的本质
6）常用API

<font size=4 color=red>第四部分:runloop</font>
1、CFRunLoopModeRef
2、CFRunLoopSourceRef
3、CFRunLoopObserverRef
4、线程保活
5、常见应用

<font size=4 color=red>第五部分: 多线程</font>
1)gcd (GNUstep)
2)pthread_rwlock/ barrier_async
3)0SSpinLock ,os_unfair_lock, pthread_mutex
4)NSLock , NSRecursiveLock ,NSCondition, NSConditionLock
5)dispatch_semaphore @synchronize ,atomic

<font size=4 color=red>第六部分:内存管理</font>
1）定时器内存泄露
2）自动释放池
3）引用计数
4）tagged pointer 
5) ARC 原理
6）__weak 原理

<font size=4 color=red>第七部分:性能优化</font>
1、卡顿检测
2、异常捕获
3、安装包瘦身
4、启动优化、内存优化、电量优化、网络优化

<font size=4 color=red>第二部分:架构设计</font>
1）设计模式
2）APP架构

<h2>有关学习思维导图</h2>
![iOS 进阶导图](../../../../asset/WechatIMG6.png "ios 进阶导图")

iOS 推荐书籍：
1.《Effective Objective-C 2.0》
2.《Objective-C 高级编程》
3.《程序员的自我修养》
4.《图解HTTP》
5.《高性能iOS应用开发》
6.《剑指Offer》|《算法图解》

平时很有必要的书籍：
1、《程序员的自我修养————链接、装载、库》 [待]



