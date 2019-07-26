# Javascript-0

1.工作原理

2.基本语法

3.变量的使用

4.运算符

5.流程控制

6.函数应用

7.js 对象

8.js常用的

9.js的事件处理

10.DOM中内及属性

11.html将html元素转为js

12.通过自己定义的方式

13.Dom节点的创建

14.JS的bom

15.bom的重点对象

16.位置和事件对象

17.对戏哦昂应用event应用

18.js表单

19.表单注册

20.js开发

21.Ajax在开发中的应用

22.js的Dom

23.Dom的节点操作

24js 常见开发



# javascript数据类型-0

基本数据类型

- 字符串
- 数值型 int float (近似数) 
- 布尔型（boolean）Fales  True =逻辑运算符（&& || ！多个条件链接起来）

复合数据类型

- 对象
- 数组

其他数据类型

- 函数
- null 为假
- Undefined 未定义的  返回NaN =1/0。infinity无穷大；空字符串；为假

数据类型的转换

- 隐式数据类型
- 显式数据类型



# 一、javascript介绍以及起源

变量和常量的知识，基本数据类型，运算符，基本数据类型间的转换，流程控制语句

```
js一种直译型脚本语言，一种动态语言、弱类型语言、支持内置类型。它的解释器被称为javascript引擎。它浏览器的一部分。用于客户端的脚本语言，最早是html网页上使用用来给HTML增加动态效果。                                                                      没有任何关系

为了取得发展以及技术上的优势  微软曾推出过Jscript，跟javascript一样可以在浏览器上运行。为了统一规格，javascript兼容于ECMA标准，因此它也称为ECMAScript

ECMA欧洲计算机联合商协会
```

### js用途 

```
1、嵌入文本到我们的HTML页面上
2、对浏览器事件作出响应
3、读写HTML
4、在数据提交到服务器之前先做数据验证
5、检测访客的浏览信息
6、控制cookie
7、基于nodeJs技术进行服务端的编程
```

​	



### js组成部分

1、ECMAScript规定核心的语法
2、DOM（document object model）:文档对象模型
3、BOM（browser object model）：浏览器对象模型

### 二、javascrip的语法

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

```
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
```

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
	

```
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
```

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



### DOM树

### DOM节点：

- 元素节点
- 属性节点
- 文本节点

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



# 原生ajax请求的五个步骤

```javascript
//第一步，创建XMLHttpRequest对象
var xmlHttp = new XMLHttpRequest();
function CommentAll() {
    //第二步，注册回调函数
    xmlHttp.onreadystatechange =callback1;
    //{
    //    if (xmlHttp.readyState == 4)
    //        if (xmlHttp.status == 200) {
    //            var responseText = xmlHttp.responseText;

    //        }
    //}
    //第三步，配置请求信息，open(),get
    //get请求下参数加在url后，.ashx?methodName = GetAllComment&str1=str1&str2=str2
    xmlHttp.open("post", "/ashx/myzhuye/Detail.ashx?methodName=GetAllComment", true);

    //post请求下需要配置请求头信息
    //xmlHttp.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

    //第四步，发送请求,post请求下，要传递的参数放这
    xmlHttp.send("methodName = GetAllComment&str1=str1&str2=str2");//"

}
//第五步，创建回调函数
function callback1() {
    if (xmlHttp.readyState == 4)
        if (xmlHttp.status == 200) {
            //取得返回的数据
            var data = xmlHttp.responseText;
            //json字符串转为json格式
            data = eval(data);
            $.each(data,
                function(i, v) {
                    alert(v);
                });       
        }
}



//后台方法
 private  void GetAllComment(HttpContext context)
        {

            //Params可以取得get与post方式传递过来的值。
            string methodName = context.Request.Params["methodName"];

            //QueryString只能取得get方式传递过来的值。
            string str1 = context.Request.Form["str1"];

            //取得httpRequest传来的值，包括get与post方式
            string str2 = context.Request["str2"];

            List<string> comments = new List<string>();

            comments.Add(methodName);

            comments.Add(str1);

            comments.Add(str2);


            //ajax接受的是json类型，需要把返回的数据转给json格式
            string commentsJson = new JavaScriptSerializer().Serialize(comments);
            context.Response.Write(commentsJson);
        }
```









js测试题目

1.QQ号从10000开始，目前最高位10位，可以匹配QQ号的是``/^[1-9]\d{4,9}$/``

```js

第一位不能是0；
QQ一共的位数，5位-10位
（部分看到的11位是QQ里把主显设置，设为手机号才会显示的，真正的还是11位）

function isQQ(qq) {
    qq=qq+"";
    var reg=/^[1-9]\d{4,9}$/;
    if (reg.test(qq)){
        return true;
    } else{
        return false;
    }
}
console.log(isQQ(123));//false
console.log(isQQ("2222"));//false
console.log(isQQ("12222"));//true
console.log(isQQ("22222"));//true
console.log(isQQ("1234567890"));//true
console.log(isQQ("12345678901"));//false
console.log(isQQ("222w22"));//false

//对于my_data循环
// var my_data={a:’Ape’, b:’Banana’, c:’Citronella’};
// for(var key in my_data) {}


```



2.分析下面代码输出结果5



```javascript
var arr =  new Array(5);

arr(0) = 1;

arr(2) = 2;

Console.log(arr.length);


		
		var arr =  new Array(5);

		arr(0) = 1;

		arr(2) = 2;

		Console.log(arr.length);

 
变形2---输出5
emp=new Array(5);

emp[1]=1;

emp[2]=2;

document.write(emp.length);

变形3 输出6
var arr = new Array(5)
arr[1]= 1;
arr[5]=2;
console.log(arr.length);

```



