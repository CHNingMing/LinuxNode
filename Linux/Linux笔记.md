

# 待整理

#### Chrome更换主题命令

```http
chrome://flags/#top-chrome-md
```

#### 内存查看软件 xfce4-systemload-plugin 

#### Linux 毫秒转换日期

```
date -s @毫秒
```

#### 为知笔记		临时多平台笔记方案

	同步出网络错误问题：安装libssl1.0-dev依赖解决
	apt install libssl1.0-dev

# XFCE部分

#### XFCE登录会话问题

	在lightdm找问题

## XFCE主题

#### XFCE4 资源主题

```
鼠标主题目录，/usr/share/icons
图标主题目录，/usr/share/icons
桌面主题目录，/usr/share/themes
应用程序图标目录： /usr/share/pixmaps
```

#### XFCE主题不全问题

```
gtk2-engines-xfce
gtk2-engines（gtk2.0主题）

gtk2-engines-pixbuf(临时测试主题可以使用)

```

### XFCE主题样式：

#### xfwm4/themerc(窗口文件夹)

```
：gtk-color-scheme  	声明变量

	theme-main-menu-text		菜单文字背景
	bg_color					窗体内背景基础背景
	selected_bg_color			选择文本、文件背景
	fg_color					通知栏菜单字体颜色




```

### XFCE窗口阴影大小角度宽度调整

```
每个窗口主题文件夹下都有xfwm4文件夹，进入，找到themerc打开：
添加（如果有替换）属性：
	shadow_delta_height=-3		阴影高度
    shadow_delta_width=-5		阴影宽度
    shadow_delta_x=-10			阴影X位置
    shadow_delta_y=-10			阴影Y位置
    shadow_opacity=80			阴影大小
```

#### 窗口各种状态

```
close：关闭按钮
    close-active.xpm		未激活
    close-prelight.xpm		获取焦点
    close-pressed.xpm		被点击 
hide:最小化按钮
	hide-active.xpm			未激活
	hide-prelight.xpm		获取焦点
	hide-pressed.xpm		被点击
maximize：最大化按钮
	maximize-...			....和上边类似
shade：窗口隐藏按钮
	....

```

### XFCE icon 图标部分：

 icon  电池使用通知栏自带显示电池+可以细微控制屏幕亮度

### XFCE登录器(Lightdm)

#### 登录器背景:

```
打开:/usr/share/lightdm/lightdm-gtk-greeter.conf.d/01_debian.conf
找到background=背景图片路径
```
### Sublime 输入法问题
	https://github.com/lyfeyaj/sublime-text-imfix.git 下载
解压，把lib下libsublime-imfix.so复制到sublime 目录
在进入src下编辑subl,编辑libsublime-imfix.so路径和sublime路径，运行这个subl启动sublime解决输入法问题。

### 安装声卡
安装alsa-utils
手动执行：
​	alsactl init
​	alsamixer 控制音量
​	




## xfce4命令部分

### xflock4		xfce锁屏命令

### xfce4-screenshooter -r 按区域截图

### 注销Xfce

pkill Xorg

## Xfce4  自带软件：

其中依赖必需的包在你执行apt-get iinstall xfce4的时候就已经完成安装了
除了Lib库文件、主要有以下的包
gtk2-engines-xfce GTK+-2.0 对于Xfce的主题显示支持 
orage Xfce 桌面环境的日历和时间管理
thunar Xfce 的文件管理器 
xfce4-appfinder Xfce中运行命令和应用程序查找、就是应用程序菜单第一个项目
xfce4-mixer Xfce中的混音器、简单说就是音量外放和话题之类的控制
xfce4-panel Xfce中的面板管理器
xfce4-session Xfce中的会话管理器 
xfce4-settings Xfce中的设置（是指图形界面的设置、就是打开菜单能看到的那个设置）
xfce4-utils Xfce中各个方面的工具
xfconf Xfce设置管理器中的实用工具
xfdesktop4 xfce的桌面背景、图标、还有菜单管理都由这个提供
xfwm4 Xfce中的视窗管理器
desktop-base Debian 桌面环境的公共基础

tango-icon-theme Tango 主题图标 
thunar-volman Thunar 文件管理器的音量控制扩展 
xfce4-notifyd 可视化的通知守护进程

以上这些软件包是你在安装Xfce4的时候因为依赖安装的包、其中最后的三个在Debian软件仓库里面是提示推荐的包、	

xfprint4 Xfce4 桌面环境下使用的打印机管理器。

