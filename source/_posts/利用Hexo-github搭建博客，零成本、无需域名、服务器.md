---
title: 利用Hexo+github搭建博客，零成本、无需域名、服务器
date: 2017-04-14 10:16:04
tags: [hexo,node,blog,'博客']
---
之前的博客是用wordpress搭建在阿里云的一台虚拟机上，由于出了个意外，造成我在上面写的文章全部丢失了，虽然不多，但是也都是心血。吸取教训我打算换种方式搭建博客，分析了目前比较流行的博客框架ghost、Jekyll、hexo，最终选择了hexo。
hexo虽不如前两者那么火热，但还是很令我喜欢的：
1. 依赖少(node),易安装
2. 用markdown编写，生成纯静态文件，无需考虑库(前端最爱)
3. 台湾人写的，中文文档友好
4. 托管在github上，永不丢失

下面就开始文章的主要内容。
<!-- more -->

# **准备工作**
## 安装node
很简单就跟平日装软件是一样的，如果不会看下面链接或者自行百度
http://www.runoob.com/nodejs/nodejs-install-setup.html
## 安装Git
同样不难，看下面链接或者自行百度
https://jingyan.baidu.com/article/020278117cbe921bcc9ce51c.html
注意：安装git第三步，要选择第二个（命令行模式），其他直接下一步。。。

## 注册github账号
到github官网注册账号，有账号请略过
## 配置SSH Key
注册完之后需要添加 SSH Key。
SSH Key是一个认证，让github识别绑定这台机器，允许这台机器无需密码提交，修改项目。执行如下命令：
```
cd ~/. ssh
```
~这个符号，表示在用户目录下
执行代码如果提示：No such file or directory 说明你是第一次使用git。
下面就说下怎么配置SSH Key。
## 生产新的SSH Key配置
在Git Bash(在任意文件夹中鼠标右击选择Git Bash Here打开)执行代码：
```
ssh-keygen -t rsa -C "jsl1992@163.com"
```
上面的邮箱记得修改成你自己的，成功后会生成两个文件id_rsa（私钥） 以及id_rsa.pub（公钥）。
然后找到这两个文件，默认都在C盘 > 用户 > xxx > .ssh 里面（xxx是计算机名字，我这里是jsl）

![这里写图片描述](http://img.blog.csdn.net/20170414113615348?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![这里写图片描述](http://img.blog.csdn.net/20170414113658536?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

然后用文本编辑器把id_rsa_pub（公钥）这个文件打开，全选复制出来；
然后打开在github上添加SSH Key，登录github账号，点击右上角用户头像，选择setting（设置）>  SSH and GPG keys  >  NewSSH key
![这里写图片描述](http://img.blog.csdn.net/20170414113724142?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
然后把刚才复制的内容粘贴到key这里就可以了，title不用填，自己会识别
![这里写图片描述](http://img.blog.csdn.net/20170414113744599?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#  搭建博客

## 安装Hexo
在计算机上找个地方新建个blog文件夹，在Git Bash中。
输入以下命令用于安装hexo(我用的是cnpm，跟npm是一样的，比npm速度快，感兴趣可以到这里安装 http://npm.taobao.org/)
```
npm i -g hexo
```

等安装完成后，输入hexo命令测试是否安装成功，成功的话会出现下图这样
![这里写图片描述](http://img.blog.csdn.net/20170414113807643?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
继续，我们初始化hexo，输入以下命令：
```
hexo init hexo
```
初始化成功会出现下图这样
![这里写图片描述](http://img.blog.csdn.net/20170414113823424?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
现在看你blog文件夹下就会出现一个hexo的文件夹，再次输入命令 ,进入hexo文目录：
```
cd hexo
```

进入hexo目录后，输入以下命令，安装hexo项目所依赖的文件：
```
npm i
```
然后输入以下命令，本地部署hexo
```
hexo generate
```
然后输入 以下命令就可以本地运行hexo了
```
hexo server
```
![这里写图片描述](http://img.blog.csdn.net/20170414113914988?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
在浏览器中输入 http://localhost:4000  就能看到本地的默认博客页面了

![这里写图片描述](http://img.blog.csdn.net/20170414113925100?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


现在hexo是基本搭建完成，接下来就是，将hexo和github连接起来。
## 配置github
登录github，点击右上角加号，选择New repository(新建仓库)
![这里写图片描述](http://img.blog.csdn.net/20170414113949551?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
####启用GitHub Page


点击github右上角头像，点Your profile，进入到你的github主页，那里能看到你刚创建的xxx.github.io项目,点进去，然后选择Settings，就进入到项目设置页面，往下拉找到GitHub Pages的框框处，点击“Launch automatic page generator”，如下图
![这里写图片描述](http://img.blog.csdn.net/20170414114001866?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

进入后点击底部的”Continue to layouts“
之后随意选择一个模板，点击“Publish page”，
然后打开自己在github的静态网址，我的http://jiaosl.github.io 你会发现，打开是你自己刚才选择静态站点模版。
## 将本地hexo项目托管到Github

进入hexo文件夹，找到_config.yml文件，用文本编辑器打开
![这里写图片描述](http://img.blog.csdn.net/20170414114316525?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
拉到底部，看到
```
deploy:
```

在deploy: 的下面加入以下代码：
```
type: git
repository: git@github.com:jiaosl.github.io.git
branch: master
```

repository的值，对照着我的写，或者进入你刚才创建的git项目中，点击Clone or downloads，输入框里的内容就是repository的值。
此文件里的其他信息，都是网站的配置信息，以后可以自己修改，
![这里写图片描述](http://img.blog.csdn.net/20170414114359104?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 安装hexo-deployer-git插件
```
npm i hexo-deployer-git --save
```

## 部署你本地的主题到github上
依次运行以下命令
```
hexo clean
hexo generate   # or hexo g
hexo deploy  #or hexo d
```

最后打开github项目的网站 [jiaosl.github.io](https://jiaosl.github.io),就可以看到你的博客页面了.

## 域名绑定github
如果看到这里说明你已经搭建成功了，接下来如果想要把自己的域名绑定到刚搭建的博客里，请继续看。
#### 域名解析
将自己的域名添加一条CNAME记录，

![这里写图片描述](http://img.blog.csdn.net/20170414151028700?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

我用的是阿里云的域名，点击解析按钮，记录类型选择CNAME，主机记录可以不用填，记录值写你的github的二级域名，我的是jiaosl.github.io 然后保存就可以了，大约一两分钟会生效
![这里写图片描述](http://img.blog.csdn.net/20170414152851840?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 光是解析到github是不行的，还需要我们在github中配置，允许我们的域名解析到这里，我们在本地hexo目录下的source中新建一个文件： CNAME  **注意这个文件没有后缀名**
 ![这里写图片描述](http://img.blog.csdn.net/20170414153020556?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 打开CNAME文件，将我们的域名填入，然后保存，例如我的是 jiaosl.com
 ![这里写图片描述](http://img.blog.csdn.net/20170414153051106?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

 然后发布我们的代码到github，等几分钟就可以可以访问了（上传文章有延迟），发布也就是我们前面的两步
```
hexo g
hexo d
```

到这里搭建基本结束，后续还会有hexo详细操作和，换主题的文章。
