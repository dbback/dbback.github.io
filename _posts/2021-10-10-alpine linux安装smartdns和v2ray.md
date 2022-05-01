#### 1、预期目的

操作系统：alpine linux

目的：针对操作系统提供DNS服务和BBR加速，提供socks代理（1080端口）

想法：dns服务器采用smartdns，bbr通过内核开启即可，其它电脑通过此电脑作为网关，进行上网活动

#### 2、smartdns

##### 2.1 安装

软件下载地址 ：[smartdns](https://github.com/pymumu/smartdns/releases)，下载linux版本的（x86_64）

```
cd
wget https://github.com/pymumu/smartdns/releases/download/Release35/smartdns-x86_64
mv ./smartdns-x86_64 ./smartdns
chmod +x ./smartdns
mv ./smartdns /sbin
```

##### 2.2  配置

配置文件在这里： [配置文件](https://github.com/pymumu/smartdns/blob/master/etc/smartdns/smartdns.conf) ，主要修改点如下：

```
server-name smartdns
cache-size 8000
cache-persist yes
cache-file /tmp/smartdns.cache
speed-check-mode ping,tcp:80
server 223.5.5.5:53
server 114.114.114.114:53
server 119.29.29.29:53
server 8.8.8.8:53
server 180.76.76.76:53

```

##### 2.3 运行及开机启动

```
smartdns -f -c /etc/smartdns/smartdns.conf
```

开机启动，把上述命令加入 /etc/local.d/startup.start

```
bbr:~# cat /etc/local.d/startup.start

#!/bin/bash
sudo nohup /root/v2ray/v2ray &
sudo smartdns -f  -c /etc/smartdns/smartdns.conf
```



#### 3、安装BBR

[设置alpine linux BBR](https://lpvs.com/Alpine-linux-%E5%81%9A%E8%B7%AF%E7%94%B1%E5%99%A8-%E5%BC%80%E5%90%AFBBR/)

#### 3、v2ray

##### 3.1  安装

```
smartdns -f -c /etc/smartdns/smartdns.conf
```

[下载地址](https://github.com/v2fly/v2ray-core/releases/tag/v4.31.0)

```
cd
wget https://github.com/v2fly/v2ray-core/releases/download/v4.31.0/v2ray-linux-64.zip
mkdir v2ray
mv ./v2ray-linux-64.zip ./v2ray
cd ./v2ray
unzip  v2ray-linux-64.zip 
rm v2ray-linux-64.zip
```

##### 3.2 配置

```
cat /root/v2rayconfig.json #配置文件内容如下：
```

```
{
  "outbounds": [
    {
      "protocol": "freedom",
      "tag": "direct"
    },
    {
      "protocol": "blackhole",
      "tag": "blocked"
    }
  ],
  "log": {
    "loglevel": "warning"
  },
  "routing": {
    "rules": [
      {
        "type": "field",
        "outboundTag": "direct",
        "ip": [
          "10.0.0.0\/8",
          "172.16.0.0\/12",
          "192.168.0.0\/16"
        ]
      }
    ],
    "domainStrategy": "IPOnDemand"
  },
  "inbounds": [
    {
      "port": 1080,
      "protocol": "socks",
      "streamSettings": {
        "network": "tcp",
        "tcpSettings": {
          "header": {
            "type": "none"
          }
        },
        "security": "none"
      },
      "settings": {
        "auth": "noauth"
      }
    }
  ]

```

##### 3.3  开机启动

```
bbr:~# cat /etc/local.d/startup.start

#!/bin/bash
sudo nohup /root/v2ray/v2ray &
sudo smartdns -f  -c /etc/smartdns/smartdns.conf
```

#### 4、开启数据转发

```
# /etc/sysctl.d 目录下新建一个 *.conf文件
bbr:~/v2ray# cat /etc/sysctl.d/aa.conf
net.ipv4.ip_forward=1
reboot #需要重新启动
```

#### 4、设置此主机位网关

​	需要在routeros命令行设置，登录10.0.0.1

```
/ip dhcp-server network set numbers=0 gateway=10.0.0.8 #假设此主机为10.0.0.8
```

