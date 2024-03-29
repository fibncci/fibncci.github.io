---
官员layout: post
title: "spark查询3"
date: 2022-02-14
tag: 机器学习machineLearning	
---

`[TOC]`

# spark查询

版本

```
pd.show_version() 
#跳板机 ： 
SciPy库依赖于NumPy，它提供了便捷且快速的N维数组操作。os: linux	
python：2.7.11.final.0;				pandas:0.18.0 ;		numpy:1.10.4;
pip:8.1.1;		 scipy:0.17.0 					matplotlib:1.5.1; 
#本机：
Darwin 是MacOSX 操作环境的操作系统成份
python  : 3.8.8.结束.0  ；	pandas: 1.2.4；		numpy   : 1.20.1			
pip: 21.0.1	 ；						scipy  : 1.6.2；			matplotlib : 3.3.4
```







## 1.1 SQLContext
SQLContext是通往SparkSQL的入口。

```sql
one = sqlCtx.sql("sql语句")
scala> spark.sql("select * from ptable").show(100,false)
+---+---+----+
|c1 |c2 |step|
+---+---+----+
|1  |2  |a   |
|3  |4  |a   |
|5  |6  |b   |
|7  |8  |b   |
```

## 1.2 HiveContext
HiveContext是通往hive入口。**HiveContext具有SQLContext的所有功能。 

```sql
one = hive.sql("sql语句")

```



## 1.3 SparkSession
SparkSession是在Spark 2.0中引入的，通过访问SparkSession，我们可以自动访问SparkContext。

```spark2.0
```



## 1.4 操作-高阶操作

```sql
三个join一起上：
one = s_loy_number.join(cx_mem_auto,col('mem_id') == col('member_id'),'left').join(其他表，关联).join()  #可以直接写 


LEAD()函数访问当前行之后的特定物理偏移量的行
LEAD(net_sales,1) OVER ( PARTITION BY brand_name ORDER BY month ) as next_month_sales


.write.saveAsTable("dh_seiz.BMD_yyn_vin_mile2a" ,'parquet','overwrite')  写文档 parquet拼花地板；overwrite覆盖
data.write.saveAsTable(‘shuangshi_dh.dot_analysis’, mode=“append”, format=“hive”, partitionBy=“dt”)

mode=’overwrite’ 模式时，会创建新的表，若表名已存在则会被删除，整个表被重写。
而 mode=’append’ 模式会在直接在原有数据增加新数据。
partitionBy指定分区字段，默认存储为 parquet 文件格式 
partitionBy=['pt_day']；partitionBy='parquet'

df.repartition(5).write.saveAsTable(...)
或
df.repartition(5).registerTempTable('temp_table')
以上设置一个分区只会保存 5 个数据文件。
```

### pyspark.sql 核心类

```

pyspark.SparkContext: Spark 库的主要入口点，它表示与Spark集群的一个连接，其他重要的对象都要依赖它.SparkContext存在于Driver中，是Spark功能的主要入口。 代表着与Spark集群的连接，可以在集群上创建RDD，accumulators和广播变量
pyspark.RDD: 是Spark的主要数据抽象概念，是Spark库中定义的一个抽象类。
pyspark.streaming.StreamingContext 一个定义在Spark Streaming库中定义的类, 每一个Spark Streaming 应用都必须创建这个类
pyspark.streaming.DStrem：离散数据流，是Spark Streaming处理数据流的主要对象
pyspark.sql.SparkSession: 是DataFrame和SQL函数的主要入口点。
pyspark.sql.DataFrame: 是Spark SQL的主要抽象对象，若干行的分布式数据，每一行都要若干个有名字的列。 跟R/Python中的DataFrame 相像 ,有着更丰富的优化。DataFrame可以有很多种方式进行构造，例如： 结构化数据文件，Hive的table, 外部数据库，RDD。
pyspark.sql.Column DataFrame 的列表达.
pyspark.sql.Row DataFrame的行数据
环境配置
os: Win 10
spark: spark-2.4.4-bin-hadoop2.7
python：python 3.7.4
java: jdk 1.8.0_221
```





```
df_customers.cache() # 以列式存储在内存中
df_customers.persist() # 缓存到内存中
df_customers.unpersist() # 移除所有的blocks
df_customers.coalesce(numPartitions= 1) #返回一个有着numPartition的DataFrame
df_customers.repartition(10) ##repartitonByRange
df_customers.rdd.getNumPartitions()# 查看partitons个数
df_customers.columns # 查看列名
['cID', 'name', 'age', 'gender']

df_customers.dtypes # 返回列的数据类型
df_customers.explain() #返回物理计划，调试时应用


```





