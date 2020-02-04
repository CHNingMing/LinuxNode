# 安装

## 准备

msdn下载 6.22    ed2k://|file|SC_MSDOS622sc.exe|10020288|0B2B0878B8BBD2233D23022EE5339637|/

UltraISO  			 把系统打包，当时MS-DOS只支持1.44软盘，由于系统太大，所以把系统分成各个文件，通过UltraISO把文件打包成软盘格式，加载到虚拟机。



## 安装

下载好MS-DOS 6.22   ,双击解压，或者用压缩工具解压，解压得到DISK1-DISK4 ,PDOS1-PDOS5, WC1

只安装系统，用DISK1-DISK4就可以。DISK1是引导安装文件，其余是安装时需要的文件。

打开UltraISO,新建 - 软盘影像 ，选择MSDOS6.22，先把DISK1的IO.SYS和MSDOS.sys拖到UltraISO，在吧剩下的文件拖进去(网上都这样说，UltraISO的BUG吧);

[**重要**]重命名光盘名称为: DISK      1.IMG,光盘名称不一样安装时不认！！！DISK和1.IMG之间6个英文下的空格。

保存，保存为DISK      1.IMG

其余的DISK2-DISK4，新建硬盘映像。选择无系统，名称和上边规则一样DISK      2.IMG....

## VBOX安装：

新建虚拟机，类型选择Other，版本DOS，下一步，下一步...

设置 - 存储 - 删除没有盘片，选择控制器(模拟的软盘)，软件映像选择打包好的DISK      1.IMG。

按两个F3进入名两行模式，格式化硬盘，安装

通过fdisk格式化硬盘，输入setup /g /h 开始安装，依次提示请插入地 x 张软盘。

对应的就是DISK     x.img,每个DISK就是软盘。

选择菜单设备 - 分配软驱 - 选择一个虚拟硬盘   ，选择DISK     x.img







