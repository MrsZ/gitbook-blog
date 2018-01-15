awk

xargs

sed

df -h

df -hi

Clear system logs

```bash
cat /dev/null > /path/to/logfile
```

host files

environment variable

crob

create service

# Concepts

* inodes
* probes

# Tools

ncdu: [https://dev.yorhel.nl/ncdu](https://dev.yorhel.nl/ncdu)

analysis disk usage

# Trouble Shot

disk analysis:

df -h 显示整个磁盘空间使用状况

df -hi显示整个磁盘inodes使用状况

network analysis

dig \[domain name\]

分为question和answer section

answer section返回DNS records

[http://www.ruanyifeng.com/blog/2016/06/dns.html](http://www.ruanyifeng.com/blog/2016/06/dns.html)

# Network

check for open prots

```bash
sudo netstat -pltn
```

# Web Server

Apache不适合处理大流量高并发，Nginx没有Built-in动态内容处理，两者可以联合使用。

nginx reverse proxy: [https://www.nginx.com/resources/admin-guide/reverse-proxy/](https://www.nginx.com/resources/admin-guide/reverse-proxy/)

nginx load balancer: layer 7 HTTP traffic, layer 4 database traffic [https://www.nginx.com/resources/admin-guide/load-balancer/](https://www.nginx.com/resources/admin-guide/load-balancer/)

常见配置

```other
http {
    upstream backend {
        server backend1.example.com weight=5;
        server backend2.example.com;
        server 192.0.0.1 backup;
    }
}
```

Load balancing method, server weights, health check, limit number of connections, persistence session

HTTPS

# 数据同步

scp

sftp

rsync

