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

## ListView自定义项



1.创建一个普通视图,表示集合项样式

2.创建一个类,继承ArrayAdapter类,重写构造方法和getView方法,通过getiView方法动态设置控件属性达到自定义每一个项样式效果

通过getView方法控制item项

```java
    
	public PlanItemAdapter( Context context, int resource,  List<PlanItem> objects) {
        super(context, resource, objects);
    }

    @NonNull
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        PlanItem planItem = (PlanItem) getItem(position);
        View view = LayoutInflater.from(getContext()).inflate(R.layout.activity_item_layout,null);
        TextView textView = view.findViewById(R.id.t_plan_state);
        Button button = view.findViewById(R.id.btn_ok);
        ImageView imageView = view.findViewById(R.id.img_head);
        textView.setText(planItem.getPlan_name());
        button.setText(planItem.getPlan_id()+"");
        imageView.setImageDrawable(view.getResources().getDrawable(R.drawable.smile_fill));

        return view;
    }
```

List\<PlanItem>				集合类型

(PlanItem) getItem(position)	通过构造设置的集合类型,可以直接这样获取便利的每一个项

LayoutInflater.from(getContext()).inflate(R.layout.activity_item_layout,null) 表示在当前视图实例化一个R.layout.activity_item_layout  View对象 activity_item_layout

activity_item_layout			要载入的视图

R.drawable.smile_fill			图片资源文件







## ImageView

图片显示

尽量把图片文件放在drawable文件夹下

### xml中设置

app:srcCompat="@drawable/文件名称"

### java中设置

获取ImageView对象,调用setImageDrawable(Drawable )方法设置图片

Drawable对象中存储图片信息,Drawable对象通过view.getResource.getDrawable(R.drawable.xxx)获取

## EditText

文本输入框

## 自定义组件

1. 创建类继承View子类 (FrameLayout/ConstraintLayout[约束布局])

   ​	FrameLayout：通过layout_marginXxx控制控件位置

   ​	ConstraintLayout： 通过定位控制控件位置

   ​	继承以上两个类后，创建两个构造

   ```java
   //自定义控件属性和属性get/set方法，后期在创建这个组件时动态设置
   
   //必须，自定义属性会调用这个构造
   public classname(Context context, AttributeSet attrs) {
           super(context, attrs);
   }
   public classname(@NonNull Context context) {
           super(context);
   }
   ```

2. 在values静态资源中，创建attr xml文件，声明控件属性

   ```xml
   <resources>
       <!-- 自定义公共属性 -->
       <attr name="" format="" />
       <!-- 指定控件属性 -->
       <declare-styleable name="自定义控件类名">
           <attr name="属性" format="类型" />
       </declare-styleable>
   </resources>
   
   ```

    待验证：添加 format表示创建一个特有属性，不添加format表示使用父类继承属性

3. 在布局文件中正常通过 类名/全类 名使用这个控件

   ​	可以通过这个控件将一部分控件包裹起来组成一个整体，给这自定义控件声明个别属性，可以通过这个属性取到一部分控件。







# 问题：

## onItemClick点击没效果

是因为onItemClick项中有其他可交互控件，如：checkbox，button...挡住了item项，需要在这些控件添加：

```xml
android:descendantFocusability="blocksDescendants"
```

如果这些组件有一个统一的父容器包裹，直接在包裹容器上添加。

## 组件属性(Attr):

### 组件 包裹 组件时，父组件和子组件属性名不能重复