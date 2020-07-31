# Frp 内网穿透

## 使用

编写 `/etc/frp/frps.init`

```
[common]
bind_addr = 0.0.0.0
bind_port = 7000
vhost_http_port = 80
vhost_https_port = 443
dashboard_port = 7500
privilege_mode = true
privilege_token = 12345678

[ssh]
type = tcp
auth_token = 123
bind_addr = 0.0.0.0
listen_port = 6000
```

运行 docker

```shell
sudo docker pull fatedier/frp

sudo docker run \
    -itd \
    --network host \
    --name frps \
    --mount type=bind,source=/etc/frp/frps.ini,target=/etc/frp/frps.ini \
    snowdreamtech/frps
```

## 资料

- [Github frp](https://github.com/fatedier/frp)
- [Doc zh-cn](https://github.com/fatedier/frp/blob/master/README_zh.md)
- [Docker hub](https://hub.docker.com/r/fatedier/frp)
