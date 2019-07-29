。

# Javascript目录

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





# 1.javascript概念

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

###    2、常用的标识符格式：

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

### 6.JavaScript 显示数据

JavaScript 可以通过不同的方式来输出数据：

- 使用 **window.alert()** 弹出警告框。
- 使用  **document.write()** 方法将内容写到 HTML 文档中。
- 使用 **innerHTML** 写入到 HTML 元素。
- 使用 **console.log()** 写入到浏览器的控制台。



```javascript
<script>
window.alert(5 + 6);
</script>

//段落更改
<p id="demo">我的第一个段落。</p>
<script>
document.getElementById("demo").innerHTML = "段落已修改。";
</script>


//Sun Jul 28 2019 10:00:31 GMT+0800 (中国标准时间)
<button onclick="myFunction()">点我</button>
<script>
document.write(Date());
</script>

<script>
a = 5;
b = 6;
c = a + b;
console.log(c);
</script>
```









# 2、js数据类型

> 基本数据类型
>
> - 字符串 string
> - 数值型 int float (近似数) 
> - 布尔型（boolean）Fales  True =逻辑运算符（&& || ！多个条件链接起来）
>
> 复合数据类型
>
> - 对象
> - 数组
>
> 其他数据类型
>
> - 函数
> - null 为假
> - Undefined 未定义的  返回NaN =1/0。infinity无穷大；空字符串；为假
>
> 数据类型的转换
>
> - 隐式数据类型
> - 显式数据类型



数据类型 就是我可以了解到的是描述数据的类型

js基本的数据类型 ：数字类型，字符串型，布尔型，undefined，null
对象类型 数组 

# JS保存数据类型(work)

包括number、string、boolean、undefined、object、function。

### 1.typeof类型的

typeof 是一个一元运算，放在一个运算数之前，运算数可以是原始数据类型，也可以是引用复杂类型。

它返回值是一个用来表示表达式的数据类型的字符串。

```javascript
typeof 的格式
typeof   expression ;
expression 参数是需要查找类型信息的任意表达式。

 typeof一般测试基本类型（Undefined、Boolean、null、Number、String)，
 对引用类型返回object（Function引用类型返回Function）
 
 	//原始数据类型(string,number,boolean,undefined)
	//原始数据值是一种没有额外属性和方法的单一简单数据值。
	var a="abc";
	var b=10;
	var c=true;
	var d;
	var e=null;
	alert("a 	"+typeof a);//string
	alert("b 	"+typeof b);//number
	alert("c 	"+typeof c);//boolean
	alert("d 	"+typeof d);//undefined
	alert("e 	"+typeof e);//object

	//复杂类型（object，function）
	var obj1=new Array();
	var obj2=new Date(); 
 	var obj3=new Number();
	var obj4=new String(); 
	var obj5=new Function();
	var obj6=new Boolean();
	alert("obj1  "+typeof(obj1));//object
	alert("obj2  "+typeof(obj2));//object
	alert("obj3  "+typeof(obj3));//object
	alert("obj4  "+typeof(obj4));//object
	alert("obj5  "+typeof(obj5));//function
	alert("obj6  "+typeof(obj6));//object
```

### 2.instanceof运算符

因为typeof遇到null,数组,对象时都会返回object类型，所以当我们要判断

一个对象具体是否为一个数组时或者判断某个变量是否为某个对象的实例,

则要选择使用另一个语法instanceof，instanceof返回的是一个布尔值。

```javascript
instanceof的格式
expression instanceof class 表达式运算符类
expression  必选项。任意对象表达式。
class　　必选项。任意已定义的对象类。

//instanceof 运算符与 typeof 运算符相似，用于识别正在处理的对象的类型。
//与 typeof 方法不同的是，instanceof 方法要求开发者明确地确认对象为某特定类型。
var a = {};
alert(a instanceof Object);  //true
var b = [];
alert(b instanceof Array);  //true

//需要注意的是，instanceof只能用来判断对象和函数，不能用来判断字符串和数字等，如：
var b = '123';
alert(b instanceof String);  //false
alert(typeof b);  //string

var c = new String("123");
alert(c instanceof String);  //true
alert(typeof c);  //object

//另外，用instanceof可以判断变量是否为数组：
var arr = [1,2,3]; 
alert(arr instanceof Array);   // true
```







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
		