3.下列选项Dom的节点类型：





5.js月份

```javascript
<script type="text/javascript">

var d=new Date()

var month=new Array(12)
month[0]="January"
month[1]="February"
month[2]="March"
month[3]="April"
month[4]="May"
month[5]="June"
month[6]="July"
month[7]="August"
month[8]="September"
month[9]="October"
month[10]="November"
month[11]="December"

document.write("The month is " + month[d.getMonth()])

</script>

//输出The month is July
```

### 输出b

```
var s = "abcdefg";
alert(s.substring(1,2));
```







| **4.****AD** | **下列(   )可以使窗口显示前一个页面(选择二项)** |            |
| ------------ | ----------------------------------------------- | ---------- |
|              |                                                 |            |
|              | **A.**                                          | back( )    |
|              | **B.****加载历史列表中的下一个URL页面**         | forward( ) |
|              | **C.**                                          | go(1)      |
|              | **D.**                                          | go(-1)     |

| **27.B** | **下列正则表达式中,(   )可以匹配首位是小写字母,其他位数是小写字母或数字的最少两位字符串.(选择一项)** |                    |
| -------- | ------------------------------------------------------------ | ------------------ |
|          |                                                              |                    |
|          | **A.**                                                       | /^\w{2,}/          |
|          | **B.**                                                       | /^[a-z][a-z0-9]+$/ |
|          | **C.**                                                       | /^[a-z0-9]+$/      |
|          | **D.**                                                       | /^[a-z]\d+$/       |

| **31.AB** | **以下关于jQuery选择器使用正确的是(   )(选择二项)** |                                                              |
| --------- | --------------------------------------------------- | ------------------------------------------------------------ |
|           |                                                     |                                                              |
|           | **A.**                                              | 对于<div id=”id#a”>welcome</div>的正确方法是$(“#id\\#a”)     |
|           | **B.**                                              | 对于<div id="id[2]">welcome</div>的正确方法是$(“#id\\[2\\]”) |

37在JavaScript中，把字符串“123”转换为整型值123的正确方法是：

```
var str="123";

var num=parseInt(str);
```







| **38.D** | **对于ECMAScript的描述中，以下说法错误的是(   )(选择一项)** |                                                            |
| -------- | ----------------------------------------------------------- | ---------------------------------------------------------- |
|          |                                                             |                                                            |
|          | **A.**                                                      | 它是一个重要的标准，并不是javascript唯一的部分             |
|          | **B.**                                                      | 是一种开放的，国际上广为接受的，标准的脚本言规范。         |
|          | **C.**                                                      | 它主要描述了语法、变量、数据类型、运算符、逻辑控制语句等。 |
|          | **D.**no                                                    | ECMAScript遵循了JavaScript标准。                           |









| **46.B** | **关于document对象的常用方法，以下说法错误的有(   )(选择一项)** |                                                     |
| -------- | ------------------------------------------------------------ | --------------------------------------------------- |
|          |                                                              |                                                     |
|          | **A.**                                                       | getElementById( )  返回拥有指定id的第一个对象的引用 |
|          | **B.**                                                       | getElementById( )  返回拥有指定id的对象的集合       |
|          | **C.**                                                       | getElementsByName( )  返回拥有指定名称的对象的集合  |
|          | **D.**                                                       | write( ) 向文档写文本，HTML表达式或javascript代码   |

 

| **47.D** | **对于Math对象常用方法，以下描述不正确的是(   )(选择一项)** |                                      |
| -------- | ----------------------------------------------------------- | ------------------------------------ |
|          |                                                             |                                      |
|          | **A.**                                                      | ceil( ) 向上舍入                     |
|          | **B.**                                                      | floor( )向下舍入                     |
|          | **C.**                                                      | round( )四舍五入                     |
|          | **D.**                                                      | random( )返回0~1中的随机数，包括0和1 |

 49.在JavasScript中，若要实现复选框全选功能，document.getElementsByName("chk");

```javascript
<script type="text/javascript">

  function allChecked( ){

         var allck=document.getElementsByName("chk");//这儿
         for(var i = 0 ;i<allck.length;i++){

                   allck[i].checked=true;

          }

  }

</script>

<body>

<p><input name="chk" type="checkbox" value="滑雪">滑雪

<p><input name="chk" type="checkbox" value="游泳">游泳

<p><input name="chk" type="checkbox" value="爬山">爬山

<p><input name="btn" type="button" onClick="allChecked( )" value="选择">

</body>
```

**在JavaScript中，页面中显示当天日期**今天是2019年7月25日

```
<script type="text/javascript">

	
var today;

today=new Date( );

document.write("今天是"+today.getFullYear( )+"年"

        +(today.getMonth( )+1)+"月"+today.getDate( )+"日");

</script>
```



# 应用题

5现需要实现ajax 请求，详细信息如下：

请求的url ： user.php

发送方式:post

发送数据：id位userid的文本框的值

返回数据：json格式

请求成功：将返回数据写入id位username的文本框中

请求失败：弹出文本"操作失败"

请提供代码实现上述功能

```

```



实现代码：

```


var arr = [2,3,4,5,6];
var sum =0;
for (var i = 1; i <= arr.length; i++) {
	sum+= arr[i];
}
console.log(sum);
```







1. 
2. 4
3. 6
4. u