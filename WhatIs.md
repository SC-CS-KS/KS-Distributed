
# What Is
```md
	分布式就意味着分治与协作，一件事一个人只负责一部分。
```
```md
三个问题
	可扩展性
	负载均衡
	容错处理
```
```md
评价
	性能
		吞吐量：某一时间可以处理的数据总量
		响应延迟：完成某一功能需要使用的时间
		并发能力：QPS(query per second)
	可用性
		系统停服务的时间与正常服务的时间的比例
	可扩展性
		通过扩展集群机器提高系统性能、存储容量、计算能力的特性，是分布式系统特有的性质
	一致性
```
```md
		进程与线程
		并发
		锁
		并行
		集群
		状态特性
		系统重发与幂等性
		硬件异常
```
## SOA 到 MSA的 进化
```md
SOA面向服务架构
由于业务发展到一定层度后，需要对服务进行解耦，进而把一个单一的大系统按逻辑拆分成不同的子系统，
通过服务接口来通讯，面向服务的设计模式，最终需要总线集成服务，而且大部分时候还共享数据库，
出现单点故障的时候会导致总线层面的故障，更进一步可能会把数据库拖垮，所以才有了更加独立的设计方案的出现。
```
```md
微服务是真正意义上的独立服务，从服务入口到数据持久层，逻辑上都是独立隔离的，无需服务总线来接入，
但同时增加了整个分布式系统的搭建和管理难度，需要对服务进行编排和管理，所以伴随着微服务的兴起，
微服务生态的整套技术栈也需要无缝接入，才能支撑起微服务的治理理念。
```

## 节点
```md
传统的节点也就是一台单体的物理机，所有的服务都揉进去包括服务和数据库；
随着虚拟化的发展，单台物理机往往可以分成多台虚拟机，实现资源利用的最大化，节点的概念也变成单台虚拟机上面服务；
近几年容器技术逐渐成熟后，服务已经彻底容器化，也就是节点只是轻量级的容器服务。
总体来说，节点就是能提供单位服务的逻辑计算资源的集合。
```

## 网络
```md
分布式架构的根基就是网络，不管是局域网还是公网，没有网络就无法把计算机联合在一起工作，但是网络也带来了一系列的问题。
网络消息的传播有先后,消息丢失和延迟是经常发生的事情。
```
***网络工作模式***
* 同步网络同步网络
```md
节点同步执行
消息延迟有限
高效全局锁
```
* 半同步网络
```md
锁范围放宽
```
* 异步网络
```md
节点独立执行
消息延迟无上限
无全局锁
部分算法不可行
```

## 场景
* 文件系统
```md
HDFS
FastDFS
Ceph
mooseFS
```
* 数据库
```md
列式存储：Hbase
文档存储：Elasticsearch，MongoDB
KV类型：Redis
关系型：Spanner
```
* 计算
```md
离线：Hadoop
实时：Spark
流式：Storm，Flink/Blink
``
* 缓存
```md
持久化：Redis
非持久化：Memcache
```
* 消息
```md
Kafka
RabbitMQ
RocketMQ
ActiveMQ
```
* 监控
```md
Zookeeper
```
* 应用
```md
HSF
Dubble
```
* 日志
```md
日志采集：flume
日志存储：ElasticSearch/Solr，SLS
日志定位：Zipkin
```
* 账本
```md
比特币
以太坊
```

