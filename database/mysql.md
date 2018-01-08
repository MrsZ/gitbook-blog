# Normal Form 范式

在范式化的数据库中， 每个事实数据会出现并且只出现一次。 相反， 在反范式化的数据库中， 信息是冗余的， 可能会存储在多个地方。

反范式的优点在于不需要关联表。

第一范式\(1NF\)：字段值具有原子性,不能再分\(所有关系型数据库系统都满足第一范式\);  
 例如：姓名字段,其中姓和名是一个整体,如果区分姓和名那么必须设立两个独立字段;

第二范式\(2NF\)：一个表必须有主键,即每行数据都能被唯一的区分;  
 备注：必须先满足第一范式;

第三范式\(3NF\)：一个表中不能包涵其他相关表中非关键字段的信息,即数据表不能有沉余字段;  
 备注：必须先满足第二范式;

# Storage Engine

MySQL有两种存储引擎

MyISAM和InnoDB

一般情况下都会选择InnoDB, 在大数据量情况下更优，支持事务

# 权限管理

创建用户

设置权限

对于连接数据库，只允许使用内网域名，而不是ip

1. 出于安全性
2. 机器迁移/平滑升级/运维管理

# 表规范

必须使用utf8mb4字符集

utf8mb4是utf8的超集，emoji表情以及部分不常见汉字在utf8下会表现为乱码，故需要升级至utf8mb4。

禁止使用存储过程、视图、触发器、Event

**禁止**使用foreign key，如果有外键完整性约束，需要应用程序控制。

外键会导致表之间的耦合，update和delete操作都会涉及关联的表,十分影响sql 的性能，甚至会造成死锁。高并发情况下容易造成数据库性能，大数据高并发业务场景数据库使用以性能优先

# 类型规范

存储价格金额时，使用INT或者使用decimal\(m, n\).

1. float和double等浮点数据类型在计算时可能出错。
2. 使用INT类型的话，以分为单位存储
3. 尽量少使用除法

表必须有主键，例如自增主键

1. 主键递增，数据行写入可以提高插入性能，可以避免page分裂，减少表碎片提升空间和内存的使用
2. 主键要选择较短的数据类型，Innodb引擎普通索引都会保存主键的值，较短的数据类型可以有效的减少索引的磁盘空间，提高索引的缓存效率
3. 无主键的表删除，在row模式的主从架构，会导致备库夯住

时间

**禁止**把字段定义为NULL，至少需要默认值

1. null的列使索引/索引统计/值比较都更加复杂，对MySQL来说更难优化
2. null这种类型MySQL内部需要进行特殊处理，增加数据库处理记录的复杂性；同等条件下，表中有较多空字段的时候，数据库的处理性能会降低很多
3. null值需要更多的存储空，无论是表还是索引中每行中的null的列都需要额外的空间来标识
4. 对null的处理时候，只能采用is null或is not null，而不能采用=、in、&lt;、&lt;&gt;、!=、not in这些操作符号。如：where name!=’shenjian’，如果存在name为null值的记录，查询结果就不会包含name为null值的记录

对于手机号使用varchar\(20\)存储

1. 涉及到区号或者国家代号，可能出现+-\(\)
2. 手机号会去做数学运算么？
3. varchar可以支持模糊查询，例如：like“138%”

禁止使用ENUM，可使用TINYINT代替

1. 增加新的ENUM值要做DDL操作，即会改变表结构
2. ENUM的内部实际存储就是整数

大文件和图片存在文件系统中，数据库只存URI

# SQL规范

**禁止**使用单独的负向查询NOT、!=、&lt;&gt;、!&lt;、!&gt;、NOT IN、NOT LIKE等，会导致全表扫描

1. 单独的负向查询会导致全表扫描，如果要使用负向查询的话需要在前面加上过滤语句。例子：

```sql
SELECT oid FROM t_order WHERE uid=123 AND status != 1;
```

**禁止**大表使用JOIN查询，禁止大表使用子查询

**禁止**使用SELECT \*，只获取必要的字段，需要显示说明列属性

1. 读取不需要的列会增加CPU、IO、NET消耗
2. 不能有效的利用覆盖索引
3. 使用SELECT \*容易在增加或者删除字段后出现程序BUG

禁止使用INSERT INTO t\_xxx VALUES\(xxx\)，必须显示指定插入的列属性

1. 容易在增加或者删除字段后出现程序BUG

**禁止**使用属性隐式转换，见案例1

# 索引规范

# 案例

案例1

```sql
SELECT uid FROM t_user WHERE phone=13812345678
```

会导致全表扫描，而不能命中Phone索引。因为phone是varchar类型，SQL语句带入的是整型，改为

```sql
SELECT uid FROM t_user WHERE phone=’13812345678’
```

# Reference

[58到家数据库30条军规解读](https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651959906&idx=1&sn=2cbdc66cfb5b53cf4327a1e0d18d9b4a&chksm=bd2d07be8a5a8ea86dc3c04eced3f411ee5ec207f73d317245e1fefea1628feb037ad71531bc&scene=21#wechat_redirect)

[再议数据库军规](https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651959910&idx=1&sn=6b6853b70dbbe6d689a12a4a60b84d8b&chksm=bd2d07ba8a5a8eac6783bac951dba345d865d875538755fe665a5daaf142efe670e2c02b7c71&scene=21#wechat_redirect)

