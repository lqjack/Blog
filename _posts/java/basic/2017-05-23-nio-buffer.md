---
layout: post
title: NIO Buffer
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
- NIO
star: true
category: blog
author: Jack
description: NIO Buffer
---

## 内部元素
* 内容： 包含基本类型，线性、有限特定基本类型序列。
* 容量（capacity) : Buffer对象最大能写入的大小、不变量。
* 最大读取位置(limit) : Buffer对象当前写入的最大位置，读取时候最大的读取位置。
* 当前位置(position) : 当前索引，下一个要写入和读取的位置。

1. A buffer's capacity is the number of elements it contains. The capacity of a buffer is never negative and never changes.
2. A buffer's limit is the index of the first element that should not be read or written. A buffer's limit is never negative and is never greater than its capacity.
3. A buffer's position is the index of the next element to be read or written. A buffer's position is never negative and is never greater than its limit.


#### 几个概念的关系：
**0 <= mark <= position <= limit <= capacity**

## 易混淆方法
* clear: 设置limit为capacity,position为零。
* flipping: 设置limit为当前位置,position为零。
* rewinding: limit未设置,position为零。

1. clear makes a buffer ready for a new sequence of channel-read or relative put operations: It sets the limit to the capacity and the position to zero.
2. flip makes a buffer ready for a new sequence of channel-write or relative get operations: It sets the limit to the current position and then sets the position to zero.
3. rewind makes a buffer ready for re-reading the data that it already contains: It leaves the limit unchanged and sets the position to zero.

## 实现
Buffer 抽象类，由Builder模式设计与实现。

