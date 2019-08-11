# JavaScript测试

> 出题: 邹义良 2019-08-08

## 不定项选择题，0个或多个，如果没有正确答案，填E

1. 以下说法正确的是________。

   ```none
   A. js是跨平台、面向对象的动态编程语言 
   B. js是一种具有函数优先的解释型编程语言   c语言可以传来传去的
   C. js是基于原型、多范式的编程语言       
   不是基于面向对象的，是原型链的继承考核。函数式执行-面向对象式的编程
   D. js的核心语言叫ECMAScript
   es5 es6  ecsa这个组织定了这个标准。
   
   
   abcd 学习前端框架
   ```

2. 以下说法正确的是________。

   ```none
   A. js能运行在浏览器中
   B. js能运行在服务端
   C. js能绘制出动态图像
   D. js具有基于事件循环的并发模型
   
   abcd
   
   nodejs  
   画布-canvas
   ```

3. 下面代码运行结果________。

   ```none
   var userName = "jack"
   console.log(username)
   
   A. 输出:jack
   B. 报错:缺少分号
   C. 报错: username is not defined
   D. 报错: console.log is not a function
   
   
   c
   知识点。
   职业敏感性。--name
   js的class不区分大小写。
   
   
   ```

4. 下面代码运行结果________。

   ```none
   if(true){
       var foo = 1
       let bar = 2
   }
   
   console.log(foo)
   console.log(bar)
   
   A. 输出 1 然后报错 bar is not defined
   B. 输出 1 2
   C. 报错 foo is not defined 然后输出 2
   D. 没有输出，只报错 bar is not defined
   
   a
   var是在函数作用域中生效的，
   
   var foo =1 
   fun()[{ var foo =2  }
   let  es6 限制在这个花阔的 里面， var 是可以到里面去的，let访问的到
   
   if也是花阔好{}, 所以访问不到。
   
   ```

5. 下面代码运行结果________。

   ```none
   var a = 1
   var a = 2
   {
       let a = 3
   }
   console.log(a)
   
   A. Identifier 'a' has already been declared
   B. Uncaught SyntaxError: Unexpected identifier
   C. 输出2
   D. 输出3
   
   es6
   自闭和的函数：{}  用let
   就是做成一个作用域，不污染全局空间。
   var a 
   var a.这个不会报错，
   
   let b 
   let b。不会报错，能用代码 ，
   花阔好是语句，不是对象。
   
   ```

6. 下面代码运行结果________。

   ```none
   const PI = 3.14
   function test(){
       var PI = 3.14159
   }
   test()
   console.log(PI)
   
   A. 输出 3.14
   B. 输出 3.14159
   C. Identifier 'PI' has already been declared
   
   var是定义到全局，
   但是在函数里面不会改变。所以选择a
   ```

7. 下面代码运行结果________。

   ```none
   let foo = 1
   const bar = 2
   foo = 3
   bar = 4
   console.log(foo)
   console.log(bar)
   
   A. 输出 3 4
   B. 输出 3 2
   C. 输出 1 2
   D. 报错 Assignment to constant variable
   
   d
   ```

8. 下面代码能正确运行的有________。

   ```none
   A. var 姓名 = "张三";       console.log(姓名)
   B. var $name = "李四";     console.log($name)
   C. var 7niu = "王五";      console.log(7niu)
   D. var user-name = "赵六"; console.log(user-name)
   
   
   尊严之战。
   $ 解块润， 可以单用¥变量,
   js  字母 数字 下划线 $ 还支持 中文 繁体 小日本 法文，  
   这种表情符号，用excel 是存不进去的  
   mysql 都是 uff8m64 字符
   
   不能数字开头
   ab
   ```

9. 下面代码运行结果________。

   ```none
   var foo
   console.log(foo)
   
   A. null   赋值为空
   B. undefined  声明了 但是没赋值；
   C. false
   D. None
   
   
   b
   ```

10. 下面代码运行结果________。

    ```none
    var myvar = "foo"
    
    function test(){
      console.log(myvar)
      var myvar = "bar"   //变量的声明提前，在同一个作用里面就会比输出提前。
    }
    test()
    
    A. undefined
    B. null
    C. foo
    D. bar
    
    
    堆
    栈：从上往下压， 
    同一个作用域就混乱，所以找不到，
    var a = 2
    ==> var a;
    		a = 2
    		
    变量都是先声明，再使用
    
    a
    ```

11. 下面代码在Chrome中运行结果________。

    ```none
    var myvar = "foo";
    
    console.log(myvar)
    console.log(window.myvar)
    console.log(globalThis.myvar)
    
    A. foo undefined undefined
    B. foo null null
    C. foo foo foo
    D. foo 
        window.myvar is not defined 
        globalThis.myvar is not defined 
        
    语言本身是数据类型：变量 循环 math数学对象。7个核心对象
    settimeout console 的宿主 node 浏览器都可以用，mongodb也可以运行js。
    
    alter数组环境中找，window.alter 
    
    window   window.alter 顶层对象，
    var a=1 ,全局对象就是 wondow.a =1  ; 如果 是放在函数中，定义定义的都是局部变量。
    globathis。 是不论什么环境都是顶层对象，
    globa。 顶层对象，放一些无归的，panseInt就在顶层对象中，， 
    myvar
    
    api 小到一个登陆接口，get post ；java中 函数的调用 也是api
    js 可以定义：node  浏览器  手机开发里；浏览器对象模型；提供了环境。
    浏览器中定义了很多东西有多高，浏览器都是大家抄的；
    
    
    
    宿主环境不同
    
    
    
    c
    ```

