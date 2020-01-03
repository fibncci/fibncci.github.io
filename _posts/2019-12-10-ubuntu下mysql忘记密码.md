---
layout: post
title: "ubuntu下mysql忘记密码"
date: 2019-12-10
tag: sas
---



## ubuntu下mysql忘记密码（已解决）

> 参考：ubuntu下mysql忘记密码，重置； mysql修改密码
>
> https://www.cnblogs.com/qingsong/p/11077171.html



方法一：

1）：编辑mysqld.cnf文件

```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

2）：在文件中的skip-external-locking一行的下面添加一行：

```
skip-grant-tables
```

3）：重启MySQL服务

```
sudo service mysql restart
```

4）：终端输入mysql进入MySQL，输入USE mysql切换至mysql数据库

```
mysql
USE mysql
```

5）：把root用户的密码修改为04120412

```
UPDATE mysql.user SET authentication_string=password('04120412') WHERE User='root' AND Host ='localhost';
```

6）：修改字段plugin

```
UPDATE user SET plugin="mysql_native_password";
```

7）：

```
flush privileges;
```

8）：退出

```
quit;
```

9）：注释掉/etc/mysql/mysql.conf.d/mysqld.cnf文件中添加的一行

 

方法二：利用mysql自带的用户debian-sys-maint进行重置密码，只有Debian或Ubuntu服务器才有，存在于/etc/mysql/debian.cnf文件中

1）：打开/etc/mysql/目录下的debian.cnf文件，里面包括用户名和密码

```
sudo vim /etc/mysql/debian.cnf
```

![img](https://img2018.cnblogs.com/blog/427641/201906/427641-20190624145700309-67432844.png)

2）：使用文件中提供的用户名和密码进入mysql

```
mysql -u debian-sys-maint -p
```

3）：选择mysql数据库

```
use mysql;
```

4）：更新root用户的密码为123456

```
update user set authentication_string
```





## 安装mysql



**MySQL 8.0中的增强功能**

- 支持 Atomic DDL 语句
- 增强安全性和账户管理
- 改进资源管理
- InnoDB 的一些增强功能
- 新的备份锁
- 默认字符集已从 latin1 更改为 utf8mb4
- JSON增强
- 使用 Unicode 的国际组件（ICU）提供正则表达式支持
- 新的错误日志记录现在使用 MySQL 组件体系结构
- MySQL 复制的增强
- 支持公用表表达式（非递归和递归）
- 增强的优化器
- ……



