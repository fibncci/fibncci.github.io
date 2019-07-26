---
layout: post
title: "创建 GitHub Pages"
date: 2019-07-17 
description: "记录创建 GitHub Pages 过程"
tag: 学习
---




### 1. 创建存储库

​		转到[GitHub](https://github.com/)并[创建一个](https://github.com/new)名为*username* .github.io [的新存储库](https://github.com/new)，其中*username*是GitHub上的用户名

### 2. 克隆存储库

​		转到要存储项目的文件夹，然后克隆新存储库：

```
git clone https://github.com/username/username.github.io
```

### 3.  创建 index

​		输入项目文件夹并添加index.html文件：

```
cd username.github.io

echo "Hello World" > index.html
```

### 4. 上传

​		添加，提交和推送更改：

```
git add --all

git commit -m "Initial commit"

git push -u origin master
```

### 5. 完成

​		启动浏览器转到 **https：// username .github.io**。

