---
layout: post
title: "Node的聊天室"
date: 2019-08-05
tag: 网页webPage
---









## Node

```
//on 为事件 enevt
//方法 （）   ; 直接 用.
//属性 无括号;直接 用.
变量 白色的；
 let 命令所在的代码块 {} 内有效，在 {} 之外不能访问。let定义局部变量
Socket就是端口号 加  url
 
\r是回车，英文是Carriage return，表示使光标下移一格
\n是换行，英文是New line，表示使光标到行首
测试：https://www.runoob.com/quiz/python-quiz.html

```

## **Node聊天室完成版**

```javascript
var sockSa = []  //定义用户存放(地)点
const net = require('net');  //导入模块，给一个常量
const server = net.createServer(function (sock) {  //创建服务器
    console.log('连接')
    sockSa.push(sock)   //把sock=客户端socket放在数组里面
    console.log('这是所有sock的个数：'+ sockSa.length)
    // console.log(sockSa)
    sock.on('end',function(){
        console.log('断开')
    });
    sock.on('data', (data) => {
        data = data.toString()
        console.log(data);  //在服务端显示，数据以字符串输出
        // 判断是否是第一句话
        //sock.name = data
        if(sock.name == null ){
            data = data.slice(0,3)
            console.log(data.length)
            sock.name = data
            return
        }
        if (data[0]=='@') {
            //取名字
            var at = data.match(/@\w{3}/)[0].slice(1);
            //打出说的话私聊对他说的话。
            console.log('@' + at + 'say:' + data.slice(4))

            for (var i = 0; i < sockSa.length; i++) {
                if (at == sockSa[i].name) {
                    sockSa[i].write(sock.name + '对'+at +' say:' + data.slice(4))
                    //把接收到的数据分发给单人。
                }
            }
        }else{
            for(var i= 0; i<sockSa.length ;i++){
                if(sock==sockSa[i] ){
                    continue;  //如果出现了指定的条件，然后继续循环中的下一个迭代。
                }else{
                    sockSa[i].write(sock.name+'对大家说:' + data)
                    //把接收到的数据分发给每个人。(广播功能)
                }

            }
        }
    })
});
server.on('error',(er) => {
    throw er;           //对于报错不发
});
server.listen(8889,()=>{
    console.log('绑定上8889')
})



//--------------------------客户端


process.stdin.setEncoding('utf8'); //格式
const net = require('net');   //加载net的模块
var client = new net.Socket();   //客户端的socket

client.on('data', (data) => {     //net下socket的事件，data是变量
    console.log(data.toString());//收到服务器返回的数据
});

client.on('end', () => {
    console.log('退出聊天');
});

client.on('connect',()=>{
    console.log('连接成功！')
    process.stdin.on('readable', () => {
        let chunk;  //定义局部 变量

        while ((chunk = process.stdin.read()) !== null) {
            // if(chttps://www.runoob.com/nodejs/nodejs-net-module.html
            client.write(chunk)
            //死循环 就是你可以输入，我服务端可以接受
        }
    });
});

client.connect(8889,'127.0.0.1')

const net = require('net');
var users = {};
// var count = 0
const server = net.createServer(function (socket) {
    const id = socket.remoteAddress +  socket.remotePort

    users[id] = {
        nickname :"匿名",
        socket
    };

    console.log(users[id].nickname+'上线')

    server.getConnections((err, connect) => {
        // count = connect
        socket.write('你好，当前在线用户'+connect+'人')
        console.log('当前在线用户'+connect+'人')
        for (let v_id in users) {
            if (v_id !== id){
                users[v_id].socket.write(users[id].nickname+'上线')
                users[v_id].socket.write('当前在线用户'+connect+'人')
            }
        }
    })

    socket.setEncoding('utf8');
    socket.on('data',function (data) {
        data = data.replace(/[\r\n]/g,"");
        var flag = data.slice(0,1);
        switch (flag) {
            case '#':{
                let s = ''
                for (let v_id in users) {
                    s += [users[v_id].nickname + "   "]
                }
                socket.write('当前用户表：'+s)
                break;
            }
            case '@':{
                let t = data.slice(1).split(' ');
                let text = t[1];
                let toUser = t[0]
                let toSocket = null
                for (let v_id in users){
                    if (users[v_id].nickname === toUser) {
                        toSocket = users[v_id];
                        break;
                    }
                }
                if (toSocket) {
                    toSocket.socket.write(users[id].nickname+':'+text)
                } else {
                    socket.write('对不起，你输入的用户名不存在!')
                }
                break;
            }
            case '!':{
                let text = data.slice(1);
                users[id].nickname = text;
                socket.write('修改成功！');
                break;
            }
            default :{
                let text = data.slice(0);
                for (let v_id in users) {
                    if (v_id !== id) {
                        users[v_id].socket.write(users[id].nickname+':'+text)
                    }
                }
            }
        }
    });
    socket.on('end',function (){
        count = Object.keys(users).length
        outman = users[id].nickname

        for (let v_id in users) {
            if (v_id !== id){
                users[v_id].socket.write(outman +'离开')
                users[v_id].socket.write('在线人数：'+ (count-1))
            }
        }
        console.log(outman +'离开')
        console.log('在线人数：'+ (count-1))
        delete users[id]
        console.log(count-1)
        // })

    })
});

server.on('error', (er) => {
    throw er;           //对于报错不发
});
server.listen(8889, () => {
    console.log('绑定上8889')
})
```

