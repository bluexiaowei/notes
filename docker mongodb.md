# docker mongodb

### 创建配置文件

```
# /etc/mongo/mongod.conf
systemLog:
   destination: file
   path: "/var/log/mongodb/mongod.log"
   logAppend: true
storage:
   journal:
      enabled: true
processManagement:
   fork: true
net:
   bindIp: 127.0.0.1
   port: 27017
setParameter:
   enableLocalhostAuthBypass: false
```

### 安装

```shell
sudo docker pull mongo:latest

sudo docker volume create mongodb

sudo docker volume create mongocfg

sudo docker run \
  -itd \
  -p 27017:27017 \
  --name mongo \
  --mount source=mongodb,target=/data/db \
  --mount source=mongocfg,target=/data/configdb \
  --mount type=bind,source=/etc/mongo/mongod.conf,target=/etc/mongod.conf.orig \
  mongo
```

or

```shell
sudo docker pull mongo:latest

sudo docker volume create mongodb

sudo docker volume create mongocfg

sudo docker run \
  -itd \
  -p 27017:27017 \
  --name mongo \
  -v mongodb:/data/db \
  -v mongocfg:/data/configdb \
  mongo
```

### 创建用户

```shell
$ sudo docker exec -it mongo bash

root@d03d2a6318ae:/# mongo

> use admin;

> db.createUser({ user:'admin',pwd:'admin',roles:[ { role:'userAdminAnyDatabase', db: 'admin'}]});

Successfully added user: {
	"user" : "admin",
	"roles" : [
		{
			"role" : "userAdminAnyDatabase",
			"db" : "admin"
		}
	]
}

> db.auth('admin', '123456')

1
```

### 设置远程链接

```shell
apt-get update

apt-get install vim -y

vim /etc/mongodb.conf

/etc/init.d/mongodb restart
```

```
# bind_ip = 127.0.0.1
bind_ip = 0.0.0.0
```
