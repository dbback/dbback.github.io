前言今年是一个不同寻常的开年，相信每个人身上都发生了很多变化，所以博主琐事缠身博客更新没跟上，望谅解。回归正题，最近有朋友问 Mark 一些构建 Docker 方面的问题，自然说到镜像优化方面的...

前言
--

今年是一个不同寻常的开年，相信每个人身上都发生了很多变化，所以博主琐事缠身博客更新没跟上，望谅解。  
回归正题，最近有朋友问 Mark 一些构建 Docker 方面的问题，自然说到镜像优化方面的东西，索性就聊一下 `Alpine` 。

* * *

介绍
--

Alpine Linux 是一款独立的、非商业的通用 Linux 发行版，专为追求安全性、简单性和资源效率的用户而设计。  
可能很多人没听说过这个 Linux 发行版本，但是经常用 `Docker` 的朋友可能都用过，因为他因 小，简单，安全而著称，所以作为基础镜像是非常好的一个选择，可谓是麻雀虽小但五脏俱全，简直不要太方便, 镜像非常小巧，不到 `6M` 的大小，所以特别适合容器打包。

* * *

容器体验 Alpine
-----------

使用命令

```
docker run -it alpine /bin/sh

```

可运行 Alpine Linux，由于 Alpine Linux 没有内置`bash`，所以这里使用的`sh`作为伪终端，在为 Alpine Linux 编写 shell 脚本的时候也需要注意，使用 `sh` 而不是`bash`。

* * *

软件管理
----

Alpine Linux 使用`apk`指令来管理软件，类似 CentOS 的`yum`或 Debian 的`apt-get`，首次使用建议用`apk update`更新下软件，以免无法正常使用。apk 的常用指令如下：

```
#更新软件
apk update
#搜索某个软件
apk search xxx
#安装软件
apk add xxx
#卸载软件
apk del xxx
#查看使用帮助
apk -h

```

* * *

设置时区
----

Alpine 时区非东八区，某些项目需要和北京时间保持同步，因此我们需要对默认时区做出修改，方法如下：

```
#安装timezone
apk add -U tzdata
#查看时区列表
ls /usr/share/zoneinfo
#拷贝需要的时区文件到localtime
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
#查看当前时间
date
#为了精简镜像，可以将 tzdata 删除了
apk del tzdata

```

* * *

修改软件源
-----

如果是国内网络使用 Alpine，可以使用国内镜像源，这样速度更加理想，常用的国内镜像源如下：

*   清华 TUNA 镜像源：[https://mirrors.tuna.tsinghua.edu.cn/alpine/](https://mirrors.tuna.tsinghua.edu.cn/alpine/)
*   中科大镜像源：[http://mirrors.ustc.edu.cn/alpine/](http://mirrors.ustc.edu.cn/alpine/)
*   阿里云镜像源：[http://mirrors.aliyun.com/alpine/](http://mirrors.aliyun.com/alpine/)

软件源的配置文件位于`/etc/apk/repositories`，内容如下：

```
http://dl-cdn.alpinelinux.org/alpine/v3.11/main
http://dl-cdn.alpinelinux.org/alpine/v3.11/community

```

可以看到这里使用的 Alpine 软件源版本为`v3.11`，所以我们在修改的时候需要版本保持一致，比如修改为阿里的软件源：

```
http://mirrors.aliyun.com/alpine/v3.11/main
http://mirrors.aliyun.com/alpine/v3.11/community

```

更多软件源可参考官方列表：[](https://mirrors.alpinelinux.org/)[https://mirrors.alpinelinux.org/](https://mirrors.alpinelinux.org/)

* * *

结语
--

Alpine 官方网站：[https://www.alpinelinux.org](https://www.alpinelinux.org/)  
Alpine PKGS：[https://pkgs.alpinelinux.org/packages](https://pkgs.alpinelinux.org/packages)  
Alpine Linux 体积非常小巧，但功能不输其它 Linux 发行版，非常适合用来打包 Docker 镜像，在 DockerHub 搜索镜像的时候您会发现很多都是基于 Alpine Linux，简直就是天生为容器所准备。