## 1.5 sql函数

rdd.foreach(println) 或者 rdd.map(println)

rdd.collect().foreach(println),但因为collect()会将整个RDD的数据放到主机上，会使得驱动主机内存溢出。

如果你只想打印出有限个RDD数据，rdd.take(100).foreach(println) 

数据类型： string（姓名、电话、年月日、vin）

```sql

win = 
st_bo = sqlCtx.table("库.表1").             --库表
join(表2,表1.VIN==表2.B_VIN,'left').drop('B_VIN') -- 左链接，删除B_VIN
selectExpr("vin as B_VIN","列名").          --查看列名
					length(列名)-------查看字符的长度
					cast(列名 as int )   #  cast不可以转换日期类型，convert 不可 	
					 avg(列名)

withColumn("rn", row_number().over(win)).  --创建的窗口函数
filter("rn = 1").   												where条件
drop('rn')   																删除字段

sqlCtx.table("dh_seiz.BMD_yyn_vin_mile4").   # library 库；表 table
filter("if_ext=1").      # 过滤
selectExpr("vin","'里程' as EXT_INS_EXP_desc").  # 选择 表达式 expression
distinct()       # 不同的
orderBy(desc('b'))
groupBy("")

time time() 返回当前时间的时间戳（1970纪元后经过的浮点秒数）

spark dataframe的select和selectexpr的区别

select&selectExpr区别
select是把要遍历的集合ienumerable逐一遍历，每次返回一个t，合并之后直接返回一个ienumerable，而selectmany则把原有的集合ienumerable每个元素遍历一遍，每次返回一个ienumerable，把这些ienumerable的“t”合并之后整体返回一个ienumerable。
w = window.partitionBy('b_vin').orderBy(desc('b_start_time'))   select(*,row_number().over(w).alias("cn"))   

selectExpr：可以对指定字段进行特殊处理，可以直接对指定字段调用UDF函数，或者指定别名等。传入String类型参数，得到DataFrame对象。if \case  when \ contant



　　示例，查询id字段，c3字段取别名time，c4字段四舍五入：
jdbcDF .selectExpr(“id” , “c3 as time” , “round(c4)” ).show(false) 

cast(celling(rand()*8))  取值1-8
```





动态加权平均，权重系数修正模型





## 1.7  sql_pandas函数

rdd的 dataframe

函数one = one.toPandas()  这个就是 dataframe的形式了，可以使用这个形式，进行dataframe的运算。

```sql

# 函数one = one.toPandas()

 
SELECT    case when 条件 then 结果 else 结果2  end 
			==>	==>	
count()  			
			==>		==>			one['animal'].value_counts() # 统计动物的每一类的和   count()
FROM      表  
			==>	==>	
join （left join \ right \ inner (两者都存在)\full join（取并集） ）
			==>	==>	
WHERE  	   过滤条件
			==>	==>	
GROUP BY   分组条件
				==>	==>
ORDER BY  (DESC)  排序依据，正序、倒序
				==>	==>
LIMIT 1    				
			==>	==>			df[:1]


```

### dataframe 函数 crud

```sql
增删改查
增	insert into [table] ([column],[column])
删	delete from [table] where ---
改 update [table] set column =    where --- 
查	select --
```

### Create 增 （创建）

| 函数     | Python2.7.11 | python3.8.8                      | 含义 |
| -------- | ------------ | -------------------------------- | ---- |
| Create增 |              | df.loc['k'] = [5.5,'dog','no',2] | 增加 |
|          |              |                                  |      |
|          |              |                                  |      |
|          |              |                                  |      |

### Update改（更新） change 

| 函数          | Python2.7.11 | python3.8.8                                                  | 含义                                    |
| ------------- | ------------ | ------------------------------------------------------------ | --------------------------------------- |
| Update\change |              | df1.columns = ['animal','age','访问','优先']                 | 修改列名                                |
| Update\change |              | df.loc['f','age'] = 1.555                                    | 修改值；df查看                          |
|               |              | df['priority'] = df['priority'].map({'yes': True, 'no': False}) | 把priority 中的 yes、no改成 True、False |