**版本（服务端）**



**node聊天室**

![weChar](../images/image/weChar.png)

![weChar](/images/image/weChar.png)



**要求：**

```

每个人有自己的昵称，在进入聊天室的时候自己输入。
每个人都可以发言

有一个区域用来展示所有的发言，并且要实时更新

有人加入的时候提示xxx加入了群聊
```

补加：群聊 私聊 加好友

了解长连接



用户和服务器的通信就只能是：用户发送请求 -> 服务器接受请求 -> 服务器返回结果 -> 用户收到结果。

```
➜  node-chat1 git:(master) ✗ node -v
v10.16.0
➜  node-chat1 git:(master) ✗ npm -v 
6.9.0

因为npm是国外的库可能有点慢，可以安装cnpm，执行下面命令
mac继续在终端输入：sudo npm install -g cnpm --registry=https://registry.npm.taobao.org

➜  test-js git:(master) ✗ cnpm -v
cnpm@6.1.0 (/usr/local/lib/node_modules/cnpm/lib/parse_argv.js)

linux乌班图
npm install -g cnpm --registry=https://registry.npm.taobao.org

然后输入
cnpm install --save express
等待安装成功，再安装
cnpm install --save socket.io
都安装成功之后我们就可以开始着手Coding了。

➜  test-js git:(master) ✗ node /Users/tianzi/Desktop/test-js/node-chat1/server.js
listening on *:3000


```

**聊天室模型：**

```
listening on *:3000



a user connected
a user connected
a user connected

---------------------------聊天内容
1 加入了群聊
2 加入了群聊
111
wocao
sdjj
dsadasd
dasdjajdsa
d
dskandjaskdjjdsajljkld;lkldall;kadkl;kl;dslkl;ks
saasd .
dsadjksajodas
hfjklsakjlfjjiojjfjijiofjjfjkjkfwjkfwjjojkjkkjjkjojpojkfwjojwjoojwjopjowjjowjopjopejojopvjopjopejojopjopjopjopjopjjopjjwopjwjopfjjfjwnfnwnlkfpjwjfpjowjfwp
5 加入了群聊

```





**在server.js中写下以下代码：**

```
用Nodejs搭建一个服务器。其中用到了express这个框架


【二】server.js 服务器接受消息

只需要两步：
监听前端的message事件
在监听到事件之后，将新消息广播给全体用户，这里也将广播事件的名字叫message吧。

 var app = require('express')(); //引入express库
var http = require('http').Server(app); //将express注册到http中

//当访问根目录时，返回Hello World
app.get('/', function(req, res){
  res.send('<h1>Hello world</h1>');
});

//启动监听，监听3000端口
http.listen(3000, function(){
  console.log('listening on *:3000');
});
```



**index.html**

```html
【一】index.html 将用户消息发送给服务器

用户输入消息，然后点击发送我们将用户的消息发送给服务器，然后服务器将消息广播给所有的用户。
我们需要给form的提交绑定一个事件，让它来处理新消息的发送。
【三】index.html 客户接受新消息

客户接收到服务器发来的message事件，将新消息呈现在面板中。

<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      * { margin: 0; padding: 0; box-sizing: border-box; }
      body { font: 13px Helvetica, Arial; }
      form { background: #000; padding: 3px; position: fixed; bottom: 0; width: 100%; }
      form input { border: 0; padding: 10px; width: 90%; margin-right: .5%; }
      form button { width: 9%; background: rgb(130, 224, 255); border: none; padding: 10px; }
      #messages { list-style-type: none; margin: 0; padding: 0; }
      #messages li { padding: 5px 10px; }
      #messages li:nth-child(odd) { background: #eee; }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>发送</button>
    </form>
  </body>
</html>
```

