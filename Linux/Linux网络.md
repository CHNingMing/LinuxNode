# Route 

路由

所在包:net-tools

所有路由操作默认都是临时生效的.重启/注销 恢复

除非设置保存在/etc/sysconfig/static-routes文件中,默认linux没有这个文件,需要手工创建.

## 列出linux路由表

### ip route 

列出路由详细配置信息

### netstat -nr

列出路由详细网络信息

#### 相关标记:

U : 路由是活动的		[√]

H : 目标是一个主机	[√]

G : 路由指向网关

R : 恢复动态路由产生的表项

D : 由路由后台程序动态安装

M : 有路由后台程序修改

! : 拒绝路由

## 设置默认路由

```
ip route replace default dev 网卡
```

## 删除默认路由

```
route del default
```

## 删除指定主机路由

```
route del -host ip dev 网卡
```

## 操作路由导致不能上网时:

```
route add default gw 当前局域网网关 dev wlp2s0
```





# 连接VPN

```shell
pptpsetup --create vpnname --server xx.xxx.xxx.xxx --username xxx --password xxx [--encrypt] [--start]
```

--start : 创建完VPN后立马连接.

--encrypt : 有时VPN连接服务器要求加密,VPN服务器要求加密时添加此参数

创建后,后期可用pon / poff 开关vpn





# 搭建VPN服务器:

参照:https://blog.csdn.net/dongdong9223/article/details/80790203

## 安装相关网络工具:

```
net-tools : 包含ifconfig,netstat,route...
pptpd : VPN搭建工具
配置163源 顺利apt-get 安装.
```

## 1.编辑/etc/pptpd.conf,配置VPN

安装完成后,配置连接到这个VPN的ip:

​	局域网下:本机ip

​	通过路由映射到外网,当前宽带动态ip

编辑pptpd.conf,最后添加,pptpd.conf中已注释localip/remoteip:

```
localip 192.168.1.1
remoteip 192.168.1.100-200
```

localip: 网关

remoteip : 客户端IP必须在这个设定的范围内      

## 2.配置用户信息

编辑:/etc/ppp/chap-secrets

```
# client        server  secret                  IP addresses
	ming		* 		123456		192.168.1.101
	yan			* 		123456		192.168.1.102
```

用户名（tab） 主机名（tab） 密码（tab） 分配到的ip地址(个人理解:连入客户分配到所在局域网下IP地址,* 自动分配)

ip地址最好不要用*，写具体的服务器中没有用到的ip.

设置 * 可能导致链接后，ping不同内网IP

手机端链接VPN：

​	打开PPP加密

​	打开高级选项，DNS服务器填写：8.8.8.8

​	可正常访问。

## 3.重启pptpds

/etc/init.d/pptpd restart

## 4.修改/etc/sysctl.conf

去掉“net.ipv4.ip_forward=1”注释			#####中I重要，如果客户端之间不通，可以检查这个设置。ip_forward=1 为 0 时可能出现客户端之间不通问题

修改后使修改配置生效:

```
sysctl -p
```

## 5.设置转发规则

```
iptables -t nat -A POSTROUTING -s 192.168.2.0/16 -o eth0 -j MASQUERADE  //是ifconfig得到的IP
iptables-save > /etc/iptables.pptp
```

192.168.2.0/16   :   通过 ip addr / ifconfig 得到的ip

eth0	: 	连接本地局域网 网卡名称

## 6.重启pptpds

```
/etc/init.d/pptpd restart
```

## 7.启动pptpds

```shell
/etc/init.d/pptpd start
```

## 列出当前连接VPN客户端:

```
route -n
```







# ssh安装:

安装:**openssh-server**

yum install **openssh-server** -y

-y : 一路自动y

编辑 /etc/ssh/sshd_config

有类似同名文件，一定要确认是**sshd_config**而不是 ssh_config

```
# 感觉是打开监听
Port 22
ListenAddress 0.0.0.0
ListenAddress ::

# 允许远程登录
PermitRootLogin yes

# 开启使用用户名密码验证
PasswordAuthentication yes
```

生成主机key:

```
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key


ssh-keygen -t rsa -f /etc/ssh/ssh_host_ecdsa_key


ssh-keygen -t rsa -f /etc/ssh/ssh_host_ed25519_key
```

设置密码:

passwd 

开启ssh服务

/usr/sbin/sshd -D

### 设置密码:

passwd [username]



## 没有service

安装initscripts

```
yum install initscripts -y
```

## 客户端连接时出现 no kex alg

编辑/etc/ssh/sshd_config,在末尾添加:

```
KexAlgorithms diffie-hellman-group1-sha1
```



连接ssh出现：

```
Unable to negotiate with xxx.xxx.xxx.xxx port 22: no matching key exchange method found. Their offer: diffie-hellman-group1-sha1  
```

是客户端原因，客户端在链接时添加参数：

```
ssh -oHostKeyAlgorithms=+ssh-dss -oKexAlgorithms=+diffie-hellman-group1-sha1 xxx.xxx.xxx.xxx/域名  
```













