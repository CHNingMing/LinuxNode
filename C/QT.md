# QT 快捷键

Ctrl+;		 粘贴板记录



## QT不能调试解决

安装adb解决

```
apt-get install gdb
```



坑：

Windows搭建QT时，一定要把${QT安装目录}\bin添加到path,不然在构建时会报系统找不到文件。大概是构建时会用qt自己的命令，qt安装时又不会把自己的bin文件夹路径放入path

