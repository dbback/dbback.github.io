




https://hub.docker.com/r/kylemanna/openvpn/

快速开始
$OVPN_DATA为数据卷容器选择一个名称。建议使用ovpn-data-前缀与参考 systemd 服务无缝操作。鼓励用户example用他们选择的描述性名称替换。

```
OVPN_DATA="ovpn-data-example"
```

初始化$OVPN_DATA将保存配置文件和证书的容器。容器将提示输入密码以保护新生成的证书颁发机构使用的私钥。

```
docker volume create --name $OVPN_DATA
docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_genconfig -u udp://VPN.SERVERNAME.COM
docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn ovpn_initpki
```

启动 OpenVPN 服务器进程

```
docker run -v $OVPN_DATA:/etc/openvpn -d -p 1194:1194/udp --cap-add=NET_ADMIN kylemanna/openvpn
```
生成没有密码的客户端证书

```
docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn easyrsa build-client-full CLIENTNAME nopass
```
使用嵌入式证书检索客户端配置

```
docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn
```
