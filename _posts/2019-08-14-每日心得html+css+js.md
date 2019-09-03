---
layout: post
title: "ejs+html+css+js"
date: 2019-08-14
tag: JS
---



### 这个？

继续学习js



# ejs模板引擎

## 1.使用之前

### 1.1安装

EJS 是后台模板，可以把我们数据库和文件读取的数据显示到 Html 页面上面（解析页面视图模板）。它是一个第三方模块，需要通过 npm 安装https://www.npmjs.com/package/ejs

```
npm  install ejs --save
cnpm install ejs --save
```

### 1.2引入

```
const  ejs = require('ejs');
```

## 2.怎么使用

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

#### 选项

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

## 3模板语法

### 3.1 分隔符(定界符)

##### 开始标签(定界符)

- `<%`   '脚本' 标签，用于流程控制，无输出。
- `<%=`  输出数据到模板（输出是转义 HTML 标签）
- `<%-`  输出非转义的数据到模板
- `<%#`  注释标签，不执行、不输出内容

##### 结束标签(定界符)

- `%>`    一般结束标签

- `-%>`   删除紧随其后的换行符

  

### 3.2 模板内使用JavaScript

```ejs
<%= new Date() %>
<%= 1 + 100 %>
<%= nameList.join(',') %>
```



### 3.3 流程控制

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



### 3.4 Include

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



### 3.5 自定义分隔符(定界符)

```javascript
// 单个模板文件
ejs.render('<?= users.join(" | "); ?>', {users: users},
    {delimiter: '?'});


// 全局
ejs.delimiter = '$';
ejs.render('<$= users.join(" | "); $>', {users: users});

```



