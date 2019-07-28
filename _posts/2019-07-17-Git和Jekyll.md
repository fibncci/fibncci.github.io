```
目前常用的命令：

Last login: Sun Jul 21 21:50:39 on ttys000

(base) tianmini-2:~ tianzi$ ls

cd Documents 

cd feibo2011.github.io/

git diff

git status

git add .

git commit -m 'fibonacci'

git push origin master。上传


```









# git的规范使用



参考2014版pro git（里面有各种语言很丰富）

https://git-scm.com/book/zh/v2

### 1.如果想下载：

这儿提供两个方法：

1.点pdf右击，会有一个复制链接地址（https://github.com/progit/progit2-zh/releases/download/2.1.24/progit_v2.1.24.pdf），然后打开你的迅雷新建下载任务（+），ok！

2.同样复制链接地址，到网页版百度网盘，离线下载也是可以的。





注：github是远程仓库，本地有个仓库，需要把本地的推到github

```

然后把文件的名字改成.gitignore（注意在.前面是没有任何字符的），
并把文件放在git管理目录的根目录下。
忽略所有包含xcuserdata的文件(夹)
忽略所有文件夹中后缀是.DS_Store的文件


# git ignore
xcuserdata
.DS_Store
```





### 2.git常用

|                       |                                                              |
| --------------------- | ------------------------------------------------------------ |
| 1.git初始化仓库       | git init                                                     |
| 2.定一个名字（定则）  | git config --global user.name "feibo2011"                    |
| 2.2定一个邮箱         | git config --global user.email pc554328955@163.com           |
| 3.git的状态：在暂存区 | git status      ls(查看文件)                                 |
| 3.git提交             | git diff(查看文本修改) git status(确定状态)                  |
| 4.切分支              | fetch http  master:master2 (拉取-推送)（本地master2）        |
| 5.查看分支            | git branch                                                   |
| 6.查看历史            | git log                                                      |
| 7.回滚历史            | git reset --hard HEAD^ 或者 HEAD～                           |
| 8.暂存区提交到提交区  | git push                                                     |
| 9.添加                | git add . (添加所有)                                         |
| 10.确定提交           | git commit -m ''。m后是注释，别名                            |
| 11.远程地址           | git remote –v 查看远程库的详细信息                           |
| 12.推代码（我是http） | git push –u(第一次要用-u 以后不需要) origin master           |
| 13.拉取代码           | git clone https://github.com/feibo2011/feibo2011.github.io  克隆 |
| 14.查看差异，解决     | git diff  git status(确定差异)  git merge合并                |
|                       |                                                              |

```
关联一个库 	git remote add origin https://github.com/tugenhua0707/testgit 
删除XX文件	git rm XX 
```



### 3.创建版本库

1. 创建版本库目录

   ```
   mkdir master3
   pwd  查看
   ls 
   cd master3
    echo 'houhou' > s1.md
    vim s1.md
    echo 'dsdfs你很帅' >>s1.md
   ```

2. 通过 `git init`命令把这个目录变成Git可以管理的仓库

   ```
   cd  master3
   git init 初始化仓库
   1. 将文件放到版本库目录或子目录
   2. 把文件添加到 暂存区 git add 文件名
   使用`git commit`把文件提交到版本库仓库(本地库)
   git status` 命令查看状态
   git diff`命令查看修改了那些东西
   
   ```

   







### 4.同步远程仓库

1. 在本地仓库下运行命令

   ```
   $ git remote add origin git@github.com:fibncci/fibncci.github.io.git
   
   把本地库的内容推送到远程用`git push'
   
   git push -u origin master
   
   # 第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
   
   git push origin master
   
   SSH 警告
   因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入`yes`回车即可。
   The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established. 
   RSA key fingerprint is xx.xx.xx.xx.xx.
   Are you sure you want to continue connecting (yes/no)?
   Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：
   Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
   ```

   










### 5.新的

```
cd /Users/tianzi/Documents/GitHub/feibo2011.github.io  我的地址
git status 找差异
ls看文件
git status确定差异
 git add . 添加所有
 git commit 不展开 提交
 git commit 不展开上传  ---失败了
 
 
 git fetch 取来
 git diff 差异
 git merge 差异合并
 git commit -m 'ceshi' 			 取个名测试
 git config --global user.name "fibncci"   别人可以看到我的用户名