### Retrieve 查（读取 SELECT）



| 函数   | Python2.7.11               | python3.8.8                                                  | 含义                                        |
| ------ | -------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| select | df.loc[1]                  | df.iloc[1]                                                   | 显示第2行                                   |
| select | df.loc[3]                  | df.iloc[:3]                                                  | 显示前三行的数据                            |
| select | df.iloc[df.index[[3,4,8]]] | df.loc[df.index[[3,4,8]]]                                    | 取第4，5，9行数据                           |
| select |                            | df[(df['animal'] ==  'cat') & (df['age'] < 3)]               | 针对animal是cat和年龄小于3岁                |
| select | df[['animal', 'age']]      | df.loc[:, ['animal', 'age']]                                 | 取2列                                       |
| select |                            | df[df['age'].between(2,4)]                                   | 数值可以  ，取符合的行                      |
| select |                            | df['visits'].sum()                                           | 计算某列的和  = 19                          |
| select |                            | df.groupby('animal')['age'].mean() #先分组 ，然后取平均值    | 平均每种动物列的年龄                        |
| select |                            | df.sort_values(by = ['age','visits'],ascending = [False,True]) | 对age的值进行降序排序，对visits进行升序排列 |
|||info()|查看表的填充|
|||||
|||||

###  Delete 删（删除）





lll

| 函数   | Python2.7.11               | python3.8.8                                               | 含义                     |
| ------ | -------------------------- | --------------------------------------------------------- | ---------------------------- |
| Update\change |              | df.loc['f','age'] = 1.555 | 修改值；df查看 |
|               |              |                           |                |
|               |              |                           |                |
|               |              |                           |                |



## 1.6 sql语句

正常的 sql语句语法

```SQL
sqlContext.sql("")
SELECT    case when 条件 then 结果 else 结果2  end  
FROM      表  
join （left join \ right \ inner (两者都存在)\full join（取并集） ）
WHERE  	   过滤条件
GROUP BY   分组条件
ORDER BY  (DESC)  排序依据，正序、倒序
LIMIT 100    显示多少行

union all 使用 " select *  from new   union all select *  from old "，  操作只要保证数据 列名，列的类型相同，列的顺序可以不同，根据第一列的顺序来排序；针对 列的类型不同，列名相同的时候， 需要 " select  字段名1  from new   union all select *  from old " ，此时字段一的类型在new中是string，而在old中为 decimal(38,0) 。 写法必须是 “字段1” 在new中。

补集
select B.*
from test.dbo.m2 B
where NOT EXISTs(select 1 from test.dbo.m1 A where A.姓名=B.姓名 and A.年龄 = B.年龄 and A.学历=B.学历)
```



## 1.8 sql架构

Employee :id;salary;departmentId

Department:

```sqlite
Create table If Not Exists Employee (id int, name varchar(255), salary int, departmentId int);
Create table If Not Exists Department (id int, name varchar(255));
Truncate table Employee;
insert into Employee (id, name, salary, departmentId) values ('1', 'Joe', '85000', '1');
insert into Employee (id, name, salary, departmentId) values ('2', 'Henry', '80000', '2');
insert into Employee (id, name, salary, departmentId) values ('3', 'Sam', '60000', '2');
insert into Employee (id, name, salary, departmentId) values ('4', 'Max', '90000', '1');
insert into Employee (id, name, salary, departmentId) values ('5', 'Janet', '69000', '1');
insert into Employee (id, name, salary, departmentId) values ('6', 'Randy', '85000', '1');
insert into Employee (id, name, salary, departmentId) values ('7', 'Will', '70000', '1');
Truncate table Department;
# Truncate TABLE 的指令。在这个指令之下，表格中的资料会完全消失，可是表格本身会继续存在。 
insert into Department (id, name) values ('1', 'IT');
insert into Department (id, name) values ('2', 'Sales');
```



Persons 该表包含 5 个列，列名分别是："Id_P"、"LastName"、"FirstName"、"Address" 以及 "City"：

```sql
#--Id_P 列的数据类型是 int，包含整数。其余 4 列的数据类型是 varchar，最大长度为 255 个字符。
CREATE TABLE Persons
(
Id_P int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);
```



## 1.9 pyspark

1. 在运行时报错，错误信息为：

missing ALL at 'select' near '\<EOF>'

