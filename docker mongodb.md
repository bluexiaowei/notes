# docker mongodb

安装

```shell
sudo docker pull mongo:latest

sudo docker run \
  -itd \
  --name mongo \
  --mount source=mongoDB,target=/data/db \
  -p 27017:27017 \
  mongo
```

创建用户

```shell
$ sudo docker exec -it mongo bash

root@d03d2a6318ae:/# mongo

> use admin;

> db.createUser({ user:'admin',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'}]})

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

设置远程链接

```shell
apt-get update

apt-get install vim -y

vim /etc/mongodb.conf

/etc/init.d/mongodb restart
```

bind_ip = 0.0.0.0
