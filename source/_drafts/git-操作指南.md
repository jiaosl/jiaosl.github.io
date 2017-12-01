---
title: git 操作指南
tags: [git]
keywords: git
---

参考这里: http://www.bootcss.com/p/git-guide/

https://lluvio.github.io/blog/git-guide.html
每次新建立项目或者新建立关系的项目，执行命令时都是需要后面带上 origin master

需要设置默认提交地址 git push --set-upstream origin master


将yilia主题作为一个 项目放到github上，也就是说将yilia项目迁移地址，操作如下：
git remote add-url origin 增加资源库地址

git remote set-url origin 关联资源库地址


接下来面对两种情况，也就是新的git仓库是否是空地址。

a) 如果是空地址，ok很简单。

首先git add .

然后git commit -m ‘‘

用这个命令：git push ，如果不好使可以使用强推 git push -f

当然这是把目前的工程推送到远程默认分支（master）

扩展：如果想把本地包括master在内的所有分支一起推送出去，可以使用以下方法：

（1）git push --all -f （理论可以的）

（2）保险一点采用如下命令:(一定是可以的)

     git checkout 分支名

     git push origin test（本地分支）:test（远程分支）

     如果不好用，确定是要覆盖的话，可以加一个-f

     git push -f origin test（本地分支）:test（远程分支）



b) 如果不是空地址，ok也很简单，先将该地址清空，再push。

这里我采用的清空方式是这样。

首先，在本地创建一个文件夹，然后使用：

git clone 地址

将本地与远程库挂钩，然后使用清除命令。

git rm .

或者git rm -r 文件件名（删除文件夹）

然后再push，这样远程仓库就被清空了。然后再执行a)