Xfce4-goodies是由下面的包填充的、也就是说、你安装 xfce4-goodies其实是安装的下面这些软件包

xfce4-artwork Xfce桌面环境美化的扩展包、会安装一些图标、主题、壁纸
xfce4-battery-plugin 电池电量的显示器
xfce4-clipman-plugin 剪切板历史记录查看
xfce4-cpufreq-plugin 设置CPU频率
xfce4-cpugraph-plugin CPU利用率查看
xfce4-datetime-plugin 日期和地府插件
xfce4-diskperf-plugin 磁盘情况监控
xfce4-fsguard-plugin 文件系统监控
xfce4-genmon-plugin 显示一些命令提示
xfce4-mailwatch-plugin 邮件通知
xfce4-mount-plugin 挂载管理
xfce4-netload-plugin 网络
xfce4-notes-plugin 笔记
xfce4-places-plugin 快速管理收藏夹、最近使用、可移除驱动器
xfce4-quicklaunchers 快速启动
xfce4-sensors-plugin 传感器、可以查看硬件温度
xfce4-smartbookmark-plugin 收藏夹
xfce4-systemload-plugin 系统加载项查看
xfce4-timer-plugin 计时器
xfce4-verve-plugin 提供命令记忆功能
xfce4-wavelan-plugin 无线网运行情况
xfce4-weather-plugin 天气预报
xfce4-xkb-plugin 键盘配置
thunar-archive-plugin 压缩文件的解压插件
thunar-media-tags-plugin 提供媒体文件标签功能
mousepad 一个简单的文本编辑器
ristretto 图像查看器
xfburn DVD刻录软件
xfce4-dict 词典
xfce4-notifyd 通知
xfce4-screenshooter 截图软件
xfce4-taskmanager 任务管理器
xfce4-terminal 终端
xfce4-cellmodem-plugin 调制解调器
xfce4-linelight-plugin 一个搜索程序
xfce4-messenger-plugin DBus消息通知
xfce4-minicmd-plugin 额外的终端软件
xfce4-mpc-plugin, xfmpc Music Player Daemon播放器守护程序，管理播放列表和音乐数据库
xfce4-radio-plugin 收音机插件
xfce4-xfapplet-plugin 提供GNOME环境中的一些小应用程序支持
xfswitch-plugin 用户快速切换
xfce4-hdaps ThinkPads的HDAPS插件
thunar-thumbnailers 为文件管理器提供图像预览功能
gigolo GIO/GVfs虚拟文件系统的远程管理前端
parole 视频播放器
xfce4-power-manager 电源管理
以上软件包可以单独安装的、所以看你需要添加即可

级之后我比较在意这几个：
xfce4-weather-plugin天气插件检测地点更智能，天气预测也比较准确
xfce4-whiskermenu-plugin 是一款新的应用程序菜单，打开和LinuxMint的样式比较接近
然后就是面板设置里面有了桌面栏一个选项，相信Xfce4的死忠早已经注意到了，有了这个之后设置docky的效果更方便简洁。


PDF阅读器：Zathura
以前用的是evince-gtk，后来发现选择文本时中文乱七八糟的，而且有的打开之后缺页什么的，换了Mupdf用了一段时间，不过还是有些文档打开缺页，然后用新立得搜索PDF挖到Zathura，感觉超级爽，相当于Muodf的超级版～～

下拉终端：Tilda
不知道这么称呼这个对不对，就是一键滚动下拉终端的意思，记得以前有人要过，后来发现这个可以做到，设置下透明很好看，默认F1下拉终端，正在用这个

字体管理：Font-manager
换字体的时候就希望能有一个和GNOME一样查看字体的软件阿，然后小老鼠果然不负所望的有了这个，很好用的

文件管理：tuxcmd 
以前说MC？Winodws下面的神器TotalCMD？试试看这个


便签：xpad
以前用的xfce4-note，后来找到这个，界面比较清新，还不错


文件查找：catfish
猫和鱼？这个名字挺有意思的，相当于是locate加了个界面，对找文件懒得补全路径的人很方便


密码和密钥：seahorse
安装之后在设置里面可以看到


计算器：galculator,qalculate-gtk
貌似其实不需要计算器？python搞定简单的一切～～Q比G功能强大，菜单栏那里就能看出来的，不过我不需要那么霸气的功能，所以还是装个中文界面的G意思一下


视频编辑：openshot
一打开就可以上手编辑的那种，以前用过会声会影的原因么？感觉这个比较好用，不过还没在这个里面真正完成一个视频


截图：shutter
以前用的xfce4组件里面那个，现在换到这个了