12. 最新的 ECMAScript 标准定义的数据类型，选出正确的________。abd 

    ```none
    A. boolean、number
    B. null、undefined
    C. int、string
    D. symbol、object
    
    js无int 有number
    剩下都是他的数据类型。
    
    boo t f
    number -1  0 1  0.1 
    3/0是正无穷大Infinity  -3/0 -Infinity
    abc 转不出的东西是NaN 非数值（not a number）
    passInt 是number类型
    bigint 不能和int做运算的；
    js中是比较完备的数字类型
    
    fuction也是对象。
    原始数据类型 是7中。
    对象： boo num null undef string symbol  bigint
    
    
    
    
    symbol符号:成为不相等的，用来做唯一标记的
    const u =symbol() 都是调用不同的东西
    
    对象是默认就是引用的；
    var u = { name :"a"}
    var u2 = u 
    在内存中都是一个，只是两个名字， 存储在堆中；
    go就是结构体，没有对象
    c就是指针
    php $ 就是饮用传递
    数组是拷贝，对象的赋值是用的
    
    abd
    ```

13. 下面代码运行结果________。

    ```none
    var a = 1
    var b = 2
    var c = "3"
    console.log(a+b+c)
    console.log(a+c-b)
    
    A. 6   2
    B. 123 2
    C. 15  11
    D. 33  11 
    
    
    
    
    d
    ```

14. 下面代码运行结果________。

    ```none
    var n = "2"
    switch(n){
        case 1:
            console.log("星期一")
        case 2:
            console.log("星期二")
    }
    
    A. 星期一
    B. 星期二
    C. 星期一 星期二
    D. 什么也不输出
    
    
    js是弱类型，但是也是注意数据类型，类型不统一就是什么也不输出
    d
    ```

15. 下面代码运行结果________。

    ```none
    function test(n){
        try{      
            throw new Error("foo")   //js的反印号解析变量
            console.log(n)
        }catch(e){   
            console.log(e.message)
            return
        }finally{    //无论如何都会执行
            console.log("{$n}")
        }
    }
    
    test("bar");
    
    A. foo {$n}
    B. foo bar
    C. bar foo
    D. bar foo {$n}
    
    
    a
    ```

16. 下面代码运行结果________。

    ```none
    for(var i=0;i<=3;i++){
        if(i==2){
            continue
        }
        console.log(i)
    }
    
    A. 0 1
    B. 0 1 2
    C. 0 1 3
    D. 0 2 3
    
    continue 跳过当前
    break 结束
    return函数返回
    c
    ```

17. 下面代码运行结果________。

    ```none
    var data = ['a','b','c','d']
    for(var i in [1,2,3]){
        console.log(data[i])
    }
    
    A. abc
    B. bcd
    C. 123
    C. 012
    
    for ---in 取 0，1，2 取的索引
    for ----of 取得1，2，3。  php ：for each  python ：for --in
    arr =[ 4,5,4]
    结果一样都是
    
    a
    ```

18. 下面代码运行结果________。

    ```none
    let arr = [3, 5, 7];
    arr.foo = "hello";
    
    for (let i of arr) {
       console.log(i)
    }
    
    A. 0 1 2 foo
    B. 3 5 7
    C. 0 1 2 hello
    D. 3 5 7 hello
    
    
    
    of 换成 of 就是a
    b
    ```

19. 下面代码能正确输出3的是________。

    ```none
    let arr = [3, 5, 7];
    A. console.log(arr.count)
    B. console.log(arr.length)
    C. console.log(len(arr))
    D. console.log(size(arr))
    
    
    b
    a无count
    解块瑞size
    ```

20. 下面代码运行结果________。

    ```none
    let arr = [3, 5, 7];
    A. console.log(arr.count)
    B. console.log(arr.length)
    C. console.log(len(arr))
    D. console.log(size(arr))
    ```

