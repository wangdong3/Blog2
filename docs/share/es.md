# ElasticSearch  

## 一、ES了解  

### what  
es是一个**实时**分布式搜索和分析引擎，它让你以前所未有的**速度**处理大数据成为可能。

### 使用场景  
es用于**全文搜索**、**结构化搜索**、**分析**以及将这三者混合使用

### 安装  
[https://www.elastic.co/cn/downloads/elasticsearch](https://www.elastic.co/cn/downloads/elasticsearch ) 
下载、解压、启动

### 集群和节点  
节点是一个运行着es的实例。集群是一组具有相同cluster.name的节点集合。

### API  
es为Java提供两种客户端：node client，transport client。
- **节点客户端(node client)**：
节点客户端以无数据节点(none data node)身份加入集群，换言之，它自己不存储任何数据，但是它知道数据在集群中的具
体位置，并且能够直接转发请求到对应的节点上。

- **传输客户端(Transport client)**：
这个更轻量的传输客户端能够发送请求到远程集群。它自己不加入集群，只是简单转发请求给集群中的节点。

两个Java客户端都通过9300端口与集群交互，使用Elasticsearch传输协议(Elasticsearch Transport Protocol)。集群中的节点之间也通过9300端口进行通信。如果此端口未开放，你的节点将不能组成集群。

**基于HTTP协议，以JSON为数据交互格式的RESTful API**

### 索引类型文档  

Elasticsearch集群可以包含多个索引(indexes)（数据库），每一个索引可以包含多个类型(types)（表），每一个类型包含多个文档(documents)（行），然后每个文档包含多个字段(Fields)（列）。

## 使用方式  

## 监控工具  

- head 
浏览器端，可以看到每个分片信息；可以发送rest API请求

## 内部原理  

## 搜索过程  

