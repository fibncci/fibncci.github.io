# 一、javascript介绍以及起源

变量和常量的知识，基本数据类型，运算符，基本数据类型间的转换，流程控制语句

	js一种直译型脚本语言，一种动态语言、弱类型语言、支持内置类型。它的解释器被称为javascript引擎。它浏览器的一部分。用于客户端的脚本语言，最早是html网页上使用用来给HTML增加动态效果。                                                                      没有任何关系
	
	为了取得发展以及技术上的优势  微软曾推出过Jscript，跟javascript一样可以在浏览器上运行。为了统一规格，javascript兼容于ECMA标准，因此它也称为ECMAScript
	
	ECMA欧洲计算机联合商协会

### 	js用途 


	1、嵌入文本到我们的HTML页面上
	2、对浏览器事件作出响应
	3、读写HTML
	4、在数据提交到服务器之前先做数据验证
	5、检测访客的浏览信息
	6、控制cookie
	7、基于nodeJs技术进行服务端的编程


​	



### js组成部分


1、ECMAScript规定核心的语法
2、DOM（document object model）:文档对象模型
3、BOM（browser object model）：浏览器对象模型

### 	二、javascrip的语法

js可以有几种写法：


​	
​	1、写在script标签内
​	2、写在外部js文件里面
​	3、写在标签内部的


​	
### 三、标识符和关键字

### 1、什么是标识符：

/*
     * 标识符
      *     - 在JS中所有的可以由我们自主命名的都可以称为是标识符
      *     - 例如：变量名、函数名、属性名都属于标识符
      *     - 命名一个标识符时需要遵守如下的规则：
      *         1.标识符中可以含有字母 、数字 、下划线_ 、$符号
      *         2.标识符不能以数字开头
      *         3.标识符不能是javascript中的关键字或保留字
      *         4.标识符一般都采用驼峰命名法
      *             - 首字母小写，每个单词的开头字母大写，其余字母小写
      *             helloWorld  xxxYyyZzz
      * 
      *     - JS底层保存标识符时实际上是采用的Unicode编码，
      *         所以理论上讲，所有的utf-8中含有的内容都可以作为标识符
            */
          /*

### 2、常用的标识符格式：

​	i j
​	xxx_zzz
​	_xxxx
​	$xxx
​	a1
​	aaaBbbCcc
​	AaaBbbCcc
​	！！！！注意一点：标识符不要跟关键字同名，数字不允许作为首字母出现，这样我们js比较容易的区分开标识符和数字
​	

### 3、关键字：

关键字是指我js语言中有特定含义，称为js语法中一部分的 那些单词
var let const for if foreach break continue do while switch....

### 4、保留字：

未来某个js版本会称为关键字的单词，一样是不可以当成变量名或者方法名来使用      

### 5、注释：

//:单行注释
/**/：多行注释


​	
​	
### 四、js的数据类型

数据类型 就是我可以了解到的是描述数据的类型

js基本的数据类型 ：

数字类型，字符串型，布尔型，undefined，null
对象类型 数组 

### 1、数字类型（Number）

只有一种数字类型，数字 可以是小数 ，也可以的整数
以0开头 默认使用8进制来表示我的这个数字
以0x开头 默认使用16进制来表述我的这个数字
如果以-开头 默认以负数
如果我带有e：以科学计数法来解析我的这个数字


​	
### 2、字符串型（string）

字符串是存储字符的变量，用来表示文本的数据类型，程序中的字符串是包含单引号/双引号的，由单引号来界定我双引号中包含的字符串 反过来
es6模板字符串("`")

### 3、布尔类型（boolean）

一般是用在流程控制语句中，字符串和数字类型都是无穷多个，然而我们的布尔数据类型只有两个：true 和 false
这两个个值一般用于说明某个事物是真或者假
js一般用布尔类型来比较所得到的结果

### 4、null（空）

null
关键字null是一个特殊的值，它表示变量为空值，用来定义空的或者是不存在的引用。
如果试图去引用一个没有定义的值，就会返回一个null。
这里注意一点：null并不等于"" 或者0

### 5、undefined（未定义）

这个值表示变量不含有值，没有定义的值，或者被定义了一个不存在的属性值


​	
### ！null和undefined区别：

null它表示一个变量被赋予一个空值，而undefined是表示变量还没有被赋值

### 五、运算符

用于执行程序代码运算，会针对一个以上操作数来进行

	1、算术运算符
	+   -   *   /   %  ++  --
	字符串拼接使用“+”
	
	2、比较运算符
	
	<
	>
	==
	！=
	<=
	>=
	=== 全等于：将数值以及数据类型一并比较
	！==不全等于：将数值以及数据类型一并比较
	
	3、赋值运算符
	=
	+= 
	
	-=
	*=
	/=
	%=
	a=a+2;==>a+=2
	a=a-2;==>a-=2
	a=a*2;==>a*=2
	a=a/2;==>a/=2
	a=a%2;==>a%=2	
	
	4、逻辑运算符
	 &&  全真为真
	||  一个为真就是真
	
	！  取反
	
	逻辑短路
	
	5、三元运算符（三目运算符）
	表达式1?表达式2:表达式3
	
	当我的表达式1成立时  执行表达式2  否则执行表达式3