# 隐式数据转换（work）

js的数据类型非常弱的，在使用算术运算符的时候,运算符两边的数据类型可以是任意的  这是因为js的引擎它在代码运行之前偷偷把数据类型进行转换 ，这种转换我们称之为隐式转换
	

小类型向大类型转换

### 一、自动类型转换也叫“隐式类型转换”。

小类型向大类型的转换会自动完成，不需要程序员编写额外的代码，由jvm负责。

自动类型转换的规则：符号位会自动扩展，负数补1，正数补0

自动类型转换包含以下情况：

​             1.byte->short->int->long

​													->double->

​			2.int和char类型的数据在某些情况下可以自动相互转换。

### 二、

int类型为32位，最高位为符号位，其余31位为尾数。

long类型为64位，最高位为符号位，其余63位为尾数。

 ps：尾数：精度值，用来存放数据。

int类型转换成long类型后，因为是负数，所以符号位补了32位1。

 小类型向大类型转型一般情况下是安全的。----------

当小类型的精度高于大类型时要注意精度丢失的隐患。

### 三、

int类型为32位，最高位为符号位，其余31位为尾数，float类型为也是32位，但是尾数是23位。

int类型存放了一个28位的数，而flaot类型只能承载23位，转换后精度丢失最后一位的数据。

当小类型的精度（尾数）高于大类型时，要注意精度丢失问题。

#### 小练习：

```javascript
  <script type="text/javascript">
   
    var a='7'
    var b=3
    var c = 2
    alert(a+b)
    console.log(a-b-c)   //2
    console.log(a+b+c)	//732
    console.log(b+c+a)	//57
  </script>
```





### 流程控制语句:

```

if语句
if(条件){
	函数体
}
------------
if else语句
if(条件){
	函数体1
}else{
	函数体2
}
--------------
if.....else if......else语句
if(条件1){
	
}else if(条件2){
	
}else if(条件n){
	
}else{
	
}

------------
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

>1、while循环：先判断条件 当条件成立 再执行
>while(循环成立条件){
>	....
>}
>
>2do...while循环:不论条件成不成立 先执行一遍 再判断
>do{
>	.....
>}while(循环成立条件)
>
>3、for循环
>4、for in循环
>
>continue：
>跳过当前循环，直接进入循环的下一个步骤
>
>break:
>结束循环



# 3.DOM操作

属性、文本操作，css操作，对象与数组，面向对象编程

```
ECMAScript规定核心的语法:bom dom
BOM（browser object model）：浏览器对象模型
```

## 2.DOM总结

#### 1. DOM基本介绍

DOM 是 Document Object Model 文档对象模型

- HTML DOM
- XML DOM

#### 2. HTML DOM 对象参考

- 2.1 document 对象

- 属性 ….

- 方法 见手册

- 2.2 form 对象

- 2.3 image 对象

- 2.4 anchor 对象

- 2.5 base 对象

- 2.6 canvas 对象

- 2.7 Event 对象

- 2.8 input 系列对象

- 2.9 select 对象

- 2.10 option 对象

- 2.11 style 对象

- 2.12 table 对象

- 2.13 tableRow 对象

- 2.14 tableCell 对象 ~~~

  #### 3. XML DOM 对象

### HTML DOM

- 2.2 form 对象
- 2.3 image 对象
- 2.4 anchor 对象
- 2.5 base 对象
- 2.6 canvas 对象
- 2.7 Event 对象
- 2.8 input 系列对象
  - focus() 获焦
  - blur() 失焦
  - select() 选中
- 2.9 select 对象
- 2.10 option 对象
- 2.11 style 对象
- 2.12 table 对象
- 2.13 tableRow 对象
- 2.14 tableCell 对象

------

### 节点操作 (XML DOM)

#### XML DOM 节点

#### 1.节点介绍

- 1.1 什么是节点 node HTML文档中 所有的组成部分 都称之为节点
  - document 文档
  - element 元素
  - attr 属性
  - text 文本
  - comment 注释
- 1.2 节点树 子节点 父节点 同辈节点 后代节点 先辈节点
- 1.3 节点的访问
  - 得到节点
    - document 直接 document
    - element getId/getTagName..
    - attr element.getAttributeNode(‘attrname’)
    - text 子节点
    - comment 子节点
  - 获取子节点 childNodes
  - 获取子元素节点 children
  - 获取第一个子节点 firstChild
  - 获取最后一个子节点 lastChild
  - 获取父节点 parentNode
  - 获取父元素节点 parentElement
  - 获取前一个节点 previousSibling
  - 获取后一个节点 nextSibling
- 1.4 节点属性 nodeName documnet: #document element: 标签名 attr: 属性名 text: #text comment: #comment nodeValue document: null element: null attr: 属性值 text: 文本内容 注释: 注释内容 nodeType document: 9 element: 1 attr: 2 text: 3 commnet: 8

#### 2.节点操作

2.1 获取节点 element: ID/TAGNAME/子节点/父节点/同辈 attr: element.getAttributeNode() 属性节点 element.getAttribute() 属性值 element.attr 属性值

2.2 改变节点(改变节点的值) nodeValue 2.3 删除节点 2.4 替换节点 2.5 插入节点 2.6 创建节点 2.7 克隆节点

#### 3. XML 对象

- node
- nodeList
- document
- element
- attr
- text
- comment

#### 4. HTMLElement(**元素**)对象

```javascript
className   类名

