

ADBwifi调试

usb连接电脑,adb devices列表中有就可以

adb shell

setprop service.adb.tcp.port 5555

exit

adb tcpip 5555

adb connect  192.168.1.100