另外以前说过的Abiword千万别用来编辑文档了，查看还可以将就用用，不然会被坑死，播放器推荐deadbeef和VLC，其他地方想必推荐过。

转自百度贴吧：https://tieba.baidu.com/p/2822201373?red_tag=0925185221

#### Git图形化管理界面解决方案

	GitKraken 或者 idea 自带git

#### FirFox中文包

```
https://ftp.mozilla.org/pub/firefox/releases/版本号/xpi/ch_Zh.xpi
```

#### XTerm中文问题解决

打开/etc/X11/app-defaults/XTerm		文件，**追加**

```
*VT100.utf8Fonts.font:  -misc-fixed-medium-r-semicondensed--13-120-75-75-c-60-iso10646-1 
*VT100.utf8Fonts.font5: -misc-fixed-medium-r-semicondensed--13-120-75-75-c-60-iso10646-1
*VT100.utf8Fonts.font5: -misc-fixed-medium-r-normal--18-120-100-100-c-90-iso10646-1
*VT100.utf8Fonts.font: -misc-fixed-medium-r-normal--18-120-100-100-c-90-iso10646-1
```

重新打开XTerm查看效果

#### 网络监视插件

xfce4-netload-plugin

### XFCE快捷键:

Alt+双击		:		放大/缩小屏幕



​	

### XFCE问题解决：

解决XFCE快捷键冲突问题 ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-keyboard-shortcuts.xml

#### 切记：修改完配置文件后注销是没有用的，需要重启

### 发送桌面通知

1.安装libnotify-bin

notify-send 通知标题 通知主体

```
notify-send 'Hello world!' 'This is an example notification.' --icon=dialog-information
```

### xfce桌面没图标，右键没反应解决

运行:

xfdesktop

# lxde部分：

### lxde设置快捷键：

​	打开位置：
​		~/.config/openbox/lxde-rc.xml

```xml
<keybind key="W-C-Up">
  <action name="Execute">
    <command>/opt/sendOption.sh +</command>
  </action>
</keybind>

包含在 keyboard 节点中

W=Windows键盘
C=Ctrl
A=Alt
Up 箭头上
Down 箭头下
注意：  快捷键连接符不是下划线，是 - 不是 _ 
```
## 新磁盘结构

```
45G Win7    
40G 软件
系统：Debian9	25
```

# 软件部分
## Redis和RedisDesktopManager安装
```
redis安装
	解压redis
	执行make
	执行make install
	redis-server运行redis
RedisDesktopManager安装：
	打开网址：https://github.com/uglide/RedisDesktopManager/releases?after=0.8.7-1
	下载，因为新版本的redisDesktopManager已经开始收费了......好像还只是linux 
```

## electron-ssr安装

/root/.config/electron-ssr     是客户端安装基础文件

### Shadowsocks-Qt5+SwitchyOmega临时快速解决上网问题

https://github.com/shadowsocks/shadowsocks-qt5/releases  Shadowsocks-Qt5下载地址只支持ss链接

SwitchyOmega安装完成后创建情景模式,配置代理服务器,完成后选择**应用选项**,切换情景模式为刚才配置的情景模式

## PHP idea 开发环境搭建：

#### 安装三个插件:

Behat Support

PHP

PHP Remote Interpreter

#### 配置:

Languages & Frameworks -> PHP -> CLI Interpreter 选择 PHP运行文件

Debug 配置好 调试端口

创建服务：

Servers - > + -> Host /port 

创建一个PHP Web Page,URL写可以访问到指定php文件路径





## IBus重启

ibus-daemon -r -d -x



## 搭建GTK+环境

直接安装:libgtk-3-dev包

编译时使用：

```
gcc C源文件.c -o [执行文件名称] `pkg-config --cflags --libs gtk+-3.0`
```



## SmartGit不能切换输入法

在{SmartGit安装目录}/bin/smartgit.sh

```
export GTK_IM_MODULE=ibus
改为：
export GTK_IM_MODULE=fcitx
```

## 

## Qt Create 安装后切换输入法问题：

```
安装CMake

下载fcitx-qt5源码：https://github.com/fcitx/fcitx-qt5.git  

编译前确认安装：libgl1-mesa-dev   libglu1-mesa-dev  extra-cmake-modules
安装完以上以来cmake报错，安装
（三组其中一个，后期待验证）
extra-cmake-modules

fcitx-libs-qt5 

fcitx-libs-dev 
libfcitx-qt5-dev 


添加环境变量：export CMAKE_PREFIX_PATH="{gcc版本目录}/gcc_64/lib/cmake/"

进入fcitx目录， 执行cmake .

在目录找makefile，有表示成功。

make编译，得到platforminputcontext文件夹
进入platforminputcontext，cmake .   得到makeFile 
make 得到:libfcitxplatforminputcontextplugin.so
```