提示少了 ALL。查询了官网关于union的用法说明，发现，Hive在1.2.0之前的版本只支持union all，在1.2.0之后的版本才支持union.而我的Hive版本是1.1.0。

解决办法只能是使用union all，然后再在外边套一层 select distinct 自己手动实现去重  

spark.sql("select * from HalfStruct").toPandas()

## 2.0 持久化

Spark对RDD的持久化操作(`cache()`、`persist()`、`checkpoint()`)是很重要的，可以将rdd存放在不同的存储介质中，方便后续的操作能重复使用。

1、cache只有一个默认的缓存级别`MEMORY_ONLY`

2、persist可以根据情况设置其它的`缓存级别`。

3、checkpoint接口是将RDD持久化到HDFS中，与**persist的区别**是checkpoint会切断此RDD之前的依赖关系，而persist会保留依赖关系。checkpoint的两大作用：一是spark程序长期驻留，过长的依赖会占用很多的系统资源，定期checkpoint可以有效的节省资源；二是维护过长的依赖关系可能会出现问题，一旦spark程序运行失败，RDD的容错成本会很高。

注意：**checkpoint执行前要先进行cache，避免两次计算。**

StorageLevel类的主构造器包含了5个参数:

- useDisk：使用硬盘（外存）
- useMemory：使用内存
- useOffHeap：使用堆外内存，这是Java虚拟机里面的概念，堆外内存意味着把内存对象分配在Java虚拟机的堆以外的内存，这些内存直接受操作系统管理（而不是虚拟机）。这样做的结果就是能保持一个较小的堆，以减少垃圾收集对应用的影响。
- deserialized：反序列化，其逆过程序列化（Serialization）是java提供的一种机制，将对象表示成一连串的字节；而反序列化就表示将字节恢复为对象的过程。序列化是对象永久化的一种机制，可以将对象及其属性保存起来，并能在反序列化后直接恢复这个对象
- replication：备份数（在多个节点上备份）



FRDS

Balance_num  配件

balance



## 2.1 FROM_UNIXTIME -mysql 

 

### 1、简介：

​    FROM_UNIXTIME，即将时间戳转换为日期类型进行显示。  FROM_UNIXTIME(unix_timestamp,format)

  ps：format是可选参数

### 2、format参数：

```sql
%M 月名字(January……December)
%W 星期名字(Sunday……Saturday)
%D 有英语前缀的月份的日期(1st, 2nd, 3rd, 等等。）
%Y 年, 数字, 4 位
%y 年, 数字, 2 位
%a 缩写的星期名字(Sun……Sat)
%d 月份中的天数, 数字(00……31)
%e 月份中的天数, 数字(0……31)
%m 月, 数字(01……12)
%c 月, 数字(1……12)
%b 缩写的月份名字(Jan……Dec)
%j 一年中的天数(001……366)
%H 小时(00……23)
%k 小时(0……23)
%h 小时(01……12)
%I 小时(01……12)
%l 小时(1……12)
%i 分钟, 数字(00……59)
%r 时间,12 小时(hh:mm:ss [AP]M)
%T 时间,24 小时(hh:mm:ss)
%S 秒(00……59)
%s 秒(00……59)
%p AM或PM
%w 一个星期中的天数(0=Sunday ……6=Saturday ）
%U 星期(0……52), 这里星期天是星期的第一天
%u 星期(0……52), 这里星期一是星期的第一天
%% 一个文字“%”。
```



# 业务

### DTC实时消息发送场景

```
DTC实时消息发送场景
flink
KafKa
Flume
流式数据处理 ：针对 爆胎、遇险、车上故障损坏报警，传送到云端onstar ；然后我们针对后台的数据，进行实时操作，进行风险分类划分等级，作出相应，传送给安吉星。
一个imoment项目的子分类
```





### 保养到期提醒别克官微

````
消息模版数量3  日均发送数量 8383
消息模版数量1  日均发送数量 1
````



## imoment

- 场景
- 1、消息模版数目。
- 2、日均发送数量。
- 3、日均到达数量  
- 4、日均点击数量
- 5、日均点击率 
- 









| 消息模版数目 | 日均发送数量 | 日均到达数量 | 日均点击数量 | 日均点击率4/3 |
| ------------ | ------------ | ------------ | ------------ | ------------- |
| 27--10-11    | 78244        | 3377         |              |               |
| 30--10-10    |              |              |              |               |
| 30--10-9     | 94916        | 5218         | 986          | 18.90%        |
| 27--10-8     | 78277        | 3845         | 708          | 18.41%        |
| 25--10-7     | 63182        | 569          | 124          | 21.79%        |

