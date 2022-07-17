---
title: XML&XML Schema
date: 2021-10-30 18:18:25
categories: XML
tags:
---
## Types
* Structured data :   highly organized  DB(数据库)
* Unstructured data: with little or no internal organization Characters( text , PDF)
* Semi-structured data: partially organized XML , JSON


## Features
* Hierarchical Elements are nested in other elements (a tree structure).
* Open-Ended 动态性 We can add flexibly add new structure.
* Self-Describing 自描述性 Structure does not necessarily conform to an external description (may be schemaless)

## XML 
the eXtensible Markup Language 可扩展的标记语言

* MARKUP(annotate with tags <>) text data to indicate structure
* Extensible


## XML VS HTML
*  HTML has a fixed set of around ˜100tags.
* HTML tags mainly provide structure for the presentation of web pages,e.g.headings,paragraphs.
* HTML has a messy syntax based on SGML (Standard Generalised Markup Language) —  a complex precursor to XML.
* XML is extensible.
* XML tags can represent whatever you like, so can encode more useful structure.
* enforces strict syntax, so is easier to process.

## XML Schema

XML Schema 的作用是定义 XML 文档的合法构建模块，类似 DTD。

XML Schema:
- 定义可出现在文档中的元素
- 定义可出现在文档中的属性
- 定义哪个元素是子元素
- 定义子元素的次序
- 定义子元素的数目
- 定义元素是否为空，或者是否可包含文本
- 定义元素和属性的数据类型
- 定义元素和属性的默认值以及固定值

---

**举例**：

`xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`

xmlns:xsi 定义了一个命名空间前缀 xsi 对应的唯一字符串 `http://www.w3.org/2001/XMLSchema-instance`。
 
但是， 这个 xmlns:xsi 在不同的 xml 文档中似乎都会出现。 

这是因为， xsi 已经成为了一个业界默认的用于 XSD(（XML Schema Definition) 文件的命名空间。

那么，有了上述的理解，再来看：

`xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd"`

上面这行的语法其实是：

`xsi:schemaLocation = "键" "值"`

即 xsi 命名空间下 schemaLocation 元素的值为一个由空格分开的键值对。

前一个"键" `http://maven.apache.org/POM/4.0.0` 指代 【命名空间】， 只是一个全局唯一字符串而已。

后一个值指代 【XSD location URI】 , 这个值指示了前一个命名空间所对应的 XSD 文件的位置， xml parser 可以利用这个信息获取到 XSD 文件， 从而通过 XSD 文件对所有属于 命名空间 `http://maven.apache.org/POM/4.0.0` 的元素结构进行校验， 因此这个值必然是可以访问的， 且访问到的内容是一个 XSD 文件的内容。


## XSD 简易元素

定义简易元素的语法：

`<xs:element name="xxx" type="yyy"/>`

此处 xxx 指元素的名称，yyy 指元素的数据类型。XML Schema 拥有很多内建的数据类型。

最常用的类型是：
- xs:string
- xs:decimal
- xs:integer
- xs:boolean
- xs:date
- xs:time