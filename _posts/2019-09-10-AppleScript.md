---
layout: post
title: "数据分析方法"
date: 2019-09-05
tag: da
---





## AppleScript-jsx

首先了解一下 Apple 公司创造 AppleScript 的初衷，它是用来编写运行于mac的脚本的。重要的是它是 mac 上操作应用程序为数不多的途径之一。

**用途**

------

- 可以用来书写脚本直接生成脚本文件(.scpt)、App 文件；
- 可以用来编写 Cocoa App（也可以创建 Automation Action）；
- 可以在 Alfred.app 和 Autormator.app 中使用；
- 可以非常方便的在 Shell 和 OC 中调用执行；

**编辑器**

ScriptEditor；MacOS 上有自带的脚本编辑器，目前支持 AppleScript 和 JavaScript。
其中有模版工程、模版代码、应用词典等功能，极大方便了 AppleScript/JavaScript 脚本的编写。

## **语法**

AppleScript有4种最基本的数据类型：number、string、list和record；数值、字符串、数组和字典。

**number 类型**

```applescript
set x to 2
get x
set y to 3
get y
set xy to x * y
set x3 to y ^ 3

output：27.0
```

**string 类型**

```javascript
set strX to "Hello "
set strY to "AppleScript"

-- 字符串拼接
set strXY to strX & strY
-- 获取字符串长度
set lengthOfStrXY to the length of strXY

-- 分割成单个字符并组成一个新的列表
set charList to every character of strXY

-- 通过 AppleScript's text item delimiters 来指定分隔号，然后通过 every text item of 来实现分割
set defaultDelimiters to AppleScript's text item delimiters
set AppleScript's text item delimiters to " "
set listAfterDelimiter to every text item of strXY
set AppleScript's text item delimiters to defaultDelimiters


-- number 与 string 类型转换
set numberToString to 100 as string
set stringToNumber to "1234" as number


output :1234
```

**list 类型**

```
set firstList to { 100, 200.0, "djfif", -10 }
set emptyList to {}
set currentList to { 2, 3, 4, 5 }

-- 列表拼接
set modifiedList to firstList & emptyList & currentList

-- 获取和更改列表中的元素
set item 2 of modifiedList to "2"
get modifiedList
set the third item of modifiedList to "abcde"
get modifiedList

-- 用列表中的随机元素赋值
set randomX to some item of modifiedList

-- 获取最后一个元素
set lastItem to the last item of modifiedList

-- 负数表示从列表尾端开始获取元素
set aLastItem to item -2 of modifiedList

-- 获取第一个元素
set firstItem to the first item of modifiedList

set longList to { 1,2,3,4,5,6,7,8,9,10 }
set shortList to items 6 through 8 of longList

-- 逆向获取子列表
set reversedList to reverse of longList
set listCount to the count of longList
set the end of longList to 5
get longList

-- 将 string 转换为 list
set string1 to "string1"
set stringList to string1 as list

-- 可以用&将字符串和列表连接起来，结果取决于&前面的变量
set strAndList to string1 & stringList

output:
"string1string1"
```



**record 类型**

```
set aRecord to { name1:100, name2:"This is a record"}
set valueOfName1 to the name1 of aRecord

set newRecord to { name1:name1 of aRecord }

set numberOfProperties to the count of aRecord

output:2 
```

---



**条件/循环**

```
set x to 500

if x > 100 then
	display alert "x > 100"
else if x > 10 then
	display alert "x > 10"
else
	display alert "x <= 10"
end if


set sum to 0
set i to 0
repeat 100 times
	set i to i + 1
	set sum to sum + i
end repeat
get sum


repeat with counter from 0 to 10 by 2
	display dialog counter
end repeat

set counter to 0
set listToSet to {}
-- 注意下这个 ≠ 符号是使用 Option+= 输入的
repeat while counter ≠ 10
	-- display dialog counter as string
	set listToSet to listToSet & counter
	set counter to counter + 2
end repeat
get listToSet

set counter to 0
set listToSet to {}
repeat until counter = 10
	-- display dialog counter as string
	set listToSet to listToSet & counter
	set counter to counter + 2
end repeat
get listToSet

set aList to {1, 2, 8}
repeat with anItem in aList
	display dialog anItem as string
end repeat


output :输出
x>100
0
2
4
6
8
10
1
2
8

{button returned:"好"}
```



