---
layout: post
title: "Ubuntu 中安装 Sublime"
date: 2019-07-24
tag: 学习
---



### 安装

​	在 Ubuntu 软件中 安装 sublime



### 汉化

1.  汉化需要安装一个package control，通过这个插件管理器可以使用很多插件来扩展sublime的功能。

2. 使用`Ctrl+`\`快捷键或者通过`View->Show Console`菜单打开命令行，输入

   ```
   import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf),'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
   ```

3. 点击`package control`，输入或 `install package`

4. 输入 `chineselocalization` 并安装



### 代码补全

1. 打开首选项中的设置-用户

2. 加上一句`"auto_complete": true,"auto_match_enabled": true,`

3. 保存关闭重开

4. html 代码不全:

   打开`package control`,直接在输入框内输入 emmet 安装