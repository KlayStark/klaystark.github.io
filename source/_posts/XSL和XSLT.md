---
title: XSL和XSLT
date: 2021-11-5 20:09:25
categories: XML
tags:
---
## XSL 

指扩展样式表语言（EXtensible Stylesheet Language）, 它是一个 XML 文档的样式表语言。

## XSLT 

指 XSL 转换（XSL Transformations）

### 元素

`<xsl : template> `元素用于构建模板

`<xsl:apply-templates> `元素可向当前元素或当前元素的子节点应用模板。

### Namespace 命名空间

使用前缀来避免命名冲突: Use prefixes to avoid naming conflicts

当在 XML 中使用前缀时，一个所谓的用于前缀的命名空间必须被定义。

命名空间是在元素的开始标签的 xmlns 属性中定义的。

For example, we always begin XSLT stylesheets by identifying the x s l prefix: 

`<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"`

## Xpath

XPath 使用路径表达式来选取 XML 文档中的节点或节点集。

`<xsl:copy> `copy element, attribute or text nodes

`<xsl:copy-of> `copy element, attribute or text nodes with content and attributes

## For-each和template的区别

使用 xsl:for-each 和 xsl:template 的最大区别在于一个是迭代器（或循环）函数，而另一个是递归函数。

从本质上讲，这意味着它们的处理方式存在根本差异。

使用 for-each 时，与 select 属性匹配的元素一次循环通过一个，并且针对该元素处理 for-each 循环的开始和结束标记之间的指令。

当调用 xsl:apply-templates 时，当前上下文中与模板规则匹配的每个元素都作为节点提交给模板规则。

然后，模板中的所有指令都针对该节点进行处理。