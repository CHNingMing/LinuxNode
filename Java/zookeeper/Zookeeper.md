# zookeeper

主要用来管理分布式程序间通信。

存储结构类似文件树,有目录,有文件。

## 节点类型

EPHEMERAL: 临时节点,客户端断开连接后,节点消失

PERSISTENT: (默认): 持久节点,除主动删除外,不会消失

PERSISTENT_SEQUENTIAL: 持久节点,自动追加序号

EPHEMERAL_SEQUENTIAL: 临时阶段,自动追加序号

## zookeeper启动

```shell
bin/zkServer.sh
```













