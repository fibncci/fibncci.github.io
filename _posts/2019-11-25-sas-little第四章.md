---
layout: post
title: "sas-little4"
date: 2019-11-28
tag: sas
---





## 第四章 排序、打印并描述你的数据

> The little SAS book 学习笔记

### 4.1 使用SAS过程步

​                                                    

使用过程步就像填写一个如左图的表格，当然每个过程步都有独特的地方，本部分主要讨论各过程步相同的地方：

 

 

大部分过程步都有一个必须的语句，也有可选的语句，比如打印语句：proc print，这两个词是必须的，但可选的语句也有很多。

**Proc****语句** 所有的语句的必须部分为proc+过程名，比如print、contents等。后面接一些可选项。比如proc print data=banana；

data=banana选项告诉SAS打印哪个文件，如果不加，则SAS默认打印最近使用的数据。前面还可以家libname语句，建立一个对本地文件的链接（2.20），比如：

LIBNAME tropical 'c:\MySASLib';

​       PROC CONTENTS DATA=tropical.banana;

或者直接引用（2.21）：PROC CONTENTS DATA='c:\MySASLib\banana';

**BY****语句** BY语句只在过程proc sort中是必须的，它用来对观测值排序。其他过程BY告诉过程对变量进行分别分析，且是可选的。比如要对每个州进行分别分析，则为：BY State

另外，除了proc sort，其他过程都假设了数据已经进行了排序，所以如果数据还没有排序，那么在分析之前要用proc sort排序。

**TITLE** **和****FOOTNOTE****语句** 这是为输出加上标题和脚注。最基本的title语句为：title ‘标题’，双引号、单引号皆可，比如：

TITLE'This is a title';

如果标题中带有撇号，则需用双引号，或者将撇号换为双撇号：

TITLE”Here’s another title”;

TITLE’Here’’s another title’;

可以通过在tile、footnote后面加上数字来添加多个标题和脚注，

FOOTNOTE3’This is the third footnote’;

但是小数字的标题会代替大数字的标题，如title2会代替title3。

标题的去处可以用title+空值：TITLE;

**Label****语句** 它可以为输出的变量加上标签，一个标签最大256字节，下面的代码为receivedate和shipdate创建了标签：

 

LABEL ReceiveDate=’Date order was received’

ShipDate=’Date merchandise was shipped’;

注意的是，在数据步中使用label语句，则标签会保存在数据集中；在过程步中使用，标签只在这个过程中有效。

**定制输出** 使用系统选项，可以为输出设置诸如居中、日期、单行长度、页长度等。使用Output Delivery System，还可以改变输出的风格，以不同的格式输出（HTML、RTF），甚至改变输出的任何细节。

**输出数据集** 可以用ODS OUTPUT语句为输出结果创立一个数据集（5.3），一些过程中也可以用out=option。

### 4.2 用where语句在过程中构造子集

也可以用where构造子集，它方便快捷，因为他不创建新的数据集。且能够用在过程步中。

Where语句的基本形式为：

WHERE condition;

只有满足条件的观测值才进行proc过程。

一些使用最多的操作符及例子：

   

**例子** 有一份关于画家的数据，artists.dat，包含画家的姓名、主要风格、国籍：

   

第一步首先是数据步，读取数据、使用直接指代在C盘mysaslib目录下创建一个名为style的数据集。

   

某天如果想打印出印象派impressionism画家的情况，那么可以使用where语句

   

输出结果为：

   

 

### 4.3 用proc sort为数据排序

基本形式为：

PROC SORT;

​           BY variable-1...variable-n;

SAS首先会按照第一个变量排序，再对后面的排序。

Data=，out=用来指定输入和输出数据，如果缺失out=，则SAS会将排序后的数据集代替原来的数据集。下面的代码告诉SAS对数据messy排序，并将排序后的数据存在neat中：

PROC SORT DATA=messy OUT=neat;

选项nodupkey告诉SAS排序时删除重复值，比如：

PROC SORT DATA=messy OUT=neat NODUPKEY;

SAS默认是升序，可以用选项DESCENDING来变成降序，将DESCENDING加在要降序的变量前面：

BY State DESCENDING City;

