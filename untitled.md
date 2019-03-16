---
layout: post
title: Java Core
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
star: true
category: blog
author: Jack
description: Java Core
---

Java局部变量使用需要赋予初始值：方法在运行时会自动创建局部变量表、操作数栈等；其中局部变量表所需的内存空间在编译期间完成分配，不同的方法的生命周期不同，局部变量会重用局部变量表中的部分位置，这个方法需要在栈帧分配多大的局部变量空间是完全确定的，在方法运行期间不会改变局部变量表的大小。这句话就说明了局部变量在创建时就必须进行初始化以确定分配内存大小。

Java堆存放所有对象的实例，几乎所有的对象实例都在这里分配内存。在hotspot虚拟机中，内存分配后，虚拟机需要将分配到的内存空间都初始化为零值。这一步操作保证了对象的实例字段在java代码中可以不赋初始值就直接使用，程序能访问到的这些字段的数据类型所对应的零值。