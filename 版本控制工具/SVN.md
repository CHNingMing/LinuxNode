

## SVN

#### 目录结构：

```
branches:分支
	项目分支源码
	一般使用在:当主干项目开发过程中,之前发行的项目有紧急BUG需要修复,这时候就需要从tags中拿到发行版tag,解开放到branches分支中针对bug修复,在发行
tags:标志
	一般管理员才有对tags写权限
	当一个项目全部开发完成后,会打成tag,其实就把当前项目文件夹在赋值一份
	tag存放的是某个项目版本,如:测试版、发行版、...
trunk:主干项目
	项目源码
document:项目文档管理
```

在profile文件中添加:	**export LC_CTYPE="zh_CN.UTF-8"**

linux SVN管理软件:RapidSVN

