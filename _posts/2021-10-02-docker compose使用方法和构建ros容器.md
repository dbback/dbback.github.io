1、构建docker-compose 方法如下：

```
1、新建一个文件夹

2、文件夹下touch一个文件 docker-compose.yml

3、输入内容

4、docker-compose up -d
```

2、docker-compose常见命令

```
1. docker-compose up -d 启动；
2. docker-compose logs 打印日志；
3. docker-compose pull 更新镜像；
4. docker-compose stop 停止容器；
5. docker-compose restart 重启容器；
6. docker-compose down 停止并删除容器；
```

安装 centos

```
yum install docker
yum install docker-compose
```



routeros docker ，构建如下：

```
version: "3.3"

services:

  ros:
    image: cnblogme/routeros:latest
    container_name: ros
    restart: always
    ports:
      - "121:21"
      - "122:22"
      - "123:23"
      - "150:50"
      - "151:51"
      - "80:80"
      - "443:443"
      - "1500:500"
      - "1194:1194"
      - "11701:1701"
      - "11723:1723"
      - "14500:4500"
      - "5900:5900"
      - "8080:8080"
      - "8291:8291"
      - "8728:8728"
      - "8729:8729"
      - "1111:1111"
      - "2222:2222"
      - "3333:3333"
      - "5555:5555"
      - "6666:6666"
      - "7777:7777"
      - "8888:8888"
      - "9999:9999"
    environment:
      - "VNCPASSWORD=false"
    network_mode: bridge
    privileged: true


  winbox:
    image11 cnblogme/novnc-winbox
    container_name: winbox
    hostname: winbox
    restart: always
    #volumes:
    #  - ./user-data/.wine:/home/alpine/.wine
    links:
      - "ros"
    ports:
      - "5901:5900"
      - "18081:8080"
    network_mode: bridge
```

