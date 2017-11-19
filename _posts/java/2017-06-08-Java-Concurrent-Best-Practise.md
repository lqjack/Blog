---
layout: post
title: 线程总结
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
- Thread
star: true
category: blog
author: Jack
description: 线程
---

# 线程同步：
* 不变形
* 枷锁
* 线程封闭
* 栈封闭


## Deque BlockDeque

### 线程窃取
# 线程状态：
1. 新建 		
2. 就绪  
3. 阻塞
4. 运行
5. 死亡



# `ConcurrentHashMap<String,Future<?>>`


# 可变状态是至关重要的
*	可变状态越少，越容易保证线程安全
*	尽量将域声明为final
*	不可变对象一定是线程安全的
*	封装有助于管理复杂性
*	锁控制可变变量
*	保证同一个不变性条件的所有变量时，需要使用锁
*	进行复合操作需要锁
*	禁止随意推断不需要加锁
*	同步策略文档化


# 同步工具类

1. 栅栏Barrier CycleBarrier Exchange
<p>闭锁用于等待事件，而栅栏用于等待线程。</p>
2. 信号量Semaphore  
<p>控制同时访问特定资源的数量。二值信号量互斥。</p>
3. 闭锁CountDownLatch  FutureTask
<p>延迟到线程的进度到达终止状态，</p>


# ExecutorService
CompletionService  Executor BlockQueue

# 线程池

* newFixedThreadPool
* 	newCachedThreadPool
* 	newSchedueledThreadPool
* 	newSingleThreadPool


*shutdown 平缓关闭，等待正在执行的完成，取消将要执行的线程*
*shutdownNow 取消所有正在运行的任务，不启动在队列中的任务*



* DelayQueue
	管理一组Delayed对象，每个对象都有一个延迟时间，只有某个元素逾期后才执行take操作，按照延迟时间排序。


* ReentrantLock
	定时
	重入
	可中断
	
* ReadWriteLock

* ReentrantReadWriteLock
	
* Condition内置条件队列
	
* AQS

```Java
boolean acquire() throws InterruptedException {
	while(当前状态不允许操作) {
		if(需要阻塞获取请求) {
			如果当前线程不在队列中，则将其插入队列
			阻塞当前线程
		}
		eles
			返回失败
	}
	可能更新同步器状态
	如果线程位于队列中，将其移除队列
	返回成功
}
```

```Java
void release() {
	更新同步器状态
	if(新的状态允许某个被阻塞的线程获取成功) {
		解除队列中一个或者多个阻塞状态
	}
}
```

# 原子类
* AtomicInteger
* 	AtomicReference<V>
* 	AtomicReferenceFieldUpdate<Node,Node>
* 	AtomicStampReference<V>



# 内存模型

1. 重排列

2. Happens-Before规则：
	程序顺序规则
	监视器规则
	voliate变量规则
	线程启动规则
	中断规则
	终结器规则
	传递性	

3. 当缺少Happens-Before规则时候，就可能出现重排列		

# Improve 

>  queue arrayList -> LinkedList<> 	

