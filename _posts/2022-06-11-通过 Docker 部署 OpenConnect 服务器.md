> 什么是 OpenConnect ServerOpenConnect server (ocserv) 是一个基于 SSL 的 VPN 服务器。

[](#什么是-OpenConnect-Server "什么是 OpenConnect Server")什么是 OpenConnect Server
--------------------------------------------------------------------------

[OpenConnect server (ocserv)](https://www.infradead.org/ocserv/) 是一个基于 SSL 的 VPN 服务器。它是基于 OpenConnect SSL VPN 协议实现的，同时（实验性质）兼容使用 [Cisco AnyConnect SSL VPN](https://www.cisco.com/c/en/us/support/security/anyconnect-vpn-client/tsd-products-support-series-home.html) 协议的客户端。

[](#如何部署服务器 "如何部署服务器")如何部署服务器
-----------------------------

考虑到架设 OpenConnect Server 对于大多数用户来说比较困难，所以我制作了一个 Docker 镜像。以下所有教程都是基于该 Docker 镜像的。如果你不知道什么是 Docker，请先访问 Docker 的网站了解相关信息。如果你对镜像文件不放心，可以在以下地址找到该镜像的原始 Dockerfile 和相关信息：[Docker Hub](https://registry.hub.docker.com/u/tommylau/ocserv/)，[GitHub](https://github.com/TommyLau/docker-ocserv)

### [](#开始前的准备工作 "开始前的准备工作")开始前的准备工作

*   知道并了解 [Docker](https://www.docker.com/) 的运行原理和机制
*   掌握基本的服务器架设能力，熟悉 Linux 命令，并且在服务器上成功部署了 Docker
*   如果你使用的是 VPS 的话，请联系 ISP 确认是否支持 TUN 设备

### [](#OpenConnect-Server-的安装 "OpenConnect Server 的安装")OpenConnect Server 的安装

一条如此简单的命令，就可以把 OpenConnect Server (ocserv) 安装到你的服务器了：

```
docker pull tommylau/ocserv
```

使用下面的命令，就可以马上运行 ocserv 来体验了：

```
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -d tommylau/ocserv
```

上述命令会创建并运行一个新的 container，同时会添加一个用户名和密码均为 `test` 的用户。如果你只需要临时使用一下，不关心安全问题的话，那么看到这里就可以结束了。如果你需要更多的设置，请继续阅读。

[](#用户操作 "用户操作")用户操作
--------------------

所有的用户操作必须在实例运行的时候才可以进行。如果你的 Docker 实例名不是 `ocserv` 的话，请根据实际情况自行调整。

### [](#添加用户 "添加用户")添加用户

假如说，你想创建一个名为 `tommy` 的用户，使用如下命令

```
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd tommy
Enter password:
Re-enter password:
```

当提示输入密码的时候，输入两次密码，便可创建该用户。

### [](#删除用户 "删除用户")删除用户

删除用户与添加用户类似，唯一的区别就是在用户名前面增加 `-d` 参数

```
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -d test
```

如果你在创建实例的时候，没有使用环境变量 `NO_TEST_USER`，那么上述命令将帮你删除默认的 `test` 用户。

### [](#修改密码 "修改密码")修改密码

修改密码与添加用户的操作是完全一致的，请参考上面添加用户的章节。

[](#高级使用 "高级使用")高级使用
--------------------

这个部分会介绍一些高级的使用方法，包括通过环境变量的设置来配置不同的 CA 名称等。

### [](#环境变量 "环境变量")环境变量

对于 `tommylau/ocserv` 这个 Docker 镜像来说，所有的环境变量都是可选的，也就意味着你拥有一个开箱即用的产品，而不用输入任何参数。当然，如果你是一个定制狂或者有强迫症，那么下面就是为你准备的。

`CA_CN`，这是用于生成 CA(Certificate Authority) 证书的名称 (common name)。

`CA_ORG`，这是用于生成 CA 证书的组织名称 (organization name)。

`CA_DAYS`，这是用于生成 CA 证书的有效期。

`SRV_CN`，这是用于生成服务器证书的名称 (common name)。

`SRV_ORG`，这是用于生成服务器证书的组织名称 (organization name)。

`SRV_DAYS`，这是用于生成服务器证书的有效期。

`NO_TEST_USER`，当这个变量设置为非空时，将不会创建 `test` 用户。你必须要手动添加你自己的用户，并设置密码。默认情况下，系统会自动创建用户名为 `test`，密码也为 `test` 的用户。

上述变量的默认值：

<table><thead><tr><th>变量</th><th>默认值</th></tr></thead><tbody><tr><td><strong>CA_CN</strong></td><td>VPN CA</td></tr><tr><td><strong>CA_ORG</strong></td><td>Big Corp</td></tr><tr><td><strong>CA_DAYS</strong></td><td>9999</td></tr><tr><td><strong>SRV_CN</strong></td><td><a target="_blank" rel="noopener" href="http://www.example.com/">www.example.com</a></td></tr><tr><td><strong>SRV_ORG</strong></td><td>My Company</td></tr><tr><td><strong>SRV_DAYS</strong></td><td>9999</td></tr></tbody></table>

### [](#一些运行范例 "一些运行范例")一些运行范例

使用开箱即用的方式，用户名和密码均为 `test`

```
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -d tommylau/ocserv
```

创建服务器名为 `my.test.com`，组织为 `My Test`，有效期为 `365` 天的实例

```
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -e SRV_CN=my.test.com -e SRV_ORG="My Test" -e SRV_DAYS=365 -d tommylau/ocserv
```

创建一个签发机构为 `My CA`，签发组织为 `My Corp`，有效期为 `3650` 天的实例

```
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -e CA_CN="My CA" -e CA_ORG="My Corp" -e CA_DAYS=3650 -d tommylau/ocserv
```

一个包含 CA 和服务器证书的，完全定制化的实例

```
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -e CA_CN="My CA" -e CA_ORG="My Corp" -e CA_DAYS=3650 -e SRV_CN=my.test.com -e SRV_ORG="My Test" -e SRV_DAYS=365 -d tommylau/ocserv
```

如上述的完全定制化的实例，但是不创建 `test` 用户

```
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -e CA_CN="My CA" -e CA_ORG="My Corp" -e CA_DAYS=3650 -e SRV_CN=my.test.com -e SRV_ORG="My Test" -e SRV_DAYS=365 -e NO_TEST_USER=1 -v /some/path/to/ocpasswd:/etc/ocserv/ocpasswd -d tommylau/ocserv
```

**警告：**ocserv 在启动的时候需要 ocpasswd 文件，如果你设置了 `NO_TEST_USER=1`，ocpasswd 文件将不会被创建，进而导致到服务器启动后立即停止。你必须要像上面示例中那样，使用 Docker 的 `-v` 挂在参数，指定一个 ocpasswd 文件到 `/etc/ocserv/ocpasswd`。