​	




​	
### 六、数据类型间转换

### 1、显示数据类型转换

​	1.1转数字类型：

### 1.Number()：

可以将任意类型的参数转换为数字类型，遵循以下规则：
​	1、如果它是一个布尔值true和false将被分别转成1和0；
​	2、如果它是以个数字，返回它本身
​	3、如果是null，返回0；
​	4、如果是undefined，返回NaN
​	5、如果是一个字符串：
​		1）如果这个字符串只包含数字，则直接将它转成10进制数字（忽略前面的0）
​		2）如果有有效浮点格式，将它转成一个浮点数值
​		3）如果是空字符串,转换为0
​		4）如果以上都不符合==>NaN

### 2.parseInt(string,num):

可以解析一个字符串，返回一个整数

1）忽略字符串前面所有的空格，直到找到第一个非空字符为止
2）如果第一个字符不是数字或者“-” 直接返回NaN
3）如果第一个字符是数字，它解析到遇到的第一个不是数字的字符为止




4）如果上面解析完结果是以0开头，就将它当成一个八进制来解析
		5）如果以0x开头，则当成十六进制来解析。
		6）如果我指定了num参数，那么 它就以num进制来解析

### 3.转字符串类型：

​		1.String():将任意的一个类型的值转换为字符串，遵循一下下规则：
​		1）如果是null，==>"null"
​		2)如果是undefined ==>"undefined"

toFied(num):可以把Number类型四舍五入为指定小数位的字符串。
		返回的字符串，num保留小数位
	
Boolean():如果这个值是空字符串（""）、数字零（0）、undefined或者null 会返回false，否则返回true
!空格并不是空字符串
		

### 2、隐式数据类型转换

js的数据类型非常弱的，在使用算术运算符的时候,运算符两边的数据类型可以是任意的  这是因为js的引擎它在代码运行之前偷偷把数据类型进行转换 ，这种转换我们称之为隐式转换
	

	流程控制语句:
	if语句
	if(条件){
		函数体
	}
	
	if else语句
	if(条件){
		函数体1
	}else{
		函数体2
	}
	
	if.....else if......else语句
	if(条件1){
		
	}else if(条件2){
		
	}else if(条件n){
		
	}else{
		
	}
	switch语句:多分支语句
	
	switch(变量){
		case a:
		.....
		break;
		case b:
		.....
		break;
		case c:
		...
		break;
		........
		default:
			....
			break;
	}


​	


### 循环结构：

1、while循环：先判断条件 当条件成立 再执行
while(循环成立条件){
	....
}

2do...while循环:不论条件成不成立 先执行一遍 再判断
do{
	.....
}while(循环成立条件)

3、for循环
4、for in循环

continue：
跳过当前循环，直接进入循环的下一个步骤

break:
结束循环









# jsDOM操作

属性、文本操作，css操作，对象与数组，面向对象编程



###  DOM树

### DOM节点：

* 元素节点
* 属性节点
* 文本节点

### js操作节点（增删改查）

### 一、获取节点：

1、通过id获取
document.getElementById("id")
节点.getElementById("id值")
！返回的是一个具体的节点

2、通过标签名来获取节点
getElementsByTagName("div")
！返回的是一个节点数组,即使只有一个

3、通过标签的Name值来获取
getElementsByName("标签的name值")
!返回的是一个节点数组

4、通过class值来获取节点
getElementsByClassName("类名")
!返回的是一个节点数组

*5、querySelector('选择器')//根据我选择器的结果集返回第一个
*6、querySelectorAll('选择器')//根据我选择器的结果集返回

!!!getElementsByClassName在IE9以下无效的

7、获取节点.parentNode-->获取到节点的父节点
8、获取节点.children-->获取到节点的子节点集合
     获取节点.childNodes-->获取到节点的子节点集合（带有前后两个空白的文本节点）

### 二、创建插入节点

1、document.createElement("div")//创建一个元素节点
2、document.createTextNode("文本文本")//创建一个文本节点

### 被插入的节点

.appendChild(创建的节点)//在节点后面添加

### 父节点

.insertBefore(创建的节点，被插入的节点)//在已知父节点的某个孩子前面添加内容

### 改变文本内容：

选中的元素.innerText='';//直接将HTML代码当做字符来处理
选中的元素.innerHTML='';//可以识别HTML代码
删除：直接设置为空（""）

### 替换节点：

父节点.replaceChild(新节点,老节点)

### 克隆(复制节点)