scrollLeft  滚动条至 左边界像素
scrollTop   滚动条至 上边界像素

offsetLeft  距离已定位父元素的 左偏移量
offsetTop   距离已定位父元素的 上偏移量

innerHTML   元素内部的内容(不含标签)
innerText   元素内部所有的文本内容
outerHTML   元素的内容(含标签)

offsetWidth  盒子模型,实际的宽: 内容+内边距+边框
offsetHeight  盒子模型,实际的高: 内容+内边距+边框

clientWidth  宽 + 内边距
clientHeight 高 + 内边距

scrollWidth  宽 + 内边距 + 计算里面元素的大小
scrollHeight 高 + 内边距 + 计算里面元素的大小

document.documentElement.clientHeight  视口高度
document.documentElement.scrollHeight  文档高度
```

### PS. 补充

- PS1. DOM 元素对象的 属性和方法 http://www.runoob.com/jsref/dom-obj-all.html
- PS2. MDN文档
  - Mozilla 开发者社区(MDN): https://developer.mozilla.org/zh-CN/
  - JavaScript MDN文档 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript





## 2.DOM树

#### DOM节点：元素节点/属性节点/文本节点

### js操作节点（增删改查）

#### 一、获取节点：

##### 1、通过id获取

document.getElementById("id")
节点.getElementById("id值")
！返回的是一个具体的节点

##### 2、通过标签名来获取节点

getElementsByTagName("div")
！返回的是一个节点数组,即使只有一个

##### 3、通过标签的Name值来获取

getElementsByName("标签的name值")
!返回的是一个节点数组

##### 4、通过class值来获取节点

getElementsByClassName("类名")
!返回的是一个节点数组

##### *5、querySelector('选择器')//根据我选择器的结果集返回第一个

##### *6、querySelectorAll('选择器')//根据我选择器的结果集返回

!!!getElementsByClassName在IE9以下无效的

##### 7、获取节点.parentNode-->获取到节点的父节点

##### 8、获取节点.children-->获取到节点的子节点集合

​     获取节点.childNodes-->获取到节点的子节点集合（带有前后两个空白的文本节点）

#### 二、创建插入节点

1、document.createElement("div")//创建一个元素节点
2、document.createTextNode("文本文本")//创建一个文本节点

##### 被插入的节点

.appendChild(创建的节点)//在节点后面添加

##### 父节点

.insertBefore(创建的节点，被插入的节点)//在已知父节点的某个孩子前面添加内容

##### 改变文本内容：

选中的元素.innerText='';//直接将HTML代码当做字符来处理
选中的元素.innerHTML='';//可以识别HTML代码
删除：直接设置为空（""）

##### 替换节点：

父节点.replaceChild(新节点,老节点)

##### 克隆(复制节点)

选中的元素.cloneNode(true/false):
当clone参数为true的时候：选中元素里面所有懂得内容克隆
当clone参数为false的时候：选中元素本身克隆

##### 删除节点：

父节点.removeChild(子节点)	

##### 节点的属性操作

如何来获取属性：
	选中的元素.getAttribute("属性名")
更改属性：
	选中的元素.setAttribute("属性名","新的属性值")
新增属性
	选中的元素.setAttribute("原本没有的属性名","属性值")
删除属性
	选中的元素.removeAttribute("属性名");
	







# BOM

### 1. 什么是BOM

```
ECMAScript规定核心的语法:bom dom
Browser Object Model  浏览器对象模型
```

### 2. JavaScript 对象层次

#### 2.1 对象种类

- 自定义对象 Object

- 内置对象 A/S/B/N/D/M/R/G

- BOM 浏览器对象模型

- DOM Document Object Model 文档对象模型 ~~~

  #### 2.2 对象树 (倒树状结构)

```
                     window
                        |
