如果table只有primary key，用其他非primary key的字段查询就需要遍历table.

这时候就需要secondary index. Secondary index数目不限。

对于不支持secondary index的数据库

法1重复建多张相同的表，每张用不同的key。缺点是只适用于相对static的数据，不适合需要经常改变的数据

![](/assets/index table1.png)

法2 新建index table, 映射secondary key和原表的primary key

![](/assets/index table2.png)

法3 新建index table, 映射secondary key和原表的数据

![](/assets/index table3.png)

对于shard data, index table用来映射partition key

![](/assets/index table4.png)

# Reference

[https://docs.microsoft.com/en-us/azure/architecture/patterns/index-table](https://docs.microsoft.com/en-us/azure/architecture/patterns/index-table)

