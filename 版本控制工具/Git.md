## Git

设置git 账号/密码：

git config --global user.name "github账号"

git config --global user.passowrd "github密码"

Pull时出错问题:

打开.git/config,添加

```
    [branch "master"] 
        remote = origin 
        merge = refs/heads/master 
    [remote "origin"] 
        url = 项目地址
        fetch = +refs/heads/*:refs/remotes/origin/*
```

.gitignore	提交过滤配置文件

maven过滤子工程需要手动添加子工程项目名,因为聚合工程下就是一个一个的子工程文件夹

```
文件情况:
	*.xx扩展名
文件夹情况:
	/xxx文件夹/
单个文件:
	xxx.xxx具体文件名


```

### git更新被拒绝，当前分支落后于远程分支解决：

```shell

git remote add origin https://xx.com/*.git
git fetch origin			//获取远程更新
git merge origin/master		//把更新的内容合并到本地分支

```







