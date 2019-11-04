---
layout: post
title: "html+css+js"
date: 2019-10-28
tag: topic
---





## HTML+CSS+JS 

1. 有哪些标签可以正常使用 `src`属性, 至少写出4个

   ```
   <img src = "">  图片
   <video src = "">视频
   <audio src =""> 音频
   
   答案
   img图片
   frame iframe框架集
   input type为image的提交按钮
   scirpt	脚本
   style	样式表 
   
    src 不是本身，有实际的位置，
    href导入图标 两个之间有联系,css 是用link导入
   
   ```

   > ​	img, video, audio, frame, iframe, script

2. 点击文本`百度`, 在新标签页中打开`http://www.baidu.com` 

   ```
   <a href ="http://www.baidu.com">百度</a>
   ```

   > <a href="http://www.baidu.com" target="_blank"> 百度 </a><a href ="http://www.baidu.com">百度</a>
   >
   > ```
   > <a href="http://www.baidu.com" target="_blank"> 百度 </a>
   > 目标空白
   > ```

3. 写出至少5个HTML5新增属性

   ```
   3d
   ```

   > placeholder
   >
   > autofocus
   > autocomplete
   > multiple
   > required

4. 网页中的汉字变成了乱码, 如何解决

   ```
   
   <meta charset="UTF-8">
   ```

5. 文件路径有哪些形式

   ```
   绝对定位  
       有盘符的
       带着url全地址
   相对定位  就是指以当前文件开始 
       ./当前目录  
       ../表示上一级目录 
       /根目录
   ```

   > 相对路径: 
   > ./  	当前目录
   > ../ 	上级目录
   > / 	    根目录
   >
   > 绝对路径:
   > 	在线地址
   > 	本地地址

6. 请简述css的权重规则

   ```
   tag 1  , .class 10  ; #id 100 ； !important
   选择器相加
   ```

   > 元素选择器 占权重: 1
   >
   > class选择器 占权重: 10
   > id选择器 占权重: 100
   > 最高权重: !important 	写在属性值的后面
   >
   > 权重相同时, css离元素越近, 优先级越高
   > 权重不同时, 权重越高, 优先级越高

7. 如何利用伪对象来实现清除浮动

   ```
   display：block
   clean
   
   父级标签:befor{
       content:'';
       display:block;
       clear:both;
   }
   
   
   ```

   > 父级::after{
   > content:'';
   > display:table;
   > clear:both;
   >
   > }

8. 文本如何实现水平居中, 块级元素又如何实现水平居中

   ```
   text-align ： center
   ```

   > 	文本: 给包含文本的元素赋予 text-align: center
   >
   > 块级: 给块级本身赋予 margin-left:auto 和 margin-right:auto

9. 广告永远在窗口两侧, 不会随着页面的滚动而滚动, 请问这是如何实现的

   ```
   相对定位
   position:fixed;
   ```

   > 广告1{
   > position: fixed;
   > left: 0;
   >
   > }
   >
   > 广告2{
   > 	position: fixed;
   > 	right: 0;
   > }

10. 子元素如何基于父元素的四个角作为原点

    ```
    子集元素
    position：absplute
    
    
    父级元素{
        position:relative;
    }
    子集元素{
        position:absolute;
    }
    ```

    > 父元素: 任意定位 	(常用相对定位)
    >
    > 子元素: 绝对定位
    >
    > 

11. 为什么要做css初始化

    ```
    做初始化的目的是为了能让css的样式规整，不出问题
    避免了页面的问题
    ```

    > 因为各大浏览器对标签的默认效果不统一, 就会出现同样的css, 在不同的浏览器中, 显示不同的效果. 
    >
    > 所以需要css初始化, 统一各大浏览器对标签的默认效果.

12. `==` 和 `===` 有什么区别

    ```
     == 是值的大小相等
     === 是值 和 typeof类型相同
    
    ```

    > ==   只能判断两边的数据大小是否一致
    >
    > ===  判断两边的数据大小是否一致 且 两边的数据类型是否一致 

13. Js的原始类型有哪些?  引用类型有哪些?

    ```
     整数number 字符串string  布尔boolean  未定义undefined  null 
     function函数 对象object  array数组 
    
    ```

    > 原始类型: number, string, boolean, null, undefined
    >
    > 引用类型: array, object, function

