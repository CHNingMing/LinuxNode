# fakemeta

可以修改游戏中大部分数据。

主要方法:

## pev

获取指定数据

pev(id,获取数据名称,预留容器)

## set_pev

设置指定数据

set_pev(id,设置数据名称,值)





# 事件

## FM_UpdateClientData

类似玩家在思考时调用效果，也是在整个游戏中频繁执行。

```
register_forward(FM_UpdateClientData,"funFM_UpdateClientData",1)
public funFM_UpdateClientData(id,sendweapons,cd_handle){
	
}
```

