**测试：**

```
1. 开启服务器node server.js。
node /Users/tianzi/Desktop/test-js/node-chat1/server.js
listening on *:3000


2. 开一个标签（网页），输入地址localhost:3000，回车，填写昵称为1 。
http://localhost:3000/
或者127.0.0.1:3000
3. 再开一个标签，网页，填写昵称为2。

然后开始让两个人互相发送消息吧。
至此，聊天室以就做完了。
```



**总结**

用户a将自己的消息用*`message`*事件发送给服务器，服务器监听*`message`*事件接收其中的消息，将消息用事件*`message`*广播给全体用户，全体用户监听*`message`*事件，将事件接受到的消息呈现在聊天框中。PS:这一段是整个socket编程的核心，可以多读几遍细细理解。

























## node实现一个简单的登陆注册

**用户注册：**

1，输入用户名和密码，点击登陆
2，如果用户已注册提示用户已存在，第一次注册提示注册成功，其他不做验证

**用户登陆：**

1，输入用户名和密码，点击登陆
2，如果用户不存在做出相应提示，如果用户名或者密码输入错误做出相应提示，如果登陆成功，提示登陆成功

**一、前端部分**

在nodenote文件夹下创建www文件夹，用于存放user.html，因为需要交互所以额外引入一个ajax文件，创建一个index.js,用户写js逻辑代码
1，user.html代码

2，index.js注册部分

3.index.js登陆部分





**二、后台部分**

在nodenote文件夹下创建server.js
1,引入需要用到的模块，创建服务

2，接收数据完毕，在end中处理数据过程

这个时候你启动服务，输入localhost:8080,会报错，{ok：false,msg:'未知的act'}这是什么原因，原来是url有问题，我需要判断，可以打印处理url看一下，只有只想接口‘/user’的时候才能请求数据，而且页面用了ajax也需要用到服务环境，所以需要判断如果不是接口‘/user’，这个时候我应该在登陆页面，这里用到了fs的读取文件





**通讯和协议**

**已知**

```
学习node的基本东西：拆解难点：
1.在控制台输入东西
2.具备输入
3.接受端口------昨天解决，服务端的程序可以做出来。
4.定义协议，后面与百度的通讯

5.做一对一（客户端-服务器）聊天	process.stdin（过程）.on
6.然后做一对多（一个客户端 -- 服务端/客户端） for循环sockSa[i]
7.

做一个curl 80端口

https://www.cnblogs.com/chenliyang/p/6558756.html
深入理解HTTP协议、HTTP协议原理分析


node提供环境。 浏览器提供环境。 dom是浏览器提供的。

```



**\r\n的区别：**

```
\r是回车，英文是Carriage return，表示使光标下移一格
\n是换行，英文是New line，表示使光标到行首
nodejs对\r的处理与在浏览器控制台对\r的处理不同，
在nodejs里
var str = 'a\rb';
console.log(str);  =>  b
在控制台里
var str = 'a\rb';
console.log(str);  =>  ab
```

**官网node** 

```js
//on 为事件 enevt
//方法 （）   ; 直接 用.
//属性 无括号;直接 用.


curl 模拟命令
curl -i www.baidu.com


短连接，node定义一个长连接。
login :name =xx
all:hello
@jack:aaaa
console.log(data.toString)

connection 连接

redis 就是非常高效。
mysql就是二进制

socket.io 封装了太多
node 回调函数。


net.createServer() section:
const net = require('net');
const client = net.createConnection({ port: 8124 }, () => {
  // 'connect' listener
  console.log('connected to server!');
  client.write('world!\r\n');
});
client.on('data', (data) => {
  console.log(data.toString());
  client.end();
});
client.on('end', () => {
  console.log('disconnected from server');
});


//面向百度编程永远入不了门，http协议


```







**Net1.js**

