---
title: 利用Hexo+coding搭建博客，优化github博客打开速度
date: 2017-04-17 16:32:25
tags: [hexo,github,blog,'博客']
keywords: hexo,blog,前端,html
---
上次用hexo和github上搭建博客后，用了几天发现博客搭建在github上有一定的局限：
					1. github服务器在国外，可能访问量太大，国内访问速度有些慢;
					2. github屏蔽百度爬取，不利于seo;
所以，打算在[coding](https://coding.net)上也搭建同样的hexo，然后通过解析让国内用户访问coding上的博客，国外用户访问github上的博客（貌似没什么国外的用户会看 ❥(^_-)）。
上篇文章[利用Hexo+github搭建博客，零成本、无需域名、服务器](http://blog.csdn.net/wkzd2016/article/details/70170786),对于整个流程讲的已经很详细，本文就简单介绍下流程。
<!-- more -->
## 什么是coding？
简单的说coding就是类似于github的开源代码仓库，几乎是完全仿照github做的；虽然现在代码量并不多，但是部分地方还是比github方便一些的：
1. 中文界面，对我们来用起来更加方便；
2. 可以免费创建私有仓库；
3. 虽然服务器也在国外，但访问速度比github要快不少
## 注册coding并创建项目
这一部分很简单，不多说。需要注意的是创建项目的时候项目名称跟我们在github上创建时候类似，项目名一定要是：用户名 + coding.me
这样写的原因是此类pages服务中大都可以通过 {user_name}.域名 的项目名来访问此主页，(有兴趣请看coding的文档[用户 Pages 与项目 Pages](https://coding.net/help/doc/pages/index.html) )
![这里写图片描述](http://img.blog.csdn.net/20170417144930611?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
## 开启pages服务
进入刚创建好的项目，点pages服务，选择来源处选择master分支，
![这里写图片描述](http://img.blog.csdn.net/20170417152117134?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

点击保存后，提示coding已运行在jiaosl.coding.me，说明开启成功，如下图:
![这里写图片描述](http://img.blog.csdn.net/20170417152433839?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
## 配置SSH key
此部分跟github上配置SSH Key完全相同，进入项目，设置，部署公钥，将你电脑上的公钥粘贴上就行。不懂的看上一篇文章。
## hexo中添加coding仓库
打开本地的hexo项目根目录下的_config.yml 配置文件，找到deploy，将coding中的项目地址填入进去。
我们之前的repository是这样的
![这里写图片描述](http://img.blog.csdn.net/20170417150844137?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

现在要同时发布到hithub和coding上，所以repository的值，就要改成键值对的形式列出来。如下图：
![这里写图片描述](http://img.blog.csdn.net/20170417150610087?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
要注意：.yml文件格式非常严格，冒号后面必须要有空格。
## 部署hexo到coding和github上
在git bash中执行命令：
```
hexo d
```
现在我们每次执行部署命令，代码会同时提交到github和coding上。现在打开coding已经可以看到我们部署的hexo项目了,然后访问我们刚才开启的pages服务的域名[jiaosl.coding.me](https://jiaosl.coding.me),就可以看到我们的博客已经可以在coding上访问了。
后面的内容依然是为需要使用自己的域名访问博客的用户写的，如果不需要自己的域名请略过。
## 解析域名到coding
#### 1. 将github的解析改成海外
进入我的阿里云控制台，上次添加的解析是这样的![这里写图片描述](http://img.blog.csdn.net/20170414152851840?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

现在我们需要修改这个解析，点击 修改，然后将解析线路改成海外，然后保存，这样国外的用户访问你的博客的话会跳转到你的github的页面。
#### 2. 添加CNAME解析到coding
然后，点添加解析，我们再添加一条到coding的解析，记录类型选CNAME，记录值填你刚才pages服务给的地址，如：[jiaosl.coding.me](https://jiaos.coding.me) ，点击保存，如下图红色框框；
![这里写图片描述](http://img.blog.csdn.net/20170417153831882?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

这样算是解析到了coding，接下来我们需要在coding的pages服务里，绑定我们的域名，解析才会有效果，进入项目的pages服务中，找到在绑定域名那里，填入你的域名，点击绑定，出现下图这样，就说明绑定成功。
![这里写图片描述](http://img.blog.csdn.net/20170417154113550?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
现在访问你的域名，就可以看到你的博客了。

最后我分别ping了两个网站的服务器，可以看出访问coding上的博客相对访问github还是要快一些的
![这里写图片描述](http://img.blog.csdn.net/20170417154954460?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2t6ZDIwMTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


到这里文章就结束了，如果文章对你有帮助，点个赞鼓励一下哦！

个人独立博客：[jiaosl.com](http://jiaosl.com)
