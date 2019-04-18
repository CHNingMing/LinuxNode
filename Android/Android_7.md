# 组件事件

## setOnLongClickListener

默认为长按2秒触发事件

重写的onLongClick方法中，返回一个布尔值:

​	ture时，阻断click方法,触摸抬起后不会触发click事件

​	false当长按控件触摸抬起时,触发click事件

因为click事件是 按下 - 抬起  才会触发。



## 组件触发事件传入VIew

组件触发事件后都会传一个VIew对象，这个View对象中，只能获取触发事件组件对象，其他获取都是NULL。









