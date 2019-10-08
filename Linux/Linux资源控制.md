# cgroup

控制CPU，内存，IO等..

针对某个进程PID，限制资源使用

cgroup分组动态管理资源信息。在指定位置创建文件夹后，新创建文件夹内自动生成与之相关配置文件。

## 安装Cgroup

debian:cgroup-bin

## 限制CPU使用

### 创建一个管理组

```shell
cd /sys/fs/cgroup/cpu,cpuacct
mkdir cpu_test
```

### 设置限制CPU使用大小

编辑/sys/fs/cgroup/cpu,cpuacct/cpu_test/cpu.cfs_quota_us

10000大概时CPU使用率10%

-1 表示不控制

### 添加进程PID控制

编辑tasks文件，添加管理进程PID

可以通过TOP动态查看设置前和设置后进程变化











# memtester

辅助测试工具，主要测试内存，在测试过程中CPU也会到100%，也可测试控制CPU使用。









