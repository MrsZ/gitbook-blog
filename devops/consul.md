functionalities:

* service registration and discovery
* health check
* key-value store

Consul is distributed system where agent nodes communicate with server nodes:

Servers are responsible to maintain the cluster' state

An agent is responsible to perform health checks of the node it's running on and also of the services running on that node

# example {#example}

## 1. run consul agent {#1-run-consul-agent}

```
consul agent -dev -client=0.0.0.0
```

## 2. Check the members of the cluster {#2-check-the-members-of-the-cluster}

```
consul members
```

or

```
curl localhost:8500/v1/catalog/nodes
```

## 3. Register a service {#3-register-a-service}

run a container

```
docker run --name nginx -d -p 80:80 nginx
```

register to consul

```
echo
 '{

"ID"
: 
"web"
,

"Name"
: 
"web"
,

"Address"
: 
"127.0.0.1"
,

"Port"
: 80
}' 
>
 web.json
```

```
curl -X PUT --data-binary @web.json http:
//
localhost:
8500
/v1/
agent
/service/
register
```

test

```
curl 
http:
//localhost:8500/v1/agent/services
```

## 4. Use DNS embedded server {#4-use-dns-embedded-server}

```
dig @
127.0
.
0.1
 -
p
8600
 web
.service
.consul
```

```
dig @
127.0
.
0.1
 -
p
8600
 web
.service
.consul
 SRV
```

## 5. Health Check {#5-health-check}

deregister the previous service

```
curl 
http:
//localhost:8500/v1/agent/service/deregister/web
```

defining a health check

```
echo
 '{

"ID"
: 
"web"
,

"Name"
: 
"web"
,

"Address"
: 
"127.0.0.1"
,

"Port"
: 80,

"check"
: {

"http"
: 
"http://127.0.0.1:80"
,

"interval"
: 
"10s"
,

"timeout"
: 
"1s"

   }
}' 
>
 web-health.json
```

```
curl -X PUT --data-binary @web-health.json http://localhost:8500/v1/agent/service/register
```

## 6. Key value store {#6-key-value-store}

```
consul kv put redis/config/maxconns 25
```

```
consul kv get redis/config/maxconns
```

# Docker {#docker}

## 1. start agent {#1-start-agent}

```
docker run -d --name=c1 -p 8500:8500 consul agent -dev -client=0.0.0.0 -bind=0.0.0.0
```

## 2. add additional agents {#2-add-additional-agents}

use IP to locate consul cluster

```
IP=$(docker inspect --format '{{ .NetworkSettings.IPAddress }}' c1); echo
$IP
```

```
docker run -d --name c2 consul agent -dev -bind=0.0.0.0 -join=$IP
```

to see cluster logs

```
docker logs c1
```

## 3. Simulate Node Failure {#3-simulate-node-failure}

check members of consul cluster

```
docker exec -t c1 consul members
```

```
docker kill c3
```

```
docker exec -t c1 consul members
```

the state of member will change from active to failed

```
docker logs c1
```

## 4.UI {#4ui}

UI is on port 8500