**例子** 下面的数据显示了一些鲸鱼和鲨鱼品种的平均长度：

   

下面的代码读取并排序数据

   

输出结果为：

   

因为SAS认为缺失值是比字符串和数值都小，所以排在了第一位。另外，由于whale shark 40的数据有两个，故因为nodupkey选项而被删除一个。说明可见日志：

   

 

### 4.4 用proc print打印你的数据

基本形式：PROC PRINT;

SAS默认打印最近使用的数据集，DATA=可以指定数据集：

PROC PRINT DATA=data-set;

SAS默认打印观测值数，noobs选项可以取消。SAS默认打印时用变量标签代替变量，用label可以改变取消：

PROC PRINT DATA=data-set NOOBS LABEL;

还有下面的选项：

BY variable-list;   前提是数据必须进行排序

ID variable-list; 

SUM variable-list; 打印变量总数

VAR variable-list; 指定打印哪部分变量以及打印顺序，默认打印全部。

**例子** 有学生卖糖果的数据，Candy.dat，记录学生名、所属班级、销售日期、卖的糖果类型、卖出的糖果数。

   

下面的程序读取数据、计算每个学生赚得的利润（每买一块赚1.25美元），并用proc sort按班级排序。接着在proc print语句中加入by，以分班级打印，加入sum，计算每个班级总利润：

   

输出结果为：

   

 

### 4.5 用formats改变打印外观

打印数据时，SAS会自动为你安排最好的格式，小数点位数、空格等。

当不需要默认格式时，可以用SAS formats改变打印的外观。

对于字符串、数值、日期变量，SAS有很多格式。比如可以用commaw.d格式打印有逗号的数字，用$w.格式控制打印的字符串数，用MMDDYYw.格式将日期（以1960.1.1为基点的数字）打印成12/03/2003这样的格式。甚至可以将格式打印成十六进制、区位十进制、压缩十进制等。

SAS格式的普通形式为：

   

符号说明：$说明了是字符串、format是格式名、w是包括包括在小数点在内的长度、d是小数位数。句号非常重要，它用来区分格式名和变量名。

**Format****语句** 可以用format语句同时将格式和变量联系起来，用format+变量名+格式名，比如想要将格式DOLLAR8.2和变量profit、loss联系起来，把格式MMDDYY8.和格变量saledate联系起来：

FORMAT Profit Loss DOLLAR8.2 SaleDate MMDDYY8.;

Format可以用在数据步和过程步中，前者将把格式永久储存，后者只是临时储存。

**Put****语句** 当写原始数据或者报告时，也可以在put语句中使用formats，在每个变量后面加上格式：

PUT Profit DOLLAR8.2 Loss DOLLAR8.2 SaleDate MMDDYY8.;

例子 在上面的学生卖糖果的案例中，可以看到输出的日期是SAS日期值，这里用format变换成日期格式，并且用DOLLAR6.2将利润换成货币格式，

   

输出结果为：

   

 

### 4.6 可供选择的formats

   

   

下面是例子

   

   

 

### 4.7 使用proc format创建自己的格式

有时候变量值用数字代表实际的变量值，比如1代表男性，2代表女性，这种代码在打印的时候不好解读，可以用proc format使得打印出想要的值。

基本形式为：

   

Value语句中的name是格式的名字，如果格式是位字符串设计，则必须以$开头，长度不能超过32个字节（包括$），不能以数字结尾，除了下划线，不能包含其他任何特殊符号。且名字不能与已有的格式名冲突。Range是分配给等号右边文本的变量值，文本可以达到32767个字节，有的过程只会打印前面8或16个字节。下面是一个例子：

   

变量值是字符串要加上引号，range不止一个值要用逗号隔开，连续的range要用-，关键字low和high可以用来指代变量中最小和最大的的非缺失值。也可以用<来排除或指代某些范围，other可以给任何没有列在value语句中的变量分配格式。

例子 有一份关于汽车公司客户的调查信息。包括客户年龄、性别（1为男性，2为女性）、每年收入、偏爱的汽车颜色（yellow,gray,blue,or white）：

   

下面的代码读取数据，并使用format过程为颜色、性别和汽车创建格式，并在打印数据时用format为变量指定这些输出格式：

   

