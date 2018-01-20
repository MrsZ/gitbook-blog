[Helmet](https://helmetjs.github.io/)

[https://expressjs.com/en/advanced/best-practice-security.html](https://expressjs.com/en/advanced/best-practice-security.html)

# HTTP security header

* **Strict-Transport-Security **强制将HTTP请求替换为HTTPS请求

* **X-Frame-Options** 防止点击劫持

* **X-XSS-Protection** 开启跨站脚本攻击（XSS）的过滤，大多数现代浏览器支持这个设置

* **X-Content-Type-Options** 禁用浏览器对响应内容MIME类型的嗅探，严格使用响应的Content-Type的值

* **Content-Security-Policy** 能有效防止多种攻击，包括跨站脚本和跨站注入

# 认证

暴力攻击保护

ratelimiter module

# 数据验证

XSS

反射性XSS: 当攻击者用特制的链接将可执行JavaScript代码注入到HTML响应中时发生。

存储型XSS: 当存储了未经严格过滤的用户输入时发生，它会在在Web应用程序的权限下在用户的浏览器中运行。

Solution: 严格过滤用户输入

SQL注入

例子

    ``select title, author from books where id=$id``
    // 注入$id = 2 or 1=1
    ``select title, author from books where id=2 or 1=1``

solution：用问号替换

命令行注入

命令注入是攻击者在远程Web服务器上运行OS命令所使用的技术。通过这种方法，攻击者甚至可以从系统获得到密码。

```
https://example.com/downloads?file=user1.txt
```

可以用如下攻击

```
https://example.com/downloads?file=%3Bcat%20/etc/passwd
```

solution: 过滤用户输入

# 安全传输

检查SSL version, algorithms, key length

使用nmap和sslyze分析

检查证书信息

```
nmap --script ssl-cert,ssl-enum-ciphers -p 443,465,993,995 www.example.com
```



使用sslyze测试SSL/TLS漏洞

```
./sslyze.py --regular example.com:443
```



# DoS

正则表达式DoS \(Evil Regexpes\)

* 使用重复分组
* 重复组中出现: 
  * 重复
  * 交替重叠

例子

```
([a-zA-Z]+)*
(a+)+
(a|a?)+
```

solution: 用类似safe-regex检查正则表达式

# Reference

[https://mp.weixin.qq.com/s/xiy4nTRKCDlFPGi1xn1cnQ](https://mp.weixin.qq.com/s/xiy4nTRKCDlFPGi1xn1cnQ)

