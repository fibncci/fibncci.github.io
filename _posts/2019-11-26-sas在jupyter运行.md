

## pip不是内部文件

'pip' 不是内部或外部命令，也不是可运行的程序
或批处理文件。

解决办法：添加环境变量

```
pip的环境变量
F:\Users\123\Anaconda3\Scripts\
或者
C:\Program Files (x86)\Python\Python36-32\Scripts 中包含了对应的pip

python的环境变量的添加
F:\Users\123\Anaconda3


javac的编译环境变量
F:\Program Files\Java\jdk1.8.0_92\bin


git的编译环境变量
F:\Program Files\Git\cmd


sas的编译环境变量
都是配置文件添加的环境变量
D:\Program Files\SASHome\x86\SASFoundation\9.4\core\sasexe

sascfg.py
F:\Users\123\Anaconda3\Lib\site-packages\saspy
F:\Users\123\Anaconda3\Lib\site-packages\saspy
F:\Users\123\Anaconda3\Lib\site-packages\saspy\sascfg.py

R的编译环境变量
D:\Program Files\R\R-3.6.1\bin
```

## jupyter中编写 sas 代码

```
1.会安装 SASPy 模块，因为SASPy是sas_kernel 的依赖包
pip install sas_kernel
检查是不是存在
(base) C:\Users\123>jupyter kernelspec list
Available kernels:
  sas        C:\Users\123\AppData\Roaming\jupyter\kernels\sas
  python3    F:\Users\123\Anaconda3\share\jupyter\kernels\python3


2.只需要python能够连接windows平台本地的sas服务，所以重点说明winlocal 的配置。
2.1
>>> import saspy
>>> saspy.SAScfg
<module 'sascfg_personal' from 'C:\\Users\\51377\\Anaconda3\\lib\\site-packages\\sascfg_personal.py'>
或者
F:\Users\123\Anaconda3\Lib\site-packages\saspy\sascfg.py
2.2
可以配置连接本地机器的SAS；只要配置winlocal 即可。
也可以配置连接远程机器的SAS Server，无论是Linux Server还是Windows Server都可以。此处就以连接本地SAS为例进行说明。
2.3
需要将cpW变量中的5个Jar包的路径修改为自己电脑实际的路径。
注：此处需严格按照自己电脑的SAS安装目录和Anaconda的安装目录来修改。只是修改路径，Jar包的文件名不需要修改。
winlocal连接方式中的参数“encoding”的值修改为“euc-cn”。因为这是SAS在Windows下的默认编码方式。如果编码方式不对，中文会出现乱码。
```

sascfg.py文件

```python
# build out a local classpath variable to use below for Windows clients   CHANGE THE PATHS TO BE CORRECT FOR YOUR INSTALLATION 
cpW  =  "D:\\Program Files\\SASHome\\SASDeploymentManager\\9.4\\products\\deploywiz__94520__prt__xx__sp0__1\\deploywiz\\sas.svc.connection.jar"
cpW += ";D:\\Program Files\\SASHome\\SASDeploymentManager\\9.4\\products\\deploywiz__94520__prt__xx__sp0__1\\deploywiz\\log4j.jar"
cpW += ";D:\\Program Files\\SASHome\\SASDeploymentManager\\9.4\\products\\deploywiz__94520__prt__xx__sp0__1\\deploywiz\\sas.security.sspi.jar"
cpW += ";D:\\Program Files\\SASHome\\SASDeploymentManager\\9.4\\products\\deploywiz__94520__prt__xx__sp0__1\\deploywiz\\sas.core.jar"
cpW += ";F:\\Users\\123\\Anaconda3\\Lib\\site-packages\\saspy\\java\\saspyiom.jar"

F:\Users\123\Anaconda3\Lib\site-packages\saspy\java\thirdparty
# These jars provide CORBA support for Java 10+ which no longer provides CORBA itself.  CHANGE THE PATHS TO BE CORRECT FOR YOUR INSTALLATION 
cpW += ";F:\\Users\\123\\Anaconda3\\Lib\\site-packages\\saspy\\java\\thirdparty\\glassfish-corba-internal-api.jar"
glassfish-corba-omgapi.jar"
glassfish-corba-orb.jar"
pfl-basic.jar"
pfl-tf.jar"

# And, if you've configured IOM to use Encryption, you need these client side jars.  CHANGE THE PATHS TO BE CORRECT FOR YOUR INSTALLATION 
#cpW += ";C:\\Program Files\\SASHome\\SASVersionedJarRepository\\eclipse\\plugins\\sas.rutil_904300.0.0.20150204190000_v940m3\\sas.rutil.jar"
sas.rutil.nls.jar"
 sastpj.rutil.jar"


170行
winlocal = {'java'      : 'java',
            'encoding'  : 'windows-1252',
            'classpath' : cpW
            }
```



### 报错

> sas.svc.connection.jar文件

```
sas.svc.connection.jar文件

D:\Program Files\SASHome\SASDeploymentManager\9.4\products\deploywiz__94520__prt__xx__sp0__1\deploywiz

D:\Program Files\SASHome\SASDeploymentManager\9.4\products\deploywiz__94520__prt__xx__sp0__1\deploywiz
```

Java环境有问题，要么重新安装Java，并配置Java的环境变量；要么直接在sascfg.py配置文件中将Java的路径定义为SAS 9.4私有的Java环境。



## 参考文献

```
jupyter notebook 中编写 sas 代码
https://blog.csdn.net/Guo_ya_nan/article/details/80754346

pip不是内部命令问题
https://blog.csdn.net/wochunyang/article/details/52312370


在Jupyter Notebook中使用SAS
http://www.sohu.com/a/218339423_278472
```

