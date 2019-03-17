---
layout: post
title: 继承
date: 2019-03-17 12:00
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
star: true
category: blog
author: Jack
description: Java 核心卷1 继承
---

1，类型转换
唯一目的：暂时忽略对象实际类型，使用对象的全部功能。

2，Object

2.1， equals
检测两个对象是否相等

if(this == otherObject) return true;
if(otherObject == null) return false;
if(getClass() != otherObject.getClass()) return false;
ClassName other = (ClassName)otherObject;
return filed1 == otherObject.filed && Object.equals(field2,otherObject.field2)

如果子类定义，需要调用super.equals(other)
如果是数组，使用Arrays.equals

2.2 hashCode

由对象导出一个整数值。如果重新定义equals方法，那么hashCode必须重新定义
同一个类中不同的属性使用 7 * a + 11 * b + 13 * c 
多个组合多个散列使用Objects.hashCode
如果存在数组类型使用，Arrays.hashCode

2.3 toString
返回对象值的字符串
getClass().getName() + "[name=" + name + ", salary=" + salary + "]";

3，自动装箱

自动装箱（编译器处理）规范要求boolean,byte,char <= 127,-128 < short(int) < int 被包装到固定的对象（即相等）

4，枚举

是一个类，刚好具有跟枚举种类相等的实例，使用==判断相等，所有枚举类都是Enum的子类

EnumType enumType = Enum.valueOf(EnumType.class,"EnumType")

ordinal 位置从0开始

5, 反射
能够分析类的能力
提供了丰富精心设计的工具包，能够动态操纵Java 代码的程序。

运行时，Java为每个对象维护运行时类型标示，跟踪对象所属于的类。

受限于Java访问控制，如果没有受到安全管理器的控制，就可以覆盖访问控制（setAccessible(true)）。


Object newArray = Array.newInstance(componetType,length)

6，异常捕获

程序运行时发生错误，抛出异常。由异常处理程序处理。如果没有，程序会终止，并打印错误信息。

未检查异常：应该避免发生的错误
已检查异常：

7, 继承设计技巧

* 将公共操作和域放在超类中
* 不要使用受保护的域
* 使用继承实现is-a
* 除非所有继承都有意义，否则不要使用继承
* 在覆盖方法时，不要改变预期的行为
* 使用多态，非类型信息（if (x is type of 1))
* 不要过多的使用反射


