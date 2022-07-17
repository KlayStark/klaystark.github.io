---
title: MongoDB简介
date: 2021-12-08 18:09:50
categories: MongoDB
tags:
---
## 简介 

*转自[Github](https://github.com/qianjiahao/MongoDB/wiki)*

MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。

MongoDB是面向文档的数据库，不是关系型数据库。

## 特点

- 它将原来 **行（row）** 的概念换成了更加灵活的**文档（document）**模型。

- 面向文档的方式可以将文档和数组内嵌进来，所以用一条记录就可以表示很复杂的层次关系。 

- MongoDB没有模式，文档的键不会事先定义也不会固定不变。

- MongoDB所采用的面向文档的数据模型，使其可以自动的在多台服务器之间分割数据，还可以平衡集群的数据和负载，自动重排文档。

- 管理简便：MongoDB的管理理念就是尽可能的让服务器自动配置，让用户能在需要的时候调整设置。

## 概念/术语解析

### 文档

文档是一组键值(key-value)对(即 BSON)。

文档是MondoDB的核心概念，多个键及其关联的值有序的存放在一起便是文档。可以非常类似关系型数据库里的“行”。

在JavaScript里，文档对象通常长这个样子：
>{"greeting":"Hello world"}
* greeting(**key**)/Hello world(**value**)

在MongoDB里可能会长这样：
>{"greeting":"Hello world","foo":3}
{"foo":"3","greeting":"hello world"}

需要注意的是：

- 文档中的键/值对是有序的。
- 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)。
- MongoDB区分类型和大小写。
- MongoDB的文档不能有重复的键。
- 文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符。

### 集合

集合就是 MongoDB 文档组，类似于 RDBMS （关系数据库管理系统：Relational Database Management System)中的表格。

集合存在于数据库中，集合没有固定的结构，这意味着你在对集合可以插入不同格式和类型的数据，

但通常情况下我们插入集合的数据都会有一定的关联性。

### 数据库

一个mongodb中可以建立多个数据库。

MongoDB的默认数据库为"db"，该数据库存储在data目录中。

MongoDB的单个实例可以容纳多个独立的数据库，每一个都有自己的集合和权限，不同的数据库也放置在不同的文件中。

`show dbs` 命令可以显示所有数据的列表。

## 配置、启动

* 第一步：登上[MongoDB官网](http://www.mongodb.org/)，找到自己的适合的版本下载
* 第二步：解压（免安装），改名mongodb（举例命名，可以任个人喜好），放在你喜欢的位置（任喜好）
* 第三步：通过命令行:
  *  cd mongodb(进入mongodb目录)
  *  cd bin（进入bin目录）
  *  ./mongod(运行启动命令)

### 常见问题

*  mongodb默认的数据目录为/data/db，如果这个目录**不存在**或者**不可写**，服务器会启动失败
  *  解决方案：mkdir -p /data/db，手动创建目录，并确保有**写**权利
*  还有可能27017端口被占用，什么意思呢？就是你已经启动了./mongod了，没有关闭，所以端口占用了，因为mongodb的默认端口为27017
  *  解决方案：另打开命令行，输入ps -A，查看./mongod的PID（进程号），找到后输入 kill -15 PID。
*  还有可能是需要在sudo下才能执行
  *  依然要再bin目录下，输入sudo ./mongod


---

目录/bin -- mongod启动数据库服务

mongo 启动数据库进程 进行操作

## 常用命令

use klay - 切换至klay数据库（如没有则创建klay数据库）

show dbs - 查看所有数据库

```
> db.klay.insert({"name":"Klay"})
WriteResult({ "nInserted" : 1 })
```

### 创建集合

>创建集合(数据表)后要再插入一个文档(记录)，集合才会真正创建。

`db.dropDatabase() `删除数据库

`db.createCollection("klay")` 先创建集合

`show collections` 显示集合

`db.runoob.drop()` 删除集合

在 MongoDB 中，你不需要创建集合。当你插入一些文档时，MongoDB 会自动创建集合。

`> db.mycol2.insert({"name" : "克莱"})`



### 插入文档

`db.collection_name.insert()`

`db.collection.insertOne() `用于向集合插入一个新文档，语法格式如下：
```
db.collection.insertOne(
   <document>,
   {
      writeConcern: <document>
   }
)
```

`db.collection.insertMany() `用于向集合插入一个多个文档，语法格式如下：
```
db.collection.insertMany(
   [ <document 1> , <document 2>, ... ],
   {
      writeConcern: <document>,
      ordered: <boolean>
   }
)
```

参数说明：
* document：要写入的文档。
* writeConcern：写入策略，默认为 1，即要求确认写操作，0 是不要求。
* ordered：指定是否按顺序写入，默认 true，按顺序写入。


### 查询文档
`db.collection_name.find()`

易读：`db.collection_name.find().pretty()`

以下实例演示了 AND 和 OR 联合使用，类似常规 SQL 语句为： 

`'where likes>50 AND (by = '菜鸟教程' OR title = 'MongoDB 教程')'`

`>db.col.find({"likes": {$gt:50}, $or: [{"by": "菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()`

输出：
```
{
        "_id" : ObjectId("56063f17ade2f21f36b03133"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "菜鸟教程",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}
```


### 更新文档

`db.klay.update({'age':22},{$set:{'age':23}})`

如果数据不存在需要插入，设置 upsert:true

`db.klay.update({'age':22},{$set:{'age':23}}, {update:true})`

### 删除文档

如删除集合下全部文档：

`db.inventory.deleteMany({})`

删除 status 等于 A 的全部文档：

`db.inventory.deleteMany({ status : "A" })`

删除 status 等于 D 的一个文档：

`db.inventory.deleteOne( { status: "D" } )`