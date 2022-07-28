
- 安卓手机设置


1. 没有root :


连上电脑，安装adb套件


```
adb tcpip 5555

```


2. root :
3. 

下载 adb wireless 通过、google应用商店


- PC端


下载 https://github.com/Genymobile/scrcpy/blob/master/README.zh-Hans.md


直接运行如下命令

```
scrcpy  -S  --tcpip=192.168.15.172:5555 --display-buffer=20  # ip地址根据实际情况修改

```

-IOS端

通过应用商店下载scrcpy remote

默认浏览器以下链接

scrcpy2://adb

打开软件，输入ip，端口5555，可以进行连接。bitrate可以设置为 4M ，FPS默认可以 
