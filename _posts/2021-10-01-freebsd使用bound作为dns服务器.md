\- 安装pkg，shell输入pkg即可安装



\- 安装unbound



  \```

  pkg install unbound

  \```



\- 配置文件  /usr/local/etc/unbound/unbound.conf



\```

\##########################

\# Unbound Configuration

\##########################



\# Server configuration

server:

chroot: /mnt

username: unbound

directory: /mnt

root-hints: /mnt/root.hints

use-syslog: yes

port: 53

verbosity: 1

extended-statistics: no

log-queries: no

hide-identity: no

hide-version: no

harden-referral-path: no

do-ip4: yes

do-ip6: yes

do-udp: yes

do-tcp: yes

do-daemonize: yes

so-reuseport: yes

module-config: "iterator"

cache-max-ttl: 86400

cache-min-ttl: 0

harden-dnssec-stripped: no

serve-expired: yes

outgoing-num-tcp: 50

incoming-num-tcp: 50

num-queries-per-thread: 4096

outgoing-range: 8192

infra-host-ttl: 900

infra-cache-numhosts: 50000

unwanted-reply-threshold: 0

jostle-timeout: 500

msg-cache-size: 512m

rrset-cache-size: 1024m

num-threads: 1

msg-cache-slabs: 2

rrset-cache-slabs: 2

infra-cache-slabs: 2

key-cache-slabs: 2



prefetch: yes

prefetch-key: yes



\# Interface IP(s) to bind to

interface: 127.0.0.1

interface: 0.0.0.0 #本机ip地址

interface: ::1

\# DNS Rebinding

\# For DNS Rebinding prevention

\# All these addresses are either private or should not be routable in the global IPv4 or IPv6 internet.

\# IPv4 Addresses

private-address: 0.0.0.0/8       # Broadcast address

private-address: 10.0.0.0/8

private-address: 100.64.0.0/10

private-address: 127.0.0.0/8     # Loopback Localhost

private-address: 169.254.0.0/16

private-address: 172.16.0.0/12

private-address: 192.0.2.0/24    # Documentation network TEST-NET

private-address: 192.168.0.0/16

private-address: 198.18.0.0/15   # Used for testing inter-network communications

private-address: 198.51.100.0/24 # Documentation network TEST-NET-2

private-address: 203.0.113.0/24  # Documentation network TEST-NET-3

private-address: 233.252.0.0/24  # Documentation network MCAST-TEST-NET

\#

\# IPv6 Addresses

\#

private-address: ::1/128         # Loopback Localhost

private-address: 2001:db8::/32   # Documentation network IPv6

private-address: fc00::/8        # Unique local address (ULA) part of "fc00::/7", not defined yet

private-address: fd00::/8        # Unique local address (ULA) part of "fc00::/7", "/48" prefix group

private-address: fe80::/10       # Link-local address (LLA)



\# Access lists

include: /mnt/access_lists.conf

\# Static host entries

include: /mnt/host_entries.conf

\# DHCP leases (if configured)

include: /mnt/dhcpleases.conf

\# Domain overrides

include: /mnt/domainoverrides.conf

remote-control:

​    control-enable: yes

​    control-interface: 127.0.0.1

​    control-port: 953

​    server-key-file: /mnt/unbound_server.key

​    server-cert-file: /mnt/unbound_server.pem

​    control-key-file: /mnt/unbound_control.key

​    control-cert-file: /mnt/unbound_control.pem

forward-zone:

  name: .

  forward-addr: 223.5.5.5

  forward-addr: 180.76.76.76

  forward-addr: 223.6.6.6

  forward-addr: 114.114.114.114

  forward-addr: 8.8.8.8

  forward-addr: 8.8.4.4



\```



\- 其中涉及的一些外部文件



  https://github.com/mypppv/myconfig/blob/6ab4aa8e250155b55d508c4532c305ebc4c75fc2/unbound_config.zip



  下载之后解压拷贝到 /mnt即可



\- 以下是unbound常见命令



  \```

  unbound               unbound-checkconf     unbound-control-setup

  unbound-anchor        unbound-control       unbound-host

  \```



  



\- 启动unbound 



  \```

  unbound

  \```





\- 设置开机启动



  \```

  ee /etc/rc

  \#增加 

  unbound_enable="YES"

  \```