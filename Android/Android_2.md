# 创建消息对话框

## 步骤

1.窗口正常打开

2.设置打开窗口主题为消息对话框



## 编辑AndroidManifest.xml

在指定Activivy添加一个theme属性

```xml
<activivy //... android:theme="@style/Theme.AppCompat.Dialog" ></activivy>

```



### onSaveInstanceState(Bundle)

垃圾回收机制回收前调用方法,stop的活动在内存不足时会销毁,销毁后用户输入的数据就会消失,一般用此方法存储用户输入的临时数据,在通过 onCreate方法赋值

利用传入的Bundle对象可以存储一些临时数据

### Bundle

putString(key,object);		//添加一个字符串数据

putInt(key,int);				//添加一个数字

put的数据在窗口创建方法(onCreate)中传入的Bundle对象中直接可以获取



# 活动启动模式

## standard

每次启动都会创建新实例

## singleTop

重复请求页面时,如果发现**栈顶页**就是要启动的页面,则不会创建新实例,直接引用栈顶页

## singleTask

整个应用中,这个活动只会被创建一次,请求页面时查找整个应用

## singleInstance

单独用一个栈管理这个活动,和正常其他的栈区分开.

这样做是因为其他程序在调用本程序某个singleInstance窗口时,保证这个活动只会创建一次.这样不同程序调用这个活动时都不会重新创建.可以通过getTaskId验证singleInstance模式活动和普通模式活动是否在同一栈中

### getTaskId

int getTaskId()

获取当前栈id

### 杀掉当前进程

android.os.Process.killProcess(android.os.Process.myPid());

#### 获取当前进程ID

android.os.Process.myPid()

# 组件

## visibility控制组件是否可见



### xml控制

gone:隐藏

visiable:显示

invisible:隐藏,占用组件位置

android:visibility=""

### 程序控制

组件都有一个setVisibility(int)方法,设置显示/隐藏

View.GONE		隐藏

View.VISIABLE	显示

View.INVISIBLE	隐藏,位置保留



### int getVisibility()

判断组件是否可见

返回值:

​	View.GONE

​	View.VISIABLE

​	View/INVISIBLE



# 布局

在活动xml中,android:orientation属性设置布局.

## 线性布局

vertical 		竖向布局

horizontal	横向布局