### Appimage解包:

```
*.Appimage --appimage-extract
```

### Appimage打包：

```
appimagetool
```

## DbVisualizer插入中文乱码

右键连接项 - 编辑连接 - propertis选项卡 - 选择右侧  Driver Properties 列出连接参数列表:

characterEncoding 设置 utf8

generateSimpleParameterMetadata 设置成 true





# 数据库部分

## 安装navicat

### navicat打开后打开乱码问题

编辑start_navicat脚本,删除	export LANG="en_US.UTF-8"

破解navicat:

	取出/root(当前用户)下/.navicat64/userdef.reg做临时备份(**user.reg存储数据库链接信息**,**system.reg存储注册信息,如果只删除system.reg打开表时会报错,不能正常使用**)
	
	删除/root(当前用户)下/.navicat64文件夹
	
	启动navicat64初始化配置文件
	
	会发现配置文件又自动生成了,把备份的userdef.reg替换过去

## workbean升级后不能降级解决

首先搜索libgdal20,把libgdal20降级 ,在正常强制版本安装workbench就可以了  

不能降级主要原因是workbench依赖一个虚包:[gdal-abi-2-1-2],由libgdal20填实,所以直接降级workbench肯定不会成功

# 框架部分

## elasticsearch + head + ik安装

```
启动:
	./elasticsearch -Des.insecure.allow.root=true
安装head:
	./plugin install mobz/elasticsearch-head
	访问head:http://localhost:9200/_plugin/head/
安装ik:
	https://github.com/medcl/elasticsearch-analysis-ik
	下载ik分词器
	需要根据版本下载:
		es:2.4.0	对应ik	1.10.0
		es:2.4.1	对应ik	1.10.1
		es:2.4.2	对应ik 	1.10.2
		es:2.4.3	对应ik	1.10.3
		......
	下载完先后解压
		mvn clean
		mvn package
		复制target/releases/elasticsearch-analysis-ik-*.zip到{项目目录}/plgins/ik/下
		解压压缩包,进入项目目录config/elasticsearch.yml最后一行添加:
		 index.analysis.analyzer.ik.type: "ik"
		重启es
		测试链接:
http://localhost:9200/_analyze?analyzer=ik&pretty=true&text=我是中国人
```

## Redshift详细配置:

```
根据一天中的时间设置显示器的色温。

  -h		显示此帮助信息
  -v		详细输出
  -V		显示程序版本

  -b DAY:NIGHT	应用的屏幕亮度 (介于 0.1 和 1.0)
  -c FILE	从指定的配置文件加载设置
  -g R:G:B	应用的附加伽马校正设置
  -l LAT:LON	你当前的位置
  -l PROVIDER	选择自动位置更新的服务提供者
  		(输入“list”来查看可用的服务提供者)
  -m METHOD	用来设置色温的模式
  		(输入“list”来查看可用的模式)
  		  drm
		  randr
		  vidmode
		  dummy

  -o		单触发模式 (不要平滑地调节色温)
  -O TEMP	单触发手动模式 (设置色温)
  -p		打印模式 (只打印参数值并退出)
  -x		重置模式 (从屏幕上移除调节)
  -r		禁用色温过渡
  -t DAY:NIGHT	设置日间/夜间的色温

中性色温为 6500K。使用该值不会改变
显示器的色温。设置色温值高于它会
导致更多的蓝光，而设置低于它的色
温值会导致更多的红光。

默认值：

  日间色温：5500K
  夜间色温：3500K

```

# Eclipse

## 快捷键:



## 设置部分:

### Eclipse 命令行可以运行,直接点击不能运行解决方案:

#### 在写一个脚本,脚本中执行

```
source /etc/profile	# 刷新环境变量,让eclipse找到JAVA_HOME

/.../eclipse目录/eclipse
```

#### 修改目录下eclipse.ini文件

```
文件下顶部添加
```

```
-vm 
/djk路径/jre/bin
-startup
....
```

### 设置保护色：

```
**204红 232绿 207蓝**
```

### Eclipse 菜单运行和命令行运行个别不正常显示问题(方法类描述不正常)

目前我只是在Linux碰见这个问题,WIndows暂时还没碰见

