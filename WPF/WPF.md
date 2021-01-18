# WPF

## 文件结构

### app.xaml

1. 设置全局要重复用的东西(静态资源、对象)

2. 设置启动窗口入口

3. 设置local:标签命名空间

### MainWindow.xaml

默认启动窗口

## 标签

### x名称空间

#### x:Class

制定一个类，告诉XAML编译器将XAML标签编译结果和后台那个类合并

后台和现实页面绑定，后台可以直接使用展示页面内元素，展示页面内控件事件也写在这个后台类中

#### x:ClassModifier

指定类访问级别

#### x:Name

指定控件名称，在后台类中可以直接访问

#### x:FieldMotifier

制定空间访问级别

#### x:Key

制定标签全局位置ID，后台通过this.findResource(空间ID)直接查到

#### x:Shared

x:Shared bool类型，默认为true

在windows.resouces中声明的重复使用的变量，默认不管获取多少次，引用的都是同一个变量

为flase时，每次获取都是获取变量的一个副本

### 名称空间中标签

#### x:Type

可以指定一个类型

```xml
<local:ClassA TypeA="{x:Type TypeName=local:ClassA}"></local:ClassA>
```

ClassA: 自定义类

TypeA: ClassA类下的一个字段，类型为Type

#### x:Null

制定一个属性为null

```xml
<local:ClassA TypeA="{x:Null}"></local:ClassA>
```

TypeA 属性就变成了NULL

#### x:Array

给List属性添加集合

```xml
<local:ClassA>
    <ClassA.StrList>
        <x:Array Type="sys:String">
            <sys:String>A</sys:String>
            <sys:String>B</sys:String>
            <sys:String>C</sys:String>
        </x:Array>
    </ClassA.StrList>
</local:ClassA>

```

给ClassA对象下的`List<String>`类型的StrList变量添加元素

#### x:Static

访问类的静态变量

`x:Static local:ClassA.STATIC_STR`

ClassA.STATIC_STR 为静态变量

```xml
<local:ClassA StringA="{x:Static local:ClassA.STATIC_STR}"></local:ClassA>
```

## 控件与布局

### 控件分类

1. 布局控件

   可以容纳多个控件的容器,Grid、StackPanel、DockPanel等控件

2. 内容控件

   只能容纳一个控件的容器，Window、Button等控件

3. 带标题的内容控件

   内容控件 添加了一个标题,如 GroupBox、TabItem等

4. 条目控件

   可以显示一列数据,这列数据的数据类型相同,如ListBoxComboBox等

5. 带标题条目控件

   条目控件 加了一个标题

6. 特殊内容控件

   TextBox容纳一个字符串、TextBlock可以容纳自由格式文本、Image可以容纳图片等

### 布局

#### Grid

表格，自定义行、列，行高、列高调整控件布局

```xml
<Grid>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto"></ColumnDefinition>
            <ColumnDefinition Width="*"></ColumnDefinition>
            <ColumnDefinition Width="80"></ColumnDefinition>
            <ColumnDefinition Width="4"></ColumnDefinition>
            <ColumnDefinition Width="80"></ColumnDefinition>
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition Height="20"></RowDefinition>
            <RowDefinition Height="1*"></RowDefinition>
            <RowDefinition Height="20"></RowDefinition>
        </Grid.RowDefinitions>
        <TextBlock Text="请选择您的部门并留言:"></TextBlock>
        <ComboBox Grid.Column="1" Grid.Row="0" Grid.ColumnSpan="4" />
        <TextBox Grid.Row="1" Grid.ColumnSpan="5" Text="编辑框内容" BorderBrush="Black"></TextBox>
        <Button Grid.Column="2" Grid.Row="2">提交</Button>
        <Button Grid.Column="2" Grid.Row="2">提交1</Button>
        <Button Grid.Column="4" Grid.Row="2">重置</Button>
</Grid>
```

1. Grid类型下有两个属性: ColumnDefinitions、RowDefinitions,分别代表行和列，和HTML不同的是，行跟列是分开定义的
2. 行中可以定义每一行的行高,列中可以定义每一列的宽
3. 数值可以是
   1. Auto: 自动,一般设置自动后会设置MinWidth/MaxWidth/MinHeight/MaxHeight
   2. x*: 按比例
   3. x: 绝对值px
4. Grid中的每一个控件，应都设置Grid.Column和Grid.Row属性，表示这个控件在第几行、第几列，默认在0行0列
5. 通过Grid.ColumnSpan横向合并列，通过Grid.RowSpan纵向合并行