具体



| 消息模版数目-2020-09-30举例                      | 日均发送数量 | 日均到达数量 | 日均点击数量 |        |
| ------------------------------------------------ | ------------ | ------------ | ------------ | ------ |
| 1. 凯迪app金卡保级礼提醒（提醒新）               | 20           | 0            | 0            |        |
| 2. 凯迪APP入会关怀纪念礼（提醒新）               | 3153         |              |              |        |
| 3.凯迪官微金卡保级礼（提醒新）                   | 15           | 无数据       |              |        |
| 4.凯迪官微入会关怀纪念礼（提醒新）               | 1781         |              |              |        |
| 5.雪佛兰**保险**到期提醒（车机品牌APP）          | 674          | 无数据       |              |        |
| 6. 雪佛兰保养到期提醒（车机品牌APP）             | 465          |              |              |        |
| 8.雪佛兰年检到期提醒（车机品牌APP）              | 342          | 无数据       |              |        |
| 9.别克保险**到期提醒（车机品牌APP）              | 1386         |              |              |        |
| 10. 别克保养到期提醒（车机品牌APP）              | 1514         |              |              |        |
| 11.别克年检到期提醒（车机品牌APP）               | 295          |              |              |        |
| 12.凯迪拉克保险到期提醒（车机品牌APP）           | 1455         |              |              |        |
| 13. 凯迪拉克保养到期提醒（车机品牌APP）          | 1418         |              |              |        |
| 14.凯迪拉克年检到期提醒（车机品牌APP）           | 563          |              |              |        |
| 15. 加油CP合作车机端--------3条                  | 18938        |              |              |        |
| 16.大雾天气预警-------3条                        | 10539        |              |              |        |
| 17.凯迪官微**保养到期提醒** && <u>别克可能有</u> | 593          | 437          | 84           | 19.22% |
| 18.雪佛兰官微**保养提醒**                        | 600          | 2            |              |        |
| 19.雪佛兰官方APP保养提醒                         | 820          |              |              |        |
| 20.DTC实时消息发送场景-----3条                   | 33507        |              |              |        |
| 合计                                             | 78078        | 439          | 84           | 19.13  |
| 1-别克官微当日积分过期提醒                       | 215          | 108          | 21           | 19.44  |
| 2-雪佛兰官微保养提醒                             | 1131         | 11           |              |        |
| 12日出错                                         |              |              |              |        |
|                                                  |              |              |              |        |
|                                                  |              |              |              |        |
|                                                  |              |              |              |        |
|                                                  |              |              |              |        |
|                                                  |              |              |              |        |
|                                                  |              |              |              |        |



当月的20号没有，当月的数据







阳性 =1 要发leads，

阳性 ： 需要进行回站后才去

、阴性 



二分类模型





## icare

- 11.30开始运行





## 算法

逻辑程序员：只会写业务，不会涉及到框架、算法、也不会涉及到底层；不要做这种；快速学习python3-10、加班现状要更好的身体

1. 粒子算法
2. 距离算法：聚类算法

## dataframe

### 1、数据类型

