## yum

列出所有软件包:

```
yum list installed
```





## ssh安装:

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





