---
layout: post
title: "Github commit时出现event not found"
excerpt: 
categories: articles
tags: [github]
comments: true
share: true
---

在Windows下使用Git配置代理服务器时，需要使用
```
git config --global proxy.http http://userid:password@proxy.company.com:8080
```
 来配置代理。其中因为password中含有感叹号“！”,在git终端中显示
 **“！:event not found”**。
 在本以为是git的问题，Google了“git ！:event not found “，发现大多数使用git碰到这个问题的人，都是在`git commit -m "some commit"`时碰到了同样的问题。其中提交时的备注中含有了感叹号，比如：
 `git commit -m "First commit!"`
就会报错！:event not found，很明显，commit时出现的错误和配置代理服务器时出现的错误是一个原因。

##原因
linux下bash中，单引号和双引号的含义是不同的：单引号中的字符串，其中的特殊字符的意义都被剥夺了，而双引号中的某些特殊字符是有意义的。比如'$'（参数替换）和'`'（命令替换）。

```
NUM=3
echo '$NUM' ##终端将会显示NUM
echo "$SUM" ##终端将会显示3
```

再比如：

```
echo "`pwd`" ##终端将会显示当前路径
echo '`pwd`' ##终端将会显示pwd
```

很不幸，感叹号'!'在bash中也有特殊含义，称之为"事件指示器"
> 下面摘自ubuntu10的中文man页，参照英文man页做了少许的修改。
事件指示器 (event designator) 是一个对历史列表中某个命令行条目的引用。
!      开始一个命令替换，在后面跟随的字母不是“空格、换行、回车、=和(”时。
!n     引用命令行 n.
!-n    引用当前命令行减去 n.
!!     引用上一条命令。这是 `!-1' 的同义词。
!string
引用最近的以 string 开始的命令。
!?string[?]
引用最近的包含 string 的命令。尾部的 ? 可以被忽略，如果 string 之后紧接着一个新行符。
^string1^string2^
快速替换。重复上一条命令，将 string1 替换为 string2.  与 ``!!:s/string1/string2/'' 等价 (参见下面的 修饰符 (Modifiers))。
!#     到此为止输入的整个命令行。

我们在终端 commit时，备注使用了双引号，结尾输入了感叹号，bash将其解析成了时间指示器，但之后却没有事件，所以会报这个错误。

##解决方案
在commit时，最好的解决方案是将双引号该为单引号

```
git commit -m 'First commit!'
```

或者，在感叹号之后加一个空格，因为事件指示器指出：感叹号之后不能是空格。

```
git commit -m "First commit! "
```

在配置代理服务器的时候，似乎加空格的方法就没有效果了，只能使用单引号了，或者，改个密码吧。