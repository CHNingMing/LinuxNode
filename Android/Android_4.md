# 组件

## ListView

### ListView设置数据来源:

#### XML设置:

android:entries="@array/[arrayname]"

#### Java设置:

ListView显示项:数据源(数据库/xml[arrays] - > xxAdapter -> ListView展示数据

getResources().getStringArray(**R.array.names**)		//获取xml中配置的array数组

```java
//..
ListView listView = findViewById(R.id.list_planitem);
ArrayAdapter<String> arrayAdapter = new ArrayAdapter<String>(MainActivity.this,R.layout.support_simple_spinner_dropdown_item,arrs);
listView.setAdapter(arrayAdapter);
```







