---
title: vim简单操作指南-cheat sheet
date: 2017-04-20 20:54:26
tags: [vim]
keywords: vim
---
在这里记录几个vim的常用命令和一张cheat sheet，方便查看

#### 1. 选中。使用v进入可视模式，移动光标键选定内容。

#### 2. 复制的命令是y，即yank（提起） ，常用的命令如下：
    y      在使用v模式选定了某一块的时候，复制选定块到缓冲区用；
    yy     复制整行（yny ，复制n行，n为数字）；
    y^     复制当前到行头的内容；
    y$     复制当前到行尾的内容；
    yw     复制一个单词（ynw，复制n个单词，n为数字）；
<!--more  -->
#### 3. 剪切的命令是d，即delete，d与y的用法基本相同.  
    d      剪切选定块到缓冲区；
    dd     剪切整行
    d^     剪切至行首
    d$     剪切至行尾
    dw     剪切一个word
    dG     剪切至档尾  

#### 4. 撤销
    u           撤销，可以无限撤销
    U           撤销某一行最近所有修改
    Ctrl+R      重做


> ##注：
     在正则表达式中，^表示匹配字符串的开始位置，$表示匹配字符串的结束位置。
     命令前面加数字表示重复的次数，
     加字母表示使用的缓冲区名称。
     使用英文句号"."可以重复上一个命令。


下面为一张vim cheat sheet 网上确实不好找 😂
![vim-cheat-sheet.png](http://upload-images.jianshu.io/upload_images/1969397-fce6a4861fbc8fad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
