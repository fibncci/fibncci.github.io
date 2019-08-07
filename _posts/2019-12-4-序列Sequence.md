---
这里使用了Typora 这款极简的MarkDown编辑器，还集成了非常多的扩展。
---



### sequence语法

这里我大体上分为四类：

- 标题：sequence 图标题。
- 注释：对参与构成序列图成员的描述，这里有三种，1 在成员左边，2在成员右边，3悬浮在成员体上。
- 流向(箭头)：定义序列的方向，有虚线，实线，空箭头和黑体箭头。
- 成员：定义参与的成员。

### 标题

使用title关键字输入冒号（英文状态下）和 标题内容即可。

示例：

```
​```sequence
title: MarkDown 画sequence图
participant finefine as ff
participant kunkun as kk
ff-->kk: this is kunkun?
kk-->ff: yes!
​```
```



```sequence
title: MarkDown 画sequence图
participant finefine as ff
participant kunkun as kk
ff-->kk: this is kunkun?
kk-->ff: yes!
```





### 注释

使用note 关键字表明注释，left of、right of、over 表明注释的位置。

left of

示例：

```
​```sequence
title: 注释演示
participant A
note left of A: note 在A左边
​```
```

```sequence
title: 注释演示
participant A
note left of A: note 在A左边
```





right of

示例：

```
​```sequence
title: 注释演示
participant A
note right of A: note 在A右边
​```
```

```sequence
title: 注释演示
participant A
note right of A: note 在A右边
```

over

示例：

```
​```sequence
title: 注释演示
participant A
note over A: note 浮在A上
​```
```

```sequence
title: 注释演示
participant A
note over A: note 浮在A上
```

over 还可以同时浮在两个成员上

示例：

```
​```sequence
title: 注释演示
participant A
participant B
note over A,B: note 浮在A和B上
​```
```

```sequence
title: 注释演示
participant A
participant B
note over A,B: note 浮在A和B上
```

over 跨过中间成员

示例：

```
​```sequence
title: 注释演示
participant A
participant B
participant C
participant D
note over A,D: note 跨过BC
​```
```



```sequence
title: 注释演示
participant A
participant B
participant C
participant D
note over A,D: note 跨过BC
```

### 流向

"-"表示实线，"--"表示实线，">"表示黑体箭头，">>"表示空心箭头。

1. "-->>"

示例：

```
​```sequence
title: 流向演示
participant A
participant B
A-->>B: 虚线空心演示
​```
```

```sequence
title: 流向演示
participant A
participant B
A-->>B: 虚线空心演示
```



1. "-->"

示例：

```
​```sequence
title: 流向演示
participant A
participant B
A-->B: 虚线实心演示
​```
```



```sequence
title: 流向演示
participant A
participant B
A-->B: 虚线实心演示
```

1. "->>"

示例：

```
​```sequence
title: 流向演示
participant A
participant B
A->>B: 实线空心演示
​```
```

```sequence
title: 流向演示
participant A
participant B
A->>B: 实线空心演示
```

1. "->"

示例：

```
​```sequence
title: 流向演示
participant A
participant B
A->B: 实线实心演示
​```
```



```sequence
title: 流向演示
participant A
participant B
A->B: 实线实心演示
```

### 成员

使用 participant 可定义成员，使用as 可以为成员定义别名。

participant

示例：

```
​```sequence
title:成员定义
participant Client
​```
```



```sequence
title:成员定义
participant Client
```

participant 和 as，使用as 的目的是为了简写成员

示例：

```
​```sequence
title:定义成员
participant finefine as ff
participant kunkun as kk
ff->kk: say hello 
ff->ff: say hello to my self
​```
```



```sequence
title:定义成员
participant finefine as ff
participant kunkun as kk
ff->kk: say hello 
ff->ff: say hello to my self
```

## Sequence实战（ 按顺序排好）

这里使用sequence 画一个Token 原理图，token 校验的原理，这里简单说一下，客户端使用密码和用户名登录，如果服务端认证成功，则会返回token，下次客户端去请求数据时，只需携带token即可通过安全认证从而获取所需的数据。（参与者participant）

```
​```sequence
title: Token Valid logic
participant Client as C
participant Server as S
C->S: 1.login with username and password
S->C: 2.response with token and something
note left of C: such as Android App、IOS\n App and so on.
note right of S: supply Api Service
C->S: 3.request data with token
S->C: 4.response with data
note right of S: if token is valid then return\n the data that Client needed
note over C,S: This is the Token principle
​```
```

```sequence
title: Token Valid logic
participant Client as C
participant Server as S
C->S: 1.login with username and password
S->C: 2.response with token and something
note left of C: such as Android App、IOS\n App and so on.
note right of S: supply Api Service
C->S: 3.request data with token
S->C: 4.response with data
note right of S: if token is valid then return\n the data that Client needed
note over C,S: This is the Token principle
```