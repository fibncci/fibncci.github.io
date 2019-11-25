# The little SAS book 学习笔记 第二章(2)

# www.jiayounet.com

## 第二章 将你的数据放入SAS（2.11-2.21）

### 2.12 一行有多个观测值的原始文件读取

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image001.jpg)

当一行出现多个观测值时，可以在input语句结尾加一个停止符号@@

 

例子 有一个关于降水量的数据，precipitation.dat，文件包含城市名、州名、月平均降水量、月平均降水天数：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image002.jpg)

这个数据文件中，第一行包含了两个观测值，可以用@@的程序读取：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image003.jpg)

 

日志记录如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image004.jpg)

中间的说明，SAS went to a new line when INPUT statement reached past the end of a line.是指读取第二个值时达到第一行末尾，并转到下一行继续读取。通常这些信息会预示一个问题出现，但在这里它们都是你所想要的（为什么？）

输出结果如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image005.jpg)

 

### 2.13 读取原始数据的部分观测值

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image006.jpg)

有时候只需要读取原始数据的部分观测值，比如只需要年鉴中的女性数据、收入超过10万的人口数据等。

此时的数据读取方式如下：在SAS读取某一行观测值时，首先读取足够的变量以便决定是否需要保留此行的观测值。然后在input语句结尾加符号@，叫做a trailing at（called a trailing at），这告诉SAS先停在（hold）此行，同时用IF语句检测此观测值是否满足需要，如果是，那么可以再用一个input语句来读取现有的变量。

例子 有一个关于当地交通的数据，traffic.dat数据包含街道的类型（freeways和surface）、街道类型、早晨每小时的机动车流动量、晚上每小时机动车流动量。

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image007.jpg)

如果现在你只需要freeway的数据，可以用下述程序：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image008.jpg)

第一个input读取字符串变量，@是SAS停留在观测值上并用IF检测，第二个input读取input后面的变量值。

程序执行后日志包括两部分说明，一个说明读取了8个记录，另一个说明新数据集中只包含三个观测值。

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image009.jpg)

输入结果如下所示：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image010.jpg)

 

**@ vs @@** @的作用类似于@@，都是行停留指示符（line-hold specifiers），不同地方在于停留多久，@能使SAS停留到下一个input语句（也不换行），@@能使停留的时间到下一个data步（也不换行）。

比如这段代码：

data test;                                                                                                                              

​    infile cards ;                                                                                                                      

​    input x @;                                                                             

​    input y;                                                                 

​    input z @@;                                                                       

cards;                                                                                                                                  

1 2 3 4 5 6                                                                                                                             

7 8 9 10 11 12                                                                                                                          

13 14 15 16 17                                                                                                                          

;                                                                                                                                       

run;

test输出结果就是![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image011.jpg)：

 

 

### 2.14 用infile语句中的选项控制输入

读取原始数据时，SAS做了某些假设，比如从第一行开始读取数据，对于跨行观测值，会自动转到下一行继续读取。但有的特殊数据不满足这些假设，infile语句中的选项可以让SAS读取这些特殊数据。

**FIRSTOBS=** FIRSTOBS= 选项告诉SAS从哪一行开始读取数据，当数据开头有些说明信息，或者想要跳过某些行时，这个选项很有用。例如，如下原始数据文件中，开头两行是关于数据的描述：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image012.jpg)

那么用如下程序可以让SAS从第三行开始读取数据：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image013.jpg)

**OBS=** OBS=告诉SAS一直读取到哪一行位置，注意是行而不是观测值（有的观测值占据多行）比如，如下的原始数据文件中，结尾处还有一句不需要的数据说明时。就需要这个选项：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image014.jpg)

用FIRSTOBS=3和OBS=5就可以读取第三行到第五行的数据：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image015.jpg)

MISSOVER 在input语句中输入的几个变量，SAS在观测值中就读取几个变量，如果一行未读完，则进入下一行直到输入的变量都读取了变量值。missover可以让SAS不进入下一行读取，未赋值的变量就使其成为缺失值。当如下这种数据，就需要missover选项，一个学生应该有5门课的成绩，但由于最后两门是自学课程，不是所有学生都完成，故而缺失：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image016.jpg)

如下的程序可以让SAS将Nguyen第五门课的成绩设为缺失值，从而不牵扯到下一行：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image017.jpg)

**Truncover** 使用column input或formatted input输入时可能会需要这个选项，因为这时有的数据行比其他的短。如下的原始数据中，由于三行的长度都不一样，input中只能指定最长的一行：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image018.jpg)

程序如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image019.jpg)

