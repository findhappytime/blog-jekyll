---
layout: post
title:  简析Storm-Spark-Flink及如何保证不丢数据
date:   2018-08-10 19:00:00 +0800
categories: 理论
tag: 原创
---

* content
{:toc}

# 简析Storm-Spark-Flink及如何保证不丢数据

# 1.带着问题分享

## 1.1.如何保证不丢数据，实时计算几种语义的实现?
## 1.2.Storm 如何保证数据不丢?
## 1.3.Storm 如何保证数据不重复?
## 1.4.Storm 如何保证数据分支,分组?
## 1.5.Spark-Flink是如何实现的?
## 1.6.Storm-Spark-Flink使用场景?


# 2.如何保证不丢数据，实时计算几种语义的实现

At most once - 每条数据最多被处理一次（0次或1次）
At least once - 每条数据最少被处理一次 (1次或更多)
Exactly once - 每条数据只会被处理一次（没有数据会丢失，并且没有数据会被多次处理）

![storm](http://otferhktu.bkt.clouddn.com/%E4%BF%9D%E8%AF%81%E6%95%B0%E6%8D%AE%E4%B8%8D%E4%B8%A2.png)


# 3.简单介绍Storm-Spark-Flink
## 3.1.Storm
### 3.1.1.Storm-简单介绍-work count举例
![storm](http://otferhktu.bkt.clouddn.com/storm1.png)

spout：负责从数据源接收数据
bolt：负责数据处理，最下游的bolt负责数据输出

spout不断从数据源接收数据，然后按一定规则发送给下游的bolt进行计算，最下游的bolt将最终结果输出到外部系统中（这里假设输出到DB），这样我们在DB中就可以看到最新的数据统计结果。
Storm每一层的算子都可以配置多个，这样保证的水平扩展性。

## 3.1.2.Storm-容灾
容灾是所有系统都需要考虑的一个问题，考虑一下：假如运行过程中，一个算子（bolt）因某种原因挂了，Storm如何恢复这个任务呢？
![storm](http://otferhktu.bkt.clouddn.com/storm2.png)

批处理解决方案就比较简单，拿MR举例，假如一个运行中map或reduce失败，那么任务重新提交一遍就ok（只不过重头计算又要花费大量时间），下面我们看看Storm是如何解决的：
storm的spout有一个buffer，会缓存接收到的record，并且Storm还有一个acker（可以认为是一个特殊的bolt任务），每条record和该record所产生的所有tuple在处理完成后都会向对应的acker发送ack消息，当acker接收到该record所有的ack消息之后，便认为该record处理成功，并通知spout从buffer中将该record移除，若receiver没有在规定的时间内接收到ack，acker则通知spout重放数据。

## 3.1.3.Storm-数据不重不丢
![storm](http://otferhktu.bkt.clouddn.com/storm3.png)


sink处的重复输出：假如运行过程中，boltA数据入库后，boltB因为某种原因crash了，这时候会导致该record重放，boltA中已经处理过的数据会再次入库，导致部分数据重复输出。

不仅sink处存在重复输出的问题，receiver处也同样存在这种问题。

那么有没有一种架构，可以满足高吞吐、低延迟的要求，同时也提供exactly once功能？有的，下面我们来看看Spark streaming。

## 3.2.Spark

## 3.3.Flink

## 4.Storm-Spark-Flink 对比及使用场景


