# http 证书生成脚本

> acme.sh 实现了 acme 协议, 可以从 letsencrypt 生成免费的证书.

## 安装

安装命令

`curl  https://get.acme.sh | sh`

安装完成后

`~/.acme.sh/`

设置别名 alias

`alias acme.sh=~/.acme.sh/acme.sh`

## 生成证书

生成好的证书在 `~/.acme.sh/` 文件夹下面。

### http

只需要指定域名, 并指定域名所在的网站根目录. acme.sh 会全自动的生成验证文件, 并放到网站的根目录, 然后自动完成验证. 最后会聪明的删除验证文件. 整个过程没有任何副作用。

`acme.sh  --issue  -d mydomain.com -d www.mydomain.com  --webroot  /home/wwwroot/mydomain.com/`

如果你用的 apache服务器, acme.sh 还可以智能的从 apache的配置中自动完成验证, 你不需要指定网站根目录:

`acme.sh --issue  -d mydomain.com   --apache`

如果你用的 nginx服务器, 或者反代, acme.sh 还可以智能的从 nginx的配置中自动完成验证, 你不需要指定网站根目录:

`acme.sh --issue  -d mydomain.com   --nginx`

生成完成需要手动修改配置。

### dns

## copy/安装 证书

前面证书生成以后, 接下来需要把证书 copy 到真正需要用它的地方.

注意, 默认生成的证书都放在安装目录下: ~/.acme.sh/, 请不要直接使用此目录下的文件, 例如: 不要直接让 nginx/apache 的配置文件使用这下面的文件. 这里面的文件都是内部使用, 而且目录结构可能会变化.

正确的使用方法是使用 --install-cert 命令,并指定目标位置, 然后证书文件会被copy到相应的位置, 例如:

**Apache example:**

```
acme.sh --install-cert -d example.com \
--cert-file      /path/to/certfile/in/apache/cert.pem  \
--key-file       /path/to/keyfile/in/apache/key.pem  \
--fullchain-file /path/to/fullchain/certfile/apache/fullchain.pem \
--reloadcmd     "service apache2 force-reload"
```

**Nginx example:**

```
acme.sh --install-cert -d example.com \
--key-file       /path/to/keyfile/in/nginx/key.pem  \
--fullchain-file /path/to/fullchain/nginx/cert.pem \
--reloadcmd     "service nginx force-reload"
```

(一个小提醒, 这里用的是 service nginx force-reload, 不是 service nginx reload, 据测试, reload 并不会重新加载证书, 所以用的 force-reload)

Nginx 的配置 ssl_certificate 使用 /etc/nginx/ssl/fullchain.cer ，而非 /etc/nginx/ssl/<domain>.cer ，否则 SSL Labs 的测试会报 Chain issues Incomplete 错误。

--install-cert命令可以携带很多参数, 来指定目标文件. 并且可以指定 reloadcmd, 当证书更新以后, reloadcmd会被自动调用,让服务器生效.

## 更新证书

* 手动升级 `acme.sh --upgrade`
* 自动升级 `acme.sh --upgrade --auto-upgrade`
* 关闭自动升级 `acme.sh --upgrade --atuo-upgrade 0`

## 调试

`acme.sh --issue ..... --debug`

或者

`acme.sh --issue ..... --debug 2`


## 资料

* [acem.sh REAMDE 中文](https://github.com/acmesh-official/acme.sh/wiki/%E8%AF%B4%E6%98%8E)

## 问题

### 1. Create new order error. Le_OrderFinalize not found.

申请太过频繁被 let’s Encrypt 限制申请。

* [let's Encrypt 官方说明](https://letsencrypt.org/zh-cn/docs/rate-limits/) 
* [acme.sh issue](https://github.com/acmesh-official/acme.sh/issues/2213)