1、安装时选择上SSH，或者源码安装SSH

2、使用root登陆系统（初始无密码）

4、编辑/etc/rc.conf，添加一行sshd_enable="YES"

5、编辑/etc/ssh/sshd_config，将

\#PermitRootLogin no改为PermitRootLogin yes //允许root登陆

\#PasswordAuthentication no改为PasswordAuthenticationyes//使用系统PAM认证

\#PermitEmptyPasswords no改为PermitEmptyPasswords no//不允许空密码



修改端口号：/etc/ssh/sshd_config



\#**port=22改为 Port=number（你想修改的数字）**



保存退出

6、启动SSHD服务，/etc/rc.d/sshd onestart

7、查看服务是否启动，netstat -an，如果看到22端口有监听，恭喜！！！