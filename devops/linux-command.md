awk

xargs

```bash
xargs -I {} rm {}
```

-I {} 指定{}为需要替换的位置

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



生成任意大小的文件

```bash
dd if=/dev/zero of=junk.data bs=1M count=1
```

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

---

Remote disk usage health monitor

```bash
#!/bin/bash
#Filename: disklog.sh
#Description: Monitor disk usage health for remote systems


logfile="diskusage.log"

if [[ -n $1 ]]
then
  logfile=$1
fi

if [ ! -e $logfile ]
then
  
  printf "%-8s %-14s %-9s %-8s %-6s %-6s %-6s %s\n" "Date" "IP address" "Device" "Capacity" "Used" "Free" "Percent" "Status" > $logfile
fi

IP_LIST="127.0.0.1 0.0.0.0"
#provide the list of remote machine IP addresses 

(
for ip in $IP_LIST;
do

  ssh slynux@$ip 'df -H' | grep ^/dev/ > /tmp/$$.df

  while read line;
  do
    cur_date=$(date +%D)
    printf "%-8s %-14s " $cur_date $ip
    echo $line | awk '{ printf("%-9s %-8s %-6s %-6s %-8s",$1,$2,$3,$4,$5); }'
    
  pusg=$(echo $line | egrep -o "[0-9]+%")
  pusg=${pusg/\%/};
  if [ $pusg -lt 80 ];
  then
    echo SAFE
  else
    echo ALERT
  fi
  
  done< /tmp/$$.df	
done

) >> $logfile
```



logrotate

It helps to restrict the size of logfile to the given SIZE



config file 

```
/etc/logrotate.d/
```

example 

```bash
$ cat /etc/logrotate.d/nginx
/var/log/nginx/*.log {
	daily
	missingok
	rotate 14
	compress
	delaycompress
	notifempty
	create 0640 www-data adm
	sharedscripts
	prerotate
		if [ -d /etc/logrotate.d/httpd-prerotate ]; then \
			run-parts /etc/logrotate.d/httpd-prerotate; \
		fi \
	endscript
	postrotate
		invoke-rc.d nginx rotate >/dev/null 2>&1
	endscript
}

```



