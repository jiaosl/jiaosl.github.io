---
title: mongoDB 基础教程笔记
tags: [mongoDB]
keywords: mongoDB, 数据库
categories: mongoDB
---
![](http://upload-images.jianshu.io/upload_images/1969397-c05a921a1107f26a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!-- more -->
## 安装
从[mongoDB官网](http://www.mongodb.org/downloads) 下载 MongoDB 的最新版本,直接一路next，如果想自定义安装Choose Setup Type处选择Custon


## 创建数据目录
数据目录需要我们手动创建，这里我在F盘根目录创建了data，在data下面创建了db（命令行，手动都可以）

## 启动MOngoDB

在命令行中执行mongod.exe文件，（必须在你所安装的MongoDB目录下的bin目录内执行）
```
mongod.exe --dbpath F:\data\db
```
  ## 连接MongoDB
  在上一步启动过的前提下，双击MongoDB目录下bin目录中的mongo.exe就可以用mongoDB的shell连接数据库，其他种连接方式以后再实验

## 创建数据库
输入命令：
```
> use jsl
swiched to db jsl   # 输出信息
```
这时，就会创建出jsl命名的数据库

查看当前所在的数据库:
```
> db
jsl # 输出信息
```


查看数据库列表:
```
> show dbs
admin 0.000GB   # 输出信息
local 0.000GB   # 输出信息
```
这时，并看不到我们刚创建的jsl的数据库，这是因为个人创建的，空数据库是不会显示的

我们往这个数据库里放一些数据

```
> db.jsl.insert({"name":"jsl"})
WriteResult({ "nInserted":1 })  # 输出信息
```
再次查看数据库列表：
```
> show dbs
admin 0.000GB   # 输出信息
jsl   0.000GB   # 输出信息
local 0.000GB   # 输出信息

```
## 删除数据库

语法格式
```
db.dropDatabase()
```
先查看数据库：
```
> show dbs
admin 0.000GB   # 输出信息
jsl   0.000GB   # 输出信息  
local 0.000GB   # 输出信息
```
然后切换到jsl数据库中:
```
> use jsl
switched to db jsl  # 输出信息
```
执行删除命令:
```
> db.dropDatabase()
{ "dropped" : "jsl", "ok": 1 }
```
然后验证一下，是否删除成功：
```
> show dbs
admin 0.000GB  # 输出信息
local 0.000GB  # 输出信息
```
数据库列表只剩下两个，说明jsl数据库已经删除
### 删除集合
语法：
```
db.collection.drop()
```
重新再创建一个叫jsl的数据库，并且切换到jsl中，插入数据:
```
db.jsl.insert({"name": "jsl"})
```
查看集合：
```
> show tables
jsl
```
删除集合：
```
> db.jsl.drop()
true
```
再查看集合：
```
show tables

```
输出为空，说明删除成功


## 插入文档
所有存在集合中的数据都是BSON格式（BSON是 类json的一种二进制形式的存储格式，简称Binary JSON）
### 插入文档
MongoDB 使用 insert() 或 save() 方法向集合中插入文档，语法如下：
```
db.COLLECTION_NAME.insert(document)
```
#### 实例:
在jsl数据库中的col表中插入文档：
```
> db.col.insert(
    title: 'MongoDB ',
    description: 'MongoDB 是一个 Nosql 数据库'
})
```
col是集合名，如果集合名不存在，就会自动创建一个，并插入文档，执行下列命令查看是否插入文档：
```
> bd.col.find()
{ "_id" : ObjectId("56064886ade2f21f36b03134"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库" }   # 输出信息
```
还有另一种方式是一样的效果：将数据定义为一个变量，将变量插入到数据库
```
> document= {title: 'MongoDB 教程',
    description: 'MongoDB 是一个 Nosql 数据库'
};
```
然后执行插入操作：
```
> db.col.insert(document)
WriteResult({ "nInserted" : 1 })  # 输出信息
```

注：db.sol.save(document)命令也可以达到同样的效果，save()传 '_id'字段参数的话可以完成更新该 '_id'的数据。


## 更新文档

MongoDB 使用 update() 和 save() 方法来更新集合中的文档。接下来让我们详细来看下两个函数的应用及其区别。
### update()方法

**update()方法用于更新已存在的文档** ，语法格式如下：
```
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```
参数说明:
* **query**: update的查询条件
* **update**: update的对象和一些更新的操作符(如$,$inc)
* **upsert**: 可选,意思是如果不存在update的记录,是否插入objNew; 默认是false.
* **multi**: 可选,默认是false:只更新找到的第一条记录;如果参数为true,就是把所有查找到的记录全部更新
* **writeConcern**: 可选,抛出异常的级别.

#### 实例
在集合col中插入数据:
```
>db.col.insert({
    name: '张三',
    age: 20
})
```
然后用update()来更新name:
```
> db.col.update('name': '我是名字',{$set:{'name':'我是已更新的名字'}})
WriteResult({ "nMatched":1,"nUpserted":0,"nModified":1 })  # 输出信息
```
再次输入命令查看数据:
```
> db.col.find()

{ "_id" : ObjectId("5911725e0275fd608c69ed6a"), "name" : "我是已更新的名字" }  #输出信息
```
可以看得出,我们的名字已经被更新.
后面如果加参数,的格式如下
```
db.col.update('name': '我是名字',{$set:{'name':'我是已更新的名字'}}, {multi:true})
```

### save()方法
语法如下:
```
db.collection.save(
    <document>,
    {
        writeConcern: <document>
    }
)
```
参数说明:
* **document**: 文档数据.
* **writeConcern**: 可选,抛出异常的级别.



#### 实例
```
db.col.save({ "_id" : ObjectId("591192d80275fd608c69ed6b"), "name" : "我是来替换之前名字的名字", "age" : 20 })
```
