---
title: JS快速笔记
date: 2019-11-06 15:30:50
tags:
---

### 请勿使用 new Object()
    var x1 = {};           // 新对象
    var x2 = "";           // 新的原始字符串值
    var x3 = 0;            // 新的原始数值
    var x4 = false;        // 新的原始布尔值
    var x5 = [];           // 新的数组对象
    var x6 = /()/;         // 新的正则表达式
    var x7 = function(){}; // 新的函数对象

向未声明的变量赋值，此变量会自动成为全局变量。

    MYFunction();
        function myFunction(){
        carName="BMW";//全局变量
    }

### JS  Hoisting
将所有声明提升到当前作用域（当前脚本或当前函数）顶部。

let和const声明的变量和常量不会被提升。

初始化不会被提升。
Ex: 初始化：var x = 5;  
     声明   ：   x = 5;

严格模式中的 JavaScript 不允许在未被声明的情况下使用变量。

### 减少DOM访问：

如果期望访问某个DOM元素若干次，那么只访问一次，并把它作为本地变量来使用。

    var obj;
    obj = getElementById("demo");
    obj.innerHTML = "Hello";

### call() 和 apply() 之间的区别

不同之处是：
call() 方法分别接受参数。
apply() 方法接受数组形式的参数。
如果要使用数组而不是参数列表，则 apply() 方法非常方便。

    var y = person.fullProfile.call(player2,"Lakers","USA");
    //------------------------.apply(player2,["lakers","USA"]);


区分apply,call就一句话:

    foo.call(this, arg1,arg2,arg3) == foo.apply(this, arguments)==this.foo(arg1, arg2, arg3)

来自 <https://blog.csdn.net/disiwei1012/article/details/51787870> 


### JavaScript 使用 32 位按位运算数

JavaScript 将数字存储为 64 位浮点数，但所有按位运算都以 32 位二进制数执行。

在执行位运算之前，JavaScript 将数字转换为 32 位有符号整数。

执行按位操作后，结果将转换回 64 位 JavaScript 数。

上面的例子使用 4 位无符号二进制数。所以 ~ 5 返回 10。

由于 JavaScript 使用 32 位有符号整数，JavaScript 将返回 -6。

00000000000000000000000000000101 (5)

11111111111111111111111111111010 (~5 = -6)

有符号整数使用最左边的位作为减号。