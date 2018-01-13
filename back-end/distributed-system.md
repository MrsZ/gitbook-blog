# 分布式锁

[http://www.hollischuang.com/archives/1716](http://www.hollischuang.com/archives/1716)

三种实现方式

1. 基于数据库
2. 基于缓存
3. 基于Zookeeper

## 数据库锁

法1：在数据库中建一个表，每次调用函数先查表

```sql
CREATE TABLE `methodLock` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `method_name` varchar(64) NOT NULL DEFAULT '' COMMENT '锁定的方法名',
  `desc` varchar(1024) NOT NULL DEFAULT '备注信息',
  `update_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '保存数据时间，自动生成',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uidx_method_name` (`method_name `) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='锁定中的方法';
```

加锁/执行方法

基于unique key的约束

```sql
insert into methodLock(method_name,desc) values (‘method_name’,‘desc’)
```

解锁

```sql
delete from methodLock where method_name ='method_name'
```





队列的效果更优于锁

![](/assets/producer_consumer.png)

