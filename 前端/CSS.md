# 颜色

### 颜色透明度设置：

background-color:#CC00FF;

background-color: rgba(255, 0, 0, 0.14);

#### rgba

给出rgb，算出16进制颜色码





# 定位

## absolute

### absolute下居中屏幕

左右居中：

```css
left: 0;
right: 0;
margin:auto;
```

上下居中：

```
top:0;
bottom:0;
margin: auto;
```

上下左右居中:

上下左右全是0，margin:auto;







# 动画

## 过渡动画

### transition

从一个位置过渡到另一个位置;

从一个颜色过渡到另一个颜色;

从一个大小过渡到另一个大小;

```
transition: 2s;
```

## 动画

### 声明动画：

from/to

```css
@keyframes 动画名称{
    from{
        /*样式*/
    }
    to{
        /*样式*/
    }
} 
```

百分比

```css
@keyframes 动画名称{
    0%{
        /*样式*/
    }
    25%{
        
    }
    50%{
        
    }
    100%{
        
    }
} 
```

### 使用动画：

animation: [动画名称]\[动画总共时间 */s][是否重复]

```




```

# 苗点切换平滑滚动：

scroll-behavior:smooth;



# 字体

## 使用自定义ttf字体

```css
/*定义*/
@font-face{
    font-family: "自定义字体名称";
    src: url('*.ttf');
}
/*使用*/
*{
    font-famil: "自定义字体名称";
}

```