输出结果为：

   

 

### 4.8 定制一个简单的报告

数据步可以帮助在报告中完成一些个性的需求，比如一页打印一个观测值等。

用file语句和put语句 ，基本形式为：

FILE‘file-specification’PRINT;

如input，put语句也有list，column，formatted方式，但因为SAS已经知道变量类型，因此不用符号$。且如果使用list ，SAS会自动在两个变量之间加上空格；使用column或者formatted，SAS将会把变量放在任何你指定的地方。使用指示器@n指定移动到第n列，+n指定移动n列，/跳动到下一行，#n跳动到第n行。用@hold住当前行。

例子 再一次使用学生卖糖果的案例，Candy.dat，记录学生名、所属班级、销售日期、卖的糖果类型、卖出的糖果数。

   

老师想看每位学生的销售情况，故要每页分别打印一位学生的情况，代码如下：

   

   

Data null是告诉SAS不要写数据集名，以便使得程序更快。File语句创建了一个输出文件，空标题title语句告诉SAS去除所有的自动标题。

第一个put语句以一个指示器开头，@5，告诉SAS移动到第5列，接着打印出“candy sales report for”，后面是姓名name。变量name、class和quantity都是以list方式打印，而profit是使用formatted方式打印，并给定格式dollar6.2。一个斜杠是指跳到下一行，两个斜杠是跳到下两行。最后，语句put_age_是在每个学生报告下面插上页码，程序运行后，日志说明如下：

   

前三页报告如下：

   

   

   

 

### 4.9 使用proc means描述数据

可以用proc mens查看一些简单的统计量，Means过程开始于关键词proc means，后面接需要打印的统计量，基本形式：

PROC MEANS options;

如果不加选项，则默认打印出非缺失值个数、均值、标准差、以及最大最小值，下面是用选项可以查看的统计量：

   

如果没有其他语句，proc means语句会给你数据集中所有观测值和所有数值变量的统计量，这里是一些可以用到的语句：

l  BY variable-list; 分变量单独分析，但数据必须先按照variable-list的变量顺序排序（proc sort）。

l  CLASS variable-list; 也是分变量单独分析，看起来会更集中一些，且不需要排序。

l  VAR variable-list; 指定分析中使用哪种数值变量，默认则使用所有的数值变量。

例子 有一个花朵销售的数据，Flowers.dat，包括顾客ID，销售日期，petunias，snapdragons，marigolds三种花的销售量：

   

下面的代码读取数据，计算新变量销售月份，month，并使用proc sort按照月份排序，并使用proc means的by语句来按照月份描述数据：

   

输出结果为：

   

 

### 4.10 将描述性统计写入SAS数据集中

有两种方法可以在SAS数据集中储存描述性统计量，Output Delivery System(ODS)，或者output语句。前者在5.3，后者的基本形式为：

OUTPUT OUT=data-set output-statistic-list;

Data-set是要储存结果的数据集名，output-statistic-list则界定需要保存哪些统计量和名称，可能的形式为：

statistic(variable-list)=name-list

statistic可能是proc means语句中的任何一种统计量（sum，n，mean…），variable-list则界定VAR语句中哪些变量需要输出，name-list则定义统计量的新名字。比如，proc means语句产生了一个数据集ZOOSUM，包括一个观测值和变量lionweight（the mean of the lions’weights），BearWeight（the mean of the bears’weights）。

   

Noprint是告诉SAS不需要产生任何打印结果，因为已经将结果存入数据集中。

**例子** 仍然是花朵销售的数据

   

要描述数据，每个顾客只有一个观测值，包括SUM和MEAN，并且将结果储存到数据集中以便日后分析。下面的程序读取程序，按照CustomerID排序，使用means过程，结果存在totals数据集中。以原始名Petunia,SnapDragon,and Marigold给出sum，以新变量名MeanPetunia,MeanSnapDragon,and MeanMarigold给出mean

   

结果如下：

   

 

### 4.11 用proc freq为数据计数

对一个变量计算频数叫做one-way，两个叫做two-way，多个叫做交叉表。使用proc freq最明显的目的是现实分类数据的分布情况，基本形式为：

