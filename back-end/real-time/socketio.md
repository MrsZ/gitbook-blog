Socket.IO分为client和server端

[https://hackernoon.com/scaling-websockets-9a31497af051](https://hackernoon.com/scaling-websockets-9a31497af051)

how to scale [https://socket.io/docs/using-multiple-nodes/](https://socket.io/docs/using-multiple-nodes/)

1. use a load balancer
   1. Nginx
   2. Cluster module
2. add a pub/sub layer for it: redis, rabbitmq, kafka, rethinkdb
   1. main concept is register room info of nodes in redis, then when broadcast use for loop to send message to all nodes 



