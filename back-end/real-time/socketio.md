Socket.IO分为client和server端

[https://hackernoon.com/scaling-websockets-9a31497af051](https://hackernoon.com/scaling-websockets-9a31497af051)

how to scale [https://socket.io/docs/using-multiple-nodes/](https://socket.io/docs/using-multiple-nodes/)

1. use a load balancer
   1. Nginx
   2. Cluster module
2. add a pub/sub layer for it: redis, rabbitmq, kafka, rethinkdb
   1. main concept is register room info of nodes in redis, then when broadcast use for loop to send message to all nodes 

# Authentication

以event的moderator为例，假设发送event中有N个用户，M个moderator，一共发送C条命令

1. join之后注册所有Listener, 后每次收到命令检查是否为moderator， 查询次数为C
2. join之后检查是否为moderator, 根据是否为moderator注册不同的listener，之后不再检查，查询次数为N
3. 分为两个room，分别只包含moderator和所有用户，当用户加入moderator room之后注册所有moderator的listener，查询次数为M



