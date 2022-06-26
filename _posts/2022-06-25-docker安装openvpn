


https://hub.docker.com/r/kylemanna/openvpn/

快速开始
$OVPN_DATA为数据卷容器选择一个名称。建议使用ovpn-data-前缀与参考 systemd 服务无缝操作。鼓励用户example用他们选择的描述性名称替换。

OVPN_DATA="ovpn-data-example"
初始化$OVPN_DATA将保存配置文件和证书的容器。容器将提示输入密码以保护新生成的证书颁发机构使用的私钥。

docker volume create --name $OVPN_DATA
docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_genconfig -u udp://VPN.SERVERNAME.COM
docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn ovpn_initpki
启动 OpenVPN 服务器进程

docker run -v $OVPN_DATA:/etc/openvpn -d -p 1194:1194/udp --cap-add=NET_ADMIN kylemanna/openvpn
生成没有密码的客户端证书

docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn easyrsa build-client-full CLIENTNAME nopass
使用嵌入式证书检索客户端配置

docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn
下一步
更多阅读
docs文件夹中提供了有关高级配置的其他 文章。

Systemd 初始化脚本
一个systemd初始化脚本可用于管理 OpenVPN 容器。它将在系统启动时启动容器，如果容器意外退出，则重新启动容器，并从 Docker Hub 拉取更新以使其保持最新状态。

请参阅systemd 文档以了解更多信息。

码头工人撰写
如果您更喜欢使用，docker-compose请参阅文档。

调试技巧
创建一个名为 DEBUG 且值为 1 的环境变量以启用调试输出（使用“docker -e”）。

  docker run -v $OVPN_DATA:/etc/openvpn -p 1194:1194/udp --cap-add=NET_ADMIN -e DEBUG=1 kylemanna/openvpn
使用正确安装了 openvpn 的客户端进行测试

  $ openvpn --config CLIENTNAME.ovpn
如果事情不能正常工作，请在客户端上运行一连串的调试检查

  $ ping 8.8.8.8    # checks connectivity without touching name resolution
  $ dig google.com  # won't use the search directives in resolv.conf
  $ nslookup google.com # will use search
