# 数据库：

clients2channel		客商和销售渠道关联表

​	cc_id	渠道id​		

price_baserule		商品基础价格

price_agreerule		商品协议价格

goods_detail		商品信息

​	gd_packnum	拆单后的数量要是这个值的倍数

pub_account		客商信息

​	auto:系统每隔一定时间自动审核,如果没有审核过时会在auto上打上标记,添加到未审核列表,人工审核.审核:运输方式 ,其他

goods				药品信息

pub_dept			公司信息

goods_detail_label	商品标签

clients_channel		销售渠道

pub_clients_managerange	经营范围

goods_giftrule		商品满减满赠规则

pub_address		送货地址表

collect				收藏表

cart					购物车

​	srcod_id
​	srco_id

​	唐山红瓷医院对接借口时使用

lrt_lx_xs_001			历史销售记录

goods_label			商品标签

goods_detail_label	商品标签绑定

salesman_opinion	业务员审核表


CMD和b2b分别维护自己的客商id和业务员id

Orders				订单表		客服审核状态(o_status)

salesman_opinion	业务员审核表

emp_goods2goods	业务员已导入订单

```
id	导入订单id
业务员导入订单记录
```

imporders_cstid_empid	未导入订单

goods_pic			商品图片

browsing_history	历史记录

emp_goodsdict		字典表

transport			业务员运输方式主表

transport_code		业务员运输方式明细		(客户运输方式在CMS中注册时设置了一个默认运输方式)

orders_return		退货信息表

orders_comment	订单评价

pub_clients			客户信息表

stock_agreerule		库存基本策略

gift					赠品信息

goods_group		商品组合表

integral_shop		积分商城表

integral_rule		赠品表

cms_article			文章信息

home_catalog		首页目录,首页分层展示

pub_role			角色

pub_menu			菜单表

pub_feedback		反馈信息

diffprice_group		差价单组

lrt_type				商品大类

custom_iotype		自动审核

​	iotype

​		50		自动审核

​		69		手动审核





客户:

​	一个客户只能购买指定类型药品	

客商:

​	客商下有可能有多个客户账户,通过不同客户账户去买药



### 经营范围（pub_clients_managerange）：

​	用户cstid  货主id(cmpid)  确定经营范围		（一个客户有多个货主情况下能保证正确经营范围）

​	经营范围默认1年到期

​	goods通过managerange绑定经营范围id

​	查询商品时,过滤客商只能看到他自己所属经营范围商品

### 下单:

​	

​	



### 搜索商品:

销售渠道、经营范围



 查询销售渠道 -> (cc_id - cleve)基础价格表 -> 

(gd_id - > gd_id) 商品明细表 -> 商品表 ->

 (sownerid - >ownerid) 部门表 - >pub_dept ->

goods_label ->  goods_detail_label    商品标签/商品标签明细 ->

catalog_label -> 

goods_giftrule满减满赠 -> gift赠品 

pub_clients_managerange 经营范围





### 客商通过货主确认销售渠道：

客商- >货主->多个销售渠道

### 取商品价格

活动价格 - > 协议价格(末次购买价格) -> 基础价格 -> 0

### 商品协议价





### 取商品库存

协议库存 - > 基础库存



### cstid CMS维护id

会定时同步CMS默认收货地址，一般货主收货地址也就一条,CMS默认收货地址

```
AccountService 
	869:show_stock
	879:show_stock_limit
```

### 下单流程：

    代发货：待审核：客服人员审核（如果不同意，参考业务员审核意见对订单修改，并且和用户协商）：
    业务员审核：CMS 流程 ： 客户回执单 ： 回写订单数量(客户实际收到商品的数量)

#### 下单：

写入CMS中时，需要两个字段表示一单：

​	o_no

​	明细id+9000W

后期回写订单状态时也通过这两个值确定一单







#### 客户人员审核

```
客户下单 -> 微信小程序消息提醒业务员 -> 
```

如果订单已经半小时没业务员审单，表示业务员同意,业务员看到订单半小时没人申,直接通过

### 订单数量：

订单数量是等订单所有流程走完之后才会生成

```
商品id - 基础表 -
```

### 取商品价格：

cstid,商品gid,sownerid

```
HttpPostObject.getPriceStore(cstid,g_id,sownerid)
```



三个类型:

​	客户

​	客商

​	业务员

### 商品显示过滤:

销售渠道

  1. 拿到客商所属货主  查询clients2channel

  2. 左连接 price_baserule ,clevel = cc_id

  3. 左连接 goods_detail   gd_id = gd_id

     返回商品结果就是客商可以看见那些商品

### 经营范围

每一个货主在cms中都有一个默认收货地址









# 后台

### 最后一次削价(修改协议价):

订单写进CMS中最后一次修改价格，实际下单价格

只有后台能修改最后一次削价,每天早上后台向前台同步价格

后台修改订单价格



### 渠道管理

#### 渠道管理:

