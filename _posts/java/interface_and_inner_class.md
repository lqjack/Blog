---
layout: post
title: 接口与内部类
date: 2019-03-17 22:00
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
star: true
category: blog
author: Jack
description: Java 核心卷1 接口与内部类
---

1， 接口

不是类，是对需求的描述

回调：某个事件发生时候触发的动作

2， 克隆

默认时浅拷贝，没有包含克隆对象中的内部对象

* 默认的clone是否满足要求
* 默认的clone是否可以通过调用可变变量的clone满足需求
* 是否不应该使用clone

3， 内部类

内部类可以访问类定义的作用域中的数据，包括私有数据
内部类可以对同一个包中的其他类进行隐藏
定义回调函数，使用匿名类更便捷
内部类有一个外部类的引用：OutClass.this.fieldName
编译器将内部类编译为用$分割外部类和内部类的普通类

4， 代理

