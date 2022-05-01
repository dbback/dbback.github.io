#### 1、期待路由器达到什么程度

（1）作为主路由网关，处理其他主机的数据转发

（2）可以进行pppoe拨号

（3）通过iptables，使其具有ros防火墙的一些特性

（4）具有DNS缓存功能，作为dns服务器，暂时选择方案为smartdns

（5）dhcp服务，为局域网主机分配ip地址

（6）BBR加速功能，针对tcp请求进行加速

#### 2、准备alpine linux 镜像

​	下载 [alpine linux镜像](https://raw.githubusercontent.com/mypppv/images/master/2021/2021-10/alpine%20linux.zip)，下载完成后使用VMware启动。需要注意的是部署到EXSI时，需要转换兼容对用版本。也可以自己到官网下载镜像ISO安装。账号root，密码0

#### 3、设置ip地址

​	下载 [alpine linux镜像](https://raw.githubusercontent.com/mypppv/images/master/2021/2021-10/alpine%20linux.zip)，下载完成后使用VMware启动。需要注意的是部署到EXSI时，需要转换兼容对用版本。也可以自己到官网下载镜像ISO安装。账号root，密码0

#### 

#### 4、设置iptables

#### 5、设置DNS服务器

#### 6、设置DHCP服务器

#### 7、开启BBR

​	从 Linux 4.9 版本开始，TCP BBR 就已经成为了 Linux 系统内核的一部分。因此，开启 BBR 的首要前提就是当前系统内核版本大于等于 4.9。

​	查看当前内核版本：

```
uname -r
```

只有返回的值大于等于 4.9 时才可以进行下一步操作，否则需要先手动将内核版本升级至 4.9 以上（这里不再赘述）

#####  7.1开启 BBR

整个开启过程其实很简单，在特定文件中写入几行配置就行了。

##### 7.2 修改系统配置

使用 `echo` 写入配置：

```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
```

##### 7.3 保存生效

修改完之后需要保存才能生效：

```
sysctl -p
```

##### 7.4 验证开启状态

操作完后最好验证一下 BBR 是否正常开启并启动。

##### 7.5查看内核开启情况

```
sysctl net.ipv4.tcp_available_congestion_control
```

显示内容如下，包含含“bbr”字样则 BBR 已正常开启

```
# sysctl net.ipv4.tcp_available_congestion_control
net.ipv4.tcp_available_congestion_control = bbr cubic reno
```

##### 7.6查看 BBR 是否启动

```
lsmod | grep bbr
```

显示如下则已启动成功（后面的数字不一定跟我这里一样）

```
# lsmod | grep bbr
tcp_bbr                20480  14
```