PROC FREQ;

​      TABLES variable-combinations;

产生一维频率表，只要列出变量名。下面的语句列出了变量yearseducation的每一个值的个数。

TABLES YearsEducation;

建立两个变量的交叉表需要一个*号，下面的语句显示变量Sex by YearsEducation的频数情况：

TABLES Sex*YearsEducation;

这个语句之后可以用/option的形式添加选项，主要下面几个：

LIST：用list形式打印交叉表（而不是网格）

MISSING：频率统计量中包含缺失值

NOCOL：强制在交叉表中不打印列百分比

NOROW：强制在交叉表中不打印行百分比

OUT=data-set：输出数据集

比如说，使用第二个选项：      TABLES Sex*YearsEducation/MISSING;

**例子** 有一家咖啡店的销售数据，记录了销售的咖啡种类（cappuccino,espresso,kona,or iced coffee），以及每次购买的顾客是打包还是原地就饮：

   

下面的代码就产生了一个one-way和two-way的频率表：

   

代码告诉SAS打印两个表，一个是one-way的频率表，一个是交叉表。交叉表的每个小方格内，SAS打印了频数、百分比、行百分比和列百分比。左边和右边是累积百分比。注意计算频数时没有考虑缺失值。

 

数据表的错误kon？

 

   

 

### 4.12 用proc tabulate产生一个表格报告

比起print，means，freq，Proc tabulate过程产生的报告更耐看。

Proc tabulate的基本形式为：

PROC TABULATE;

CLASS classification-variable-list;

TABLE page-dimension,row-dimension,column-dimension;

Class语句告诉SAS哪些变量将数据分成不同部分。

Table语句可以定义一个表，可以用多个table语句定义多个表，

**维度** table语句可以在报告中指定三个维度：页、行、列。如果只指定一个维度，则默认是列维度；如果指定两个，则是行和列。

**缺失数据** 默认下不考虑缺失数据，在proc语句后面增加missing选项可以改变这种默认：

PROC TABULATE MISSING;

例子 有关于船的一些数据，Boats.dat，记录了每艘船的姓名、港口、移动方式（sailing或者power vesse）l，类型（schooner,catamaran,or yacht），使用它远行的价格

   

你想得到一份报告，包含了每一个港口的、sailing或者power vessel的、每一种类型的、船的数量，下面的代码用proc tabulate创建了一个三维报告：港口作为页、移动方式作为行、类型作为列：

   

报告分两页，及港口的每个值情况为一页：

   

### 4.13 为proc tabulate输出增加统计量

Class语句列出分类变量，而VAR语句告诉SAS那些变量装的是连续数据。基本形式为：

PROC TABULATE;

VAR analysis-variable-list;

CLASS classification-variable-list;

TABLE page-dimension,row-dimension,column-dimension;

**关键词** 下面是tabulate可以计算的值：

ALL:增加行、列或页，显示总数

Max：最高值

Min：最低值

Mean：算术均值

Median：中位数

N：非缺失值个数

Nmiss：缺失值数

P90：90th分位数

Pctn：某类的观测值百分数

Pctsum：某类值总和的百分数

STDDEV：标准差

SUM：求和

Concatenating,crossing,and grouping 维度、变量和关键词可以Concatenating,crossing,and grouping，Concatenating变量或关键词，只需用空格分开列出即可；cross变量或关键字只需要用*分开列出即可；group变量只需要用括号括住变量或关键词。

Concatenating:                          TABLE Locomotion Type ALL;

Crossing:                               TABLE MEAN*Price;

Crossing,grouping,and concatenating:        TABLE PCTN*(Locomotion Type);

例子 仍然是船的例子，

   

下面的代码类似4.12，但多了VAR语句，table只包括两维，但使用了Concatenate,cross,and group：

   

输出结果如下：

   

### 4.14 提升proc tabulate的输出外观

三种方式可以提升输出的外观：

**Format=option** 可以改变数据的格式，比如，在表中使得数字有逗号，并不含小数，则使用：

PROC TABULATE FORMAT=COMMA10.0;

