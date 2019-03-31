---
title: iOS 杂烩
date: 2018-07-03 17:43:48
tags: ios 杂烩
categories: oc
---

[iOS 跳转到app store](https://www.jianshu.com/p/d81a0ca7b149)
 
1、
有关container View的使用，就是子视图和父视图之间的关系，注意addchildContainer 的使用
[container view 上面的实现](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/ImplementingaContainerViewController.html)


2、
A shell task (/usr/bin/env git clone --bare --quiet https://chromium.googlesource.com/webm/libwebp /Users/felix/Library/Caches/org.carthage.CarthageKit/dependencies/libwebp) failed with exit code 128:
fatal: unable to access 'https://chromium.googlesource.com/webm/libwebp/': Failed to connect to chromium.googlesource.com port 443: Operation timed outA shell task (/usr/bin/env git clone --bare --quiet https://chromium.googlesource.com/webm/libwebp /Users/felix/Library/Caches/org.carthage.CarthageKit/dependencies/libwebp) failed with exit code 128:
fatal: unable to access 'https://chromium.googlesource.com/webm/libwebp/': Failed to connect to chromium.googlesource.com port 443: Operation timed out
这个libwebp 这个库下载不下来，这个怎么处理? pod 里面讲对应的库下载下来放到缓存里面就行了； 
carthage :  
1） 放到缓存里面好像不行；
2）。。。