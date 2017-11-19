---
title: 优化
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- MySQL
star: true
category: blog
author: Jack
description: 优化
---

* 访问请求限量 超过一定数量，直接返回


* 根据用户请求查询条件，动态组装查询语句
避免  SQL注入问题

* SQL语句优化  索引的使用


* AND 组装为一个子查询 
* OR 划分为 union 连接


```Sql
select  t1.* from
(
select *  from agent where name like '"2%' 
union 
select *  from agent where email like '"2%' 
union 
select *  from agent where ContactPerson like '"2%'
) t1	
```
这种查询结果是所有的集合，也可以把union换成or


* 查询异步 

* 界面渲染异步处理

* 是否采用MQ，讲查询进入队列处理；






