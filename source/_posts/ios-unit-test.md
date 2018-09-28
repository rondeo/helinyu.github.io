---
title: ios unit test
date: 2018-09-28 19:16:43
tags: oc
categories: iOS
---

1、 iOS单元测试是为了什么？


2、iOS上的基本测试
	1）测试接口的逻辑，这个过程应该尽可能的考虑方位和一些特殊的情况，对于用例里面的每个接口；
	eg： 在ViewController里面写了一个方法的代码
	```
		- (NSInteger)custom1 {
		    return arc4random() % 100;
		}

	```
	下面是基本的测试代码：
		在UnitTests.m 文件里面写对应的代码，
	```
		- (void)testPerformanceExample {
		    // This is an example of a performance test case.
		    
		    NSInteger result = [self->_vc custom1];
		    NSLog(@"reuslt ;%zd",result);
		    NSAssert(result >10, @"获取的数据只能够大于10才可以");
		    
		    [self measureBlock:^{
		        // Put the code you want to measure the time of here.
		      
		        NSInteger result = [self->_vc custom1];
		        NSLog(@"reuslt ;%zd",result);
		        // 执行的性能
		    }];
		}

	```
	执行cmd+u 执行测试的代码，
	cmd +5 查看对应的信息。

3、性能问题:（对代码执行的时间性能进行控制）
![性能测试](../../../asset/Snip20180928_95.png)
