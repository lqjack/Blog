---
layout: post
title: MYSQL主从同步原理
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- MySQL
star: true
category: blog
author: Jack
description: MYSQL主从同步原理
---

## 整体上来说，复制有3个步骤：   
* master将改变记录到二进制日志(binary log)中（这些记录叫做二进制日志事件，binary log events）；
* slave将master的binary log events拷贝到它的中继日志(relay log)；

* slave重做中继日志中的事件，将改变反映它自己的数据。
下图描述了复制的过程 
![MySQL Master-Slave sync](/images/java/master_slave.jpg "MySQL Master-Slave sync")

1. master记录二进制日志。在每个事务更新数据完成之前，master在二日志记录这些改变。MySQL将事务串行的写入二进制日志，即使事务中的语句都是交叉执行的。在事件写入二进制日志完成后，master通知存储引擎提交事务。
2. slave将master的binary log拷贝到它自己的中继日志。首先，slave开始一个工作线程——I/O线程。I/O线程在master上打开一个普通的连接，然后开始binlog dump process。Binlog dump process从master的二进制日志中读取事件，如果已经跟上master，它会睡眠并等待master产生新的事件。I/O线程将这些事件写入中继日志。
SQL slave thread（SQL从线程）处理该过程的最后一步。SQL线程从中继日志读取事件，并重放其中的事件而更新slave的数据，使其与master中的数据一致。只要该线程与I/O线程保持一致，中继日志通常会位于OS的缓存中，所以中继日志的开销很小。
3. 在master中也有一个工作线程：和其它MySQL的连接一样，slave在master中打开一个连接也会使得master开始一个线程。复制过程有一个很重要的限制——复制在slave上是串行化的，也就是说master上的并行更新操作不能在slave上并行操作。
