# nginx 服务器配置

## 安装

Linux 安装

`sudo apt-get install nginx`

查看

`nginx`

查看安装路径

`whereis nginx`

## nginx 命令

* `nginx`  启动
* `nginx -t` 测试配置文件
* `nginx -s stop` 快速停止
* `nginx -s quit` 快速退出
* `nginx -s reload` 修改配置后重载生效
* `nginx -s reopen` 重新打开日志文件

## 资料

* [配置HTTPS服务器 官方说明](http://nginx.org/en/docs/http/configuring_https_servers.html)