# Docker

## 安装

```shell
sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo docker run hello-world
```

or

```shell
sudo apt install docker.io
```

## 卸载

```shell
sudo apt-get purge docker-ce docker-ce-cli containerd.io

sudo rm -rf /var/lib/docker
```

or

```shell
sudo apt-get purge docker.io
```

## 换源

`vim /etc/docker/daemon.json`

```json
{
    "registry-mirrors": [
        "https://mirror.css.tencentyun.com"
    ]
}
```

```shell
$ systemctl daemon-reload

$ service docker restart

$ docker info

Registry Mirrors:
 https://mirror.ccs.tencentyun.com

```

## 权限

```shell
sudo groupadd docker

sudo usermod -aG docker $USER

newgrp docker 
```

## 使用

