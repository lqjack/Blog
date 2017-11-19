---
layout: draft
title: Java范型
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
star: true
category: blog
author: Jack
description: Java范型 
---

```Java
List<? extends Number>, 上界为class java.lang.Number, 属于Class类型
List<? extends List<T>>, 上界为java.util.List<T>, 属于ParameterizedType类型
List<? extends List<String>>, 上界为java.util.List<java.lang.String>, 属于ParameterizedType类型
List<? extends T>, 上界为T, 属于TypeVariable类型
List<? extends T[]>, 上界为T[], 属于GenericArrayType类型
```