history   location   document screen   navigator
                        |
                    doc    html
                            |
                    head   body
                     |       |
                title...   div span p h4 li  ul...
```

### 3. BOM 对象

#### 3.1 window

- 描述整个浏览器窗口的对象

- 它是JS中所有对象的根对象

- 使用window的属性或方法,可以省略window的调用

- 自定义对象 / 变量 / 函数

- 属性: 见手册

- 方法: clearInterval() 取消由 setInterval() 设置的 timeout。 clearTimeout() 取消由 setTimeout() 方法设置的 timeout。 setInterval() 按照指定的周期（以毫秒计）来调用函数或计算表达式。 setTimeout() 在指定的毫秒数后调用函数或计算表达式。

  alert() 警告框 prompt() 输入框 confirm() 确认框

  open() 打开新窗口 close() 关闭自己打开过的窗口 print() 打印

  scrollTo() 滚到哪去 scrollBy() 滚过少

#### 3.2 history 历史

length长度

back() forward() go() 后退,前进,去

#### 3.3 location位置

- 属性
- 方法

#### 3.4 screen屏幕

#### 3.5 navigator导航器





# JavaScript 事件

### 1. 事件的绑定

- 事件作为 元素的属性

  ```
    <button event="JS CODE"></button>
  ```

- 事件作为 元素对象的属性

  ```
    element.event = function(){}
    element.event = funName;
  ```

- 事件监听(标准)

  ```
    非IE:
        addEventListener('事件名字', funName, false);
    IE:
        attachEvent('事件名字', funName);
  ```

  \~~~

  ### 2. 解除绑定

- 第1种和第2种的绑定方式

  ```
    重写覆盖属性为null 或 空的function(){}
    element.event = null
    element.event = function() {}
  ```

- 监听方式

  ```
    非IE:
        removeEventListener('事件名字', funName, false);
    IE:
        detachEvent('事件名字', funName);
  ```

### 3. 给一组元素绑定事件和this的使用

- 循环绑定事件,获取触发事件的元素对象时,需要使用this
- 元素内部绑定事件时传入this.表示该元素对象自己

### 4. 闭包 closure

- 在循环绑定事件时,将循环变量保留下来,就必须使用闭包

- 用一组元素去控制另一组元素时 请使用闭包

- 语法:

  ```
    for (...) {
        (function(i,x,y){
            element.event = function (){
                // i,x,y 值皆可用
            }
        })(i,x,y);
    }
  ```

### 5. 常用事件

### 5.1 鼠标事件

- onclick 单击触发
- ondblclick 双击触发
- oncontextmenu 右击触发/return false阻止系统菜单
- onmouseover 鼠标指向触发
- onmouseout 鼠标移开触发
- onmousedown 鼠标按下触发
- onmouseup 鼠标松开触发
- onmousemove 鼠标移动触发

### 5.2 键盘事件

- onkeydown 按下按键触发
- onkeyup 松开按键触发
- onkeypress 按下并松开触发(JS高级事件) 不是所有的按键都能触发,无输出的按键是无法触发 (方向键/shift/ctrl/alt/fn/tab/大小写切换)

### 5.3 表单事件

- onsubmit 表单被提交时触发
- onreset 表单被重置时触发
- onfocus 获取焦点时触发
- onblur 失去焦点时触发

### 5.4 框架/对象事件

### 5.5 其他事件

### 6. event事件对象

- 6.1 获取 `var e = e || window.event;`

- 6.2 属性

  ```
    e.x       鼠标X坐标
    e.y       鼠标Y坐标
    e.button  检测鼠标按键 0左键/1中键/2右键
    e.offsetX 鼠标相对于 触发事件元素的x坐标
    e.offsetY 鼠标相对于 触发事件元素的y坐标
    e.keyCode 按键键码
  ```

### 7. 常用HTML元素属性

```
    innerHTML   双标签之间的文本

    当前元素 相对与body 或已定位的父元素的 偏移量
    offsetTop
    offsetLeft

    当前元素 左边缘或顶边缘 滚过的像素值
    scrollTop
    scrollLeft

    className   当前元素的class属性值
    tagName     当前元素的标签名
