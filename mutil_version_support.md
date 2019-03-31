---
layout: post
title: Java 多版本支持 思路
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- JVM
star: true
category: blog
author: Jack
description: Java 多版本支持 思路
---



实现多版本的思路： 


1， 将指定路径下的所有jar ，进行元数据描述。 对于重复的 （可以配置的）， 构造依赖树

动态构造classpath， 将需要的版本动态放置在classpath。 不同的版本，构造的classpath不同，实现了多版本的加载（需要测试）

2， 卸载

计数， 当指定版本的依赖需要加载时候，动态更新计数。若计数为零，那么采用卸载流程。

