Basic objects

Pod: pod是最基本单元，一个Pod可以运行一个或多个container. Pod通常不单独使用，通常需要controller控制

```
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
```

Service是Pod的逻辑集合

Volume

Namespace：用于区分资源

# Controllers

ReplicaSet: 维护Replica

Deployments: 用于更新pod和ReplicaSets

StatefulSets: 创建stateful应用

DaemonSet: 在所有的node上运行相同的pod，类似于docker swarm的global.

Job: 运行完之后结束Pod。