选中的元素.cloneNode(true/false):
当clone参数为true的时候：选中元素里面所有懂得内容克隆
当clone参数为false的时候：选中元素本身克隆

### 删除节点：

父节点.removeChild(子节点)	



节点的属性操作
如何来获取属性：
	选中的元素.getAttribute("属性名")
更改属性：
	选中的元素.setAttribute("属性名","新的属性值")
新增属性
	选中的元素.setAttribute("原本没有的属性名","属性值")
删除属性
	选中的元素.removeAttribute("属性名");
	

### js对象及数组

### js对象的分类：

### 内置对象

js已经提供好的对象，这些对象它有自己的方法和属性。如：
Number，String，Boolean，Date，Math，Array，window，location......



### 自定义对象

开发人员自己去定义的一个对象

1、如何来定义对象：
	1)语法：var obj={};
	2)使用我们的new关键字来创建
		var obj=new Object()//创建一个空对象
		var arr = new Array()//创建一个空的数组对象
		var time = new Date()//创建一个初始化的日期对象
	3)通过构造函数的形式来创建对象
		var obj = new Test();
		function Test(num1,num2){
			this.number1 = num1;
			this.number2 = num2
		}
		

4)通过Object.create()创建对象
		var obj = Object.create(null)
		var obj = Object.create({"name":"tom","age"："3"})

### 2、对象的属性

​	1、对象.属性名 = 属性值
​	2、对象属性值可以是任何一种js的数据类型 包括对象

### 3、获取对象的属性

​	1、对象.属性名
​	2、对象[属性名]

### 4、遍历对象（for in循环）

​	for(var 变量  in 对象){
​		//  属性名：变量
​		//  属性值: 对象[变量]
​	}

### 二、数组

1、数组内可以存放任意数据类型的数据（本质上它也是对象）
2、数组元素不赋值的情况下 值为undefined
3、如果数组打印的时候，元素不赋值""
4、访问数组范围之外的元素，不会出现越界的问题，undefined
5、定义数组大小，照样可以添加更多元素

### 定义数组的方法：

1、var arr=[]//定义一个空数组
2、var arr=[10,20,{"name":"tomy","age":19},0.1,"string",true,["aaa","bbb"]]//定义的同时赋值
3、var arr=new Array();//定义一个空数组
4、var arr = new Array(10,20,{"name":"tomy","age":19},0.1,"string",true,["aaa","bbb"])//定义的同时赋值
5、var arr=new Array(10)//定义一个长度为10的数组

赋值：
数组名[下标] = 值

取值：
数组名[下标]

更改值：
数组名[下标] = 值

数组的分类：
索引数组：下标是数字
关联数组：下标是可以是自定义的字符

​	

### 一维数组

### 二维数组:数组里面的元素还是数组

​	var arr = [["id","aaa",10],[1,1,2,3],[1,1,1]]
​	

### 循环二维数组

var arr = [["id","aaa",10],[1,1,2,3],[["a","b","c"],1,1]]
		

### 多维数组

js 操作数组的api
！1）concat():连接两个或更多的数组的方法(不修改原数组)
	var arr1 = [1,2,3];
	var arr2 = [7,8,9];
	var newArr = arr1.concat(arr2)
！2）join()：将数组转成字符串，并通过指定的字符分割(未指定默认使用逗号“，”)
	var arr=[1,2,3]
	var str=arr.join("")
3）toString():吧数组转成字符串然后通过,隔开
	var arr=["a","b","c","d"];
	var string = arr.toString()
	console.log(string)
！4）slice():从已有的数组中返回指定的元素
	语法：
	var string = arr.slice(start,end)//start==>开始位置下标   end==>结束位置下标
	var Arr = [1,2,3,4,5,6,7,8,9,10]
	var subArr = Arr.slice(2,4)
	console.log(Arr)
5）splice():删除 插入 会修改原数组
	var arr=[]
	语法：var temp = arr.splice(num1,num2)
	arr:被切割数组
	temp：切割完获取数组元素的数组
	num1：切割开始的下标
	num2：切割多少位

var del = [1,2,3,4,5,6,7,8,9]
		var delected = del.splice(3,5)
		console.log(delected)
		console.log(del)
!6）push：向数组的末尾添加一个或多个的新元素
		var arr=[1,2,3,4,5,6,7,8,9]
		arr.push(10)

!7)	pop:删除并返回最后一个元素(直接修改原数组)
	var arr=[1,2,3,4,5,6,7,8,9]
	var a = arr.pop()
!8) shift:删除并返回第一个元素
	var arr=[1,2,3,4,5,6,7,8,9]
	var a = arr.shift()
!9) sort:排序
	var arr=[9,1,3,6,7,2,8,5,4]
	var a = arr.sort()
10）reverse:颠倒的数组顺序
	var arr=[1,2,3,4,5,6,7,8,9]
	var a = arr.reverse()


​			
​		
