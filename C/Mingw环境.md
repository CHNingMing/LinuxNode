# Mingw

Mingw类似apt包管理器，是一个windows下的包管理器，通过这个工具下载gcc,gdb,g++等

安装Mingw,默认安装在[系统所在盘]C:\Mingw

配置环境变量:C:\Mingw\bin			bin下也就一个文件Mingw-get,配置环境变量主要是使用Mingw-get方便。

依次执行:

```
mingw-get install gcc
mingw-get install g++
mingw-get  installgdb
```

也可以一次安装多个： 

```
mingw-get install gcc g++ gdb
```

安装好后的执行文件也会放在C:\Mingw\bin下，不用再配置gcc,g++等路径