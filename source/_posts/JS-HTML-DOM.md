---
title: JS HTML DOM
date: 2019-11-08 12:40:04
tags:
---
## 事件传递
有两种方式：冒泡与捕获。

事件传递定义了元素事件触发的顺序。 如果你将 <p> 元素插入到 <div> 元素中，用户点击 <p> 元素, 哪个元素的 "click" 事件先被触发呢？

在 冒泡 中，内部元素的事件会先被触发，然后再触发外部元素，即： <p> 元素的点击事件先触发，然后会触发 <div> 元素的点击事件。

在 捕获 中，外部元素的事件会先被触发，然后才会触发内部元素的事件，即： <div> 元素的点击事件先触发 ，然后再触发 <p> 元素的点击事件。

addEventListener() 方法可以指定 "useCapture" 参数来设置传递类型：

addEventListener(event, function, useCapture);

默认值为 false, 即冒泡传递，当值为 true 时, 事件使用捕获传递。

---

Internet Explorer 8 及更早版本不支持 addEventListener() 方法。

跨浏览器解决方案：

    var x = document.getElementById("myBtn");
    if (x.addEventListener) {                    // 针对主流浏览器，除了 IE 8 及更正版本
        x.addEventListener("click", myFunction);
    } else if (x.attachEvent) {                  // 针对 IE 8 及更早版本
        x.attachEvent("onclick", myFunction);
    } 

---

用以下节点属性在节点之间

导航：

* parentNode
* childNodes[nodenumber]
* firstChild
* lastChild
* nextSibling
* previousSibling

---

    <title id = "demo">DOM 教程 </title>
元素节点不包含文本。
它包含了值为"DOM教程"的文本节点。

文本节点的值能够通过节点的 innerHTML 属性进行访问：
var myTitle = document.getElementById("demo").innerHTML;

访问innerHTML属性等同于访问首个子节点的nodeValue：
var myTiltle = document.getElementById("demo").firstChild.nodeValue;

也可以这样访问第一个子节点：
var myTitle =  document.getElementById("demo").childNodes[0].nodeValue; 