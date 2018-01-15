# Http重定向

当http代理（比如浏览器）向web服务器请求某个URL后，web服务器可以通过http响应头信息中的Location标记来返回一个新的URL。

# DNS负载均衡

通过配置多个A record来实现负载均衡

# 反向代理负载均衡

HTTP层

通过Web服务器作为用户和实际服务器的中间人实现。即Web服务器转发HTTP请求

# IP负载均衡\(LVS-NAT\)

传输层

NAT服务器:它工作在传输层，它可以修改发送来的IP数据包，将数据包的目标地址修改为实际服务器地址。



# 直接路由

而直接路由是工作在数据链路层（第二层）

它通过修改数据包的目标MAC地址（没有修改目标IP），将数据包转发到实际服务器上，不同的是，实际服务器的响应数据包将直接发送给客户羰，而不经过调度器。

# 

# Ref

[https://mp.weixin.qq.com/s/5m0CwUbcw9utPwgIzLO0lA](https://mp.weixin.qq.com/s/5m0CwUbcw9utPwgIzLO0lA)

