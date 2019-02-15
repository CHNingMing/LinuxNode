# VSCode

### VSCode全局变量：

${workspaceFolder}	：	工作空间位置

${fileBasenameNoExtension}		：	文件去除后缀名称

${file}		:	文件名





## Tasks.json

Tasks和launch都在当前项目.vscode下

在程序执行前执行，一般用做编译	**保证打开的是文件夹不是单个文件**

### 创建Tasks

Ctrl+Shift+P	 输入:task

 选择：Configure Task

提示选择模板，一般Order其他

格式：

```json
{
	    "version": "2.0.0",
    "tasks": [
        {
            "label": "compareC",//任务名称,launch通过名称调任务
            "type": "shell",//执行命令类型
            "command": "",	//执行命令
            "args": [..]	//执行参数
        }
    ]
}
```



## launch.json

程序执行，执行tasks编译好的文件	**保证打开的是文件夹不是单个文件**

格式：

```json
 "configurations": [
        {
            "name": "(lldb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "preLaunchTask": "任务名称",
            "program": "  ",//执行文件位置，一般是任务编译好执行文件此处运行
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",//项目位置
            "environment": [],
            "externalConsole": true,	//是否外部终端运行
            "MIMode": "lldb"
        }
    ]
```