- 注释

  ```applescript
  -- 这是单行的注释
  
  (*
  这是多行的注释
  这是多行的注释
  *)
  ```

- 函数

  ```applescript
  on showAlert(alertStr)
    display alert alertStr buttons {"I know", "Cancel"} default button "I know"
  end showAlert
  
  showAlert("hello world")
  ```

- 换行

  ```applescript
  on showAlert(alertStr)
    display alert alertStr buttons {"I know", "Cancel"} default button "I know"
  end showAlert
  
  showAlert("hello world")
  ```

- 使用AppleScript中的对话框

  > 使用弹出框有一些要注意的地方:
  >
  > - 1.它可以有多个按钮的;
  > - 2.它是有返回值的,返回值是你最终操作的字符串;
  > - 3.它是可以增加输入框的，而且比你想的简单多了;

  ```jsx
  set dialogString to "Input a number here"
  set returnedString to display dialog dialogString default answer ""
  get returnedString
  
  --//{button returned:"好", text returned:"asdf"}
  set dialogString to "Input a number here"
  set returnedString to display dialog dialogString default answer ""
  set returnedNumber to the text returned of returnedString
  try
    set returnedNumber to returnedNumber as number
    set calNumber to returnedNumber * 100
    display dialog calNumber
  on error the error_message number the error_number
    display dialog "Error:" & the error_number & " Details:" & the error_message
  end try
  
  beep
  ```

- 预定义变量

  > 就是一些特殊的关键字，类似于其他语言中的 self、return等，有固定的含义；
  >
  > 千万不要用它来自定义变量。

  - **result**：记录最近一个命令执行的结果，如果命令没有结果，那么将会得到错误
  - **it**：指代最近的一个 tell 对象
  - **me**：这指代段脚本。用法举例 path to me 返回本脚本所在绝对路径
  - **tab**：用于string，一个制表位
  - **return**：用于string，一个换行

- 字符串比较：Considering/Ignoring语句

  在 AppleScript 的字符串比较方式中，你可以设定比较的方式：上面 considering 和 ignoring 含义都是清晰的，一个用于加上xx特征，一个用于忽略某个特征；一个特征就是一个attribute。
  atrribute应该为列表中的任意一个:

  ```jsx
  - case 大小写
  - diacriticals 字母变调符号(如e和é)
  - hyphens 连字符(-)
  - numeric strings 数字化字符串(默认是忽略的)，用于比较版本号时启用它。
  - punctuation 标点符号(,.?!等等,包括中文标点)
  - white space 空格
  ```

- 列表选择对话框

  ```jsx
  
  ignoring case
  	if "AAA" = "aaa" then
  		display alert "AAA equal aaa when ignoring case"
  	end if
  end ignoring
  
  considering numeric strings
  	if "10.3" > "9.3" then
  		display alert "10.3 > 9.3"
  	end if
  end considering
  --列表选择对话框
  display alert "这是一个警告" message "这是警告的内容" as warning
  choose from list {"选项1", "选项2", "选项3"} with title "选择框" with prompt "请选择选项"
  ```

  选择框有以下参数:

  ```
  - 直接参数 紧跟list类型参数，包含所有备选项
  - title 紧跟text，指定对话框的标题
  - prompt 紧跟text，指定提示信息
  - default items 紧跟list，指定默认选择的项目
  - empty selection allowed 后紧跟true表示允许不选
  - multiple selections allowed 后紧跟true表示允许多选
  ```

  

- 文件选择对话框

  ```applescript
  -- 选取文件名称Choose File Name
  choose file name with prompt "指定提示信息"
  
  -- 选取文件夹Choose Folder
  choose folder with prompt "指定提示信息" default location file "Macintosh HD:Users" with invisibles, multiple selections allowed and showing package contents
  
  -- 选取文件Choose File
  choose file of type {"txt"}
  ```

- 文件读取和写入

  > 文件读取用read，允许直接读取；
  >
  > 但是写入文件之前必须先打开文件，打开文件是open for access FileName；
  >
  > 写入文件用write...to语句；
  >
  > 最后记得关闭文件close access filePoint

  

- 其它语法

  上面的例子只是苹果官方文档的精简入门版，还有语言的面相对象特征，此处不再展开。

  AppleScript 中还有比较丰富的其它 Command 集合，此处也不再一一列举。

**案例**

------

