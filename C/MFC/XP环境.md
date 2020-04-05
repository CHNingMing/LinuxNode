# MFC项目生成XP下可执行文件:

- 项目 - 属性 - 常规 - 平台工具集 选择:Visual Studio 20xx - Windows XP (vxx_xp)
- (推荐设置)MFC 的使用选择: 在静态库中使用MFC (把执行文件所用的依赖打包到单个文件中)

设置完成后会包SDKDDKVer.h”: No such file or directory,下边解决。



# 无法打开包括文件: “SDKDDKVer.h”: No such file or directory

- 项目 - 属性 - VC++ 目录 - 包含目录 新增**$(WindowsSDK_IncludePath)**  库目录新增 **$(WindowsSDK_LibraryPath_x86)**



