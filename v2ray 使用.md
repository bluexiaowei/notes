# v2ray 使用

## 安装

**Linux 脚本安装**

```bash
$ bash <(curl -L -s https://install.direct/go.sh)
```

## 配置文件

### 服务端

配置文件地址：`/etc/v2ray/config.json`

```json
{
  "log": { // 日志
    "loglevel": "warning",
    "access": "/var/log/v2ray/access.log", 
    "error": "/var/log/v2ray/error.log"
  },
  "inbounds": [
    { // wmess 协议
      "port": 10086,
      "protocol": "vmess",
      "settings": {
        "clients": [{ "id": "b831381d-6324-4d53-ad4f-8cda48b30811" }]
      }
    },
    { // shadowsocks 协议 可选
      "port": 1024,
      "protocol": "shadowsocks",
      "settings": {
        "method": "chacha20-poly1305",
        "password": "sspasswd"
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```

**mkcp** 配置

```json
{
  "port": 10086, // 服务器监听端口，必须和上面的一样
  "protocol": "vmess",
  "settings": {
    "clients": [{ "id": "b831381d-6324-4d53-ad4f-8cda48b30811" }]
  },
  "streamSettings": {
    "network": "mkcp", //此处的 mkcp 也可写成 kcp，两种写法是起同样的效果
    "kcpSettings": {
        "uplinkCapacity": 5, // 上行链路容量，将决定 V2Ray 向外发送数据包的速率。单位为 MB
        "downlinkCapacity": 100, // 下行链路容量，将决定 V2Ray 接收数据包的速率。单位同样是 MB
        "congestion": true,
        "header": { // 对于数据包的伪装
          "type": "none" //  utp、srtp、wechat-video、dtls、wireguard
        }
    }
  }
},
```

## 命令行



## 资料

* [v2ray 官网](https://www.v2ray.com)
* [中文教程](https://toutyrater.github.io)