14. 页面之间的传输方式有哪些?

    ```
    一个是跳转
    
    ```

    > 传输方式有: Get 和 Post
    >
    > 区别: 
    > 	Get: 明文传输
    > 		速度快
    > 		安全性低
    > 		传输大小在HTTP协议上无限制, 在浏览器中大多限制在 2KB 以内
    > 		一般用于 查询操作
    >
    > 
    >
    > ​	Post: 密文传输
    > ​		 速度慢
    > ​		 安全性高
    > ​		 传输大小在HTTP协议上无限制, 在服务器端,根据服务器性能高低而决定
    > ​		 一般用于 增删改操作

15. 读程序, 写结果

    ```
    (function(){  
    	var a = b = 3;
    })();
    console.log(b);
    console.log(a);
    
    ```

    ```
    结果: 自带return 
    3 3 
    a是一个局部变量 在函数结束时变量消失
    b是一个全局变量
    ```

    > 	变量b = 3, 全局变量
    > 	变量a 报错, 没有定义

16. 读程序, 写结果

    ```
    console.log( 9 >> 1 );
    
    ```

    ```
    结果: 4
    ```

17. 读程序, 写结果

    ```
    const length = 4;
    const numbers = [];
    for (var i = 0; i < length; i++);{
    //这儿有问题 ；分号
      numbers.push(i + 1);
    }
    
    console.log( numbers );
    
    ```

    ```
    结果: const的用法
    []
    [5]
    ```

18. 用 Js 实现任意数的阶乘

    ```js
    //输入整数
    //大于0整数 的是 1*2*3* n
    //小于等于0 的是 -1
    
    
    var num=99
    num=Number(num) //这个地方出来小数 会报错
    num = ~~num
    var result=1
    if(num < 0){
        console.log("请输入大于等于0的数")
    }else{for(var i=num; i>0;i-- ){ //这儿用倒叙就可以少些一个else if
            result *= i
        }
        console.log(result)
    }
    
    // 9.33262154439441e+155
    
    //break 不能随便用；放在for 循环里面
    //return 在function里面
    ```

    > 1！=1，
    >
    > 2！=2，
    >
    > 3！=6，
    >
    > 4！=24，
    >
    > 5！=120，
    >
    > 6！=720，
    >
    > 7！=5040，
    >
    > 8！=40320
    >
    > 9！=362880
    >
    > 10！=3628800
    >
    > 另外，数学家定义，0！=1
    >
    > 我们所说的阶乘是定义在自然数范围里的，小数没有阶乘，像0.5！，0.65！，0.777！都是错误的。
    >
    > 但是，有时候我们会将Gamma函数定义为非整数的阶乘，因为当x是正整数n的时候，Gamma函数的值是n-1的阶乘。
    >
    > 伽玛函数（Gamma Function）
    >
    > Γ（x)=∫e^(-t)*t^(x-1)dt (积分下限是零上限是＋∞）(x<>0,-1,-2,-3,……)
    >
    > 运用积分的知识，我们可以证明Γ（x)＝(x-1) * Γ（x-1)
    >
    > 所以，当x是整数n时，Γ（n) = (n-1)(n-2)……＝(n-1)!

    ```
    递归写法
    function factorial( num ){
    
        if ( num < 0 ) {
            return -1;
        }else if( num == 0 || num == 1){
            return 1;
        }else{
            return ( num * factorial( num-1 ) );
        }
    
    }
    console.log( factorial(5) );
    ```

    