```javascript
const net = require('net');
const server = net.createServer((sock) => {
    sock.write('world!\r\n');
    sock.end();
});

server.listen(8080, ()=>{
    console.log('server on 8080');
});

------------------------------------ net.createServer() 

const net = require('net');
const client = net.createConnection({ port: 8124 }, () => {
  //'connect' listener
  console.log('connected to server!');
  client.write('world!\r\n');
});
client.on('data', (data) => {
  console.log(data.toString());
  client.end();
});
client.on('end', () => {
  console.log('disconnected from server');
});

---------------------------------connections on port 8124
const net = require('net');
const server = net.createServer((c) => {
  // 'connection' listener
  console.log('client connected');
  c.on('end', () => {
    console.log('client disconnected');
  });
  c.write('hello\r\n');
  c.pipe(c);
});
server.on('error', (err) => {
  throw err;
});
server.listen(8124, () => {
  console.log('server bound');
});

-----------------------四 服务器

const net = require('net');
const server = net.createServer(function (c) {
    console.log('连接')
    c.on('end',function(){
        console.log('断开')

    });
    c.on('data', (data) => {
        console.log(data.toString());
    })
    // c.write('hello a \r\n');
    c.write('b');

    // client.end();
});
server.on('error',(er) => {
    throw er;
});
server.listen(8889,()=>{
    console.log('bangding shang 8889')
})


```



**http协议中connection头的作用**

  在http1.1中request和reponse header中都有可能出现一个connection的头，此header的含义是当client和server通信时对于长链接如何进行处理。
   在http1.1中，client和server都是默认对方支持长链接的， 如果client使用http1.1协议，但又不希望使用长链接，则需要在header中指明connection的值为close；如果server方也不想支持长链接，则在response中也需要明确说明connection的值为close.
    不论request还是response的header中包含了值为close的connection，都表明当前正在使用的tcp链接在当天请求处理完毕后会被断掉。以后client再进行新的请求时就必须创建新的tcp链接了。
    

    如何不痛苦：网络相关的东西。都是tcp+端口
    socket：就是连接客户端和服务端的水管，连接
**定义常量 const-python**

```python
# Filename:const.py
# 定义一个常量类实现常量的功能
# 
# 该类定义了一个方法__setattr()__,和一个异常ConstError, ConstError类继承 
# 自类TypeError. 通过调用类自带的字典__dict__, 判断定义的常量是否包含在字典 
# 中。如果字典中包含此变量，将抛出异常，否则，给新创建的常量赋值。 
# 最后两行代码的作用是把const类注册到sys.modules这个全局字典中。

class _const:
    class ConstError(TypeError):pass
    def __setattr__(self,name,value):
        if name in self.__dict__:
            raise self.ConstError("Can't rebind const (%s)" %name)
        self.__dict__[name]=value
        
const = _const()
const.PI=3.14
print(const.PI)
```



**process.stdin过程**

https://nodejs.org/dist/latest-v10.x/docs/api/process.html#process_process_stdout

```java
process.stdin.setEncoding('utf8');
const net = require('net');
var client = new net.Socket();
client.on('data', (data) => {
    console.log(data.toString());
    // client.end();
});

client.on('end', () => {
    console.log('disconnected from server');
});
client.on('connect',()=>{

    console.log('fds')
    // client.write('GET / HTTP/1.1\n')
    // client.write('a')
    // client.write('dsd')
    // client.write('Host: 127.0.0.1\n\n')

    process.stdin.on('readable', () => {
        let chunk;
        // Use a loop to make sure we read all available data.
        while ((chunk = process.stdin.read()) !== null) {
            // process.stdout.write(`data: ${chunk}`);
            client.write(chunk)
        }
    });

});

client.connect(8889,'127.0.0.1')

---------------




var sockSa = []
const net = require('net');
const server = net.createServer(function (sock) {
    console.log('连接')
    sockSa.push(sock)

    console.log('这是所以sock：'+ sockSa.length)

  sock.on('end',function(){
        console.log('断开')

    });
    sock.on('data', (data) => {
        console.log(data.toString());
        for(var i= 0; i<sockSa.length ;i++){
            sockSa[i].write(data.toString())

        }

    })
    // c.write('hello a \r\n');
    // c.write('');

    // client.end();
});

server.on('error',(er) => {
    throw er;
});
server.listen(8889,()=>{
    console.log('bangding shang 8889')
})
```





## node客户端/服务端



