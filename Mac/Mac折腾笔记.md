# 快捷键

Ctrl键Command交换在设置->键盘中，个别程序还是需要Command

command + M : 最小化应用

**Command-H**：隐藏最前面的应用的窗口

Option-Command-Esc：[强制退出](https://support.apple.com/zh-cn/HT201276)应用。

Control-Command-F：全屏使用应用（如果应用支持）。

- **Command-E**：推出所选磁盘或宗卷。
- **Command-I**：显示所选文件的“显示简介”窗口。

- **Option-Command-D**：显示或隐藏“程序坞”。

- **Control–A**：移至行或段落的开头。
- **Control–E**：移至行或段落的末尾。

Option(Alt)+Command(Ctrl)+V : 剪切，复制后使用此快捷键实现粘贴效果

F11 类似window  Ctrl+D  快速显示桌面

## Finder

Command+Shift+G			打开文件夹指定目录

Command(Ctrl)+Shift+.		显示隐藏文件

## Chrome

Command(Ctrl)+Option(Alt)+I				开发者工具





# 命令

安装brew软件管理器：

https://brew.sh/index_zh-cn.html

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```



### 基本睡眠相关命令：

查看睡眠模式：

```
pmset - g | grep hibernatemode
```

设置睡眠模式：

```
pmset -a hibernatemode 0将睡眠图像仅保存到RAM，这将只是睡眠。

pmset -a hibernatemode 1将sleepimage仅保存到Disk，这将是一种“软”休眠。

pmset -a hibernatemode 3将睡眠图像保存到RAM和磁盘，这将是安全睡眠，首先是系统

将睡眠和后来的休眠。

pmset -a hibernatemode 25  将睡眠图像仅保存到  磁盘并从RAM中移除电源和一些

更多设备，这将是“真正的”休眠。
```

# 常用：

列出磁盘内容：

​	df -h

查看已挂在磁盘和挂载目录：

​	mount

# 相关插件：

**必备插件**：FakeSMC.kext

电池插件：VoodooBattery.kext

笔记本键盘插件：VoodooPS2Controller.kext

音量插件：AppleALC.kext+Lilu.kext

触摸板插件：ApplePS2SmartTouchPad.kext

显卡驱动：HibernationFixup.kext + IntelGraphicsFixup.kext

USB驱动：USBInjectAll.kext。暂时没用上

# 软件：

### 实用工具：

The Unarchiver	压缩软件

Kext Utillty		实时加载kext

欧陆词典

#### 清理工具：

Dr.Cleaner Pro(清理垃圾) + CleanMyMac X(优化系统)

MacBooster 7	（以后准备只是用Ta）

# 开发

## 软件

iTerm		连接远程SSH

Cyberduck	管理远程文件

### 搭建PHP环境

#### XAMPP:

​	直接安装

注意：

​	修改项目根目录时，修改项目到Application下并且保证有原根目录下文件，其他目录有权限问题

##### XAMPP设置ZendStudio调试：

1. 配置项目目录

   打开配置文件：

   xampp应用下 etc(快捷方式)/httpd.conf

   或者：xampp应用下/xamppfiles/etc/httpd.conf

   ```xml
   DocumentRoot "/Applications/PHPWork"
   <Directory "/Applications/PHPWork">
   ```

   尽量目录在/Applications下，没有权限访问问题，因为/Applications是所有用户都能访问的路径

2. 配置XDebug

   同样在etc下找到php.ini,搜索xdebug，如果没有添加：

   ```xml
   
   [xdebug]
   zend_extension=/Applications/XAMPP/xamppfiles/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so
   xdebug.remote_autostart=on
   xdebug.remote_enable=on
   xdebug.remote_enable=1
   xdebug.remote_mode="req"
   xdebug.remote_log="/Applications/XAMPP/xamppfiles/var/log/xdebug.log"
   xdebug.remote_host=localhost/127.0.0.1
   xdebug.remote_port=9000
   xdebug.remote_handler="dbgp"
   xdebug.idekey="ZendStudio"		--暂时ide没设置
   ```

   注意：zend_extension（插件目录）、remote_log（日志）、remote_host（调试主机网址）、remote_port（调试端口）

   可以写个php，用phpinfo()列出php信息，搜索xdebug



   ##### 配置解析器

   打开：左上角：Zend Studio - > Preferences.. -> PHP -> PHP Executables -> 添加

   php名称，php解析器路径：（定位到XAMPP路径下bin目录php）,debug选择xdebug,port 和刚才 (php.ini)remote_port对应

   ##### 添加服务器

   PHP 下 Servers - > new -> Local Apache Http Server -> { apache名称 、apache配置文件路径(XAMPP下etc)}

#### MAC自带PHP环境：

mac 自带php环境，但是默认不生效，配置一下：

/etc/apache2/httpd.conf		文件，搜索libphp

LoadModule php7_module libexec/apache2/libphp7.so		解开注释

#### XMAPP工具PHP环境：

下载链接：https://www.apachefriends.org/download.html

目测：5.6.40 / PHP 5.6.40	可以正常安装

安装后隐藏文件夹

​	~/.bitnami

##### http.conf

```
/Applications/XAMPP/xamppfiles/etc/http.conf
```

##### php.ini

```
/Applications/XAMPP/xamppfiles/etc/php.ini
```

/Application/XAMPP/



### PHP.ini

Mac 下没有PHP.ini,但是有PHP.ini的模板文件，位置：

```
/private/etc/php.ini.default
```



### 默认工作目录在

**/Library/WebServer/Documents**下

### Apachectl 常用命令

/ 启动Apache服务

sudo apachectl start

// 重启Apache服务

sudo apachectl restart

// 停止Apache服务

sudo apachectl stop

// 查看Apache版本

httpd -v

### 其他：

​	插上耳机人声音模糊不清时，打开：

​	声音 - 输出选项卡 - 平衡左右调下试试





# 入门

切换root用户：

```
sudo -i
```