MySQL `TIMESTAMP`是一种保存[日期](http://www.yiibai.com/mysql/date.html)和[时间](http://www.yiibai.com/mysql/time.html)组合的时间[数据类型](http://www.yiibai.com/mysql/data-types.html)。 `TIMESTAMP`列的格式为`YYYY-MM-DD HH:MM:SS`，固定为`19`个字符。 

pandas使用NumPy的数组和dtypes作为序列和数据框中列的数据类型，NumPy支持的数据类型是float、int、bool、timedelta64[ns]。pandas扩展了NumPy的类型系统，用dtype属性来显示元素的数据类型，pandas主要有以下几种dtype：

- 字符串类型：object
- 整数类型：Int64，Int32，Int16, Int8 
- 无符号整数：UInt64，UInt32，UInt16, UInt8 
- 浮点数类型：float64，float32
- 日期和时间类型：datetime64[ns]、datetime64[ns, tz]、timedelta[ns]
- 布尔类型：bool



 

要修改Spark DataFrame的列类型，可以使用"withColumn()"、"cast转换函数"、"selectExpr()"以及SQL表达式。需要注意的是，要转换的类型必须是DataType类的子类。

在Spark中，我们可以将DataFrame列修改（或转换）为以下类型，它们都是DataType类的子类：

- ArrayType
- BinaryType
- BooleanType
- CalendarIntervalType
- DateType
- HiveStringType
- MapType
- NullType
- NumericType
- ObjectType
- StringType
- StructType
- TimestampType

 ###  2、dataframe

a）、由series创建一个dataframe

```python
import numpy as np
import pandas as pd 
data = {'animal': ['cat', 'cat', 'snake', 'dog', 'dog', 'cat', 'snake', 'cat', 'dog', 'dog'],
        'age': [2.5, 3, 0.5, np.nan, 5, 2, 4.5, np.nan, 7, 3],
        'visits': [1, 3, 2, 3, 2, 3, 1, 1, 2, 1],
        'priority': ['yes', 'yes', 'no', 'yes', 'no', 'no', 'no', 'yes', 'no', 'no']}

labels = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
df = pd.DataFrame(data,index = labels)  # 数据的索引是个列表
df

	animal	age	visits	priority # 优先级，访问，年龄
a	cat	2.500	1	yes
b	cat	3.000	3	yes
c	snake	0.500	2	no
d	dog	NaN	3	yes
e	dog	5.000	2	no
f	cat	1.555	3	no
g	snake	4.500	1	no
h	cat	NaN	1	yes
i	dog	7.000	2	no
j	dog	3.000	1	no
```

### 3、 sparkdf 转换成 dataframe

```sql
RDD与spark_df
RDD 转换成spark_df
dataframe = spark.createDataFrame(RDD)
spark_df 转换成 RDD：
RDD = spark_df.rdd.map(lambda x：x)

pandas_df 与 spark_df转换
pandas_pd = saprk_df.toPandas()
spark_df = spark.createDataFrame(pandas_df)
```



### 4、numpy



| max()    | 最大值                                  |
| -------- | --------------------------------------- |
| min()    | 最小值                                  |
| ptp()    | 极差                                    |
| mean()   | 平均值                                  |
| var()    | 方差                                    |
| std()    | 标准差                                  |
| mode()   | 众数    （返回一个dataframe格式的数据） |
| count()  | 非空数目                                |
| median() | 中位数                                  |
| cov()    | 协方差                                  |



### 5、pandas

**统计方法describe()**  ：数值型数据 返回8种指标

count  mean std min 25% 50% 75% max





### 6、matplotlib 可视化 图像



图像的可视化







## 地理位置：

| lon经度   | 纬度lat | 位置                         | 参考位置                       |
| --------- | ------- | ---------------------------- | ------------------------------ |
| 105.818   | 24.98   | 黔西南布依族苗族自治州--贵州 | 浙江杭州 1929公里、1529公里    |
| 110.15677 | 38.73   | 榆林市--陕西                 | 浙江杭州 1645公里、1321.68公里 |
|           |         |                              |                                |
|           |         |                              |                                |



经纬度匹配网址：https://www.qvdv.com/tools/qvdv-coordinate.html

​                             [Spark应用程序第三方jar文件依赖解决方案](https://www.cnblogs.com/dinghong-jo/p/7873646.html)

​							[pyspark 读取 parquet：  sqlCtx.read.parquet](https://blog.csdn.net/Ni_hao2017/article/details/88392875)

 						 	[Pyspark：读取本地文件和HDFS文件](https://blog.csdn.net/abcdrachel/article/details/100122059)

````python
#-*- coding:utf-8 -*-
import  json
from pyspark.sql import SparkSession
#连接集群
spark = SparkSession.builder.master("yarn-client").appName("test").getOrCreate()
#读取数据，数据位置‘hdfs://bd01:8020/a/b/part*.parquet’
df=spark.read.format('parquet').load('hdfs://bd01:8020/a/b/part*.parquet')
print df.show()
#写数据到‘data_result_path’位置，overwrite方式可更改
data.write.mode('overwrite').parquet(data_result_path)

````





##  linux的命令

### mkdir 文件夹

mkdir -p b1/b2/b3     连续创建文件夹 b1、文件夹 b2、文件夹 b3

### rm 删除



```
批量删除：rm -f + *文件关键字*
```

### mv 剪切+复制 cp

命令格式: mv   source源文件    dest源文件

mv（cp）   data1.xlsx    ./wjq/. 



### rz 上传 

rz -be

 
