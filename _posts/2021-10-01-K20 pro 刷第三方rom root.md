1.下载第三方rom，下列为已知的



​    https://download.pixelexperience.org/raphael



​     https://t.me/redmik20proupdates



2.解压platform-tool  



3.cmd命令进入rec，命令如下



```
fastboot boot recovery.img
```

\4. 通过rec格式化所有分区，此时由于TWRP本身分区格式有问题，需要进入k20pro的rec格式化分区，然后再进入twrp挂载data分区，

\5. 拷贝rom到手机，安装rom



6、下载最新Magisk



  https://github.com/topjohnwu/Magisk/releases 



7、[Magisk-v23.0.apk](https://github.com/topjohnwu/Magisk/releases/download/v23.0/Magisk-v23.0.apk) 更改为 Magisk-v23.0.zip ；其它版本方法一样，把apk后缀更改而已



8、再次使用twrp 临时启动，刷入Magisk-v23.0.zip



9、进入手机，打开Magisk，安装更新，安装到rec，直接安装，即可获取root权限