# AppleScript

类似Windows Cmd命令

# 声明变量格式

set a to 1 =.  int a = 1,需要变量直接用，类似shell

```
set a to 1
set a to a + 1
```

## 字符串

```
set str to "字符串内容"
```

### 字符串拼接

```
"hello"&"word"
```

### 获取字符串个数

#### the length of

```
the length of 字符串
```



# Tell

调用某个东西,这里先调用应用

```
tell application "程序名称"
	
end tell
```

## Display

弹出信息框

```
Display dialog "文本"
```

### 