这里指定了第二行的长度street $ 22-37，但是第一行maple ave.并没占够至第37列（注意后面是没有空格的），故而必须用truncover，否则会转到下一行继续读取，第三行情况也是。

### 2.15 用数据步读取分隔符文件（delimited files）

分隔符文件中，变量值之间会用一些特殊的字符隔开，比如逗号或制表符。DLM=和DSD选项可以让SAS容易的读取这些分隔符文件。

**DLM=**  用list input读取文件时，变量值之间应该用空格隔开。对于其他的分隔符，可以用DLM=，DELIMITER=选项来指定，从而可以读取文件。

例子 如下的数据中，学生姓名、每周读的书的数目是用逗号隔开的：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image020.jpg)

用选项来指定分隔符即可：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image021.jpg)

如果原始数据是用制表符隔开的，那么可以使用DLM=’09’X来指定，因为制表符的十六进制值是09，如果你电脑使用EBCDIC（扩充的二进制编码的十进制交换码），那么应该用DLM=’05’X。

**DSD** DSD (Delimiter-Sensitive Data)有三个作用：忽略引号中数值的分隔符；自动将字符数据中的引号去掉；将两个相邻的分隔符当做缺失值来处理。并且，DSD默认分隔符为逗号，如果数据中的分隔符不是逗号，那么要用delimiter来指定。比如，读取一个制表符为分隔符、并且用两个制表符代表缺失值的数据文件，则要用下面的语句：

INFILE ’file-specification’ DLM=’09’X DSD;

**CSV****文件** CSV文件，Comma-separated values files，是可以用DSD选项的文件类型。Excel可以储存CSV格式的文件。

**例子** 某咖啡馆，老板每晚请不同的乐队表演来吸引顾客，他记录了乐队名称、演出日期、晚上8点、9点、10点、11点的顾客数量：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image022.jpg)

注意，其中有一个乐队的名字中用逗号来分隔，并且使用了引号。最后一条记录中还有一个缺失值，用两个连续的逗号表示。INFILE语句中的DSD选项可以用来读取这个文件，并且，由于每个记录长度不一样，还需要用missover：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image024.jpg)

注意bandname和GigDate两个变量使用了**冒号修改器**，冒号修改器告诉SAS读取信息的长度（BandName为30，GigDate为10）。输出结果如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image025.jpg)

 

### 2.16 用导入过程（IMPORT procedure）读取分隔符文件。

Proc import会浏览你的数据文件，自动决定变量类型（字符串或数值），为字符串变量分配正确的长度，辨认出日期变量。Proc import会将两个连续的分隔符视为缺失值，会读取引号中的变量值。一行读完后，会自动分配缺失值给未赋值的变量。Also,if you want,you can use the first line in your data file for the variable names。导入过程（IMPORT procedure）自动问你写下数据步，这可以在提交之后的日志窗口中查看。

一个导入过程（IMPORT procedure）的最简单形式：

PROC IMPORT DATAFILE=’filename’ OUT=data-set;

用语句DATAFILE=’filename’读取文件名，用OUT=data-set创建SAS数据集。SAS会通过文件的扩展名来检测文件的类型：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image026.jpg)

如果文件没有正确的扩展名，或者是DLM格式的，必须在proc import语句中用DBMS=option。如果想要创建的数据集名字已经存在，那么要用replace选项代替。一个使用replace和dbms的例子。

PROC IMPORT DATAFILE=’filename’ OUT=data-set DBMS=identifier REPLACE;

导入过程（IMPORT procedure）从数据文件中的第一行获取变量名，可以通过在PROC IMPORT后面增加GETNAMES=NO语句来改变这种默认，PROC IMPORT会分配给变量名字：VAR1，VAR2，VAR3等。如果你的数据文件是DLM类型的，PROC IMPORT会假定分隔符为空格，用DELIMITER=可以改变默认的分隔符。如下是一段有上述代码的程序：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image027.jpg)

例子 下面还是使用咖啡馆中，乐队表演的例子（2.15），注意其中有一个乐队的名字中用逗号来分隔，并且使用了引号：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image022.jpg)

用proc import读取数据的代码如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image028.jpg)

输出结果如下，注意GigDate的日期格式能够被proc import辨认出来：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image029.jpg)

 

### 2.17 用导入过程（IMPORT procedure）读取PC文件

如果安装了SAS/ACCESS模块，导入过程（IMPORT procedure）可以导入一些PC文件类型。它会浏览你的文件以决定变量类型，并默认使用数据的第一行来分配变量名。Windows操作环境中可以导入excel、Lotus、dBase、和Access文件。Unix系统中可以导入dBase文件，并且从SAS9.1开始，Unix系统也可以导入excel和access文件。在windows环境中有一个不需要SAS/ACCESS模块的方法——Dynamic Data Exchange(DDE)，将在2.18中讲解。

