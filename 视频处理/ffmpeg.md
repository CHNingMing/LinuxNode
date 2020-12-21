



## 截取视频制定时间图片:

```
ffmpeg -i Wildlife.wmv -y -f image2 -t 0.001 -ss 4 -s 352x240 a.jpg
```

-i : 输入文件

-y 如果目标文件存在,覆盖目标文件

-f 格式化输出

-t 记录时间,因为是截取图片,不是截取视频,所以是0.001

-ss 截取制定时间 单个数字(秒) hh:mm:ss(时分秒)

-s 设置视频帧大小   不理解..

## 按时间间隔截取多张视频图片:

```
ffmpeg -ss 00:00 -i Wildlife.wmv -f image2 -r 0.2 -t 02:45 %3d.jpg
```



























