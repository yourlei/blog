title: 初识Mongodb
date: 2015-08-22 22:41:54
tags: [Mongodb, NOSQL]
---
#### 关于Mongodb
Mongodb 是一款为web应用程序和互联网基础设施设计的数据库管理系统。Mongo的数据模型和
持久化策略的设计目标是提供高读写吞吐量，在易于伸缩的同时还能进行自动故障转移。
Mongodb是由10gen公司开发的，Mongo的出现可以说是是个巧合。10gen公司当时开发一个PaaS项目，它由服务器和数据库组成，然而在项目完成后，该项目并没有获得用户是喜爱,但是项目中的新的数据库技术却获得了大多数开发者的青睐。之后10gen将精力集中到了数据库上，也就有了Mongodb的诞生。

#### 特性
##### 文档数据模型
Mongodb的数据模型是面向文档的.文档是Mongodb的核心概念,也是Mongodb的基本数据单元,类似
于关系型数据库中的行。将多个键及其关联的值有序的放置在一起便是文档.

如javascript中可如下表示
``` js
{
	"title": "my blog",
	"content": "Here's my blog post",
	"date": new Date()
}
```
这种写法非常类似于JSON文档，不过Mongodb采用的是Binary JSON（BSON）,它是轻量的二进制
格式，能将Mongodb中的所有文档表示为字符串。BSON的编码和解码速度都很快,它采用C风格的表现方式来表示类型，在大多数编程语言中都非常快。
关于BSON的详细说明，参考http://www.bsonspec.org.

关系型数据库中数据存储在数据表的行中, 每张表都预先定义了模式(Schema);而Mongo中没有表的
概念, 取而代之的是集合,集合中保存着文档.文档的一个特点是无模式,集合中是每个文档都可以有不
同的结构,这对文档的操作提供了很大的自由度;若是在关系数据库中,当我们要添加新的字段时,必须显示的修改表结构.
<!-- more -->
#### 复制
Mongodb通过副本集的拓扑结构提供了复制功能. 副本集数据分布在多台机器上以实现冗余,在服务
器和网络发送故障时,能自动故障转移.副本集由一个主节点和多个从节点构成,主节点可接受读写操
作,从节点只能读.当主节点发送故障时, 集群中会选一个从节点提升为主节点.先前的主节点恢复后,
会变为一个从节点.
<img src="/images/study/20150822-01.jpg" alt="">

#### 数据库扩展
对大多数数据库来说, 升级硬件是最简单的扩展方法. (如内存、CPU升级, 提升单一节点上的硬件来
进行扩展称为垂直扩展或向上扩展. 它的优点是简单、可靠、某种程度上而言还是比较划算的). 当硬
件成本超出我们的承受能力时，可以考虑水平扩展或向外扩展.

水平扩展是通过将数据库分布到多台机器上，使用的是普通硬件，所有托管整个数据集的成本会显著降低.同时,将数据分布在多台服务器上可以降低故障带来的影响.Mongodb的水平扩展易于管理,它通过基于范围的分区机制，即自动分片来实现这一设计目标自动分片机制会自动管理各节点之间的数据分布.分片系统会处理分片节点的增加，帮助进行自动故障转移.
<img src="/images/study/20150822-02.jpg" alt="">

注：文章内容参考《Mongodb实战》《Mongodb权威指南》