```javascript
客户端啊
process.stdin.setEncoding('utf8'); //格式
const net = require('net');   //加载net的模块
var client = new net.Socket();   //客户端的socket

client.on('data', (data) => {     //net下socket的事件，data是变量
    console.log(data.toString());//收到服务器返回的数据
});

client.on('end', () => {
    console.log('退出聊天');
});

client.on('connect',()=>{
    console.log('连接成功！')
    process.stdin.on('readable', () => {
        let chunk;  //定义局部 变量
        
        while ((chunk = process.stdin.read()) !== null) {
            // if(chttps://www.runoob.com/nodejs/nodejs-net-module.html
            client.write(chunk)
            //死循环 就是你可以输入，我服务端可以接受
        }
    });
});

client.connect(8889,'127.0.0.1')

-------------
服务端啊 

var sockSa = []  //定义用户存放(地)点
const net = require('net');
const server = net.createServer(function (sock) {
    console.log('连接')
    sockSa.push(sock)   //把sock=客户端socket放在数组里面
    console.log('这是所有sock的个数：'+ sockSa.length)

    sock.on('end',function(){
        console.log('断开')
    });
    sock.on('data', (data) => {
        console.log(data.toString());  //在服务端显示，数据以字符串输出
        for(var i= 0; i<sockSa.length ;i++){
            if(sock==sockSa[i] ){
                continue;  //如果出现了指定的条件，然后继续循环中的下一个迭代。
            }else{
                sockSa[i].write(data.toString())
                //把接收到的数据分发给每个人。(广播功能)
            }
        }
    })
});
server.on('error',(er) => {
    throw er;           //对于报错不发
});
server.listen(8889,()=>{
    console.log('绑定上8889')
})

---------------------
  ---------------------------
//未完成版本


process.stdin.setEncoding('utf8'); //格式
const net = require('net');   //加载net的模块
var client = new net.Socket();   //客户端的socket
var isLogin = 0;   //登陆


client.on('data', (data) => {     //net下socket的事件，data是变量
    console.log(data.toString());//收到服务器返回的数据
    // client.write('')

});

client.on('end', () => {
    console.log('退出聊天');  //四次挥手
});


client.on('connect',()=>{
    console.log('连接成功,请在下面输入你的名字：')
        // 名字不可以以@开头；
        // 想发群聊必须加@，@所有人
        // 然后就是单聊，匹配名字进行聊天


    process.stdin.on('readable', () => {
        let chunk;  //定义局部 变量
         chunk = process.stdin.read()
        //输入in，标准输入，标准输出，错误输出
        while (chunk!== null) {
            client.write(chunk)   //读键盘
            //死循环 就是你可以输入，我服务端可以接受
            chunk = process.stdin.read()
        }
    });




});
client.connect(8889,'127.0.0.1')

-----------------


var sockSa = []  //定义用户存放(地)点
const net = require('net');
const server = net.createServer(function (sock) {
    console.log('连接')
    // sock.write('请输入：'+sock)
    // sock.log(sock)
    sockSa.push(sock)   //把sock=客户端socket放在数组里面
    console.log('这是所有sock的个数：'+ sockSa.length)

    sock.on('end',function(){
        console.log('断开')
    });
    sock.on('data', (data) => {

        let msg = data.toString();
        console.log(msg);  //在服务端显示，数据以字符串输出

        if (msg =='/@所有人+/'){



            for(var i= 0; i<sockSa.length ;i++){
                if(sock==sockSa[i] ){
                    continue;  //如果出现了指定的条件，然后继续循环中的下一个迭代。
                }else{
                    sockSa[i].write(msg)
                    //把接收到的数据分发给每个人。(广播功能)
                }
            }elseif(msg == '/@sockSa[i]'){

            }
        }
    })
});
server.on('error',(er) => {
    throw er;           //对于报错不发
});
server.listen(8889,()=>{
    console.log('绑定上8889')
})

  
  
```





**客户端只可以输入**

```
var sockServer = [];
const net  = require('net')
const server = net.createServer(function (sock){
    console.log('连接'); //net 帮我们做好了三次握手
    sock.on('end',function(){
        console.log('断开')
    })

    sock.on('data',(data)=>{
        data = data.toString()
        console.log(data)

    })

});

server.on('error',(er)=>{
    throw er;
})


server.listen(8889,()=>{
    console.log('绑定上了')
})


----------------------------------
const net =require('net')
var client = new net.Socket();

client.on('data',(data) => {
    console.log(data)
});

client.on('end',() =>{
    console.log('退出了')

})

client.on('connet',()=>{
    console.log('lian')
    process.stdio.on('readable',()=>{
        let chunk;//
        while ((chunk = process.stdio.read()) !== null){

            client.write(chunk)
        }

    })
})

client.connect(8889,'127.0.0.1')
```







## tcp/ip学习总结

学会拆解问题最小化；

