# Docker常用应用示例


Kafka, MongoDB

<!--more-->


## Kafka
```bash
docker pull wurstmeister/zookeeper
docker pull wurstmeister/kafka

docker run -d --name zookeeper  -p 2181:2181 -t wurstmeister/zookeeper 

docker run -d --name kafka --publish 9092:9092 \
--link zookeeper \
--env KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 \
--env KAFKA_ADVERTISED_HOST_NAME=127.0.0.1 \
--env KAFKA_ADVERTISED_PORT=9092 \
wurstmeister/kafka

```
test

```sh
# smoke test

docker exec -it kafka /bin/bash

$ /opt/kafka/bin/kafka-console-producer.sh --topic=test --broker-list localhost:9092

$ /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 -from-beginning --topic test
```

## MongoDB

### 1. install mongodb by docker

> 转自 https://blog.csdn.net/weixin_44591832/article/details/91953189



```
# docker pull mongo:4.2.5
docker pull mongo:3.6.17
```



```
# docker run --name mongodb -p 27017:27017 -d mongo:4.2.5 --auth
docker run --name mongodb -p 27017:27017 -d mongo:3.6.17
```



MongoDB添加管理员

```
docker exec -it mongodb mongo admin
```

创建admini管理员账号:

```
# 在所有数据库管理用户
db.createUser({ user: 'root', pwd: 'root', roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] });
```



```
# 授权管理所有数据库
db.createUser({ user: 'admin', pwd: 'admin123', roles: [ { role: "dbAdminAnyDatabase", db: "admin" } ] });
```



```sh
$ docker exec -it mongodb mongo admin
MongoDB shell version v4.2.5
connecting to: mongodb://127.0.0.1:27017/admin?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("685f78a0-4730-4192-a5c5-39677312e765") }
MongoDB server version: 4.2.5
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
        http://docs.mongodb.org/
Questions? Try the support group
        http://groups.google.com/group/mongodb-user
> db.createUser({ user: 'root', pwd: 'root', roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] });
Successfully added user: {
        "user" : "root",
        "roles" : [
                {
                        "role" : "userAdminAnyDatabase",
                        "db" : "admin"
                }
        ]
}
> exit
bye

```



创建普通用户:

```
docker exec -it mongodb mongo admin
```



```
db.auth("root","root");
```



```
db.createUser({ user: 'sunyh', pwd: 'hi123456', roles: [ { role: "readWrite", db: "ngc" } ] });
```



```
db.createUser({ user: 'sunyh', pwd: 'hi123456', roles: [ { role: "dbOwner", db: "ngc" } ] });
```



```sh
$ docker exec -it mongodb mongo admin
MongoDB shell version v4.2.5
connecting to: mongodb://127.0.0.1:27017/admin?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("6658ca1e-15e5-40e4-a507-8a9fab70bee1") }
MongoDB server version: 4.2.5
> db.auth("root","root");
1
> db.createUser({ user: 'sunyh', pwd: 'hi123456', roles: [ { role: "dbOwner", db: "ngc" } ] });
Successfully added user: {
        "user" : "sunyh",
        "roles" : [
                {
                        "role" : "dbOwner",
                        "db" : "app"
                }
        ]
}
> exit
bye

```



```
db.auth("sunyh","hi123456");

use ngc

db.test.save({name:"hello ngc"});
```



```sh
$ docker exec -it mongodb mongo admin
MongoDB shell version v4.2.5
connecting to: mongodb://127.0.0.1:27017/admin?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("19c22492-6b5b-4a99-bbcc-a2c852d003cb") }
MongoDB server version: 4.2.5
> db.auth("sunyh","hi123456");
1
> use ngc
switched to db ngc
> db.test.save({name:"hello ngc"});
WriteResult({ "nInserted" : 1 })
> exit
bye

```



### 2. mongo express

> https://github.com/mongo-express/mongo-express-docker



```
docker pull mongo-express:0.54
```



```
docker run -it -d --name mongo-express --link mongodb:mongo -p 28081:8081 mongo-express:0.54
```



```
docker run -it --rm \
	--name mongo-express \
	--link mongodb:mongo \
	-p 8081:8081 \
	-e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" \
	-e ME_CONFIG_BASICAUTH_USERNAME="user" \
	-e ME_CONFIG_BASICAUTH_PASSWORD="fairly long password" \
	mongo-express
```



```
docker stop mongo-express
docker rm mongo-express
```


