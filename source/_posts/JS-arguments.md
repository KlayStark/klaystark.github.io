---
title: JS arguments详解
date: 2019-11-09 20:58:04
tags:
---
## 引入

形参：函数定义的参数。
实参：函数调用时实际传递的参数。
参数匹配是从左向右进行匹配。如果实参个数小于形参，后面的参数对应赋值undefined。
实参的个数如果多于形参，可以通过arguments访问。
函数对象的length属性就是函数形参的个数。
	
<!--more-->
## 简介
	
`arguments`对象是所有（非箭头）函数中都可用的局部变量。
你可以使用arguments对象在函数中引用函数的参数。
此对象包含传递给函数的每个参数，第一个参数在索引0处。
例如，如果一个函数传递了三个参数，你可以以如下方式引用他们：
```javascript
arguments[0]
arguments[1]
arguments[2]
```

JS没有重载函数，但是Arguments对象能够模拟重载。
JS中每个函数都会有一个Arguments对象实例arguments，它引用函数的实参，可用数组下标[]的方式引用arguments的元素。
arguments.length为函数实参个数，arguments.callee引用函数自身。

```javascript
function myFunction(){
    var x = "",i,y=document.getElementById("demo");
    for(i=0;i<arguments.length;i++){
        x += arguments[i] +",";
        y.innerHTML = x;
    }
}
myFunction(2,3,3,5);
//输出2，3，3，5
```
	
1 arguments的访问就像Array对象一样，用0到arguments.length-1来枚举每一个元素 
2 arguments对象不是一个 Array 。它类似于Array，但除了length属性和索引元素之外没有任何Array属性。