### 主要就是执行  export SWT_GTK3=0

需要手动创建执行eclipse脚本

1.脚本中除了加载 java环境变量外(这是配置jdk配置好的,在这里为了保险刷新一下java环境变量)

	source /etc/profile

2.设置GTK3(也可以把这行语句写在profile文件中,和java变量放在一起,如果和java变量放在一起省略这步)

	export SWT_GTK3=0

3.cd 手动切换eclipse 目录

	cd $eclipse目录

4.执行目录下eclipse运行文件,如果是STS,就./STS

	./eclipse

5.设置执行脚本运行属性

	chmod 777 执行脚本文件名

在外部命令行执行,或者放在菜单中执行

## Eclipse 添加Git工具时提示

```
Git cannot be made visible because all of its children are in unavailable action sers
```

添加工具在windows - > Perspective - > Customize Perspective...

切换到Action Set Availability,在这下找到git选项:Git  Git Navigation Actions 两项,选择

### Eclipse GIt每次提交需要登录问题

第一次提交时选择密码下方选项,在输入登录密码

查看当前有没保存密码

Window - Preferences - Security - Secure Storage - Contents - [Default SecureStorage] - GIT(这个节点是第一提交后才有)

### Eclipse Mars Linux 下不能正常运行

打开Eclipse目录下的eclipse.ini

实验配置是否能解决问题:

```
export SWT_GTK3=0
cd eclipse目录
./eclipse 
```

添加:

```
找到 --launcher.appendVmargs 行，在其前面插入如下设置：

--launcher.GTK_version
2
```

## 插件部分:

### Eclipse 安装STS组件

别勾选任何复选框！～～！！！！，自动识别最好

### mars 安装SVN

访问	http://subclipse.tigris.org/servlets/ProjectDocumentList?folderID=2240

下载site 1.6.18.zip版本,但是这个版本SVN不支持中文....

**测试1.8可以在mars上使用，也支持中文SVN仓库路径**

下载后打开eclipse ，打开安装插件页面，选择这个包，随便起个名字，直接next安装



### Eclipse 没有main或者test解决

```
打开项目配置窗口 - Java Build Path - Libraries选项卡 - 选中JRE _ edit - Alternate JRE Finish - OK


```

### Eclipse 智能提示卡顿问题

```
Preferences - Java - Editor - Content Assist Advanced :勾选Java Proposals 和 Java Proposals(Task -Focused) - OK

```

### STS各版本总结

e4.5.1

http://download.springsource.com/release/STS/3.7.2.RELEASE/dist/e4.5/spring-tool-suite-3.7.2.RELEASE-e4.5.1-win32-x86_64.zip

http://download.springsource.com/release/STS/3.5.1/dist/e4.3/spring-tool-suite-3.5.1.RELEASE-e4.3.2-win32-x86_64.zip

Linux 4.5.1 STS  直接执行有问题

http://download.springsource.com/release/STS/3.7.2.RELEASE/dist/e4.5/spring-tool-suite-3.7.2.RELEASE-e4.5a-linux-gtk-x86_64.tar.gz



http://download.springsource.com/release/STS/3.8.1.RELEASE/dist/e4.6/spring-tool-suite-3.8.1.RELEASE-e4.6a-linux-gtk-x86_64.tar.gz

# Idea

## Idea 破解教程：

​	下载JetbrainsCrack-2.6.2.jar，最好放到Idea目录，放哪里无所谓...

​	找到idea64.exe.vmoptions，在最后添加：-javaagent:JebrainsCrack绝对路径

再通过命令行打开时会打印破解信息,选择**Activation code:**

```
ThisCrackLicenseId-{ 
“licenseId”:”ThisCrackLicenseId”, 
“licenseeName”:”idea”, 
“assigneeName”:”“, 
“assigneeEmail”:”GengMIngYan@Yeah.net”, 
“licenseRestriction”:”For This Crack, Only Test! Please support genuine!!!”, 
“checkConcurrentUse”:false, 
“products”:[ 
{“code”:”II”,”paidUpTo”:”2099-12-31”}, 
{“code”:”DM”,”paidUpTo”:”2099-12-31”}, 
{“code”:”AC”,”paidUpTo”:”2099-12-31”}, 
{“code”:”RS0”,”paidUpTo”:”2099-12-31”}, 
{“code”:”WS”,”paidUpTo”:”2099-12-31”}, 
{“code”:”DPN”,”paidUpTo”:”2099-12-31”}, 
{“code”:”RC”,”paidUpTo”:”2099-12-31”}, 
{“code”:”PS”,”paidUpTo”:”2099-12-31”}, 
{“code”:”DC”,”paidUpTo”:”2099-12-31”}, 
{“code”:”RM”,”paidUpTo”:”2099-12-31”}, 
{“code”:”CL”,”paidUpTo”:”2099-12-31”}, 
{“code”:”PC”,”paidUpTo”:”2099-12-31”} 
], 
“hash”:”2911276/0”, 
“gracePeriodDays”:7, 
“autoProlongated”:false}
```

