---
layout: post
title: JVM内存布局
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- JVM
star: true
category: blog
author: Jack
description: JVM内存介绍
---

# 1、程序计数器

当前线程所执行字节码指示器。
字节码解释是通过改变这个计数器的值来选择下一条所需要执行的字节码指令，分支、循环、跳转、异常处理、线程恢复。

每个线程有独立的程序计数器。

# 2、Java虚拟栈

线程私有，每个方法在执行同时会创建一个栈帧，用于存储局部变量、操作数栈、动态链接、方法出口灯信息。
每个方法的执行伴随着从入栈到出栈过程。

局部变量表存放基础类型： boolean char int long short double float 对象引用
其中long doube 占64位，会占用两个局部空间

线程请求栈深度超过虚拟机运行的深度，抛出StackOverflowError.
虚拟机栈如果可以动态扩展，若无法申请到足够内存，抛出OutOfMemoryError.


# 3、本地方法栈

虚拟机使用的Native的服务，
也会抛出StackOverflowError和OutOfMemoryError.


# 4、Java堆

线程共享的区域。
几乎所有的对象实例和数组所需空间在此分配，但是JIT编译器的成熟，栈上分配、标量替换优化技术。

是垃圾回收的主要区域。
新生代
+	Edgn空间
+	From Survior
+	To Survior
老年代


线程共享的Java堆中可能划分出多个线程私有的分配缓冲区（Thread Local Allocation Buffer）。与存放内容无关，仍然存储对象实例，便于垃圾回收或更快的分配内存。

逻辑上连续，物理上允许不连续。通过(-Xms -Xmx)控制。
若堆中无法继续分配，则抛出OutOfMemoryError.

# 5、方法区

线程共享区域，存放虚拟机加载的类信息、常量、静态变量、JIT编译后的代码，又称为非堆（永久代）。
使用-XX:MaxPermSize配置上限

# 6、运行时常量

方法区的一部分
Class文件除了类的版本、字段、方法、接口信息，还有常量池，用于存放编译期间生成的字面量和符号引用。

运行期间也可以添加，例如String.intern()

当无法分配时，抛出OutOfMemoryError.

# 7、直接内存

不是虚拟机云信使内存的一部分，也不在Java虚拟机规范中。
