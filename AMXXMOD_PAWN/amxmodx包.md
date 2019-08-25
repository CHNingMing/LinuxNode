

## 获取武器

返回武器id，详细文档：amxconst.inc    例如：AK47     #define CSW_AK47		28

## int get_user_weapon

获取当前武器

```
new currweap = get_user_weapon(id)
```





## get_user_weapons(id,weaps,0)

获取当期背包武器，获取的是武器ID

```
new currweaps[32]
get_user_weapons(id,currweaps,0)
//最后一个参数一般都是0

```



## register_clcmd

监听CS客户端命令方法。执行指定命令后，调用回调。

```c
//注册一个方法
register_clcmd("say hello","callback_hello")
public callback_hello(id){
   client_print(id,print_chat,"hello pawn amxx mod!")
}
```

## float cs_get_user_money

获取玩家金钱数量

```
new playermoney = cs_get_user_money(id)
```



## register_even

监听指定事件

### CurWeapon

切换武器时触发

```c

register_even("CurWeapon"，“callbackFunc”,"be","1=1")
public callbackFunc(){
    //....
}

```