**Microsoft Excel****，****Lotus****，和****dBase****文件** 下面是用导入过程（IMPORT procedure）读取PC文件的一般过程：

PROC IMPORT DATAFILE=’filename’ OUT=data-set DBMS=identifier REPLACE;

如果读取的文件是如下类型，就不用DBMS=OPTION。

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image030.jpg)

在读取excel时，有时需要指定要读取的是哪一个工作薄——sheet

SHEET=name-of-sheet;

默认情况下，导入过程（IMPORT procedure）会从工作薄的第一行中读取变量名。如果不需要，可以用如下代码使得SAS给变量赋名为F1，F2等。

GETNAMES=NO;

Microsoft Access Files 读取这种文件需要用DATABASE=和DATATABLE=，而不是DATAFILE=option。

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image031.jpg)

下面的是DBMS可以辨认的Access文件

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image032.jpg)

例子 有如下的EXCEL数据：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image034.jpg)

读取的proc import程序：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image035.jpg)

输出结果如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image036.jpg)

 

2.18 用DDE读取PC文件

DDE，动态数据交换（Dynamic Data Exchange），读取PC文件的优点为：可以直接访问存于PC文件中的数据，不要求购买其他SAS产品；缺点为：只能用在windows环境下，只能在程序运行时（比如excel），SAS才能进行读取。

有几种方式可以用DDE访问数据：

l  复制数据到剪贴板

l  指定DDE三元组

l  从SAS中启动PC程序，然后读取数据。

**复制数据到剪贴板** 可以直接复制数据至剪贴板，然后再SAS程序的DDE FILENAME 语句中是使用CLIPBOARD关键字。比如，excel中有如下的工作薄：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image038.jpg)

复制A2到G5，然后在不关闭excel的状态下，提交如下SAS程序：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image039.jpg)

FILENAME语句将指代的文件（BASEBALL）定义成DDE类型，并指定从剪贴板中去读取它（CLIPBOARD）。DDE默认空格为分隔符，如果变量值之间有空格，则要在INFILE语句中用NOTAB选项和DLM=’09’X选项，前者告诉SAS在变量值之间放置制表符，后者告诉SAS将制表符定义为分隔符。如果数据中有缺失值，则要在INFILE中加入DSD和MISSOVER选项，前者将两个连续的分隔符视为缺失值，后者告诉SAS如果此行读完，不要进入下一行给未赋值的变量赋值。

**指定****DDE****三元组** 这种方法可以不用复制数据，直接指定出文件的DDE 三元组。DDE 三元组的形式为：**application| topic ! item****。**

有一种方法可以在SAS中直接查看文件的DDE三元组，方法为：复制数据至剪贴板里，触发SAS会话，从解决方案（Solution）菜单中选择附件（accessories）——DDE三元组。一个窗口会出现你复制文件的DDE三元组。比如，一个工作薄的DDE三元组为：

Excel|C:\MyFiles\[BaseBall.xls]sheet1!R2C1:R5C7

读取这个文件的FILENAME语句为：

FILENAME baseball DDE'Excel|C:\MyFiles\[BaseBall.xls]sheet1!R2C1:R5C7';

从SAS中启动程序 这种方法可以不用在运行SAS之前启动数据程序。想要从SAS中启动程序，然后读取数据，则首先需要NOXWAIT和NOXSYNC系统选项，然后使用X语句，一个例子：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image040.jpg)

NOXSYNC和NOXWAIT语句告诉SAS不要等待用户输入。X语句告诉windows执行或打开引号中路径的文件，注意这里路径设置了两个引号，如果路径中有空格，则要设置两个引号。使用这种方法，必须要在FILENAME语句中指定DDE三元组。

### 2.19 临时和永久数据集

SAS临时数据集只在目前工作或会话中存在，关闭SAS或结束工作时则删除；永久数据集当关闭SAS或结束工作时仍然存在。

**SAS****数据集名** 所有的SAS数据集都有用句号分开的两层数据集名，如work.a。第一层前缀work是逻辑库名，第二层是在逻辑库中用于辨别自己的成员名。

名字的规则是，以字母或下划线开头，并且名字中只能包含字母、数字和下划线。而且，库名不能超过8个字节，而成员名却可以达到32个字节。

大部分数据集通过数据步创建，过程步也可以创建。如果指定了一个前缀不为work的两层数据集名，则这个数据集就是永久的。如果不指定前缀，则默认数据集是临时的，自动分配到work逻辑库中。下面是一些数据集名，对于的逻辑库，成员名，类型：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image041.jpg)