#### StackPanel

栈式面板，可以把控件水平或垂直排成一条线，当移除一个元素后，后面的元素会填充空缺

1. Orientation 内部元素是横向累积还是纵向累积
   1. Horizontal 横向
   2. Vertical 纵向(默认)
2. HorizontalAlignment 内部元素横向累积时，对齐方式
   1. Left、Center、Right、Stretch
3. VerticalAlignment 内部元素纵向累积时，对其方式
   1. Left、Center、Right、Stretch

```xml
<StackPanel Margin="10" VerticalAlignment="Center">
        <CheckBox Content="A. 我是A" />
        <CheckBox Content="B. 我是B" />
        <CheckBox Content="C. 我是C" />
        <CheckBox Content="D. 我是D" />
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right" Margin="10">
            <Button >取消</Button>
            <Button >确定</Button>
        </StackPanel>
</StackPanel>
```



#### Canvas

画布，内部元素可以以像素为单位绝对坐标定位，类似WinForm方式控件布局

```xml
<Canvas>
	<TextBlock Canvas.Right="20" Canvas.Top="20">Hello </TextBlock>
    
</Canvas>
```

1. Canvas.Right 设置距右距离
2. Canvas.Top 设置距上距离
3. Canvas.Left 设置距左距离
4. Canvas.Bottom 设置距下距离



#### DockPanel

泊靠式面板，内部元素可以选择泊靠方向

DockPanel中每一个元素都会附上DockPanel.Dock属性，最后一个控件不用设置DockPanel.Dock属性，DockPanel会自动把剩余部分填满

1. DockPanel.Dock
   1. Left、Top、Right、Bottom

```xml
<DockPanel>
    <TextBox BorderBrush="Red" DockPanel.Dock="Top" Height="50">TOP</TextBox>
    <TextBox BorderBrush="Red" DockPanel.Dock="Left" Width="60">LEFT</TextBox>
    <TextBox BorderBrush="Red" >Center</TextBox>
</DockPanel>
```

**注意**: DockPanel中从上往下排，最后一个控件DockPanel.Dock属性无效，默认为居中



#### WrapPanel

自动折行面板，内部元素在排满一行后，能自动折行

```xml
<WrapPanel>
    <Button Width="90">A</Button>
    <Button Width="90">A</Button>
    <Button Width="90">A</Button>
    <Button Width="90">A</Button>
    <Button Width="90">A</Button>
    <Button Width="90">A</Button>
</WrapPanel>
```



### 控件重叠被覆盖时

1. 隐藏上层控件

   1. Visibility = “Hidden”

2. 调整上层控件层数

   1. Opacity = “层数”

      层数越高，越接近最终显示效果

   

## WPF数据绑定

对象-控件之间数据双向绑定、两个控件之间双向绑定。

变量(基本类型)-控件之间数据双向绑定

两方数据绑定后，默认有一方值改变，都会同步到另一方

对象-控件之前双向绑定时，只能让对象一个属性和控件值绑定上

1. 要使用数据绑定，数据实体必须实现`System.ComponentModel`命名空间下的`INotifyPropertyChanged`接口，并且在实体Set方法中，要调用接口中的事件`PropertyChangedEventHandler`.

   ```c#
   using System.ComponentModel;
   
   public class XX : INotifyPropertyChanged
   {
       //接口中的属性改变时触发的事件
       public event PropertyChangedEventHandler PropertyChanged;
       private string name;
       
       private string Name 
       {
           get
           {
               return name;
           }
           set
           {
               name = value;
               if(this.PropertyChanged != null)
               {
                   PropertyChanged.Invoke(this, new PropertyChangedEventArgs("Name"));
               }
           }
       }
   }
   ```

2. 在窗口初始化的时候，设置双向绑定:

   ```c#
   
   public MainWindow()
   {
       InitializeComponent();
       //数据对象
       classA = new Class1();
       //绑定对象
       Binding bind = new Binding();
       //源
       bind.Source = classA;
       //源中那个字段
       bind.Path = new PropertyPath("Name");
       //设置绑定 参数: 目标对象(控件对象), 目标对象绑定字段类型, 绑定对象
       BindingOperations.SetBinding(this.textBoxDemo, TextBox.TextProperty, bind);
       classA
           .Name = "张三";
   }
   ```

### 控件间绑定