git config --global user.email pc554328955@gmail.com  看到我的邮箱联系me
git commit -m 'ceshi' 			测试
(base) tianmini-2:feibo2011.github.io tianzi$ git push  前面的不是，后面上传

git fetch
git push -u 报错

cd .. 上一级文件
ls查看文件下




git 帮助help
git fetch http  master:master2   取来 拉取远程master  本地的master2
git diff master2   寻找差异
git merge master2   合并到master2主人的
git push http  push会替换and上传

git status  查看差异
git add .   添加所有
git status  确定差异，然后上传
git commit -m '测试'   提交我的备注
git push http  推到我新的http的网址， 不是ssh


```







### 6.git

```git
1版本回退
#查看日志
$ git log								
//如果嫌弃输出信息太多
$ git log --pretty=oneline

$ git reset --hard HEAD^			//上一个版本是HEAD^  上上个版本是HEAD^^  上一百个是HEAD~100



2查看目前代码的修改状态
提交代码之前 首先应该检查目前所做的修改
$ git status
a)  已暂存(changes to be committed)
	new file    //表示新建文件
	modified //表示修改文件
	deleted    //表示删除文件
b)  已修改(changed but not updated)
c)  未跟踪(untracked files)




3查看代码修改内容
$ git diff <file>			//比较某文件与最近提交节点的差异
注意:如果该文件已缓存 那么应该使用
$ git diff -cached <file>

$ git diff <hashcode><hashcode><file>			//比较某文件在提交节点a 节点b的差异
技巧:如果省略后面一个hashcode则默认表示与上一次提交节点比较(也可以使用^运算符)
提交已缓存文件
$ git commit --amend			//最近一次提交 有时候提交注释书写有误或者漏提文件 可以使用次命令
$ git rm --cached  <file> 		//停止跟踪文件 但不删除


```







### 7.git使用

- 1.初始化

  - $git init

- ### 2.配置(config)

  - git config –global user.email 邮箱
  - git config –global user.name 用户名

- 3.帮助(help)

  - $ git help
  - $ git help add
  - $ git add –help

- 4忽略文件(ignore)

  - $ echo”temp/” » .gitignore
  - $ echo”private_key” » .gitignore ~~~

- ### 5状态(status)

  ​	显示当前工作区与暂存区（Index）的粗略状态。

  ​	# 显示某些文件已修改，哪些文件已准备提交等信息

  - $git status

- ### 6添加(add)

  将文件加入缓存区

  \# 添加文件

  - $ git add HelloWorld.java

  \# 添加子目录下的文件

  - $ git add /path/to/file/HelloWorld.c

  \# 通配符方式添加多个文件

  - $ git add ./*.java

  \# 添加工作目录下的所有文件

  - $ git add -A

- 7分支(branch)

  该命令用于管理分支。可以查看，修改，创建，删除分支。、

  \# 列出所有本质

  - $ git branch -a

  \# 创建新分支

  - $ git branch myNewBranch

  \# 删除分支

  - $ git branch -d myBranch

  \# 重命名分支： git branch -m

  - $ git branch -m myBranchName myNewBranchName

  \# 修改分支描述

  - $ git branch myBranchName –edit-description

- ### 8提交（commit)

  将缓存区（Index）中的内容提交到git仓库中

  \# 提交时填写说明(message)

  - $ git commit -m “Added multiplyNumbers() function to HelloWorld.c”

  \# 提交时带数字签名（由提交者的GPG密钥生成）

  - $ git commit -S -m “signed commit message”

  \# 自动将修改的文件加入缓存区（Index），再进行提交。

  - $ git commit -a -m “Modified foo.php and removed bar.php”

  \# 把本次提交与最后一次提交合并（删除最后一次提交，加入合并后的提交）

  - $ git commit –amend -m “Correct message”

- ### 9差异（diff)

  显示工作目录、缓存区（Index）、当前git库版本之间的差异

  \# 显示工作目录与缓存区（Index）之间的差异

  - $ git diff

  \# 显示缓存区（Index）与当前git库版本之间的差异

  - $ git diff –cached

  \# 显示工作目录与当前git库版本之间的差异

  - $ git diff HEAD

- 日志(log)

  显示提交到git仓库的记录信息.

  \# 显示所有提交

  - $ git log

  \# 以简化单行方式显示（每个提交）

  - $ git log –oneline

  \# 只显示合并的提交

  - $ git log –merges

  \# 在提交行的左侧以字符串图像的方式表示版本变化情况

  - $ git log –graph





# jekyll和github

```
1# jekyllrb 规范
### 本地安装
sudo gem install jekyll bundler
gem install --user-install bundler jekyll

