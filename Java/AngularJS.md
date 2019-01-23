## 高亮显示

### AngularJS

#### $sce策略

	angularJS 信任策略，防止恶意HTML攻击或JavaScript攻击
	
	trustAsHtml方法，可以把HTML文本转换成HTML效果

#### angularJS过滤器

	一个过滤器只做一种过滤，过滤HTML内容，或者JavaScript内容，防止恶意攻击

#### AngularJS计时任务

注入 $interval  $timeout

$interval	隔指定时间执行一次方法,只执行一次

$timeout	每隔指定时间,就执行一次

创建一个定时器:

	@scope.timer = $interval (fn,方法循环执行间隔毫秒,[执行次数])

终止定时器:

	$interval.cancel(定时器对象$scope.timer)



#### 注解规范

	方法注解
	
		@author	作者
	
		@since		从那个版本添加的这个成员
	
	类注解


			

	

#### Map循环

```javascript
(key（名称随意）,value（名称随意）) in Map变量集合
循环体中可以直接获取key,value内容
```

#### 删除集合元素

```javascript
delete $scope.xxx.xxx[index];		从集合中直接删除索引元素
```

	创建过滤器

```javascript
app.filter('过滤器名称',['$sce',function($sce){
    return function(data 传入内容 ){
        return $sce.trustAsHtml(信任的HTML内容 data);
    }
}])
```

#### ng-bind-html指令

```html
ng-bind-html="内容/HTML原文 | 过滤器名称"
```

#### 