```
{“code”:”II”,”paidUpTo”:”2099-12-31”}, 		//idea 到期时间
{“code”:”DM”,”paidUpTo”:”2099-12-31”}, 
{“code”:”AC”,”paidUpTo”:”2099-12-31”}, 
{“code”:”RS0”,”paidUpTo”:”2099-12-31”}, 
{“code”:”WS”,”paidUpTo”:”2099-12-31”}, 		//WebStom 到期时间
{“code”:”DPN”,”paidUpTo”:”2099-12-31”}, 
{“code”:”RC”,”paidUpTo”:”2099-12-31”}, 
{“code”:”PS”,”paidUpTo”:”2099-12-31”}, 
{“code”:”DC”,”paidUpTo”:”2099-12-31”}, 
{“code”:”RM”,”paidUpTo”:”2099-12-31”}, 
{“code”:”CL”,”paidUpTo”:”2099-12-31”}, 		//Clion 到期时间
{“code”:”PC”,”paidUpTo”:”2099-12-31”} 
```







###  Idea快捷键

格式化代码		Ctrl + Alt + L



## Idea导入 eclipse web项目

导入项目时一路next,打开idea后,选择号SDK和对应级别,级别根据JDK版本选择

### 选择Modules - Dependencies

org.eclipse.jst.server.core.container....

....

....

删除红色字体项目(红色字体代表无效的)

点击+号,选择LIbary -- 选择Tomcat 7

		选择Jar	--	选择项目中jar文件目录

### 选择Modules - Source

在Web-INF下建立classes,切换到Path选项卡,选择ue module compile output path

output path和Test output path都选择到刚才创建的classes路径

### 选择Facets

	点击+号 - WEB - 选择项目 :
	
		Deployment Descriptors选择到项目web.xml位置
	
		Web Resource Directories选择到WebContext位置,(WEB-INF上一级目录)

### 选择Artifacts

	点击+号,选择Web Application: Expload  from Models   -- 选择项目(这一步是让运行是的tomcat加载到这的lib 文件,这的lib是通过之前选择的)







# Linux软件列表:

必备:

	wifi
	
	Wine
	
	Oracle VM VirtualBox
	
	rdesktop 远程连接工具 windows
	
	putty 	ssh连接工具
	
	搜狗输入法
	
	WPS
		打开后缺失文件解决：https://pan.baidu.com/s/1eS6xIzo
	
	邮箱,如果没有合适的使用  thunderbird,还是他好使虽然统计很大
	
	XMind
	
	为知笔记
	
	VLC视频播放器
	
	Google Chrome
	
	Firefox
	
	uGet
	
	DiskUsageAnalyzer	容量清理  搜索baobab
	
	Redshift		眼睛保护
	
	Evince			PDF阅读器

开发:

	Eclipse C++ / codeblocks				--
	
	Eclipse Mars / Spring Tools Suite
	
	/GitKraken								--
	
	Idea
	
	Lantern
	
	RepidSVN/ 更好软件svn-workkbench
	
		Meld	文件比较
	
	MySql WorkBench	被替代 DbVisualizer 9.8版本可以破解专业版
	
	Postman
	
	Redis Desktop Manager
	
	Redshift
	
	SubLime Text 3
	
	Typora

其他:

	KolourPaint		有中文不能输入问题		-

## DbVisualizer9.8

9.8版本可以正常破解专业版

#### 设置智能提示:

Tools -> Tools Properties -> Sql Commander -> Auto Completion

#### 设置智能提示快捷键:

实际是按下快捷键实现菜单中某个功能