**Box=****和****misstext=options** format只能用在proc语句中，而box=和misstext=只能用在table语句中。box=的作用是在tabulete报告的左上角的空格中写下一句简洁的语句（作用类似标题）。Misstext则是位空数据格指定一个值，默认是一个句号，比如下句：

TABLE Region,MEAN*Sales/BOX='Mean Sales by Region' MISSTEXT='No Sales';

这是告诉SAS在左上角打印“Mean Sales by Region”，并且在没有数据的方格内打印“No Sales”

**例子** 仍然是船的数：

   

如下代码比前面多了format、box、misstext语句。注意format要出现在proc语句中，而box和misstext语句则出现在table语句中。

   

这是“被提升了的”外观，由于format指定dollar9.2，因此都用货币格式输出。左上角的full day excursions是由于box语句，空方格内的none是由于misstext语句。

   

### 4.15 在proc tabulate输出的顶部

有两种方法可以改变顶部信息

**Class** **变量** **变量值** 要改变class语句列出的变量值的顶部，使用format创建一个用户定义的格式，然后用format语句将格式赋给变量。

变量名和关键字 改变变量名和关键字的顶部，用=’text’赋值即可，可以用等号加空值的方法去除顶部，即=’’，语句为：

TABLE Region='',MEAN=''*Sales='Mean Sales by Region';

这是告诉SAS移去region和mean的顶部，并且将sale的顶部换为“Mean Sales by Region”

有时候当行顶部被赋为空格时，会留下一个空白空格，可以用row=float强制去除这种空白空格：      TABLE MEAN=''*Sales='Mean Sales by Region',Region=''/ROW=FLOAT;

**例子** 仍然是船的数据：

   

下面的代码和以前一样，多了对顶部的改变，format语句创建了一个用户定义的格式$typ，并用format语句把这个格式赋给变量type，table语句中locomotion、mean、type的顶部被赋为空格，price的顶部被赋值“Mean Price by Type of Boat.”

   

输出结果为：

   

这样的结果看起来清晰且紧凑。

### 4.16 为proc tabulate输出的数据方格指定多种格式

可以为不同变量指定不同格式，基本形式为：

variable-name*FORMAT=formatw.d

比如在table语句中插入这个复杂的语句：

TABLE Region,MEAN*(Sales*FORMAT=COMMA8.0 Profit*FORMAT=DOLLAR10.2);

这是给变量sales指定格式comma8.0，给变量profit指定格式dollar0.2

**例子** 仍然是船的数据，新增加了一个变量，以显示船的长度：

   

假如你想在报告中同时show出平均价格和平均长度，仅为价格指定货币格式。下面的代码这样实现，为变量price指定格式dollar6.2，为length指定格式6.0：

   

输出结果如下，注意价格和长度的格式不一样：

   

### 4.17 用proc report产生一个简单的输出

Report包含print、means和tabulate、sort的所有功能，可以用一本书来介绍，基本形式为：

​      PROC REPORT NOWINDOWS;

COLUMN variable-list;

Column语句类似于proc print的var语句，告诉SAS哪些变量该包括并以何种顺序，如果遗漏语句column，SAS默认在数据集中包括所有变量，如果遗漏选项nowINDOWS，SAS默认启用交互report窗口。为使数据和顶部能很好的区分开来，可以使用headline和headskip：

PROC REPORT NOWINDOWS HEADLINE HEADSKIP;

Headline在顶部下面拉了一条线，headskip在顶部下面留了一段空白。

**数值变量****VS****字符串变量** 从proc report得到的报告类型，部分依据于使用的数值类型。只要报告中起码有一个字符串变量，默认的报告就是每个观测值一行。但如果报告全是数值变量，默认proc report将会加总这些变量，即使是日期变量也会被加总。

**例子** 有一份关于美国国家公园（national parks）和国家纪念碑（monuments）的数据，Parks.dat，变量包括名字、类型（NP for national park or NM for national monument），地区（East or West），博物馆的数量，野营地的数量：

   

下面的代码形成了两份报告，第一份没有column语句，SAS使用所有变量，第二份使用column语句，选择部分变量：

   

第一份报告与proc print相似，第二份报告，由于只选择museum变量和camping两个数值型变量，默认直接显示加总情况：

   

