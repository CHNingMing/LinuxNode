Android 把所有XML资源看成一个类型,通过标签名定位是什么类型资源.

## String-array

```xml
<string-array name="items1">
    <item>1</item>
    <item>2</item>
    <item>30</item>
</string-array>
```

可以和Spinner列表配合.

```xml
    <Spinner
        android:id="@+id/sp_planType"
        android:layout_width="120dp"
        android:layout_height="wrap_content"
        app:layout_constraintTop_toTopOf="@+id/t_waitPlan"
        app:layout_constraintLeft_toRightOf="@+id/t_waitPlan"
        android:layout_marginLeft="20dp"
             <!-- 设置 -->
        android:entries="@array/items1"
        />
```

Java中获取:

```java
Resources res = getResources();
String[] arr_plantype = res.getStringArray(R.array.items1);
```











