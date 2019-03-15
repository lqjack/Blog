---
layout: post
title: Kafka 
date: 2018-07-18 00:06
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
- MQ
star: true
category: blog
author: Jack
description: Kafka
---


## Fundation

## Architecture

## FQ

1. 保证数据的不丢失
a. 生产者
kafka的ack机制：在kafka发送数据的时候，每次发送消息都会有一个确认反馈机制，确保消息正常的能够被收到。
同步模式：ack机制能够保证数据的不丢失，如果ack设置为0，风险很大，一般不建议设置为0
producer.type=sync 
request.required.acks=1

0：这意味着生产者producer不等待来自broker同步完成的确认继续发送下一条（批）消息。此选项提供最低的延迟但最弱的耐久性保证（当服务器发生故障时某些数据会丢失，如leader已死，但producer并不知情，发出去的信息broker就收不到）。

1：这意味着producer在leader已成功收到的数据并得到确认后发送下一条message。此选项提供了更好的耐久性为客户等待服务器确认请求成功（被写入死亡leader但尚未复制将失去了唯一的消息）。

-1：这意味着producer在follower副本确认接收到数据后才算一次发送完成。 
此选项提供最好的耐久性，我们保证没有信息将丢失，只要至少一个同步副本保持存活。

三种机制，性能依次递减 (producer吞吐量降低)，数据健壮性则依次递增。

异步模式：通过buffer来进行控制数据的发送，有两个值来进行控制，时间阈值与消息的数量阈值，如果buffer满了数据还没有发送出去，如果设置的是立即清理模式，风险很大，一定要设置为阻塞模式 
结论：producer有丢数据的可能，但是可以通过配置保证消息的不丢失
producer.type=async 
request.required.acks=1 
queue.buffering.max.ms=5000 
queue.buffering.max.messages=10000 
queue.enqueue.timeout.ms = -1 
batch.num.messages=200
b. 消费者
通过offset commit 来保证数据的不丢失，kafka自己记录了每次消费的offset数值，下次继续消费的时候，接着上次的offset进行消费即可。


