# 分布式锁

[http://www.hollischuang.com/archives/1716](http://www.hollischuang.com/archives/1716)

三种实现方式

1. 基于数据库
2. 基于缓存
3. 基于Zookeeper

## 基于数据库

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

法2： 基于数据库的排他锁

同样使用刚才那张表,查询语句后面加for update，数据库会在查询过程中给表增加排他锁。InnoDB引擎在加锁的时候，只有通过索引进行检索的时候才会使用行级锁，否则会使用表级锁。

加锁/执行方法

```java
public boolean lock(){
    connection.setAutoCommit(false)
    while(true){
        try{
            result = select * from methodLock where method_name=xxx for update;
            if(result==null){
                return true;
            }
        }catch(Exception e){

        }
        sleep(1000);
    }
    return false;
}
```

解锁

```java
public void unlock(){
    connection.commit();
}
```

## 基于缓存

给锁加上expire

加锁

```java
public boolean trylock(String key) {
    ResultCode code = ldbTairManager.put(NAMESPACE, key, "This is a Lock.", 2, 0);
    if (ResultCode.SUCCESS.equals(code))
        return true;
    else
        return false;
}
```

解锁

```java
public boolean unlock(String key) {
    ldbTairManager.invalid(NAMESPACE, key);
}
```



## 基于Zookeeper

基于zookeeper的临时有序节点

大致思想即为：每个客户端对某个方法加锁时，在zookeeper上的与该方法对应的指定节点的目录下，生成一个唯一的瞬时有序节点。 判断是否获取锁的方式很简单，只需要判断有序节点中序号最小的一个。 当释放锁的时候，只需将这个瞬时节点删除即可。同时，其可以避免服务宕机导致的锁无法释放，而产生的死锁问题。

可以直接使用zookeeper第三方库[Curator](https://curator.apache.org/)客户端，这个客户端中封装了一个可重入的锁服务。

Curator提供的InterProcessMutex是分布式锁的实现。acquire方法用户获取锁，release方法用于释放锁。

```java
public boolean tryLock(long timeout, TimeUnit unit) throws InterruptedException {
    try {
        return interProcessMutex.acquire(timeout, unit);
    } catch (Exception e) {
        e.printStackTrace();
    }
    return true;
}
public boolean unlock() {
    try {
        interProcessMutex.release();
    } catch (Throwable e) {
        log.error(e.getMessage(), e);
    } finally {
        executorService.schedule(new Cleaner(client, path), delayTimeForClean, TimeUnit.MILLISECONDS);
    }
    return true;
}
```



队列的效果更优于锁

![](/assets/producer_consumer.png)

