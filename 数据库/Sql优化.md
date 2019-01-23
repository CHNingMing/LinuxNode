# SQL优化
	针对where和order by 涉及的列上建立索引
	尽量在经常用到的字段上添加默认值，不能在字段上用NULL
	尽量避免使用不等于操作符
	尽量少使用or
	能用BETWEEN就不用in
	
	