```

------



# js对象及数组

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

# 4.AJAX(js)

## 1.Ajax概念

**AJAX 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。**

AJAX = 异步 JavaScript + XML。

```
xml可扩展标记语言，标准通用标记语言的子集，是一种用于标记电子文件使其具有结构性的标记语言。
```

AJAX 是一种用于创建快速动态网页的技术。

通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

传统的网页（不使用 AJAX）如果需要更新内容，必需重载整个网页面。



## 2.参数

- ### 1-type

  类型：String

  默认值: “GET”)。请求方式 (“POST” 或 “GET”)， 默认为 “GET”。注意：其它 HTTP 请求方法，如 PUT 和 DELETE 也可以使用，但仅部分浏览器支持。

- ### 2-url

  类型：String

  默认值: 当前页地址。发送请求的地址。

- ### 3-dataType

  类型：String

  预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息来智能判断，比如 XML MIME 类型就被识别为 XML。

  在 1.4 中，JSON 就会生成一个 JavaScript 对象，而 script 则会执行这个脚本。随后服务器端返回的数据会根据这个值解析后，传递给回调函数。可用值:

  - “xml”: 返回 XML 文档，可用 jQuery 处理。
  - “html”: 返回纯文本 HTML 信息；包含的 script 标签会在插入 dom 时执行。
  - “script”: 返回纯文本 JavaScript 代码。不会自动缓存结果。除非设置了 “cache” 参数。注意：在远程请求时(不在同一个域下)，所有 POST 请求都将转为 GET 请求。（因为将使用 DOM 的 script标签来加载）
  - “json”: 返回 JSON 数据 。
  - “jsonp”: JSONP 格式。使用 JSONP 形式调用函数时，如 “myurl?callback=?” jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。
  - “text”: 返回纯文本字符串

- ### 4-data

  类型：String

  发送到服务器的数据。将自动转换为请求字符串格式。GET 请求中将附加在 URL 后。查看 processData 选项说明以禁止此自动转换。必须为 Key/Value 格式。如果为数组，jQuery 将自动为不同值对应同一个名称。如 {foo:[“bar1”, “bar2”]} 转换为 ‘&foo=bar1&foo=bar2’。

- ### 5-success

  类型：Function

  请求成功后的回调函数。

  参数：由服务器返回，并根据 dataType 参数进行处理后的数据；描述状态的字符串。

  这是一个 Ajax 事件。

  

  

  ### 6-error

  类型：Function

  默认值: 自动判断 (xml 或 html)。请求失败时调用此函数。

  有以下三个参数：XMLHttpRequest 对象、错误信息、（可选）捕获的异常对象。

  如果发生了错误，错误信息（第二个参数）除了得到 null 之外，还可能是 “timeout”, “error”, “notmodified” 和 “parsererror”。

  这是一个 Ajax 事件。

  

  举例说明一些错误原因：

  **1. dataType错误**

  类型错误：后台返回的dataType类型和前台写的不一致会跳入error

  格式错误：jquery1.4之后对json的格式要求非常严格，json格式错误也会跳入error.{“test”:1} 注意格式

  有时，在不需要返回值的情况下，扔按模板格式，设置了dataType:”json”,参数；这时候，ajax传值正确时，出现200返回成功状态下报错的特殊情况。

  ### 2.async请求同步异步问题

   async默认是true(异步请求),如果想一个Ajax执行完后再执行另一个Ajax, 需要把async=false

   例如，你用post请求传值到另一个页面后台，但是页面一加载你的ajax就已经执行过了，传值接收是在后台才完成的，这时候就请求不到数据，所以可以考虑把ajax请求改为同步试试。

  ### 3. data不能不写

  data为空也一定要传”{}”；不然返回的是xml格式的。并提示parsererror. data:”{}”

  parsererror的异常和Header 类型也有关系。及编码header(‘Content-type: text/html; **charset=utf8**’);

  ### 4. 传递的参数

   必须是ajax支持的编码格式

  ### 5.URL路径问题

   路径不能有中文

## 3.考题

```javascript
请求的url:user.php
发送方式:post
发送数据:id为userid的文本框值
返回数据:json格式
请求成功:将返回数据写入id为username的文本框中
请求失败:弹出文本“操作失败”


