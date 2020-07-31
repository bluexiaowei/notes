# MongoDB 数据库

## 安装

```shell
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list

sudo apt-get update

sudo apt-get install -y mongodb-org
```

## 启动

```shell
$ sudo systemctl start mongod
Failed to start mongod.service: Unit mongod.service not found.

$ sudo systemctl daemon-reload

$ sudo systemctl status mongod

$ sudo systemctl enable mongod

```

## 卸载

```shell
sudo service mongod stop

sudo apt-get purge mongodb-org*

sudo rm -r /var/log/mongodb

sudo rm -r /var/lib/mongodb
```

## 说明

日志：`/var/log/mongodb/mongod.log`

配置：`/etc/mongod.conf`

安全：

默认情况下，MongoDB 在启动时 bindIp 将 set 设置为 127.0.0.1，该绑定到 localhost 网络接口。这意味着 mongod 只能接受来自同一计算机上运行的客户端的连接。除非将此值设置为有效的网络接口，否则远程客户端将无法连接到 mongod，并且 mongod 不能初始化副本集。

## 命令

| 命令                           | 解释                             |
| :----------------------------- | :------------------------------- |
| db                             | 命令可以显示当前数据库对象或集合 |
| show dbs                       | 查看所有数据库                   |
| show collections               | 查看所有集合                     |
| use                            | 创建数据库或者切换数据库         |
| .dropDatabase                  | 删除数据库                       |
| .createCollection(name, opts)  | 创建集合                         |
| .collection.drop()             | 删除集合                         |
| .repairDatabase()              | 收磁盘空间                       |
| .insert                        | 插入数据                         |
| .insertOne() / .replaceOne()   | 更新数据，如果不存在就插入数据   |
| .insertOne() / .insertMany([]) | 更新数据，如果不存在就插入数据   |
| .update(query, update, opt)    | 更新已存在的文档                 |
| .remove(query, opt)            | 移除集合中的数据                 |
| .deleteOne() / deleteMany()    | 移除集合中的数据                 |
| .find()                        | 读取数据                         |
| .find().limit()                | 读取指定数量的数据记录           |
| .find().sort()                 | 通过参数指定排序的字段           |
| .find().limit().skip()         | 跳过指定数量的数据               |
| .find().pretty()               | 可视化                           |
| .createIndex()                 | 创建索引                         |
| .getIndexes()                  | 查看集合索引                     |
| .totalIndexSize()              | 查看集合索引大小                 |
| .dropIndex()                   | 删除集合指定索引                 |
| .dropIndexes()                 | 删除集合所有索引                 |
| .aggregate()                   | 处理数据(诸如统计平均值,求和等)  |
| \$gt                           | (>) 大于                         |
| \$lt                           | (<) 小于                         |
| \$gte                          | (>=) 大于等于                    |
| \$lte                          | (<= ) 小于等于                   |
| \$or                           | (\|\| ) 或                       |
| \$type                         | 检索集合中匹配的数据类型         |

链接数据库

`mongodb://username:password@host1:port1`

## 创建用户

```shell
use admin;

db.createUser({
    user: "admin",
    pwd: "SF6aToyP9LoEyrle",
    roles: [ { role: "userAdminAnyDatabase", db: "admin"} ]
});

Successfully added user: {
        "user" : "admin",
        "roles" : [
                {
                        "role" : "userAdminAnyDatabase",
                        "db" : "admin"
                }
        ]
}
```

| RoleName             | remark                             |
| :------------------- | :--------------------------------- |
| read                 | 只读数据权限                       |
| readWrite            | 读写数据权限                       |
| dbAdmin              | 在当前 db 中执行管理操作的权限     |
| dbOwner              | 在当前 db 中执行任意操作           |
| userADmin            | 在当前 db 中管理 user 的权限       |
| backup               |                                    |
| restore              |                                    |
| readAnyDatabase      | 在所有数据库上都有读取数据的权限   |
| readWriteAnyDatabase | 在所有数据库上都有读写数据的权限   |
| userAdminAnyDatabase | 在所有数据库上都有管理 user 的权限 |
| dbAdminAnyDatabase   | 管理所有数据库的权限               |
| clusterAdmin         | 管理机器的最高权限                 |
| clusterManager       | 管理和监控集群的权限               |
| clusterMonitor       | 监控集群的权限                     |
| hostManager          | 管理 Server                        |
| root                 | 超级用户                           |

## 注意

### 保留名称

保留数据库名称 admin、local 和 config 。

### 远程连接

如果你的数据库用户不是在 admin 数据库里面创建的要指定 `authSource=xxx`, 默认值：`authSource=admin`

`mongodb://xx:xx@localhost/xx?authSource=xxx`;

### ObjectId

由于 ObjectId 中保存了创建的时间戳，所以你不需要为你的文档保存创建时间戳字段，你可以通过 getTimestamp 函数来获取文档的创建时间。

利用 `ObjectId` 的生成规则去筛选创建时间。

```javascript
function objectIdWithTimestamp(timestamp) {
  if (typeof timestamp == "string") {
    timestamp = new Date(timestamp);
  }

  const hexSeconds = Math.floor(timestamp / 1000).toString(16);

  return ObjectId(hexSeconds + "0000000000000000");
}
```