ruby -v		### 查看版本
然后使用以下内容附加路径文件，替换`X.X`Ruby版本的前两位数字。
export PATH=$HOME/.gem/ruby/X.X.0/bin:$PATH

gem env	要检查您的gem路径指向您的主目录运行：



2### 快速入门
  gem install bundler jekyll  安装
  jekyll new my-awesome-site  最后一个自己起名字 我的是
  cd my-awesome-site  到我的地址
  bundle exec jekyll serve  绑定执行器jekyll服务
  ＃=>现在浏览到http：// localhost：4000  可以看到我的地址
​```
3### 构建自己的 jekyllrb---jekyll负责美观
it添加远程仓库地址，并初步提交代码
git remote add origin git@github.com:feibo2011/feibo2011.github.io.git

git init 初始化仓库
关联远程仓库
git remote add origin git@github.com:YotrolZ/helloTest.git
git add * 添加
git commit —m"初次提交" 提交
git pull origin master	拉取
git push -u -f origin master上传

https://github.com/feibo2011
git@github.com:feibo2011/feibo2011.github.io.git
```





### 博客模版	baixin.io

```
2019-7-26再次上传
1）使用Jekyll搭建个人博客的教程
使用 HEXO 基于 Github Page 搭建个人博客
Jekyll 支持 Mac 、Windows、ubuntu 、Linux 操作系统                     
Jekyll 需要依赖：Ruby、bundler

2）[Jekyll中文官方文档](http://jekyll.bootcss.com/) 安装
$ gem install jekyll
$ git clone https://github.com/leopardpan/leopardpan.github.io.git
$ jekyll server					leopardpan.github.io/ 目录下， 开启本地服务 
在浏览器输入 [127.0.0.1:4000](127.0.0.1:4000) ， 就可以看到博客效果了。
1请把 _posts/ 目录下的文章都去掉；
2修改 _config.yml 自己的个人信息。

建立不了远程连接--------------

jekyll安装
jekyll -v
gem install bundler jekyll
jekyll new fibncci.github.io
cd  fibncci.github.io
bundle exec jekyll serve
＃=>现在浏览到http：// localhost：4000  127.0.0.1:4000

https://github.com/fibncci/fibncci.github.io.git
git clone https://github.com/fibncci/fibncci.github.io
注意如果：
连接不了，就把别人的模版先下载下来，之后，自己先下载自己的库
（https://github.com/  官网
https://github.com/fibncci/fibncci.github.io）
设置->主题选择器->设置主题，可以解决可能无画面的问题。
危险区->删除此存储库，可以删除不需要的存储库；

然后建立连接，中间下载有问题，control（ctrl）+c 结束，之后
git add . ->git commit -m 'w' ->git push -r origin master
就可以结局了。

卡的地方都可以先结束，在重新执行你的命令。


```

