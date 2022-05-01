 一键设置网卡ip地址





```
netsh interface ip set address "eth0" static 10.0.0.158 255.255.255.0 10.0.0.3

netsh interface ip set dns "eth0" static 10.0.0.3

pause
```





如下图，网卡名称手动改成了"eth0"

![](file://C:/Users/root/Documents/Gridea/post-images/1630136293101.png)

一键设置自动获取ip和dns





```
netsh interface ip set address "eth0"  dhcp

netsh interface ip set dns name="eth0" source=dhcp

pause
```



 升级版脚本,可以自动判断并设置ip地址



```
@echo off

netsh interface ip  show dnsservers | findstr 10.0.0.3

if %errorlevel% NEQ 1 GOTO set_ip_dhcp

:set_ip_static_addr

netsh interface ip set address "eth0" static 10.0.0.158 255.255.255.0 10.0.0.3

netsh interface ip set dns "eth0" static 10.0.0.3

cls

echo "设置了静态ip地址"

pause

exit

:set_ip_dhcp

netsh interface ip set address "eth0"  dhcp

netsh interface ip set dns name="eth0" source=dhcp

cls

echo "取消了静态ip地址"

pause

exit
```

