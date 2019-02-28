# 数据库：

clients2channel		客商和渠道关联表

​	cc_id	渠道id​		

price_baserule		商品基础价格

goods_detail		商品信息

goods				药品信息

pub_dept			公司信息

goods_detail_label	商品标签

clients_channel		销售渠道

pub_clients_managerange	经营范围

goods_giftrule		商品活动

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

#### 客户人员审核

```
客户下单 -> 微信小程序消息提醒业务员 -> 
```

如果订单已经半小时没业务员审单，表示业务员同意

### 订单数量：

订单数量是等订单所有流程走完之后才会生成

```
商品id - 基础表 -
```











