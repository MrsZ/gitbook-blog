# 分布式锁

http://www.hollischuang.com/archives/1716

三种实现方式

1. 基于数据库
2. 基于缓存
3. 基于Zookeeper

## 数据库锁

法1：在数据库中建一个表包含method\__name和update\_time_



