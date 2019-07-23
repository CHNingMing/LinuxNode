





## 去掉顶部Bar

1.打开android:theme指向的样式

2.在样式中添加:

```xml
<item name="windowNoTitle">true</item>
```

或者修改样式继承属性:

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
```

Theme.AppCompat.Light.NoActionBar 内部样式里就设置了\<item name="windowNoTitle">true\</item>



