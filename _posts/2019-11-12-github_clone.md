gitbub下载东西



## 方法：

第一步：去这个网站查询3个域名对应的IP地址，不能用`ping`来获取IP地址哦

[s](https://www.ipaddress.com/)

```text
https://www.ipaddress.com/
IP地址查询
本机IP: 223.167.32.194上海市上海市 联通
```

第二步：在`/etc/hosts`文件中添加类似下面的3行

```text
192.30.253.113  github.com
151.101.185.194 github.global.ssl.fastly.net
192.30.253.120  codeload.github.com
```

第三步：重启网络

```bash
sudo /etc/init.d/networking restart 
```

现在可以飞快的下载Github上的代码了。

## 1我的ip

```
https://www.ipaddress.com/

我的IPv4地址
223.167.32.194 副本
 什么是我的IP：
223.167.32.194

公用IP地址223.167.32.194位于中国上海。它已分配给ISP 中国联通上海。该地址属于ASN 17621，该地址委托给中国联通上海网络。
请查看下表以获取有关223.167.32.194的完整详细信息，或使用IP查找工具查找任何公共IP地址的近似IP位置。

223.167.32.194 IP地址位置
反向IP（PTR）	没有
ASN	17621（中国联通上海网）
ISP /组织	上海联通
IP连接类型	电缆/ DSL [ 互联网速度测试 ]
IP纬度	31.0449 / 31°2′41″ N
IP经度	121.4012 / 121°24′4″ E
IP时区	亚洲/上海
IP本地时间	2019年11月12日星期二22:40:46 +0800




```



## github

```
192.30.253.113
公用IP地址192.30.253.113位于美国。它已分配给ISP GitHub。该地址属于ASN 36459被委托给GitHub上，公司
请有看看下面的全部细节表约192.30.253.113，或者使用IP查找工具找到任何公共IP地址的大致IP位置。

反向IP（PTR）	lb-192-30-253-113-iad.github.com
ASN	36459（GitHub，Inc.）
ISP /组织	的GitHub
IP连接类型	企业[ 互联网速度测试 ]
IP位置	美国
IP大陆	北美
知识产权国家	美国（美国）
IP状态	不适用
IP城市	未知
IP邮政编码	未知
IP纬度	37.7510 / 37°45′3″ N
IP经度	-97.8220 / 97°49′19″ W
IP时区	美国/芝加哥
IP本地时间	周二，12 Nov 2019 08:53:48 -0600
IPv4地址空间前缀	192/8
区域互联网注册中心（RIR）	由ARIN管理
分配日期	1993年5月
WHOIS服务器	whois.arin.net
RDAP服务器	https://rdap.arin.net/registry、http://rdap.arin.net/registry

```



## 2

```
151.101.185.194
公用IP地址151.101.185.194位于美国伊利诺伊州芝加哥市60602。它被分配到ISP 快速度。该地址属于ASN 54113，该地址委托给Fastly。
请查看下表以获取有关151.101.185.194的完整详细信息，或使用IP查找工具查找任何公共IP地址的近似IP位置。

151.101.185.194 IP地址位置
反向IP（PTR）	没有
ASN	54113（快速）
ISP /组织	快速
IP连接类型	企业[ 互联网速度测试 ]
IP位置	芝加哥，伊利诺伊州，60602，美国
IP大陆	北美
知识产权国家	美国（美国）
IP状态	伊利诺伊州（IL）
IP城市	芝加哥
IP邮政编码	60602
IP纬度	41.8483 / 41°50′53″ N
IP经度	-87.6517 / 87°39′6″ W
IP时区	美国/芝加哥
```

## 3

```
192.30.253.120
公用IP地址192.30.253.120位于美国。它已分配给ISP GitHub。该地址属于ASN 36459被委托给GitHub上，公司
请有看看下面的全部细节表约192.30.253.120，或者使用IP查找工具找到任何公共IP地址的大致IP位置。

192.30.253.120 IP地址位置
反向IP（PTR）	lb-192-30-253-120-iad.github.com
ASN	36459（GitHub，Inc.）
ISP /组织	的GitHub
IP连接类型	企业[ 互联网速度测试 ]
IP位置	美国
IP大陆	北美
知识产权国家	美国（美国）
IP纬度	37.7510 / 37°45′3″ N
IP经度	-97.8220 / 97°49′19″ W
IP本地时间	周二，12 Nov 2019 09:38:55 -0600
```





## 方法二



国内从github上面下载代码的速度峰值通常都是20kB/s。

而常见的的方法：修改HOST或者挂VPN，实际用起来并不稳定。
这里提供一种新的方法，下载速度可以达到 1~2MB/s

1. 利用开源中国提供的代码仓库
标题已经说的很清楚了，我想对于经常使用git的人来讲，很可能已经知道了。对于新手刚接触git的人来讲，可能你只知道github。
实际上，国内也有很多代码仓库提供方，国外也不只github。只不过国内也是刚刚开始，关注的人不多。
开源中国提供的代码仓库提供了一个功能，就是它可以将github账号中的代码 clone 到开源中国的账户中去。这个代码仓库叫做 码云 ，没错就是码云?。
要求你有一个github账户，一个码云gitee账户。
步骤很简单

将github上面你想要搞下来的项目首先 frok 到你自己的github的账户中去。耗时:一瞬间
登录gitee，没有的自行注册。网页中有添加项目的按钮，一个加号。点击加号，下拉列表里面有 迁移github项目 的选项，点开后按照提示关联自己的github账号，之后选择你要迁移的项目，按提示操作。耗时:不到三分钟。
按照 clone github项目方法， clone 迁移到gitee账户中的项目。区别是 clone 链接换成了目标项目在gitee中的链接。通常下载速度是以MB/s为单位的。
按照上面的方法，基本上不再需要整夜挂机 clone 代码了。

2. 提高下载子模块的速度
有的项目里用到了第三方代码仓库，但是在你使用 clone 指令的时候这些子模块 submodule 并不会自动下载，因为他们在另外的地址中存放。你需要 clone 完目标项目后，执行

git submodule update --init --recursive

才会将目标项目所需要的依赖子模块下载下来。github项目中所用到的子模块依然是放在了github上。这就很悲剧了，这意味着你在执行上面指令后，依然需要面对上面的20KB/s的速度。虽然此时并不会显示出来，然而等待依然很久。

我们同样使用上面加速 clone 的思路。

从下载的项目中找到其使用的 submodule 的链接是哪里。
打开上一步中的链接，将使用的目标子模块的代码同样 frok 到自己的github账户中，之后同样的方法迁移到gitee中去。有多个子模块就多重复几次操作，同样的套路。
将原项目使用的 submodule 模块的链接地址修改为子模块迁移到gitee中后的地址。
这时再去执行git submodule update --init --recursive 。
以上就是提高下载子模块速度的思路。具体每步的操作，请自行搜索，网上一搜一大片。

附：：

```
关于如何修改submodule连接地址

https://blog.csdn.net/wangjia55/article/details/24400501
https://www.jianshu.com/p/c81e2bd377ad
https://blog.csdn.net/qq_22630169/article/details/74236535
https://blog.csdn.net/wangjia55/article/details/24400501
```



https://blog.csdn.net/wangjia55/article/details/24400501
https://www.jianshu.com/p/c81e2bd377ad
https://blog.csdn.net/qq_22630169/article/details/74236535
https://blog.csdn.net/wangjia55/article/details/24400501