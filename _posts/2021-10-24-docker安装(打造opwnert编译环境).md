安装容器，配置容器
apk add docker
service docker start
rc-update add docker 
docker pull ubuntu
docker run -itd -p 80:80 -p 2222:22 --name myubuntu ubuntu /bin/bash 

#docker run -itd -p 80:80 -p 2222:22 -p 443:443  -p 8080:8080 --name myubuntu ubuntu /bin/bash 
docker restart db4c611a2ec4
docker exec -it db4c611a2ec4 /bin/bash
下次进入容器方法
docker restart a13b54439940 
docker exec -it a13b54439940 /bin/bash


设置主机ip网关 10.0.0.3 （代理） setup-alpine    
设置dns  setup-dns   8.8.8.8


查看ubuntu版本 lsb_release -a


安装 ifconfig和ping
apt-get install net-tools
apt-get install iputils-ping
apt-get install nano
apt-get install traceroute

-------------------------
检查科学上网
traceroute www.google.com
ping www.google.com
测试成功，说明科学上网
---------------------------



换源：
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

apt-get update




创建新用户 adduser git
切换到git   :  su git