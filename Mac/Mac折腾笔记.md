

# 快捷键

command + M : 最小化应用

**Command-H**：隐藏最前面的应用的窗口

Option-Command-Esc：[强制退出](https://support.apple.com/zh-cn/HT201276)应用。

Control-Command-F：全屏使用应用（如果应用支持）。



- **Command-E**：推出所选磁盘或宗卷。
- **Command-I**：显示所选文件的“显示简介”窗口。

- **Option-Command-D**：显示或隐藏“程序坞”。

- **Control–A**：移至行或段落的开头。
- **Control–E**：移至行或段落的末尾。







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

#### 清理工具：

Dr.Cleaner Pro(清理垃圾) + CleanMyMac X(优化系统)

