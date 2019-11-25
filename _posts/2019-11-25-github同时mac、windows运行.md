---
layout: post
title: "mac 和 window 同时使用一个 github "
date: 2018-11-25
tag: 日志log
---



## 如何在 mac 和 window 同时使用一个 github 远程仓库



我的 github 仓库地址是：” haozhiqianga/love “，两台电脑的账号不同（同一个账号没试过），公共密钥都添加至 github

（1）两台电脑都链接仓库

```
git remote add origin https://github.com/haozhiqianga/love1
```

(2) 更新本地仓库

```
git pull origin 远程分支:本地分支

# 如果远程和本地分支都是 master
git pull origin master1234
```

(3) 将本地仓库资源同步到远程仓库

```
git push origin master1
```

------

如果不建立分支，要保证在另一台电脑工作时，每次要先同步本地数据（pull），在手工后要将本地数据同步到github上（push）。



## 参考文献

````
如何在 mac 和 window 同时使用一个 github 远程仓库
https://desktop.github.com/
0基础的git教程，傻瓜都会用的Github Desktop
https://www.jianshu.com/p/06a960d991aa
````

问题

```

github在mac 上配置好，怎么配置windows
```