$.ajax({
	type:”POST”,
​	url:”user.php”,
​	dateType:”json”,
​	date:{“id”:$(“#userid”).val()};
​	success:function(msg){
​	$(“#username”).val(msg);
​	},
​	error:function(msg){
​	alert(“操作失败”);
​	}
})
```





# 5.ajax请求五步（work）

```
小结：
	1.了解js面试题 大概内容
	2.了解ajax大致 似乎用方法
```

```javascript
原生ajax请求的五个步骤
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









# 6.js测试题目

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





# 6.JS继承（work）

JS是面向对象的弱类型语言，继承也是其非常强大的特性之一。

##### 继承 是面向对象软件技术当中的一个概念，与多态、抽象共为面向对象的三个基本特征。 

##### 继承可以使得子类具有父类的属性和方法或者重新定义、追加属性和方法等。

##### 主要分为四种: 原型继承、 构造函数继承、 组合继承以及 寄生继承

```
既然要实现继承，那么首先我们得有一个父类，代码如下：
// 定义一个动物类
function Animal (name) {
  // 属性
  this.name = name || 'Animal';
  // 实例方法
  this.sleep = function(){
    console.log(this.name + '正在睡觉！');
  }
}
// 原型方法
Animal.prototype.eat = function(food) {
  console.log(this.name + '正在吃：' + food);
};



```

##### 先提供一个父类

```
//父类
function Person(name) {
	this.name = name;
	this.sum = function(){
		alert(this.name);
	}
}
Person.prototype.age = 10; //给构造函数添加了原型属性 
```

##### 原型链继承

```
function Per(){
	this.name = "ker";
}
Per.prototype = new Person();
var per1 = new Per();
//instanceof 判断元素是否在另一个元素的原型链上
//per1 继承了Person的属性 返回true
console.log(per1 instanceof Person);//true
```

### 1、原型(链)继承（3、4两大致命缺陷）

**核心：** 将父类的实例作为子类的原型  

##### 原型和构造函数的关系：

优点：父类新增原型方法/原型属性，子类都能访问到

缺点：继承过来的属性的值都是一样的了，只能对调用对象的属性进行重新赋值

```javascript
function Cat(){ 
}
Cat.prototype = new Animal();
Cat.prototype.name = 'cat';

//　Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.eat('fish'));
console.log(cat.sleep());
console.log(cat instanceof Animal); //true 
console.log(cat instanceof Cat); //true
```

### 特点：

```


1. 非常纯粹的继承关系，实例是子类的实例，也是父类的实例
2. 父类新增原型方法/原型属性，子类都能访问到
3. 简单，易于实现

缺点：

1. 要想为子类新增属性和方法，必须要在`new Animal()`这样的语句之后执行，不能放到构造器中
2. 无法实现多继承
3. 来自原型对象的引用属性是所有实例共享的（详细请看附录代码： 示例1）
4. 创建子类实例时，无法向父类构造函传参

缺点1中描述有误：可以在Cat构造函数中，为Cat实例增加实例属性。如果要新增原型属性和方法，则必须放在new Animal()这样的语句之后执行。
--------------------
特点:(小老弟)
实例可继承的属性有: 实例的构造函数的属性
父类构造函数属性
父类原型的属性

缺点：
新实例无法向父类构造函数传参
继承单一
所有新实例都会共享父类实例的属性
```



### 2、构造继承



```
function Con(){
	Person.call(this,"jer");
	this.age = 12;
}
var con1 = new Con();
console.log(con1.name);
console.log(con1.age);
console.log(con1 instanceof Person);//false
```

- 重点: 用.call()或.apply() 将父类构造函数引入子类函数

**核心：**使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类（没用到原型）

##### 借用构造函数:构造函数名字.call(当前对象,属性,属性,属性....); 解决了属性继承,并且值不重复的问题

优点：可以实现多继承（call多个父类对象）

缺点：无法继承父类方法

```javascript
function Cat(name){
  Animal.call(this);
  this.name = name || 'Tom';
}

// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // false
console.log(cat instanceof Cat); // true
```

```
特点：

1. 解决了1中，子类实例共享父类引用属性的问题
2. 创建子类实例时，可以向父类传递参数
3. 可以实现多继承（call多个父类对象）

缺点：

1. 实例并不是父类的实例，只是子类的实例
2. 只能继承父类的实例属性和方法，不能继承原型属性/方法
3. 无法实现函数复用，每个子类都有父类实例函数的副本，影响性能

- 特点:(小老弟)
  - 只继承了父类构造函数的属性，没有继承父类原型的属性
  - 解决了原型链继承缺点
  - 可以继承多个构造函数属性(call 多个)
  - 在子实例中可向父实例传参
- 缺点
  - 只能继承父类构造函数的属性
  - 无法实现构造函数的复用 (每次用每次都有重新调用)
```





### 3、组合继承★★★★（仅仅多消耗了一点内存）

##### 组合继承(组合原型链继承和借用构造函数继承)

```
function SubType(name) {
	Person.call(this,name);//构造函数继承
}
SubType.prototype = new Person();//原型链继承
var sub = new SubType("ger");
console.log(sub.name);
console.log(sub.age);
```

- 重点: 结合了两种模式的优点，传参和复用

##### 简单来说：就是原型继承和构造函数继承的组合

优点：既可以多继承还可以继承父类的方法

缺点：要生成两个实例，比前两种要占内存

**核心：**通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

```javascript
function Cat(name){
  Animal.call(this);
  this.name = name || 'Tom';
}
Cat.prototype = new Animal();

// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); // true
```

### 特点：

```
1. 弥补了方式2的缺陷，可以继承实例属性/方法，也可以继承原型属性/方法
2. 既是子类的实例，也是父类的实例
3. 不存在引用属性共享问题
4. 可传参
5. 函数可复用

缺点：
1. 调用了两次父类构造函数，生成了两份实例（子类实例将子类原型上的那份屏蔽了）
---------------



- 特点
  - 可以继承父类原型上的属性，可以传参，可复用
  - 每个新实例引入的构造函数属性是私有的
- 缺点：
  - 调用了两次父类构造函数（耗内存），子类的构造函数会代替原型上的构造函数


```





### 4、寄生组合继承★★★★（实现复杂，扣掉一颗星）

```javascript
//寄生
function content(obj){
	function F(){}
	F.prototype = obj;
	return new F();
}
var con = content(Person.prototype);
//con实例（F实例）的原型继承了父类函数的原型
//上述就像原型链继承，只不过只继承了原型属性

//组合
function Sub(){
	Person.call(this);
}//继承了父类构造函数的属性解决了组合式两次调用构造函数属性的缺点

Sub.prototype = con;
con.constructor = Sub;//修复实例
var sub1 = new Sub();
//Sub实例就继承了构造函数属性，父类实例，con的函数属性

----------------------------------------------------------------------------------
//不同写法
function F(){};
F.prototype = Person.prototype;
function Sub(){
	Person.call(this);
}
Sub.prototype = new F();
var sub2 = new Sub();
```

- 重点:修复了组合继承的问题

**核心：**通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的构造的时候，就不会初始化两次实例方法/属性，避免的组合继承的缺点

##### 其实就是在原型式继承得到对象的基础上，在内部再以某种方式来增强对象，然后返回增强

优点：不限制调用方式，不管是new 子类()还是子类(),返回的对象具有相同的效果

缺点：不能多继承

```javascript
function Cat(name){
  Animal.call(this);
  this.name = name || 'Tom';
}
(function(){
  // 创建一个没有实例方法的类
  var Super = function(){};
  Super.prototype = Animal.prototype;
  //将实例作为子类的原型
  Cat.prototype = new Super();
})();

// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); //true
```

特点：堪称完美

缺点：实现较为复杂

### 5、实例继承（不需要看）

**核心：**为父类实例添加新特性，作为子类实例返回

```
function Cat(name){
  var instance = new Animal();
  instance.name = name || 'Tom';
  return instance;
}

// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); // false
```

 特点：

1. 不限制调用方式，不管是`new 子类()`还是`子类()`,返回的对象具有相同的效果

缺点：

1. 实例是父类的实例，不是子类的实例
2. 不支持多继承

### 6、拷贝继承（★缺点1）不用看

```javascript
function Cat(name){
  var animal = new Animal();
  for(var p in animal){
    Cat.prototype[p] = animal[p];
  }
  Cat.prototype.name = name || 'Tom';
}

// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // false
console.log(cat instanceof Cat); // true
```

特点：

1. 支持多继承

缺点：

1. 效率较低，内存占用高（因为要拷贝父类的属性）
2. 无法获取父类不可枚举的方法（不可枚举方法，不能使用for in 访问到）



## 附录代码：

示例一：

```
function Animal (name) {
  // 属性
  this.name = name || 'Animal';
  // 实例方法
  this.sleep = function(){
    console.log(this.name + '正在睡觉！');
  }
  //实例引用属性
  this.features = [];
}
function Cat(name){
}
Cat.prototype = new Animal();

var tom = new Cat('Tom');
var kissy = new Cat('Kissy');

console.log(tom.name); // "Animal"
console.log(kissy.name); // "Animal"
console.log(tom.features); // []
console.log(kissy.features); // []

tom.name = 'Tom-New Name';
tom.features.push('eat');

//针对父类实例值类型成员的更改，不影响
console.log(tom.name); // "Tom-New Name"
console.log(kissy.name); // "Animal"
//针对父类实例引用类型成员的更改，会通过影响其他子类实例
console.log(tom.features); // ['eat']
console.log(kissy.features); // ['eat']
```



```
原因分析：
关键点：属性查找过程

执行tom.features.push，首先找tom对象的实例属性（找不到），
那么去原型对象中找，也就是Animal的实例。发现有，那么就直接在这个对象的
features属性中插入值。
在console.log(kissy.features); 的时候。同上，kissy实例上没有，那么去原型上找。
刚好原型上有，就直接返回，但是注意，这个原型对象中features属性值已经变化了。
```



# 7.js里==和===



==：运算符称作相等，用来检测两个操作数是否相等，这里的相等定义的非常宽松，可以允许进行类型转换
===：用来检测两个操作数是否严格相等
1、对于string,number等基础类型，==和===是有区别的
不同类型间比较，==之比较“转化成同一类型后的值”看“值”是否相等；

##### ===如果类型不同，其结果就是不等

同类型比较，直接进行“值”比较，两者结果一样

2、对于Array,Object等高级类型，==和===是没有区别的

3、基础类型与高级类型，==和===是有区别的

对于==，将高级转化为基础类型，进行“值”比较，因为类型不同，===结果为false

# 8.应用题



实现代码：

```


var arr = [2,3,4,5,6];
var sum =0;
for (var i = 1; i <= arr.length; i++) {
	sum+= arr[i];
}
console.log(sum);
```


