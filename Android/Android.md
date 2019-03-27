# Android 热点主机 ip:192.168.43.1

# Andrpid

## AndroidManifests.xml

查看activity标签 android:name=".主程序名称"

打开主程序

## Activity

表示程序中的一个活动

### 设置主活动

程序启动时先执行的活动

```xml
<intent-filter>
    <action android:name="android.intent.action.MAIN"></action>
    <category android:name="android.intent.category.LAUNCHER"></category>
</intent-filter>
```

### 方法

#### bool isFinishing

判断当前活动是否销毁,等待回收状态true

### Toast消习提示





## R记录项目结构

### R.layout	页面

存储layout.xml视图文件名称,表示一个安卓界面

layouo在 res/layout下,R.layout.*.xml,回去res/layout下查找xml视图文件

### R.id.xx

记录定义元素 @+id/xx 名称内容





## 整体结构:

## res

drawable-*		图片文件

layout			界面文件

mipmap-*		图标文件,多个mipmap是为了适应不同设备

values			字符串、颜色、样式

​	colors.xml	颜色值保存

​	string.xml	字符串

​	style.xml	样式

## 取values某个值时只需要:

Java

​	R.string.(定义name名)

​		直接取出,字符部分会变成数字,需要用**this**/**XXXActivity**.getString(R.string.xx)转换成正常字母

​	R.style.(定义name名)

XML

​	@string/(定义name名)

​	@style/(定义name名)

# app外层build.gradle

## jcenter()

使android项目可以引入jcenter库插件

```java
    dependencies {
        classpath 'com.android.tools.build:gradle:3.0.1'
        

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
```

## com.android.tools.build:gradle:3.0.1

gradle是构建项目工具

## findViewById查找元素

findViewById(int id);

id一般通过R.id.xx(组件id名称)获取

为null时:

查看findViewById是不是在setContentView方法之前,因为没有绘制时没法取元素

调用错了视图对象,findViewById是View类的方法,用执行视图(View)对象调findViewById

## Button组件

设置组件单击事件:

```java
Button btn = (Button)findViewById(R.id.xxx);
btn.setOnClickListener(new View.onClickListener(){
    @Override
    public void onClick(View view) {
        //...被单击动作
    }
});
```

保证获取的btn不为null

# AppCompatActivity

一般活动继承AppCompatActivity,内部保函多个事件.

onOptionsItemSelected		: 选择菜单时触发

onCreateOptionsMenu		: 创建菜单时触发











## layout

对应安卓活动视图,以xml形式绘制视图

### button按钮:

```xml
<button  
        android:id="@+id/btn_hello"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        />
```

match_parent:匹配父级元素宽/高

wrap_content:根据文本宽高



# Intent

Intent 是Android 程序中各组件之间通信的中间件.

Intent 分为显示 和 隐式两种类型:

## 跳转窗口(显示类型)

Intent Intent = new Intent(当前活动,目标活动.class);

startActivity(Intent);//真正打开窗口方法,不接受返回值

### startActivityForResult跳转窗口方法,接受返回值

startActivityForResult(Intent,Int(请求码))

在打开的窗口关闭时(并且设置了setResult方法,自动触发onActivityResult.

### onActivityResult(int ,int ,Intent)

1,请求码

2,返回码	正确/取消...

3,返回Intent对象 

通过Intent对象,可以取到打开页面put的值

接受打开页面的返回值

### setResult(int,Intent)

1,设置返回状态 Result_OK 成功,Result_CANCELED

2,返回Intent对象

设置返回数据,用于调用onActivityResult方法打开的窗口

```java
Intent intent = new Intent();

intent.putxx		//添加一个或多个数据

...
//设置返回值 
    setResult();
```







## 跳转窗口(隐式类型)

### AndroidManifest中配置activity

```xml

<activity android:name=".Main2Activity">
    <intent-filter>
        <!-- 活动窗口 -->
        <action android:name="com.example.root.helloworld.Main2Activity" />
        <!-- 默认category,默认可以不用添加到action中 -->
        <category android:name="android.intent.category.DEFAULT" />
        <!-- 自定义category,调用时必须保证添加到activity中 -->
        <category android:name="com.test" />
    </intent-filter>
</activity>

```

上述配置调用时必须:

```java

Intent intent = new Intent("com.example.root.helloworld.Main2Activity");
intent.addCategory("com.test");//没有时会报错,必须保证Category和xml中 category数量,名称一致

```

## 接受打开活动参数

### getIntent() 

获取请求Intent

打开窗口时给Intent添加数据(putExtra)

```java
//打开窗口
intent.putExtra("name","zhangsan");
startActivity(intent);
```

```java
//接受参数
Intent intent = getIntent();
intent.getStringExtra("name");

```

# 活动生命周期

活动:Activity

每一个活动都是一个任务,Android通过Task管理任务.

Task是一个**后进先出**的栈,创建互动是就是入栈操作,系统总显示栈顶活动.

当按返回时,就是栈顶窗口出栈操作.

## 活动四种状态

栈:Task,活动管理器,后进先出

### 运行状态

活动(窗口)是可见的,不会被垃圾回收机制回收

### 暂停状态

**活动不在栈顶**,并且是可见的时候,一般是在活动上打开一个弹窗的时候.

### 停止状态

**活动在栈中**,并且完全不可见时,垃圾回收机制会等到其他地方需要内存时,回收

### 销毁状态

**活动不在栈中**,垃圾回收机制会随机回收.

# 状态对应事件

## onCreate

第一次被创建时调用

## onStart

在活动处于栈顶,完全可见时调用

## onResume

在获得焦点,可以与用户交互时调用

## onPause

当前窗口失去焦点时,意味着不能和用户交互时.

切换到其他窗口,或者弹出交互式对话框时调用

## onStop

在窗口完全不可见时调用,弹出交互式对话框时不会触发这个方法,因为是完全不可见时才会调用

## onDestroy

 在活动销毁之前调用

## onRestart

在窗口重新被激活时调用



## 三大类:

生存期:onCreate - > onDestroy

可见期:onStart - > onStop

前台生存期:onResume - > onPause



# Android日志打印级别

Log.v:	verbose	打印意义最小的日志信息

Log.d	debug	打印一些调试信息

Log.i	into		打印一些比较重要数据

Log.w	waring	警告信息	

Log.e	error	错误信息



Log.d(一般是当前类名,"消息内容")



# android studio总结

尽量sdk通过idea自动装



### 第一次打开出现:

```
Error:Execution failed for task ':app:preDebugAndroidTestBuild
```

从新编译试试



调试时:

关闭MIUI优化

打开usb调试

允许安装应用

关闭安全模式



必须保证编译sdk和调试机sdk一致,每个android都有一个编号如果不一致会提示















