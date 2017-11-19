---
layout: post
title: System workflow
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- DDD
star: true
category: blog
author: Jack
description: system workflow
---

# Abstract General System workflow
## 1, standard workflow
<pre>
VO -> updated VO -> Entity -> DTO -> updated DTO
</pre>

<p>
按照流程1的思路，确定了整个执行流程。如果将每个流程抽象为一个函数，用户在调用时如下：

```Java
OPServer.standard(
    // Supply refer to return the Object (E.g. VO)
    () -> vo,      //1
    //Function to conver the VO to the Entity, User can custom the logic in the function
    (v) -> ve,     //2
    //Function to call the Entity , once finish the calling , will return new New Entity
    (e) -> ue,     //3
    //Function to convert the updated Entity to DTO
    (um) -> dto,   //4
    //Function to conver the DTO to other DTO
    (ud) -> udto   //5
)
```
</p>

## 2, simple worflow
<pre>
VO -> Entity -> DTO
</pre>

<p>
在一些场景中可以将流程简化，用户在调用时如下：

```Java
OPServer.standard(
    // Supply refer to return the Object (E.g. VO)
    () -> vo,      //1
    //Function to conver the VO to the Entity, User can custom the logic in the function
    (e) -> ue,     //2
    //Function to convert the updated Entity to DTO
    (um) -> dto    //3
)
```
</p>

## 3, full workflow
<pre>
VO -> updated VO -> Entity -> DTO -> updated DTO
</pre>

<p>
为了支持灵活的扩展性，对于流程1进行2处扩展。如果将每个流程抽象为一个函数，用户在调用时如下：

```Java
OPServer.standard(
    // Supply refer to return the Object (E.g. VO)
    () -> vo,         //1
    //Function to conver the VO to the Entity, User can custom the logic in the function
    (v) -> ve,        //2
    //BiFunction to convert the origin VO and updated VO to Entity
    (ov,nv) -> m,     //3
    //Function to call the Entity , once finish the calling , will return new New Entity
    (e) -> ue,        //4
    //Function to convert the updated Entity to DTO
    (um) -> dto,      //5
    //BiFunction to conver the updated entity and DTO to other DTO
    (oe,ud) -> udto     //6
)
```
</p>

## 4 observer workflow
<pre>
[Observer]
fields : [
],
methods : [
    notify() :void
]

[Subject]
fields : [
]
methods : [
    registerObserver(observer) : void
    unRegisterObserver(observer) : void
    notifyObserver() : void
]
</pre>

<p>
解耦合Observer和Subject
</p>


## 5 event workflow
<pre>
Command -> Event (->) Service Call
</pre>

<p>
为了支持灵活的扩展性，对于流程1进行2处扩展。如果将每个流程抽象为一个函数，用户在调用时如下：

</p>