19. 请使用 冒泡排序法对数组进行排序,  数组:  [5,2,8,3,7,9,4]

    ```js
    //对于所有的数进行排序，例如 如果比较5 与 2 的值，前面比后面大就交换，
    //从小到大排序
    
    console.time()
    function maopao(){
        for (var i=0 ;i<arr.length;i++) {
            for (var j= 0;j<arr.length;j++)
              //arr.length-i-1
                if (arr[j]>arr[j+1]){
                    arr[j] ^= arr[j+1]
                    arr[j+1] ^= arr[j]
                    arr[j] ^= arr[j+1]
                }
        }
        return arr
    }
    var  arr = [5,2,8,3,7,9,4]
    console.log(maopao(arr))
    console.timeEnd()
    
    [ 2, 3, 4, 5, 7, 8, 9 ]
    //default: 3.841ms第三
    
    
    ```

    > ```js
    > var arr = [5,2,8,3,7,9,4];
    > var sign;
    > 
    > for(var i = 0; i < arr.length-1; i++){
    >     sign = false;
    > 
    >     for(var j = 0; j < arr.length-1-i; j++){
    >         if(arr[j] > arr[j+1]){
    >             arr[j] ^= arr[j+1];
    >             arr[j+1] ^= arr[j];
    >             arr[j] ^= arr[j+1];
    >             sign = true; 
    >         }
    >     }
    > 
    >     if(sign == false){
    >         break;
    >     }
    > }
    > console.log(arr);
    > 
    > //default: 3.766ms第一
    > 
    > ```
    >
    > 非正规写法
    >
    > ```js
    > console.time()
    > var att =  [5,2,8,3,7,9,4]
    > for(var i = 0; i < att.length; i++ ){
    >     for(var j = i+1; j < att.length; j++){
    >         if(att[i] > att[j] ){
    >             att[j] ^= att[i]
    >             att[i] ^= att[j]
    >             att[j] ^= att[i]
    > 
    >         }
    >     }
    > }
    > console.log(att)
    > console.timeEnd()
    > //default: 3.963ms 最慢
    > 
    > ```
    >
    > 稍微快一点
    >
    > ```js
    > [ 2, 3, 4, 5, 7, 8, 9 ]
    > default: 0.070ms
    > console.time()
    > function maopao(){
    >     for (var i=0 ;i<arr.length;i++) {
    >         for (var j= 0;j<arr.length-1-i;j++)
    >             if (arr[j]>arr[j+1]){
    >                 arr[j] ^= arr[j+1]
    >                 arr[j+1] ^= arr[j]
    >                 arr[j] ^= arr[j+1]
    >             }
    >     }
    >     return arr
    > }
    > var  arr = [5,2,8,3,7,9,4]
    > console.log(maopao(arr))
    > //default: 3.784ms 第二
    > 
    > ```
    >
    > 

20. 获取字符串中所有的汉字

    ```js
    //字符串中所有的汉字，用正则获取；或者用字符串函数
    
    var str ="s是的的撒低级 jfjj；"
    / ^a-zA-Z0-9;"?/\"`~*&^%$#@!<> /g
    ```

    > ```js
    > var str = "'12abc试;\\/;'.试水abc";
    > var reg = /[\u4e00-\u9fa5]/g
    > console.log( str.match(reg) );
    > console.log(str.match(   /[\u4e00-\u9fa5]/g ));
    > // [ '试', '试', '水' ]
    > ```
    >
    > 





## 知识整理

1. break 不能放在if语句中

   1. ```js
      var i=8
      for (var j= 0;j<i;j++){
          if (j>3) {
              console.log(i,j)
              break;
          }
          }
      //8 4
      
      ```

2.  整数number 字符串string  布尔boolean  未定义undefined  null  







## 准备

请使用 插入排序法对数组进行排序,  数组:  [5,2,8,3,7,9,4]

```js
//分析先把 2拿出来，与5做比较， 2 5 ；
//再拿出8与 5 分别比较，放在5的后面 2 5 8
//再取3 与2比较 与5比较，放在中间  2 3 5 8

function cr(){
	var j=1 
	var i=0
	if (num[i]>num[j]) {
		num[j] ^= num[i],num[i] ^= num[j],num[] ^= num[j]
	}
    for(var j=1; j< num.length;j++){
      if(num[j-1] > num[j]  ){
      	for(var i=0;i<j;i++ ){
      		if (num[i]< num[j] && num[i+1]>num[j]) {
      			num[i+1] ^= num[j], num[j] ^= num[i+1], num[i+1] ^= num[j] 
      		}
      	}
      }
	}
	return num
}
var num =  [5,2,8,3,7,9,4]
console.log(cr(num))
------------------------------------------------------------
console.time()
function insertionSort(arr) {
    var len = arr.length;
    var preIndex, current;
    for (var i = 1; i < len; i++) {
        preIndex = i - 1;
        current = arr[i];
        while (preIndex >= 0 && arr[preIndex] > current) {
            arr[preIndex + 1] = arr[preIndex];
            preIndex--;
        }
        arr[preIndex + 1] = current;
    }
    return arr;
}

console.log(insertionSort([5,2,8,3,7,9,4]))

console.timeEnd()
// [ 2, 3, 4, 5, 7, 8, 9 ]
// default: 3.873ms
// [Finished in 0.1s]
```





## 参考文献

```
阶乘
https://baike.so.com/doc/5636551-5849178.html

```

