

Linux 安装VBOX虚拟机	virtualbox-5.1_5.1.38-122592_Debian_stretch_amd64.DEB  尝试可用

历史下载地址：https://www.virtualbox.org/wiki/Download_Old_Builds

https://download.virtualbox.org/virtualbox/5.1.38/virtualbox-5.1_5.1.38-122592~Debian~stretch_amd64.deb

​	添加源
​		deb http://download.virtualbox.org/virtualbox/debian stretch contrib
​		deb http://http.kali.org/kali kali-rolling main non-free contrib
​		deb-src http://http.kali.org/kali kali-rolling main non-free contrib
​		deb http://security.debian.org/debian-security stretch/updates main 
​	从官网下载虚拟机VBOX或者源中添加
​	安装后先查看当前系统内核版本，安装headers和commons	uname -a查看当前内核版本
​	

```
https://packages.debian.org/hu/stretch/kernel/	Debian Header头文件网站，在网页上Ctrl+F搜索响应内核版本，下载Headers和common
先安装common,在安装headers头
安装完成后执行/sbin/vboxconfig
安装 gcc  make		直接apt-get install gcc make
```

​	

Linux 重启网卡
​	 /etc/init.d/networking restart
LInux 设置虚拟机vbox网卡
​	auto 网卡名称
​	iface 网卡名称 inet static
​	address 网卡地址
​	netmask 255.255.255.0 子网掩码
​	gateway 默认IP网段
Linux 修改网卡
​	临时修改：
​		fconfig 网卡名称 down  #关闭网卡
​		ifconfig 网卡名称 hw ether XX XX XX XX XX XX   #MAC地址
​		ifconfig 网卡名称 up   #打开网卡

windows xp 下网卡驱动：

在vbox种设置网卡驱动为 ： Intel PRO/1000 T 服务器，windows xp 自带这个驱动不用安装