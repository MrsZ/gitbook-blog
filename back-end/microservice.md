# API Gateway

[https://blog.risingstack.com/building-an-api-gateway-using-nodejs/](https://blog.risingstack.com/building-an-api-gateway-using-nodejs/)

API gateway主要是用来实现各个service的公用功能

问题在于使用API gateway所有流量都会经过它，所以它必须可靠稳定

已有开源方案

Netflix/zuul，Kong/kong，openresty/openresty + 自研，TykTechnologies/tyk，Netty + 自研

Features

* routing and versioning
* authentication
* data aggregation
* Serialization format transformation
* Protocol transformation
* Rate-limiting and caching

List

* **API proxying**
* **Logging**
* **Service discovery and registration**
* **Service dependencies**
* **Data sharing and synchronization**
* **Graceful failure**
* **Automated deployment and instantiation**

Share data:

use one service manage shared data

