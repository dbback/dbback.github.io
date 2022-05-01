## 整体配置流程：

| ①部署alpine linux环境 |
| :-------------------- |
| ②安装、配置docker |
| ③配置ubuntu容器   |
| ④编译openwrt      |


### 1、部署alpine linux环境

​		通过Vmware部署，[部署alpine linux](https://lpvs.com/How-to-install-Awall-on-Alpine-Linux/) ，其中需要设置科学上网如下：

- 设置主机ip网关 10.0.0.3 （代理） setup-interfaces （修改eth0的ip）    
- 设置dns  setup-dns   8.8.8.8

### 2、安装、配置docker 

```bash
apk add docker
service docker start
rc-update add docker 
docker pull ubuntu
docker run -itd -p 80:80 -p 2222:22 --name myubuntu ubuntu /bin/bash 
docker restart a13b54439940 
docker exec -it a13b54439940 /bin/bash
```

​	下次进入容器方法：	

```
docker restart a13b54439940 
docker exec -it a13b54439940 /bin/bash
```

### 3、配置ubuntu容器

部署alpine linux环境→ 安装docker → 配置ubuntu容器→ 进入容器设置ubuntu→ 编译openwrt

- 换源：修改/etc/apt/sources.list，然后apt-get update

  

```c#
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
```

- 查看ubuntu版本 lsb_release -a

- 安装 ifconfig和ping：

  

  ```bash
  apt-get install net-tools
  apt-get install iputils-ping
  apt-get install nano
  apt-get install traceroute
  ```

- 检查科学上网

  

```
traceroute www.google.com
ping www.google.com
测试成功，说明科学上网
```

- 创建普通新用户    adduser git
- 设置密码：passwd root    还有     passwd git
- 切换到git   :   su git

### 4、编译openwrt

​	具体教程参见 [lean openwrt](https://github.com/coolsnowwolf/lede)





