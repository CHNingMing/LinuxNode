# 监听各种事件包

#include <hamsandwich>

## 注册事件

pev：事件触发之前执行      实际值：0

post:事件触发之后执行		实际值：1

```
public plugin_init(){
	RegisterHam(事件,触发实体,触发方法,pev/post)
}
```

具体注册事件查看：fakemeta_const文件

## 触发实体

### Ham_TakeDamage

收到伤害后触发

调用方法传入参数：

```
id,
idinflictor,
idattacker,
damage,			收到伤害值
damagebits
```

### Ham_AddPlayerItem

仓库中添加武器时触发

```c
RegisterHam(Ham_AddPlayerItem,"player","addweap")
public addweap(id,idother){
	
	client_print(id,print_chat,"add weap!!!!")
}
```

### Ham_TakeDamage

受到伤害时触发

```
RegisterHam(Ham_TakeDamage,"player","damageEven")
public damageEven(id,idinflictor,idattacker,damage,damagebits){
	client_print(id,print_chat,"伤害 %f ",damage)
}
```

### Ham_Touch

玩家实体碰触到任何武器，触发

```
RegisterHam(Ham_Touch,"player","touchentity")
public touchentity(id,idother){
	client_print(id,print_chat,"touch !!!")
}
```

idother : 应该是触碰的实体，待验证

### Ham_Item_Deploy

切换指定武器触发事件

```c
RegisterHam(Ham_Item_Deploy,"weapon_ak47","switch_ak47")
public switch_ak47(weaponEntity){
	
}
```

weaponEntity:武器实体，切记！不是玩家ID

武器列表：

{ "", "weapon_p228", "", "weapon_scout", "weapon_hegrenade", "weapon_xm1014", "weapon_c4", "weapon_mac10", "weapon_aug", "weapon_smokegrenade",
"weapon_elite", "weapon_fiveseven", "weapon_ump45", "weapon_sg550", "weapon_galil", "weapon_famas", "weapon_usp", "weapon_glock18", "weapon_awp", "weapon_mp5navy", "weapon_m249",
"weapon_m3", "weapon_m4a1", "weapon_tmp", "weapon_g3sg1", "weapon_flashbang", "weapon_deagle", "weapon_sg552", "weapon_ak47", "weapon_knife","weapon_p90" }

### FM_PlayerPreThink

重点！！！

玩家思考事件，也可以说是整个游戏内，时刻刷新插件，并且不会卡死，类似while(true)，但不是，至少不会卡死

```c
register_forward(FM_PlayerPreThink,"think")
public think(id){
	
}
```



## 手动触发事件

### ExecuteHamB

ExecuteHamB(触发函数,目标对象,参数...)

```
ExecuteHamB(Ham_CS_RoundRespawn, id)
```

Ham_CS_RoundRespawn,玩家死亡时，复活事件。手动触发复活事件让玩家复活



# 阻止事件触发

在插件方法最后return PLUGIN_HANDLED，可以阻断原有事件执行

return PLUGIN_HANDLED的意思是结束一系列动作执行。











