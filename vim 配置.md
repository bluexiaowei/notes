# vim 配置

## 配置文件

* 全局配置 `/etc/vim/vimrc` 或者 `/etc/vimrc`
* 个人配置 `~/.vimrc`

## 资料

* [开源一键配置 spf13-vim](https://github.com/spf13/spf13-vim)

acme.sh --install-cert -d u7231.top \
--key-file       /etc/nginx/certificate/u7231.top.key  \
--fullchain-file /etc/nginx/certificate/u7231.top.pem \
--reloadcmd     "service nginx force-reload"