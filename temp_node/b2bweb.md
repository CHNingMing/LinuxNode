# 数据库：

clients2channel		客商和销售渠道关联表

​	cc_id	渠道id​		

price_baserule		商品基础价格

price_agreerule		商品协议价格

goods_detail		商品信息

goods				药品信息

pub_dept			公司信息

goods_detail_label	商品标签

clients_channel		销售渠道

pub_clients_managerange	经营范围

goods_giftrule		商品满减满赠规则

pub_address		送货地址表

collect				收藏表

cart					购物车

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

客户:

​	

客商:

​	客商下有可能有多个客户,通过不同客户取买药



### 经营范围（pub_clients_managerange）：

​	用户cstid  货主id(cmpid)  确定经营范围		（一个客户有多个货主情况下能保证正确经营范围）

​	经营范围默认1年到期

​	goods通过managerange绑定经营范围id

### 客商通过货主确认销售渠道：

客商- >货主->多个销售渠道

### cstid CMS维护id

会定时同步CMS默认收货地址，一般货主收货地址也就一条,CMS默认收货地址

```
AccountService 
	869:show_stock
	879:show_stock_limit
```

### 下单流程：

    代发货：待审核：客服人员审核（如果不同意参考业务员审核意见对订单修改，并且和用户协商）：业务员审核：CMS 流程 ： 客户回执单 ： 订单数量(客户实际收到商品的数量)

#### 下单：

洽商->	通过地址传入选入的商品ip		**,号分割**  







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











# 后台

### 最后一次削价:

订单写进CMS中最后一次修改价格，实际下单价格

只有后台能修改价格,每天早上后台向前台同步价格

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





## 服务器

​		15.234			既能连前台，也能连后台

​		15.250		消息服务器

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





















