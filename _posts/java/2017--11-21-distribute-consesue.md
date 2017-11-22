---
layout: post
title: 分布式系统一致性
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Algorithm
- Binary Tree
star: true
category: blog
author: Jack
description: 分布式系统一致性
---

## 一致性

* C 一致性
* A 可用性
* P 分区容错性

<p>
CA RDBMS
CP MongoDB HBase Redis
AP DynamoDB Cassandra CouchDB
</p>


弱一致性

DNS
Gossip

强一致性

同步 主从同步 （Master是瓶颈）
多数派 每次写入都保证大于 N/2 ,每次读保证大于 N/2 节点中读。（并发情况下的问题待解救）
Paxos 共识算法，系统的最终一致性，不仅仅需要达成共识，还需要client的行为【timeout 情况不确定】。
basic paxos

client 系统的外部角色，请求发起者。
propser 接受client的请求，向集群提出倡议(propose)。并在冲突发生时，起到冲突调节的作用。
accpector(voter) 提议投票的接受者，只有在形成法定人数（quorum,大多数），提议才会最终被接受。
learner 提议接受者，对集群没有影响

步骤：
1，Prepare 
propser 提出一个提案，编号为N，此N大于这个propser之前提出的提案编号，请求acceptors的quorum的接受。
2，Promise
如果N大于此acceptor之前接受的任何编号则接受，否则拒绝。
3，Accept
如果达到了多数派，propser会发出accpet的请求，此请求包含编号N以及档案内容。
4，Accepted
如果acceptor在此期间没有收到任何编号大于N的档案，则接受档案的内容，否则拒绝。

存在的问题：
难实现，效率低（2轮RPC），活锁。

multi paxos
Leader 唯一的prosper，所有请求都需要经过leader。

fast paxos
Raft (multi-paxos)

划分三个子问题
leader election
log replication
safety
角色
leader
follower
candidate

ZAB (multi-paxos)
将一个learder的周期称为epoch,raft称为term。
raft保证日志连续性，心跳方向为leader到follower