clients_channel表，过滤当前登录人货主

#### 客商管理:

通过销售渠道列出客商信息

pub_clients -> client2channel[当前货主] -> clients_channel

#### 无渠道客商:

pub_clients     	isauth=1

### 商品管理

#### 商品管理

大类列表:查询lrt_type,type=1000

类别列表:查询lrt_type,type=1010

goods  

goods_detail:

​	gd_delete		禁用标记,1:禁用  0:启用

​	issyn			是否同步

#### 上架:

​	跳转广告管理页面		

### 定价策略

#### 基础定价策略

查询商品明细goods_detail 商品goods 基础价格price_baserule 销售渠道clients_channel,条件:基础价格.ownerid=当前用户货主id

#### 协议定价策略

通过当前登录用户所属货主查询 price_agreerule ,分别绑定:goods, goods_detail, pub_clients

添加销售渠道条件时:

​	//过滤货主

​	price_agreerule过滤登录客商所属货主

​	//过滤出当前货主下销售渠道

​	price_agreerule中cstid 和 clients2channel 中 cstid 比对,拿到对应cc_id

​	查询选择的销售渠道(clients_channel.cc_pid)对应子渠道(cc_id),查询结果和cc_id对应

#### 活动定价策略

设置price_activityrule货主为当前登录用户货主

关联(price_activityrule) gd_id on (goods_detail) gd_id 

 goods g_id on goods_detail gd_id

price_activityrule clevel 关联 clients_channel cc_id

//选择销售渠道

clients_channel cc_pid = 选择销售渠道值

### 销售库存

404

#### 协议库存策略

查询stock_agreerule 

​	关联客户信息(pub_clients) 

​	关联goods和goods_detail

### 营销策略

#### 赠品设置

查询gift表

#### 满减满赠规则:

goods_giftrule表,过滤当前登录货主

### 优惠券

查询coupon

### 商品组合

查询good_groups

### 商品专柜

查询goods_special

##  积分商城

### 积分商品

查询integral_shop表

### 积分礼品

查询gift

### 兑换信息

404

## 积分规则

查询integral_rule表

## 内容管理

### 栏目管理

查询cms_channel表

### 文章审核

查询cms_article

### 文章管理

查询cms_article

### 广告管理

查询cms_advert

### 目录管理

查询home_catalog

## 客商管理

### 客商账号

查询pub_account表 通过cstid关联 pub_clients表

## 订单管理

### 订单审核



### 在运订单

查询orders表,type=0(表示正常) 并且 status = 4(表示已发货)

### 请货订单

查询orders,o_type=1(请货订单),

关联pub_account,(o_id->o_accountid)

过滤出业务员开启自动审核订单(auto=1)

过滤订单auto = 0

### 换货订单

查询pub_account(cstid)关联pub_clients

### 历史订单

查询orders,o_status=0或5			已完成/已退货

## 系统管理

### 部门管理

查询dept

### 人员管理

查询pub_emp (roleid/r_id)关联pub_role

关联 pub_dept	(deptid/deptid)



### 角色管理

查询pub_role

### 资源管理

查询pub_menu

### 日志管理

sys_log_(当前日期yyyy-MM-dd)

## 差价单

### 差价单组

查询diffprice_group

# 同步服务器

同步名称 CMS同步到 b2b后台

同步名称 task  b2b后台 同步到 前台



## 协议价同步：

协议价有两条记录时，取最高的价格





# orders:

auto	在自动审核出错后,auto会为1表示交给人工审核



### 销售渠道

控制商品价格/库存,一个销售渠道可以多个客户使用,一个客户也可以由多个销售渠道.

# ====标记

商业分销下命名规则

内销部

医院服务

基层医疗







### 经营范围

经营范围控制销售类型,一个经营范围对应一个客户,每个客户有自己的经营范围



## 服务器

​		15.234		既能连前台，也能连后台

​		15.250		消息服务器 客户端

​		15.231		消息服务器 服务端

前台:

​	Client	一直向后台服务器发送请求		

ZJ:

​	

积分商城:

​	客户手动兑换，兑换后由业务员看后送过去

同步时间:

​	早上5点

​	晚上11点



定价策略:

​	组合价格	表示一组商品包装起来卖，如果买只能买一组。

销售库存-协议库存策略：





# 整体流程:

前台：浏览商品,商品下单,订单审核,积分商城,账户管理

后台：接受订单信息,向前台同步商品价格,渠道管理,客商管理



同步程序:

​	同步CMS订单状态,通过b2b中cstid



CMS 

​	CMS订单通过后,临时在库存中减去对应订单商品数量,把订单写到WMS,

​	

WMS 库存

​	逻辑库:

​		把一些医院划分到一个逻辑库,这个逻辑库里指定时间内只能卖指定数量药品.

​	类似商品分组



TMS 物流系统

​	根据区域不同,客户需求不同.派送不同人员/不同车辆安排送货

​	按地区划分





































