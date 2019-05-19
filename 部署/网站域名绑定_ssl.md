# 域名解析：

临时解决方案：https://dns.xsazz.com/index.php/index/index/control.html

新势力解析网

## 解析类型：

A	：	只能输入IP地址

CNAME	：	普通字母网址





# 步骤：

## 取到解析值：

到服务器控制台处打开绑定域名操作页面，一般绑定页面都会有绑定CNAME解析值

## 绑定解析值

直接在域名网站添加解析（域名地址，等其他项），CNAME处填取到的解析值

添加好后复制添加的域名地址

## 服务器端绑定

把复制的域名地址方法服务端绑定。



## TTL

刷新地址



## MX

权重



# GitHub自定义域名绑定

freenom申请域名，dns使用DNSpod第三方管理。

测试 ： github https成功



阿里云申请SSL选择免费型SSL。

验证网站方式选择TXT验证,在DNSpod添加txt记录，对应主机和txt值，根据TTL时间(秒)长短会有延时，txt不会立即生效。

验证通过后下载证书文件，服务器类型选择**其他**。

解压压缩文件，把.key和.pem放到github根目录下。





























