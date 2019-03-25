# 约束布局ConstraintLayout

主要解决布局嵌套过多问题,以灵活方式定位和调整部件

## 相对定位:

layout_constraintLeft_toLeftOf
 layout_constraintLeft_toRightOf
 layout_constraintRight_toLeftOf
 layout_constraintRight_toRightOf
 layout_constraintTop_toTopOf
 layout_constraintTop_toBottomOf
 layout_constraintBottom_toTopOf
 layout_constraintBottom_toBottomOf
 layout_constraintBaseline_toBaselineOf
 layout_constraintStart_toEndOf
 layout_constraintStart_toStartOf
 layout_constraintEnd_toStartOf
 layout_constraintEnd_toEndOf

### 居中组件:

```
app:layout_constraintLeft_toLeftOf="parent"
app:layout_constraintTop_toTopOf="parent"
app:layout_constraintRight_toRightOf="parent"
app:layout_constraintBottom_toBottomOf="parent"
```

## 边:

top : 上

bottom : 下

left : 左

right : 右

start : 左下角

end :   右下角

layout_constraint自身边位置_to和目标边位置  对齐

# 角度定位

可以通过一个相对于一个组件的角度和距离在摆放位置.

app:layout_constraintCircle="目标id"

app:layout_constraintCircleAngle="角度"

app:layout_constraintCircleRaduis="距离dp"

# 边距

设置边距的组件在不居中一要确定了位置,没有确定位置情况下不会生效

## 常用边距:

android:layout_marginStart
 android:layout_marginEnd
 android:layout_marginLeft
 android:layout_marginTop
 android:layout_marginRight
 android:layout_marginBottom

## 偏移

取值范围 : 0-1

```
app:layout_constraintHorizontal_bias	水平偏移
layout_constraintVertical_bias			垂直偏移
```

### 宽高比

通过app:layout_constraintDimensionRatio设置宽高比例

#### 设置正方形:

```
layout_constraintDimensionRatio="1:1"
```

#### 设置宽高比值:

设置宽:2 高:1

```
layout_constraintDimensionRatio="W,2:1"
```

设置高 : 2  宽 : 1

```
app:layout_constraintDimensionRatio="H,2:1"
```





