# Sublime

## 安装:

```
下载:http://www.sublimetext.com/
Sublime 不能输入中文问题
	https://github.com/lyfeyaj/sublime-text-imfix.git 下载
	解压后src/subl 复制到usr/bin下，修改sublime安装路径
	复制解压后lib下的libsublime-imfix.so到安装目录
	复制src下的sublime-imfix.c 到安装目录
	命令行可以直接运行subl
```

## 安装插件:

### 	插件目录:

```
打开 sublime -> Preferences -> Browse Packages...
 打开的文件目录就是插件目录
```



### 	安装Package Control:

```
打开 sublime -> Preferences -> Browse Packages...
打开文件目录后,后退一级目录,找到Installed Packages,如果有Package Control相关名文件,删除(装好插件后Sublime下次启动时还会创建).
进入Packages创建Package Control(文件名必须一致,不然编译器会提示)
进入文件夹,解压文件,重启Sublime
```

### 	安装Emmet HTML智能提示:

注意:如果没效果记得关闭所有sublime打开文件标签,重启Sublime

```
下载Emmet:https://emmet.io/download/		选:Sublime
${插件目录}下创建 Emmet(名字尽量一致),解压Emmet
下载PyV8:https://github.com/emmetio/pyv8-binaries
也放到插件目录,
```

#### Emmet快捷键:

​	 html:5			Ctrl+E,执行智能提示