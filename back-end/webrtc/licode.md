Docker

```
MIN_PORT=30000; MAX_PORT=30050; docker run -d --name licode -p 3000:3000 -p $MIN_PORT-$MAX_PORT:$MIN_PORT-$MAX_PORT/udp -p 3001:3001  -p 8080:8080 -e "MIN_PORT=$MIN_PORT" -e "MAX_PORT=$MAX_PORT" -e "PUBLIC_IP=0.0.0.0" lynckia/licode
```

Roles

[http://lynckia.com/licode/roles.html](http://lynckia.com/licode/roles.html)

# set HTTPS

[http://lynckia.com/licode/nginx-dep.html](http://lynckia.com/licode/nginx-dep.html)

in licode\_config, should set

```
config.erizoController.hostname
```

otherwise will show certificate name does not match

# Build Image Base on Official Image

# Solution for Large Scale

master slave architecture

master for publishing videos

slave for subscribing videos

there should be one bridge to forward video stream from master node to slave node.