Tools -> Tools Properties -> Key Bindings -> (最好创建一个副本)Make Copy -> 依次打开 Main Menu /Edit/**Show Auto Completion**   只设置First Keystroke就可以

# Linux 搭建微信小程序

下载nw运行时

下载开发工具包

```
git clone https://github.com/cytle/wechat_web_devtools.git
```

复制包内:package.nw到nw目录,通过${nw目录}/bin/nw执行文件启动







## 磁盘结构：

120G：

​	40G：Windows

​	40G：Windows专用

​	20G：Linux

​	20G：Linux专用



## npm

npm运行必须保证 /usr/bin/下有node,也就是通过命令行可以直接使用node



## 重启Fcitx实现重启输入法操作

```
fcitx -r
```





## 安装服务端openssh-server和客户端openssh-client
```
	客户端直接 apt-get install openssh-client
		远程连接:ssh 用户名@ip地址
	服务端:
		apt-get install openssh-server
	操作命令:
		/etc/init.d/ssh stop
		/etc/init.d/ssh start
	配置:/etc/ssh/sshd_config		保证可以通过root登录
		找到# Authentication:
	    LoginGraceTime 120
	    PermitRootLogin without passwd
	    StrictModes yes
	    改成
	    # Authentication:
	    LoginGraceTime 120
	    PermitRootLogin yes
	    StrictModes yes
	重启服务器
```


## 远程上传/下载文件

应急情况scp工具实现远程上传下载

scp -P <端口号> 源 目标

远程路径格式:user@ip:/路径

```shell
# 远程下载到本机 大写P
scp -P 22 root@192.168.56.101:/opt/xx.tar.tz /opt/xx.tar.tz
# 本机上传到源 大写P
scp -P 22 /opt/xx.tar.tz root@192.168.56.101:/opt/xx.tar.tz
```

-v :显示文件传输进度

-P :大写P 执行ssh端口

-4 : 强行使用IPV4

-6 : 强行使用ipv6


# 软件使用

## 工具:

### rdesktop远程链接工具

```
rdesktop ip			简单链接远程windows
rdesktop -f ip		全屏模式链接,全屏/窗口 Ctrl+Alt+Enter
rdesktop -f -r disk:MyDisk=挂载目录,从根目录开始 ip	挂载指定目录到远程windows
			-r clipboard:PRIMARYCLIPBOARD		共享剪切板,仅限文本,不支持文件
			
```



## 日常:



# Linux 命令部分

## 刷新当前系统字体

```
fc-cache -f -v
```

### 查看当前支持字体

locale -a

## 查看/设置环境变量

#### echo $PATH

#### PATH=xxxx:xxxx:(适合临时设置变量)

​	每个环境变量用 ：(英文冒号)分割

## 列出制定进程Pid和名称

pgrep -l xxx

## 搜索命令:

```
whereis 命令名称
```

##  查看磁盘容量

```shell
df 
```



## 查看当前目录文件容量

```shell
du -h [指定文件/]
```

## 命令结果屏幕显示不全

键盘操作:

Shift + PageUp

Shift + PageDown

### more命令

例如:

```shell
netstat -n | more
```

| more  部分使用管道配合 more 实现翻页

### Less命令

例如:

```
netstat -n | less
```

| less 通过:

​	 Enter 逐行显示

​	PageDown 逐页显示

​	q	结束显示





## Vi/Vim

基本操作：
​	delete键 删除文本		（命令模式下）

​	编辑模式：

​		i	当前位置插入文本

 		a 	当前位置追加文本

​		o	追加一行出入文本

​	移动光标：

​		h左、j下、k上、l右

​	删除文字：

​		x	删除光标后文字

​		#x	删除光标后#个文字     6x光标后6个文字

​	撤销：u

​	恢复上一步操作: Ctrl+R

​	多选文本:

​		进入视图模式 : v

​		通过 h j k l 移动光标实现

​		y : 复制

​		p : 粘贴

​		d : 剪切

​	光标跳转:

​		^ 当前行开始

​		$ 当前行结束

```
搜索指定字符：
	切换到命令模式,输入 / 搜索的字符串
```

## Find

```
find 查询路径 [参数]
简单查找:
	find . -name xxx.xxx
-mount, -xdev : 只检查和指定目录在同一个文件系统下的文件，避免列出其它文件系统中的文件
-amin n : 在过去 n 分钟内被读取过
-anewer file : 比文件 file 更晚被读取过的文件
-atime n : 在过去n天内被读取过的文件
-cmin n : 在过去 n 分钟内被修改过
-cnewer file :比文件 file 更新的文件
-ctime n : 在过去n天内被修改过的文件
-empty : 空的文件-gid n or -group name : gid 是 n 或是 group 名称是 name
-ipath p, -path p : 路径名称符合 p 的文件，ipath 会忽略大小写
-name name, -iname name : 文件名称符合 name 的文件。iname 会忽略大小写
-size n : 文件大小 是 n 单位，b 代表 512 位元组的区块，c 表示字元数，k 表示 kilo bytes，w 是二个位元组。-type c : 文件类型是 c 的文件。
d: 目录
c: 字型装置文件
b: 区块装置文件
p: 具名贮列
f: 一般文件
l: 符号连结
```

```shell
列：
find ./ -name "文件/文件夹名称"
```

检查 log目录 过去7天内没修改过的.log文件：

```
find log -mtime +7 -name "*.log"
```

### -exec

​	找到文件后，为每个文件执行指定命令

```shell
## 列出查到的每个文件目录

# 一定要写;不然终端会被 \ 折行
find log -mtime +7 -name "*.log" -exec cat {} \;
```

{} : 表示每个文件名称

###  -ok

​	找到文件后，执行每个文件指定命令前，通过用户选择为每个文件确认是否执行相应命令

```shell
find log -mtime +7 -name "*.log" -ok cat {} \;
```

## ls

-h : 显示文件大小，配合-l才可以

-S : 对文件大小进行排序

## 查看Linux发行版本

lsb_release -a  比较详细











# 常用命令工具:

## zip 压缩

zip -r *.zip 目录

## rpm解压

rpm2cpio xx.rpm | cpio -idmv

###  tar 压缩

tar -cvf *.tar /xxxx目录

## putty快捷连接ssh

putty ip -l username -pw password



## 查看Debian版本

lsb_release -cs

# 端口映射

windows下：nat123方案

linux 下 : Sunny-Ngrok

​	启动时通过隧道id启动。

```shell

sunny clientid 隧道id 多个空格隔开
```







## DPKG

1.下载的软件存放位置

```
/var/cache/apt/archives2.安装后软件默认位置
```
3.可执行文件位置 
```
/usr/bin
```
4.配置文件位置
```
/etc
```
5.lib文件位置
```
/usr/lib
```

# 软件问题解决

## 网易云音乐安装和打开没反映解决

安装版本：netease-cloud-music_1.0.0+repack.debiancn-1_amd64.deb      32M

下载地址：https://repo.debiancn.org/pool/main/n/netease-cloud-music/

dpkg - i安装，新立得解决依赖问题

执行时添加 ：  --no-sandbox

## 重启Fcitx实现重启输入法操作

```
fcitx -r
```

## Ping问题：

ping 出现：network is unreachable

情况1：

```
 /etc/network/interface下配置网卡时，有没有加auto 网卡。
 如果没设置，其他的也不会生效。
```







### codeblocks切换输入法：

profile添加：

```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```

## 连接蓝牙耳机:

安装:blueman

安装:pulseaudio-module-bluetooth

```
pactl load-module module-bluetooth-discover
```

安装:bluez-firmware

启动dbus服务和蓝牙服务：

```
service dbus start
/etc/init.d/bluetooth start
```

## Protocol not available错误解决方案：

输入命令加载module-bluetooth-discover模块即可：

```
# pactl load-module module-bluetooth-discover
```

这句命令一直没执行成功





每一步别忘了移除蓝牙耳机设备重新添加

# Wine

## Wine乱码解决:

乱码主要原因还是少字体

去Wine临时目录下找到drive_c/windows/Fonts/

去正常Windows下复制文本文件:

simfang.ttf

simhei.ttf
simkai.ttf
simpbdo.ttf
simpfxo.ttf
simpo.ttf
simsun.ttc
simsunb.ttf

## Wine设置窗口

wine winecfg

# VBOX

### Win2003开机蓝屏解决

设置磁盘控制器IDE型号为：PIIX4

## VBOX命令行:

### 列出所有虚拟机UUID:

​	VBoxManage list vms

### 启动指定UUID虚拟机:

​	VBoxManage startvm uuid 	[-type parm]

​	type:

​		headless		隐藏启动

​		gui[默认]		视图界面启动

睡眠指定UUID虚拟机:

​	VBoxManage controlvm uuid savestate

​		savestate:表示保存虚拟机状态并关闭

# QT Create安装

http://download.qt.io/official_releases/qtcreator/4.8/网址下载最新版qt 

安装 gcc/g++、cmake  **不然会不能运行**



# MySql

## 不同版本数据导出后执行笔记：

​	5.7.19 - 》 5.5.27

删除

*	/*!40101 SET character_set_client = @saved_cs_client */;	每个表下，删除前保证每个创建表语句最后括号后有 ; 结束，默认低版本不支持没有;结束（通过submit多选解决）

开始和末尾

​	/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
​	/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
​	/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
​	/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
​	/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
​	/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
​	/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;*