- 使用 mac 的邮件系统

  mail.scpt文件名

  ```scpt
  --Variables
  set recipientName to " 小红"
  set recipientAddress to "aliyunzixun@xxx.com"
  set theSubject to "AppleScript Automated Email"
  set theContent to "This email was created and sent using AppleScript!"
  --Mail Tell Block
  tell application "Mail"
    --Create the message
    set theMessage to make new outgoing message with properties {subject:theSubject, content:theContent, visible:true}
    --Set a recipient
    tell theMessage
        make new to recipient with properties {name:recipientName, address:recipientAddress}
        --Send the Message
        send
    end tell
  end tell
  
  
  --Variables
  set recipientName to " 小杰"
  set recipientAddress to "pc554328955@gmail.com"
  --set recipientAddress to "2951749090@qq.com"
  set theSubject to "respect you"
  set theContent to "吾日三省吾身，传不习乎，与朋友交而不信乎，为人谋而不忠乎，"
  --Mail Tell Block
  tell application "Mail"
  	--Create the message
  	set theMessage to make new outgoing message with properties {subject:theSubject, content:theContent, visible:true}
  	--Set a recipient
  	tell theMessage
  		make new to recipient with properties {name:recipientName, address:recipientAddress}
  		--Send the Message
  		send
  	end tell
  end tell
  ```

  

- 让浏览器打开网页

  ```
  set urlMyBlog to "https://blog.csdn.net/sodaslay"
  set urlChinaSearch to "http://www.chinaso.com"
  set urlBiying to "https://cn.bing.com"
  
  --使用Chrome浏览器
  tell application "Google Chrome"
    --新建一个chrome窗口
    set window1 to make new window
    tell window1
        --当前标签页加载必应,就是不用百度哈哈
        set currTab to active tab of window1
        set URL of currTab to urlBiying
        --打开csdn博客,搜索
        make new tab with properties {URL:urlMyBlog}
        make new tab with properties {URL:urlChinaSearch}
        --将焦点由最后一个打开的标签页还给首个标签页
        set active tab index of window1 to 1
    end tell
  end tell
  ```

  **python自动发邮件**

```python
import smtplib
from email.mime.text import MIMEText
'''
发送邮件函数，默认使用163smtp
:param mail_host: 邮箱服务器，16邮箱host: smtp.163.com
:param port: 端口号,163邮箱的默认端口是 25
:param username: 邮箱账号 xx@163.com
:param passwd: 邮箱密码(不是邮箱的登录密码，是邮箱的授权码)
:param recv: 邮箱接收人地址，多个账号以逗号隔开
:param title: 邮件标题
:param content: 邮件内容
:return:
'''
def send_mail(username, passwd, recv, title, content, mail_host='smtp.163.com', port=25):
  msg = MIMEText(content)  # 邮件内容
  msg['Subject'] = title   # 邮件主题
  msg['From'] = username   # 发送者账号
  msg['To'] = recv      # 接收者账号列表
  smtp = smtplib.SMTP(mail_host, port=port)   # 连接邮箱，传入邮箱地址，和端口号，smtp的端口号是25
  smtp.login(username, passwd)          # 登录发送者的邮箱账号，密码
  # 参数分别是 发送者，接收者，第三个是把上面的发送邮件的 内容变成字符串
  smtp.sendmail(username, recv, msg.as_string())
  smtp.quit() # 发送完毕后退出smtp
  print('email send success.')

if __name__ == '__main__':
  email_user = 'pc554328955@qq.com' # 发送者账号
  
  email_user = 'pc554328955@163.com' # 发送者账号
  # email_pwd = "'ww1234','mrrzqsaxcfukbcbf'" # 发送者密码,授权码
  email_pwd = '.' # 发送者密码,授权码
  # maillist = '787119359@qq.com'
  maillist = 'pc554328955@gmail.com'
  title = 'Give you my utmost respect'
  content = '想念你了，你呢？有没有想我呢，哦，真的没有吗？ 那真的是太可惜了，算了我给你讲个故事吧 ：哈哈，没了。'
  send_mail(email_user, email_pwd, maillist, title, content)
```



- 让你的电脑说话(哈哈)

  ```
  -- You can use any of the voices from the System Voice pop-up on the Text to Speech tab in the Speech preferences pane.
  -- Default Value:
  -- The current System Voice (set in the Speech panel in System Preferences.
  
  tell current application
  	say "My name is LiMei. Nice to meet you. How are you?" using "Veena"
  	say "Fine, thanks. And you?" using "Victoria"
  	say "滚"
  	say "我跟你说" using "Sin-Ji"
  	say "love 亮亮"
  	say "祝洁琼是猪！"
  end tell
  
  beep
  ```

  

