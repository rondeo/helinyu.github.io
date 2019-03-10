---
title: RxSwfit
date: 2019-03-09 15:31:41
tags: RxSwift
categories: chain programming
---
有关RxSwift的学习

遵循学习步骤：

```
* 阅读给出来的一个文档 ————> 了解这个项目的概览， 记录涉及到知识内容, 有些内容是有安装和开始文档的。
* 运行开源项目的例子 ————> 可以去看例子里面的书写内容 【给我们提示了怎么写代码来使用】
* 测试例子，有很多新的概念以及内容不太了解————> 需要去学习基础知识 ，看start guide 文档
* 测试代码   ——————————> 查看指定的功能代码
* 涉及的文档和内容进行阅读
* 其他项目中使用的情况以及代码写法
* 按照业务查看对应的内容【对某条业务运行来查看代码】*** 不断看不懂的业务，达到查看所有的代码以及技术； 
* 总体查看里面的架构， 以及源代码涉及到延伸的技术； 
* 提出是否有问题，需求是否满足，有什么地方可以进行修改的；
```

> 先搞oc上面的内容
1、阅读了文档： 知道了使用以及有管的资料 
rxSwfit/RxCocoa 链式编程，里面记录了有关的文档； 源于rx，有时间在研究Rx

2、例子，一个简单的数字的加法的例子；
```
KVO observing, async operations and streams are all unified under abstraction of sequence.  kvo观察者模式，异步操作和流在段上是统一抽象的；
```

3、pod install 安装出现了错误， 
```
Analyzing dependencies
Downloading dependencies
Installing RxAtomic (4.4.1)
Installing RxCocoa (4.4.1)
Installing RxSwift (4.4.1)
[!] Unable to determine Swift version for the following pods:

- `RxCocoa` does not specify a Swift version and none of the targets (`TestRXCocoa`) integrating it have the `SWIFT_VERSION` attribute set. Please contact the author or set the `SWIFT_VERSION` attribute in at least one of the targets that integrate this pod.
- `RxSwift` does not specify a Swift version and none of the targets (`TestRXCocoa`) integrating it have the `SWIFT_VERSION` attribute set. Please contact the author or set the `SWIFT_VERSION` attribute in at least one of the targets that integrate this pod.
显示要设置swift的版本 ， 针对swift的不同版本，应该是不一样的； ruby语法
```
```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '4.2'
     end
   end
end
```





