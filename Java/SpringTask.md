# SpringTask

类似Quartz任务调度,定时完成任务

Task在cron表达式中没有年的概念

### 导入依赖:

```


```

### 配置文件:

```xml
<~-- 包扫描 -->

<!-- 开启task注解驱动 -->    
<task:annotation-driven/>
```

### 配置注解:

```
方法上定义:
	@Scheduled(cron="时间规则表达式")	表示在指定时间时[重复]执行这个方法
	
```

### cron时间表达式

	是一个规范,Quartz和Task都使用这个表达式

#### 表达式:

	秒	分钟	小时	一个月中的某一天	 月	星期中的某一天	[年]
	
	*	*		*		*				*		*			[*]
	
	?	 ?符号,只能出现在  **月中的某一天 或者 星期中的某一天**,有且只能出现一次
	
	-	值-值 表示一个时间范围开始执行  ,没个时间单位执行一次
	
	/	num1/num2	num1后开始执行,没间隔num2时,在执行一次
	
	,	值,值,值...	 多个没有规则的时间时使用
	
	L	num1L		只能在 月中的某一天 或者 星期中的某一天 出现,**第num1月**或者**第num1星期**的**最后一天**执行
	
	W	num1(指定日期)W		有效工作日执行,如果指定的日期是星期六或者星球日,就会推到下星期一执行,如果是工作日,就正常执行
	
	LW	num1LW,第num1星期 或者 第num1个月的最后一天执行
	
	#	num1#num2 只能出现在月中的某一天,每个月的第num2的星期num1
	
	表达式和表达式之间可以混合使用,表达式是通过空格区分域

# MavenProfile

把项目分成**开发环境**和**部署环境**两部分

通过*.properties区分,maven通过打包时指定参数来选择那个***.propertie文件

### 步骤:

#### 创建filters文件夹

创建生产环环境和部署环境 *.properties 

配置生产环境和部署环境properties配置文件

```xml
<profiles>
	<profile>
        <!-- 环境唯一标识 -->
		<id>dev</id>
        <!-- 替换的内容 -->
        <properties>
            <env>dev</env>
        </properties>
        <!-- 如果不指定固定的profile,就是用当前这个profile -->
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
	</profile>
    <profile>
        <!-- profile可以写多个 -->
    </profile>
    
</profiles>
```

#### 开发环境/上线环境 打包

	package -P pro		生产环境
	
	package -P dev		上线环境

### MongoDB简介

	查询语言非常强大

	支持多个编程语言

MongoDB没有事物

主要适合场景:

	数据价值不高,并且还有大量数据需要存

概念:

	数据库----集合(表)----文档(行)

	

	