控件和控件之间绑定/控件和静态变量之间绑定(控件改值不会刷新到静态变量)

```xaml
<TextBox x:Name="textBoxA"></TextBox>
<TextBox x:Name="textBoxB" Text="{Binding Path=Text, ElementName=textBoxA}"></TextBox>
<TextBox x:Name="textBoxC" 
         Text="{Binding Path=.[0].Name, Source={x:Static local:Class1.CLASS_LIST}}"></TextBox>
```

### Binding

描述源对象和路径

1. Path 源对象路径,支持.、/、null、属性名称、属性名称.属性名称、属性名称[x]...
   1. Path=. 时，表示Source本身就是一个值(C# 基本类型),如果Source是一个对象，也可以使用`.Name`会绑定这个对象的Name
2. Source 源对象引用

#### 绑定

1. 控件-控件绑定

   ```xaml
   <TextBox x:Name="textBoxA"></TextBox>
   <TextBox x:Name="textBoxB" Text="{Binding Path=Text, ElementName=textBoxA}"></TextBox>
   ```

2. 控件-静态变量绑定

   ```xaml
   <TextBox x:Name="textBoxC" 
            Text="{Binding Path=.[0].Name, Source={x:Static local:Class1.CLASS_LIST}}"></TextBox>
   ```

   静态变量是一个List<对象>,Path=.[0].Name 意思是说取List第0个对象的Name属性。.代表List本身

3. C#对象-控件绑定

   ```xaml
   <TextBox x:Name="textBoxA"></TextBox>
   ```
   实体
   ```c#
   using System.ComponentModel;
   
   public class Class1 : INotifyPropertyChanged
   {
       public event PropertyChangedEventHandler PropertyChanged;
       private string name;
        public string Name
        {
            get
            {
                return name;
            }
            set
            {
                name = value;
                if (this.PropertyChanged != null)
                {
                    //触发属性修改事件
                    PropertyChanged.Invoke(this, new PropertyChangedEventArgs("Name"));
                }
         }
        }
   }
   ```
   ```c#
   public MainWindow()
   {
       InitializeComponent();
       classA = new Class1();
       //描述绑定对象
       Binding bind = new Binding();
       bind.Source = classA;
       bind.Path = new PropertyPath("Name");
   	//绑定
       BindingOperations.SetBinding(this.textBoxDemo, TextBox.TextProperty, bind);
       classA.Name = "张三";
       //控件更新模式为Explicit时，手动触发刷新
       //this.textBoxDemo.GetBindingExpression(TextBox.TextProperty).UpdateSource();
   }
   ```
   

#### 没有Source的Binding

一般情况下，都会给Binding指定Source，如果没指定时，会根据绑定控件所在位置，向上找每一个控件的**DataContext**(所有的控件都有此属性)，在每一个DataContext的对象中搜索Path=xxx的属性,如果有，就把这个对象当成Binding的Source.

```xaml
<StackPanel>
    <StackPanel.DataContext>
		<local:Class1 Id="6" x:Name="ZhangSi" Name="ZhangSi" />
    </StackPanel.DataContext>
    <TextBox Background="Red" Text="{Binding Path=Id}"></TextBox>
</StackPanel>
```



#### 没有Source也没有Path的Binding

一般在DataContex中声明的类型时基本类型时(变量本身就是值),可以使用只有Binding的情况

```xaml
xmlns:sys="clr-namespace:System;assembly=mscorlib"

<StackPanel>
    <StackPanel.DataContext>
        <sys:String>ABC</sys:String>
    </StackPanel.DataContext>
    <TextBlock Text="{Binding}"></TextBlock>
</StackPanel>
```



#### **Binding没有Source时没有向上递归找DataContext

向上递归找DataContext是一个错觉，其实是父级设置了DataContext，子级没有设置时，父级会把DataContext传给子级，一路传下去,直到下一个子级





### UpdateSourceTrigger

默认情况下，控件和变量绑定后，控件值修改后，需要等到控件失去焦点时，才会把值刷新到对应变量。

可取值:

1. PropertyChanged: 当控件值改变时，立马刷新

2. LostFocus: 当控件失去焦点时，刷新  (**默认**)

3. Explicit: 手动刷新，手动调用UpdateSource

   ```c#
   [控件对象].GetBindingExpression(绑定控件数据类型Type).UpdateSource();
    this.textBoxDemo.GetBindingExpression(TextBox.TextProperty).UpdateSource();
   ```



