- 调用 mac 的通知中心

  > crontab + AppleScript + 通知中心 可以做很多定制的提醒工具

  ```
  display notification "message" with title "title" subtitle "subtitle"
  
  display notification "message" sound name "Bottle.aiff"
  -- 声音文件都在 ~/Library/Sounds 和 /System/Library/Sounds 下面
  ```

  

  

- 清理废纸篓

  ```applescript
  tell application "Finder"
    empty the trash
    beep
    -- 打开启动磁盘
    open the startup disk
  end tell
  ```

- 模拟键盘按键消息

  ```applescript
  launch application "System Events"
  launch application "TextMate"
  tell application "System Events"
    set frontmost of process "TextMate" to true
    keystroke "input string from applescript"
    keystroke "a" using command down
    keystroke "c" using command down
    keystroke "a" using command down
    key code 124 using command down
    keystroke "
  "
    keystroke "v" using command down
  end tell
  ```

  > 其中 using command 可以使用组合，例如：key code 53 using {command down, option down}
  >
  > 其中的 key code 对照表如下

  

- 切换程序前台、设置焦点窗口

  ```applescript
  -- 前提是当前 iTerm app 中打开了两个窗口，其中有个窗口名字叫 "2. bash" 并且该窗口中第一个 tab 中含有三个 session，本脚本的作用是让 "2. bash" 窗口中第一个 tab 中的第三个 session 变为焦点。
  tell the application "iTerm"
    activate
    
    set theWindow to the first item of ¬
        (get the windows whose name is "2. bash")
    if index of theWindow is not 1 then
        set index of theWindow to 1
        
        set visible of theWindow to false
        set visible of theWindow to true
    end if
    
    tell theWindow
        set theTab to the first item of theWindow's tabs
        
        select theTab
        
        select the third session of theTab
    end tell
  end tell
  ```

  ```applescript
  -- 下面是上面的逻辑的另一种实现
  tell the application "iTerm"
    activate
    
    set theWindow to the first item of ¬
        (get the windows whose name is "2. bash")
    if the index of theWindow is not 1 then
        set the index of theWindow to 2
        tell application "System Events" to ¬
            tell application process "iTerm2" to ¬
                keystroke "`" using command down
    end if
  end tell
  ```

- 粘贴板操作(有问题)

  ```applescript
  set the clipboard to "Add this sentence at the end."
  tell application "TextEdit"
    activate --make sure TextEdit is running
    make new paragraph at end of document 1 with data (return & (the clipboard))
  end tell
  ```



**何时使用？**

------

- 一些跨应用的重复操作步骤使用 AppleScript/JavaScript 实现关键步骤
- 结合 Alread.app、Automator.app、crontab 等实现一些场景的触发调用
- 本地的一些工具脚本可以直接调用 AppleScript 做一些简单的输入、弹框、通知交互
- 用 AppleScript 写一个 CocoaApp 或者 Automator Action（**但是可以用 Objective-C 我们就没必要使用相对不熟悉的 AppleScript**）
- OC 的命令行工程可以借助 NSAppleScript 操作其它应用
- CocoaApp 工程可以通过 XPCService+ScriptingBridge+AppleScript(OC版本接口调用)启动其它应用看文献

**生成 Cocoa App 的 OC 接口文件**

------

> 需要通过 OC 调用系统中某个 App 的接口，可以参照如下命令行导出其 .h 文件

```shell
sdef /Applications/Mail.app | sdp -fh -o ~/Desktop --basename Mail --bundleid `defaults read "/Applications/Mail.app/Contents/Info" CFBundleIdentifier`

```





## 他山之石

```

Mac 的自动化 AppleScript 终极入门手册
https://wenku.baidu.com/view/41c783c3aa00b52acfc7ca09.html
github样例工程
https://github.com/BenXia/AppleScriptStudy/tree/master/5_快发邮件OC版本
https://github.com/BenXia/AppleScriptStudy/tree/master/5_%E5%BF%AB%E5%8F%91%E9%82%AE%E4%BB%B6OC%E7%89%88%E6%9C%AC/SendMail

初识 AppleScript
https://www.jianshu.com/p/a22084e87b09
```





