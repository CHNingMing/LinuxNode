# NodeJS

## linux NodeJS环境安装

官网下载:https://nodejs.org/en/download/

Linux 二进制包:64

解压任意位置,打开bin下,node可以直接链接到/usr/bin/node

NPM 需要单独写脚本包一层:

```shell
#!/bin/bash
cd /...Node二进制目录/bin
./npm $*
## $* 获取所有参数
```

## linux   引入模块

obj require('模块名称')