```
Socket --
连接
data

accept队列（运维大牛）：阻塞掉； 找到socket
syn队列

c的训练 -- 数组不变。。
java --list 可以伸缩 扩容，成倍增长的。 php python
java数组不可以变


write 数据。。。on data

三次握手： （write）
客户端 找 服务端 商量个事；
服务端 说 可以的；   
客户端 那我们聊天吧；



js要熟；
connection  连接


四次挥手：（结束/end）
a不想给b说话了
b也不想给a说了
b要断开了
a也要断开了

css.div布局的训练；
字符串的操作，循环，if，正则



缺的东西
网络，
操作系统；
[]是可选参数

```















继续学习js

## ejs模板引擎

**1.使用之前**

**1.1安装**

EJS 是后台模板，可以把我们数据库和文件读取的数据显示到 Html 页面上面（解析页面视图模板）。它是一个第三方模块，需要通过 npm 安装https://www.npmjs.com/package/ejs

```
npm  install ejs --save
cnpm install ejs --save
```

**1.2引入**

```
const  ejs = require('ejs');
```

**2.怎么使用**

ejs主要功能就是渲染html

```
//第一种用法
// 渲染字符串
ejs.render(str, data, [options]);
// => 输出绘制后的 HTML 字符串

//第二种用法
const template = ejs.compile(str, [options]);
template(data);
// => 输出绘制后的 HTML 字符串

//第三种用法
// 渲染文件
ejs.renderFile(filepath, data, [options], function(err, str){
    // str => 输出绘制后的 HTML 字符串
});

```

**选项**

- cache 缓存编译后的函数，需要提供 filepath
- filepath 被 cache 参数用做键值，同时也用于 include 语句
- context 函数执行时的上下文环境
- compileDebug 当为 false 时不编译调试语句
- client 返回独立的编译后的函数
- delimiter 放在角括号中的字符，用于标记标签的开与闭
- debug 将生成的函数体输出
- _with 是否使用 with() {} 结构。如果为 false，所有局部数据将存储在 locals 对象上。
- localsName 如果不使用 with ，localsName 将作为存储局部变量的对象的名称。默认名称是 locals
- rmWhitespace 删除所有可安全删除的空白字符，包括开始与结尾处的空格。对于所有标签来说，它提供了一个更安全版本的 -%> (在一行的中间并不会剔除标签后面的换行符)。
- escape 为 <%= 结构设置对应的转义（escape）函数。它被用于输出结果以及在生成的客户端函数中通过 .toString() 输出。(默认转义 XML)。

**3模板语法**

**3.1 分隔符(定界符)**

**开始标签(定界符)**

- `<%`   '脚本' 标签，用于流程控制，无输出。
- `<%=`  输出数据到模板（输出是转义 HTML 标签）
- `<%-`  输出非转义的数据到模板
- `<%#`  注释标签，不执行、不输出内容

**结束标签(定界符)**

- `%>`    一般结束标签

- `-%>`   删除紧随其后的换行符

  

**3.2 模板内使用JavaScript**

```ejs
<%= new Date() %>
<%= 1 + 100 %>
<%= nameList.join(',') %>
```



**3.3 流程控制**

```ejs
<ul>
  <% users.forEach(function(user){ %>
    <%- include('user/show', {user: user}) %>
  <% }); %>
</ul>
```

```ejs
<% if (user) { %>
  <h2><%= user.name %></h2>
<% } %>
```



**3.4 Include**

```ejs
<ul>
  <% users.forEach(function(user){ %>
    <%- include('user/show', {user: user}) %>
  <% }); %>
</ul>
```

```ejs
<%- include('header') -%>
<h1>
  Title
</h1>
<p>
  My page
</p>
<%- include('footer') -%>
```



**3.5 自定义分隔符(定界符)**

```javascript
// 单个模板文件
ejs.render('<?= users.join(" | "); ?>', {users: users},
    {delimiter: '?'});


// 全局
ejs.delimiter = '$';
ejs.render('<$= users.join(" | "); $>', {users: users});


```







## 他山之石

```http
node 官网
https://nodejs.org/dist/latest-v10.x/docs/api/net.html#net_net_createserver_options_connectionlistener

菜鸟
https://www.runoob.com/nodejs/nodejs-net-module.html

《http_百度百科》：
http://baike.baidu.com/view/9472.htm

《结果编码和http状态响应码》：
http://blog.tieniu1980.cn/archives/377

《使用Wireshark来检测一次HTTP连接过程》：
http://blog.163.com/wangbo_tester/blog/static/12806792120098174162288/

《http协议的几个重要概念》：
http://nc.mofcom.gov.cn/news/10819972.html

《http协议中connection头的作用》：
http://blog.csdn.net/barfoo/archive/2008/06/05/2514667.aspx 


```

