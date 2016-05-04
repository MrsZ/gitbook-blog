# 读书笔记
-----
强烈推荐使用safaribookonline阅读
-----

**Storm real-time processing cookbook(2013)  **
综合评价：只能作为实例的参考书，让人又爱又恨。 $$3/5$$
简介：以实例为主，不适合初学者上手，其中对于基本概念的讲解实在让人汗颜。有完整的代码示例。
  - Chapter 3: 计算TF-IDF,作者希望通过此章介绍Trident(Storm的高级元语言)，但是除了对代码做了简单注释，对基本概念完全没有讲清楚,代码中混入了大量的Trident的复杂概念。并且除Trident编程之外，又混入了DRPC的知识，也没有讲解，让人不明所以.

**Storm Blueprints:Patterns for Distributed Real-time Computation (Packt, 2014)**
综合评价：强烈推荐！！！Storm入门首选。唯一美中不足，缺失两章代码。
简介：内容涉及方面与Storm Cookbook类似，但是对基础概念讲解相当透彻
  - Chapter :介绍了Graph analysis的基本知识，

**Graph Databases, 2nd Edition (O'Reilly, 2015)**
- Chapter 2: Options for Storing Connected Data: Relational Database和普通的NoSQL的表之间都缺乏relationship (隐含)， Graph Database删除表示relationship
- Chapter 3: Data Modeling with Graphs: 简介Cypher(Graph query language). Compare Relational database (tables, normalization, denormalization) and graph modeling

**Cassandra Design Patterns （Packt, 2014）**




## Big Data
大数据本质是掌握工具框架，入门之后还是靠语言积累，所以还是算法+数据结构。  
所有大数据工具推荐学习顺序：  
Standalone --> 运行实例 --> 修改实例 --> 开发实例 --> Cluster mode
### Storm
Standalone mode
Cluster mode
### Hadoop

### Kafka
console and java driver
####坑
DataStax的cassandra core依赖项问题


### Spark

### Apache Cassandra
分布式Column-based Database
####坑
配置文件千万不要在前面加空格，否则报错

## Visualization


## Data Visualization
### D3.js
#### Map

### Mapbox
优势：高精度， high resolution


## Database
### Graph Database
#### Cypher
Cypher: graph database query language  
examples
```
(emil)<-[:KNOWS]-(jim)-[:KNOWS]->(ian)-[:KNOWS]->(emil)
```
```
MATCH (a:Person {name:'Jim'})-[:KNOWS]->(b)-[:KNOWS]->(c),
      (a)-[:KNOWS]->(c)
RETURN b, c
```
```
MATCH (a:Person)-[:KNOWS]->(b)-[:KNOWS]->(c), (a)-[:KNOWS]->(c)
WHERE a.name = 'Jim'
RETURN b, c
```

#### Neo4j


### 经典论文


## 有趣的项目
Machine Learning预测《冰与火之歌》中的叛徒





# Open Courses
网站
- Udacity: 个人认为最适合入门的一套课程
- edx：公开课鸽子王，课程长期跳票
- Big Data University
- Coursera: 整体课程偏理论，而且并不深入，实战内容较少
- 慕课网
- 麦子学院: 有涉及到架构的课程，讲课老师的整体实力较强
- 宅客学院
- MIT opencourse
- 极客学院： 课程较新，但是讲师的水平和普通话水平参差不齐。但整体来说一年花260元买个会员还是利大于弊的。




# TODO
- [] s3-file-server
- [] MapReduce Design Pattern