**临时数据集** 如下的程序创建并打印了一个名为DISTANCE的永久数据集：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image042.jpg)

这里，只指定了成员名distance，自动分配到work库中，日志窗口中有说明：

NOTE:The data set **WORK.DISTANCE** has 1 observations and 2 variables.

**永久数据集** 可以在资源管理器窗口中定义一个新库使用：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image044.jpg)

也可以通过如下程序：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image045.jpg)

那么日志窗口就会出现如下说明：

NOTE:The data set **MYLIB.DISTANCE** has 1 observations and 2 variables.

这是一个永久数据集，因为前缀不是work。

### 2.20 用LIBNAME语句使用永久数据集

LIBNAME语句的基本形式为：LIBNAME libref’your-SAS-data-library’;

LIBNAME的后面，需要指定库名和存放的路径，在个人操作环境下LIBNAME语句的基本形式为：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image046.jpg)

**创建永久数据集** 如下的例子创建了一个永久SAS数据集，包含了magnolia trees的一些信息。每一种树，原始文件都包含它的科学名、普通名、最大高度、第一次开花的年龄、是evergreen还是deciduous、以及花的颜色。

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image047.jpg)

下面的代码将会创建一个PLANTS的逻辑库，路径为C盘下的MySASLib。然后从原始文件Mag.dat中读取数据，并创建一个名为MAGNOLIA的永久数据集，存在PLANTS库中。

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image048.jpg)

日志窗口会出现如下说明：

NOTE:The data set **PLANTS.MAGNOLIA** has 5 observations and 6 variables.

如果在电脑中打印文件的地址目录，会发现文件名不是PLANTS.MAGNOLIA。这是因为操作系统有自己对文件命名的方式，这个文件，在Windows,UNIX,和OpenVMS操作环境中名字为magnolia.sas7bdat，在OS/390或者z/OS环境中，文件名就会如LIBNAME语句中定义的data-set-name形式。

**读取永久数据集** 如果你想打印出上例中创建的数据集，可以用如下语句：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image049.jpg)

这次LIBNAME语句中的库名为example，但缺失同样路径，逻辑库名可以改变，但成员名MAGNOLIA却一样。输出如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image050.jpg)

 

### 2.21 通过直接指代使用永久数据集

可以通过直接指代来使用SAS数据集，且不需要自己定义，SAS为你做好。

直接指代，依据系统不同，使用方法也不同，如下:

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image051.jpg)

可以看到，一些系统的语句中需要指出路径，但如果遗漏了路径，SAS自动使用当前路径，比如这样一个创建名为trees的永久数据集的代码：

DATA ‘trees’;

UNIX和OPENVMS操作环境下，当前的路径默认为启动SAS的路径，可以通过工具（TOOLS）下拉菜单的选项（OPTIOPN）菜单来改变这种默认，windows环境下当前路径会显示在SAS窗口底部。可以通过双击这个路径来改变默认。

**例子** 如下还是关于magnolia trees的这个例子，

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image052.jpg)

下面的代码将从原始文件mag.dat中读取数据，创建一个名为MAGNOLIA的永久数据集，存放在C盘的Mysaslib路径中：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image053.jpg)

相应的输出窗口显示如下：

NOTE:The data set c:\MySASLib\magnolia has 5 observations and 6 variables.

如果打开MySASLib文件夹，会发现一个名为magnolia.sas7bdat的文件。在没指定库的情况下，SAS会自动为你创建一个库，在资源管理器窗口中可以看到，下图是SAS为magnolia创建的库。

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image055.jpg)

用直接指代读取SAS数据集 可以直接用引号+路径的方式读取永久数据集，比如打印magnolia数据集可以：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image056.jpg)

输出窗口如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image057.jpg)

 

2.22 列出SAS数据集目录

由于SAS是自文档化，即在自动储存了数据集的信息，因此可以通过contents过程来查看SAS数据集的描述。

Proc contents data=data-set

如果遗漏了data=的语句，SAS自动列出最近创建的数据集

例子 如下的程序创建了一个数据集，并且使用proc contents。数据步中使用了label语句，label语句为变量打上标签，并储存在数据集中，在打印时会显示。过程步中也可以使用label，但只在proc contents中有效，不会储存在数据集中。Informat和format可以指定信息和格式，储存在数据集中，也可以在过程步中使用，但不储存在数据集中。

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image058.jpg)

输出如下：

![img](file:///C:\Users\123\AppData\Local\Temp\OICE_CEFB0038-D4D0-411F-A0D8-16C9EB103069.0\msohtmlclip1\01\clip_image059.jpg)

 

 



## 参考文献

 