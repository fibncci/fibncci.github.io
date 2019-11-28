

## 电脑中已经有低版本的时候

#### 正确安装 Python 3.6+

正确的方式就是不要轻易删除 python3 及其依赖。特别是不要删除依赖。在 Ubuntu16.04 中修改 python3 指向 3.6+ 版本以后，某些软件会无法使用，比如终端，需要使用上面连接的方法进行相应的处理。

> 这里编程派更推荐的方案是通过 pyenv 安装 3.6+版本。

安装 Python3.6+ 以上版本的正确姿势：

```
# 从官网下载对应版本的源码https://www.python.org/downloads/source/# 解压$ tar -zxvf xxxxx$ cd xxxx# 创建安装目录$ sudo mkdir -p /usr/local/python3# 配置、编译、安装$ ./configure --preifx=/usr/local/python3 --enable-optimizations$ make$ sudo make install
```

安装以后，不修改 python3 的指向，可以为 python3.6+ 版本指定不同的链接名：

```
# 添加 python37 的软链接$ ln -s /usr/local/python3/bin/python3.7 /usr/bin/python37# 添加 pip3 的软链接（这样pip3就是python3.7专用的，也可以起名为 pip37，不影响python3.5的pip3）$ ln -s /usr/local/python3/bin/pip3.7 /usr/bin/pip3
```

检测版本，查看是否成功：

```
$ python37 -V$ pip3 -V
```



重新安装系统、软件、搭建实验环境，真的是心累啊。谨记，以后不要随便卸载系统自带软件，特别是不要相信某些博客写的彻底清除xxx及其依赖的操作。



## 参考文献

```
微信
```