21. 下面代码运行结果________。

    ```none
    var name = 'mary'
    var foo = {
        name:'jack',
        say1: function(){console.log(this.name)}, //是方法
        say2(){console.log(this.name)},  //(){} 就是方法，是等价的
        say3:()=>{console.log(this.name)},  //箭头函数 ，是函数，继承最外层的对象。出现的概率很高。
    }
    
    foo.say1()
    foo.say2()
    foo.say3()
    
    A. jack mary undefined
    B. jack jack jack
    C. jack jack mary
    D. jack jack undefined
    
    
    js set几何 互异 无序 不重复 关注的value值 ，不可以重复的
    		php数组的key 就是一个set集合
    		python
    		并发冲突：全局变量里面， i = 1 1+1=2  1 +1 
        数据库中并发冲突，都会2 ，做100个就是95，并发；如果是set userId就可以解决。
        加锁，还在用，不能读；别并发变成串形化
    
    redis
    
    let
    算法很重要
    
    
    怎么看是不是js es6
    setIncate(function test(){  this })  //函数是对象，7种数据类型，剩下都是对象object
    <==>setT（ ()=>{} ）
    不等价；箭头函数无this ， 自己无this ，如果有就是继承过来的。
    
    
    ajax
    name = jaek
    hi(){
    
    var _this = this  //加这个
    $get（URL，function(res){
    setmeout(fuction{
    
    _this.name =res //z这句不行
    }
    )}
    }
    
    
    ==》指向外层对象的时候，我们用箭头函数，上面就是window
    name = jaek
    hi(){
    $get(url ,res=>)
    
    
    最外层是个大的对象。
    答案：c
    ```

22. 下面代码运行结果________。

    ```none
    var a = "b"
    var user = {
        a,
        [a]:"c",
        "c":"d"
    }
    console.log(user.a)
    console.log(user.b)
    console.log(user.c)
    console.log(user[a])
    console.log(user['a'])
    
    答案：bcdcb
    
    
    
    
    var a = "b"
    var user = {
        a,   		// 前面是keys：value<=>'name'=name<=>name: name <==>name缩写，属性的缩写；方法的缩写，
        [a]:"c",  [a] //<==>求值 ‘b’= 后面的值“c”
        "c":"d"
    }
    //console.log(user['a'])
    console.log(user.a)  //就直接找  a= ['a'] 加引号就是自变量找a
    
    console.log(user.b)
    console.log(user.c)
    console.log(user[a])  //就是调用求出a ，找b的值
    
    A. b c d c
    B. b undefined d b
    C. a undefined d undefined
    D. b c d undefined
    
    
    a
    ```

23. 下面代码运行结果________。

    ```none
    const p1 = new Promise(function (resolve, reject) {
        setTimeout(() => resolve("data1"), 2000)   //2s
    })
    
    const p2 = new Promise(function (resolve, reject) {
        setTimeout(() => reject(new Error('fail')), 1000)  //1s
    })
    
    Promise.all([p1, p2]).then(result => {
        console.log(result[0])				//自动对应上
        console.log(result[1])
    }).catch(error => console.log(error.message))
    
    A. data1 fail
    B. fail data1
    C. fail fail
    D. fail
    
    Promise.all会等待1，2都回来执行。自动等。//自动对应上，他的结果。顺序对应。
    任意一个都是执行一次，解决多个异步，多个执行，。Promise.all就是解决这个问题。
    Promise.all可以解决很多场景，都类似
    
    
    
    a文件
    b文件
    a+b文件合并
    
    希望并发执行；ajax
    
    版本一：串形的。
    ajax(url,(res)=>{
    	ajax(url,(res)=>{
    		ajax(url3,(res3)={
    				ok
    			
    		})
    	})
    })
    
    版本二：
    定时器
    首先 返回每个阐述结束
    set	写一个定时器 然后进行循环结束这个定时器，进行 ajax3
    
    版本三：
    
    
    
    d
    ```

24. 下面代码能正确将该div的类名改为active的是________。

    ```none
    <div id="foo" class="invalid">
    
    A. document.getElementById('foo').class="active"
    B. document.getElementById('foo').className="active"
    C. document.getElementById('#foo').className="active"
    D. document.getElementById('#foo').class="active"
    
    
    
    
    b
    ```

25. 下面代码运行结果________。

    ```none
    var f = (function(i){
        console.log(i)
        i++
        return function(i){
            console.log(i)
        }
    })
    
    f(2)(3)
    
    
    
    
    var f = (function(i){
        console.log(i)
      
    })(1)
    
    
    变形：
    var f = (function(i){
        console.log(i)
        i++
        return function(i){console.log(i) }})
    
    f(2)(3)
    
    
    
    
    两个函数无关系。
    A. 2 2
    B. 2 3
    C. 2 4
    D. 3 4
    
    b
    ```





# 原生对象



字符串对象

数组对象

math对象

gloab对象







# 浏览器：

无标准，有有些兼容性的问题



css做好，js可以改。

css -  改成js  小驼峰写法。

不光会写，还要底层原理。





# 原型链





# 三个点的语法：

b = b||"abc" es5

b="abc" es6  多肽 重载；

b = "abc" ,  es7

(a,b,..c)   =(1,2,3,4,5). c就是一个数组，是3，4，5

Var [a,,b] = [1,2,3]  a= 1 b= 3 ，是占位符  对象的结构





va r obj = {color: rol , size : "man"}

Var [color,size] =obj

也就是color = rol，size= man





va r obj2 = {...obj，heighet ：18} 对象的扩展。js的基础语法。。。



这些可以用在 服务端 浏览器 node中；jQuery就不要用，转换机制无。