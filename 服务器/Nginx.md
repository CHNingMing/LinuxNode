# Nginx

## windows:

### 启动

```cmd
start nginx.exe
```

### 退出

```
nginx.exe -s quit
```

### 热更新

```
nginx.exe -s reload
```

### location

匹配URL，

#### 精确匹配

```
location = /abc/a.txt {
	# ...
}
```

#### alias 和 root

```
# 实际找文件路径为 /var/image/ 下找文件。
location = /img/ {
	alias	/var/image;
}
# 实际找路径为 /var/image/img/ 下找文件。
location = /img/ {
	root	/var/image;
}
```

#### autoindex on; 

列出当前目录

```

location = /img/ {
	autoindex on; 
	alias	/var/image;
}
```



### rewrite





# 坑:

## 更新配置文件总是不生效:

如果修改配置文件后总是不生效，可以看下系统中是否启动了多个nginx，如果启动多个, 在访问url时访问的是第一次启动的nginx, 而在热更新的时候，更新的是最后一次启动的nginx。





