# Docker容器

类似虚拟机

## 查看所有镜像

```
docker images
```

## 搜索镜像

```
docker search <镜像名称>
```

## 创建镜像

```
docker run -it [-p8080:80 -p9092:9092 -p2181:2181..] <镜像名称>:<TAG> bash
```

后台运行:

```
docker run -itd [-p8080:80 -p9092:9092 -p2181:2181..] <镜像名称>:<TAG> bash
```

## 查看运行中镜像

```
docker ps
```

## 查看所有运行过镜像

```
docker ps -a
```

## 删除运行过镜像

```
docker rmi <镜像ID，可以通过docker ps获取>
```

## 镜像复制文件

```
docker cp <源目录> <目标目录>
```

```
docker cp <镜像名称/镜像ID>:/etc/profile ./
```

```
docker cp ./a.txt <镜像名称/镜像ID>:/root
```

## 容器详情

```
docker inspect 容器ID
```

















