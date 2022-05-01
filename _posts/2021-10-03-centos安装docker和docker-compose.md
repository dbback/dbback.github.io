安装docker

```
yum install docker
systemctl start docker
systemctl enable docker
```

安装docker-compose

```
# 下载最新版本的 docker-compose 到 /usr/bin 目录下
curl -L https://github.com/docker/compose/releases/download/1.23.2/docker-compose-`uname -s`-`uname -m` -o /usr/bin/docker-compose

# 给 docker-compose 授权
chmod +x /usr/bin/docker-compose
```

