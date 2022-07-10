




**教程开始**  
安装 Ubuntu 系统

[![][img-0]

root权限安装必须软件包

```
#Debian/Ubuntu:
apt update -y 
apt-get install -y xz-utils openssl gawk file

#RedHat/CentOS:
yum update -y
yum install -y xz openssl gawk file

```



### 一键脚本：

```
##镜像文件在OneDrive
wget -N --no-check-certificate https://raw.githubusercontent.com/veip007/dd/master/dd-od.sh && chmod +x dd-od.sh && ./dd-od.sh

##镜像文件在GoogleDrive
wget -N --no-check-certificate https://raw.githubusercontent.com/veip007/dd/master/dd-gd.sh && chmod +x dd-gd.sh && ./dd-gd.sh

```

运行后会告诉你相关的网络信息（IP、网关、子网掩码），记录一下，或者不要关闭 ssh，并列出可以使用的镜像包。

### 指定镜像：

自定义安装请使用：bash InstallNET.sh -dd ‘您的直连’ 或者如下。

**Win8.1  推荐 [腾讯云轻量](https://www.wervps1.com/we/tag/%e8%85%be%e8%ae%af%e4%ba%91%e8%bd%bb%e9%87%8f "[腾讯云轻量]相关的文章")香港、腾讯云轻量北京已测试  其他版本往下看  
**

```
bash <(wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/InstallNET.sh') -dd "http://d1.zizuer.cn/nn/System/DD/win7emb_x86.tar.gz" --mirror 'http://mirrors.ustc.edu.cn/debian/'

```

[![][img-2]

运行后会进行下载，稍等几分钟去登录 VNC，可以看到有进度条一直 0%，不用管 耐心等待即可 再等个十几分钟就进入系统了

默认用户名：`administrator` 密码：`Vicer`  
登录后修改下默认密码，然后打开磁盘管理，扩展下磁盘   最后激活系统即可  
[![][img-3]  
[![][img-4]

 **其他镜像**把下载地址 替换到 DD 代码里面的系统地址即可  
国内的是博主网盘分流 国外的萌咖大佬的谷歌网盘  
默认密码都是`Vicer`

```
Windows 7 32位中文Thin PC
国内：http://d1.zizuer.cn/nn/System/DD/win7emb_x86.tar.gz
国外：https://image.moeclub.org/GoogleDrive/1srhylymTjYS-Ky8uLw4R6LCWfAo1F3s7
 
Windows 8.1 SP1 64位
国内：http://d1.zizuer.cn/nn/System/DD/win8.1emb_x64.tar.gz
国外：https://image.moeclub.org/GoogleDrive/1cqVl2wSGx92UTdhOxU9pW3wJgmvZMT_J

```

```
# Windows 10 ltsc 64位
国内：http://d1.zizuer.cn/nn/System/DD/win10ltsc_x64.tar.gz
国外：https://image.moeclub.org/GoogleDrive/1OVA3t-ZI2arkM4E4gKvofcBN9aoVdneh
```

```
Windows Server 2008 SP1 R2 64位
用户名：Administrator 密码：WinSrv2008x64-Chinese
国内：http://d1.zizuer.cn/nn/System/DD/WinSrv2008x64-Chinese.vhd.gz
国外：http://soft.815494.com/dd/WinSrv2008x64-Chinese.vhd.gz

```

用户名：`administrator`密码：`Password147`

```
# Windows Server 2012 R2中文版：
国内：http://d1.zizuer.cn/nn/System/DD/cn_windows2012r2.gz
国外：https://mirrors.yuntu.ca/teddysun/cn_windows2012r2.gz

# Windows Server 2016中文版：
国内：http://d1.zizuer.cn/nn/System/DD/cn_windows2016.gz
国外：https://mirrors.yuntu.ca/teddysun/cn_windows2016.gz

# Windows Server 2019中文版
国内：http://d1.zizuer.cn/nn/System/DD/cn_windows2019.gz
国外：https://mirrors.yuntu.ca/teddysun/cn_windows2019.gz

```

**相关资料**  
萌咖大佬的一键 DD 脚本 [https://github.com/veip007/dd](https://www.wervps1.com/goto/wv4630z)
