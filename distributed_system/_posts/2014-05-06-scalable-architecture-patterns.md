---
layout: post
title: "可伸缩性系统架构"
description: "可伸缩性系统架构"
tags: [可伸缩性, scalability, pattern, architecture]
---
列举一下现在比较常见的可伸缩系统架构模型。

**负载均衡 + 独立处理单元**

独立对等的处理单元，一起由一个前端负载均衡服务器分发请求。
对等处理单元的数据库可以是私有的，也可以是一个可伸缩共用数据库。一般对等处理单元是无状态。
处理单元返回的数据给客户端。这是现在最常见的一种架构。
![](/assets/distributed_system/images/1.png)

**分发聚合**

分发节点接受请求，把一个任务拆分成多个小任务分发到处理节点池中，每个处理节点处理好请求，把
结果发回分发者做聚合，然后由分发节点聚合汇总小任务的结果集，返回给客户端。这种模型普遍应用
在关键字搜索引擎中。
![](/assets/distributed_system/images/2.png)

**结果缓存**

缓存大量应用在各个层中，当收到一个请求时，首先先查看这个请求是否已经有缓存的结果，有就从缓存
中读取，没有就去执行请求。Memcached是最常见的缓存服务器。
![](/assets/distributed_system/images/3.png)

**总线模型**

所有的工作节点都监控总线服务器中自己关注的状态，读取数据，并且把处理后的数据写入总线服务器中。
这种模式有点类似于发布者和订阅者。
![](/assets/distributed_system/images/4.png)

**流水线模型**

工作节点根据服务的不同被分为不同的群，一个群的输入是上一个群的输出，以这种方式串联起来。
![](/assets/distributed_system/images/5.png)

**P2P模型**

Amazon Dynamo和Cassandra是点对点模型的典型例子。

**Map-Reduce模型**

这种模式应用于并行批处理系统，用于处理实时性不高，数据庞大且松散耦合的应用中。Google的Map-Redue,
Hadoop就是这种模型。
![](/assets/distributed_system/images/6.png)

**有向图模型**

由一个总控制节点接收请求，将请求分成小任务和任务执行图，把任务分散到工作节点池中的节点，并控制
图的执行过程。每个工作节点从输入流中读出数据，根据读取的数据处理，把处理结果写到输出流。这里的
输入流和输出流往往是分布式可伸缩存储或文件系统。[Microsoft Dryad](http://research.microsoft.com/en-us/projects/dryad/)
和[Google Pregel](http://dl.acm.org/citation.cfm?id=1807184)应该用的就是这种模型。
![](/assets/distributed_system/images/7.png)
![](/assets/distributed_system/images/8.png)
