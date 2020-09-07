# Docker Gitlab

## 安装

```yaml
# docker-compose.yml

version: "2"

services:
  gitlab:
    image: "twang2218/gitlab-ce-zh"
    restart: always
    hostname: "gitlab.shuruitech.net"
    environment:
      TZ: "Asia/Shanghai"
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://gitlab.shuruitech.net'
        gitlab_rails['time_zone'] = 'Asia/Shanghai'
    ports:
      - "1080:80"
      - "1443:443"
      - "22:22"
    volumes:
      - gitlab-config:/etc/gitlab
      - gitlab-data:/var/opt/gitlab
      - gitlab-logs:/var/log/gitlab

  gitlab-runner:
    image: "gitlab/gitlab-runner:latest"
    restart: always
    volumes:
      - gitlab-runner-config:/etc/gitlab-runner
      - /var/run/docker.sock:/var/run/docker.sock

volumes:
  gitlab-config:
  gitlab-data:
  gitlab-logs:
  gitlab-runner-config:
```

启动服务：`docker-compose up -d`

停止服务：`docker-compose down`

注册服务：`gitlab-runner register`
