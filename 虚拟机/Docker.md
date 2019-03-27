# Docker

下载:https://download.docker.com/linux/debian/dists/stretch/pool/stable/amd64/

其他linux版本的docker,切换url获取

下载:

​	docker-ce_17.03.0~ce-0~debian-stretch_amd64.deb                                       2018-06-08 17:51:26 20.3 MiB

安装成功,直接dpkg安装

## Docker设置镜像位置

/etc/docker/daemon.json  , 没有daemon.json时创建

写入:

```json
{
  "registry-mirrors": ["http://hub-mirror.c.163.com"]
}
```



## 安装Centos镜像

参考 : https://blog.csdn.net/haoxiaoyan/article/details/79755345

## docker 搜索镜像

```shell
docker search 名称
```

## 安装镜像

```shel
docker pull centos
```

centos : 安装镜像名

### 列出下载镜像

```
docker images
```

## 删除镜像

```
docker rmi 镜像 id
```

  删除时报错:

Error response from daemon: conflict: unable to delete 6fae60ef3446 (must be

添加-f参数:

```
docker rmi -f  镜像id
```



### 创建一个容器

```
docker run --privileged --cap-add SYS_ADMIN -e container=docker -it --name my_centos -p 80:8080  -d  --restart=always centos:7 /usr/sbin/init  
```

--privileged 指定容器是否是特权容器。这里开启特权模式。
--cap-add SYS_ADMIN 添加系统的权限。不然，系统很多功能都用不了的。
-e container=docker 设置容器的类型。
-it 启动互动模式。
/usr/sbin/init  初始容器里的CENTOS。

### 容器列表

```shell
docker ps -a
```

-a : 列出所有容器列表

否则只列出运行容器列表

CONTAINER ID : 每个容器唯一标示

IMAGE	: 	使用镜像

COMMAND : 运行时执行命令

CREATED : 创建时间

PORTS	: 	容器内端口映射宿主环境端口



### 进入容器

```shell
docker exec -it my_centos /bin/bash
```

### 运行容器

```shell
docker run -i -t centos:7
```

-i :  允许系统和容器交互

-t : 允许当前系统对容器标准输入(stdin)

centos:7 :  已有容器名



### 后台运行容器

```shell
docker run -d centos:7 /bin/bash -c "echo hello_world"
```

-d : (display)	后台运行

/bin/bash -c "echo hello_world"		: 	属于执行命令区域,实际执行:bash -c "echo hello_world"



#### 查看后台容器输出内容:

运行后会返回一个容器id,也可以通过docker ps -a 列出所有容器,通过CONTAINER ID 

```shell
docker logs 容器id
```

### 查看容器进程

docker top 容器id

### 退出容器

Ctrl + D / exit



