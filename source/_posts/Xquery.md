---
title: Xquery
date: 2021-11-10 15:04:25
categories: XML
tags:
---
## 简介 

---

COURSEWORK XML AND STRUCTURED INFORMATION 作业满分纪念

---

XQuery 相对于 XML 的关系，等同于 SQL 相对于数据库表的关系。

## FLWOR 

是 "For, Let, Where, Order by, Return" 的只取首字母缩写。

举例：

```xquery
for $x in doc("books.xml")/bookstore/book
where $x/price>30
order by $x/title
return $x/title
```

for 语句把 bookstore 元素下的所有 book 元素提取到名为 $x 的变量中。

where 语句选取了 price 元素值大于 30 的 book 元素。

order by 语句定义了排序次序。将根据 title 元素进行排序。

return 语句规定返回什么内容。在此返回的是 title 元素。

## 七种节点

元素、属性、文本、命名空间、处理指令、注释、以及文档（根）节点。

XML 文档是被作为节点树来对待的。树的根被称为文档节点或者根节点。

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<bookstore>
<book>
  <title lang="en">Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>
</bookstore>
```

    <bookstore> (文档节点)

    <author>J K. Rowling</author> (元素节点)

    lang="en" (属性节点)

## 语法规则

* XQuery 对大小写敏感
* XQuery 的元素、属性以及变量必须是合法的 XML 名称。
* XQuery 字符串值可使用单引号或双引号。
* XQuery 变量由 "$" 并跟随一个名称来进行定义，举例，$bookstore
* XQuery 注释被 (: 和 :) 分割，例如，(: XQuery 注释 :)

## for 

for 语句可将变量捆绑到由 in 表达式返回的每个项目。for 语句可产生迭代。

在同一个 FLWOR 表达式中可存在多重 for 语句。

如需在一个 for 语句中进行指定次数地循环，您可使用关键词 to ：

```xquery
for $x in (1 to 5)
return <test>{$x}</test>
```

## let

let 语句可完成变量分配，并可避免多次重复相同的表达式。

let 语句不会导致迭代。

```xquery
let $x := (1 to 5)
return <test>{$x}</test>
```