example

create VPC 172.20.0.0/16

create subnet for each AZ

172.20.1.0/24 ecs-a

172.20.2.0/24 ecs-b

172.20.3.0/24 ecs-c

172.20.4.0/24 ecs-d

172.20.5.0/24 ecs-e

172.20.6.0/24 ecs-f

create api gateway, attach to vpc

create route table

* internal: use nat gateway
* external: use igw

if needed, add peer connection to connect other vpc

