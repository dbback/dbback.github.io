
目前再用的命令：
```
wget -qO DebianNET.sh qiu.sh/dd && bash DebianNET.sh -dd "https://mirrors.yuntu.ca/teddysun/cn_windows2019.gz"
```
刷写腾讯云特别有效，需要在centos7下刷写

**教程开始**  
安装 Ubuntu 系统

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

### 指定镜像：

bash InstallNET.sh -dd ‘镜像链接’ 或者如下。

**Win8.1  推荐 [腾讯云轻量](https://www.wervps1.com/we/tag/%e8%85%be%e8%ae%af%e4%ba%91%e8%bd%bb%e9%87%8f "[腾讯云轻量]相关的文章")香港、腾讯云轻量北京已测试  其他版本往下看  
**

```
bash <(wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/InstallNET.sh') -dd "http://d1.zizuer.cn/nn/System/DD/win7emb_x86.tar.gz" --mirror 'http://mirrors.ustc.edu.cn/debian/'

```


运行后会进行下载，稍等几分钟去登录 VNC，可以看到有进度条一直 0%，不用管 耐心等待即可 再等个十几分钟就进入系统了

默认用户名：`administrator` 密码：`Vicer`  
登录后修改下默认密码，然后打开磁盘管理，扩展下磁盘   最后激活系统即可  

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
一键 DD 脚本 [https://github.com/veip007/dd](https://www.wervps1.com/goto/wv4630z)















一键 DD 脚本，支持性好，更智能更全面，支持国内外各种 VPS 重装，特别是对国内各种访问国外资源慢的 VPS 安装有奇效。

* * *

安装重装系统的前提组件:  
Debian/Ubuntu:

```
apt-get install -y xz-utils openssl gawk file wget screen && screen -S os

```

RedHat/CentOS:

```
yum install -y xz openssl gawk file glibc-common wget screen && screen -S os

```

如果出现异常，请刷新 Mirrors 缓存或更换镜像源。  
RedHat/CentOS:

```
yum makecache && yum update -y

```

Debian/Ubuntu:

```
apt update -y && apt dist-upgrade -y

```

使用:

```
wget --no-check-certificate -O AutoReinstall.sh https://git.io/betags && chmod a+x AutoReinstall.sh && bash AutoReinstall.sh

```

新版体验：

```
wget --no-check-certificate -O NewReinstall.sh https://git.io/newbetags && chmod a+x NewReinstall.sh && bash NewReinstall.sh

```

如为 CN 主机，可能出现报错或不能下载脚本的问题，可执行以下命令开始安装.

```
wget --no-check-certificate -O AutoReinstall.sh https://cdn.jsdelivr.net/gh/fcurrk/reinstall@master/AutoReinstall.sh && chmod a+x AutoReinstall.sh && bash AutoReinstall.sh

```

新版体验：

```
wget --no-check-certificate -O NewReinstall.sh https://cdn.jsdelivr.net/gh/fcurrk/reinstall@master/NewReinstall.sh && chmod a+x NewReinstall.sh && bash NewReinstall.sh

```

![][img-1]

输入 Y 确认 DD 后主机自动获取 IP，N 则自行设置 IP 输入 N 后会自动检测出主机现用 IP，如果正确可以按 Y 确认使用，如不正确则按 N 自行按正确的输入。

![][img-2]

25 合 1 的系统一键 DD 选择界面，输入 99 则使用自定义镜像。 以上系统密码不为默认密码的均为网络收集，如有疑虑使用自己的自定义镜像。

25 合一系统密码：  
1、CentOS 7.7 (已关闭防火墙及 SELinux，默认密码 Pwd@CentOS)  
2、CentOS 7 (默认密码 cxthhhhh.com)  
3、CentOS 8 (默认密码 cxthhhhh.com)  
4、CentOS 6 (默认密码 Minijer.com)  
5、Debian 11 (默认密码 Minijer.com)  
6、Debian 10 (默认密码 Minijer.com)  
7、Debian 9 (默认密码 Minijer.com)  
8、Debian 8 (默认密码 Minijer.com)  
9、Ubuntu 20.04 (默认密码 Minijer.com)  
10、Ubuntu 18.04 (默认密码 Minijer.com)  
11、Ubuntu 16.04 (默认密码 Minijer.com)  
12、Windows Server 2019 (默认密码 cxthhhhh.com)  
13、Windows Server 2016 (默认密码 cxthhhhh.com)  
14、Windows Server 2012 (默认密码 cxthhhhh.com)  
15、Windows Server 2012 Lite (默认密码 nat.ee)  
16、Windows Server 2008 (默认密码 cxthhhhh.com)  
17、Windows Server 2008 Lite (默认密码 nat.ee)  
18、Windows Server 2003 (默认密码 cxthhhhh.com)  
19、Windows Server 2003 Lite (默认密码 WinSrv2003x86-Chinese)  
20、Windows 10 LTSC Lite (默认密码 www.nat.ee)  
21、Windows 7 x86 Lite (默认密码 Windows7x86-Chinese)  
22、Windows 7 Ent Lite (默认密码 nat.ee)  
23、Windows 7 Ent Lite (UEFI 支持甲骨文)(默认密码 nat.ee)  
24、Windows Server 2008 Lite (UEFI 支持甲骨文)(默认密码 nat.ee)  
25、Windows Server 2012 Lite (UEFI 支持甲骨文)(默认密码 nat.ee)  
99、自定义镜像

* * *