### 4.18 在proc report中使用define语句

Define用来为单个变量指定一些选项，基本形式为：

DEFINE variable/options’column-header’;

**Usage****选项** 这个选项告诉SAS如何使用这个变量，可能的usage选项包括：

Across：为变量的每一个变量值都创建一个列

Analysis：为变量创建统计量，数值变量默认有这个usage选项，且统计量默认为sum。

Display：为数据集中的每一个观测值都创建一行，对于字符串变量，这个选项是默认的。

Group：为每个变量的变量值都创建一行。

Order：为每个观测值都创建一行，且行值的排列是是按照指定的变量来顺序。

**改变列顶部** proc report中几种方法可以改变列顶部，4.1中的label语句，或者用define语句指定列顶部，下面的代码使得SAS的report按照age排序，并且以“Age at Admission”作为列顶部：

DEFINE Age / ORDER 'Age at/Admission';

**缺失数据** 默认在order，group，和across variables中不考虑缺失值，用missing选项可以改变这种默认：

PROC REPORT NOWINDOWS MISSING;

例子 仍然是关于国家公园和纪念碑的数据，

   

下面的代码包含两个define语句，第一个用order选项来定义region，第二个为变量camping定义列顶部。Camping是一个数值变量，默认有analysis选项。Missing选项也出现在了proc语句中，因此缺失值也会被考虑在报告中：

   

输出结果为：

   

Region有三个变量值，第一个是missing缺失值。

### 4.19 用proc report创建简易报告

Group创建简易行，across创建简易列。

**Group** **变量** 下面的代码告诉SAS创建一个显示每个部门工资总和、奖金总和（数值变量将默认被加总）的报告：

 

 

   

**Across****变量** corss变量，也需要define语句，不同的是，SAS默认不是对变量值求和，而是计数。如果要加总，则需要再across变量和analysis变量之间加逗号，告诉SAS哪个变量要加总，下面的代码告诉SAS用列来显示出每个部门工资和奖金的总和：

   

**例子** 仍然是国家公园和纪念碑的例子，

   

下面的代码包含两个proc report，第一个中，region和type都被定义成group变量，第二个中，region仍然是个group变量，但type是across变量。注意两个column语句基本一样，除了第二个中增加了标点（to cross the across variable with the analysis variables.）。

   

输出结果为

   

### 4.20 给proc report输出增加

Break语句可以为报告增加停顿，为每个指定的变量的变量值增加停顿。基本形式如下：

​     BREAK location variable/options;

RBREAK location/options;

Location有两种可能值——before和after，决定是之前停顿还是之后停顿。斜杠之后的选项告诉SAS插入哪种停顿，主要类型有：

OL         停顿的地方加入横线

Page       开始一个新的页面

Skip        插入一个空行

Summarize  插入数值变量之和

UL         

需要注意的是，break要求指定一个变量，而rbreak不需要。因为rbreak只产生一个停顿（开始或结尾），而break语句为指定的变量的每一个变量值都产生停顿。这个变量必须是group变量或order变量，并且要在define语句中定义过。可以在任何报告中使用rbreak语句，但只能在有最起码一个group或者order变量的报告中使用break语句。

**例子** 仍然是国家公园和纪念碑的例子：

   

下面的代码将region定义为order变量，使用break和rbreak语句和after选项，summarize加总数值变量的和：

   

输出结果为：

   

4.21 为proc report输出增加统计量

简单的方法是在column语句中加入统计量的关键字，常用的有：

Max、min、mean、median、n、nmiss、p90、pctn、pctsum、std、sum

**给变量应用统计量** 给变量应用统计量，在变量和统计量之间插入逗号即可，统计量N不需要逗号。如：

COLUMN Age,MEDIAN N;

为多个变量应用多个统计量，需要括号，如下面代码要求一个变量age应用两个统计量min和max；两个变量height和weight应用一个统计量mean：

COLUMN Age,(MIN MAX)(Height Weight),MEAN;

**例子** 仍然是国家公园和纪念碑的数据：

   

下面的代码包括了两个proc report，都应用了统计量N和mean，但第一个定义type为group变量，第二个定义type为across变量。

   

输出结果为：

   



## 参考文献



 