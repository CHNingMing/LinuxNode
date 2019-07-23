

ADBwifi调试

usb连接电脑,adb devices列表中有就可以

adb shell

setprop service.adb.tcp.port 5555

exit

adb tcpip 5555

adb connect  192.168.1.100



### Debian连接 手机

MTP方式:

安装mtpfs/**jmtpfs**,mtp-tools

```shell
# 列出连接MTP的设备
jmtpfs
# 把设备挂在到某个目录
jmtpfs /media/mtpdir

```









