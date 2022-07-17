---
title: C++类型转换
date: 2021-7-20 23:05:12
categories: C++
tags:
---

## 隐式类型转换

对于内置类型，低精度的变量给高精度变量赋值会发生隐式类型转换。

对于只存在单个参数的构造函数的对象构造来说（并不是指构造函数只能有一个形参，而是它可以有多个形参，但那些形参都是有默认实参的），函数调用可以直接使用该参数传入，编译器会自动调用其构造函数生成临时对象。

```c++
class A{
    A(int f, int d = 0){}
};
int main(){
    A a = 10;
}
```

关键字**explicit**：标明类的构造函数是显式的，不能进行隐式转换。


## 四种类型转换关键字

### const_cast

用于将const指针、引用、对象转为非const。

```c++
const int a = 1;
const int* b = &a;
cout << *b << endl;
int* c = const_cast<int*>(b);
*c = 10;
cout << *b << endl;
```

### static_cast

隐式类型转换，可以实现C++中内置基本数据类型之间的相互转换，enum、struct、 int、char、float等，能进行类层次间的向上类型转换和向下类型转换（向下不安全，因为没有进行动态类型检查）。它不能进行无关类型(如非基类和子类)指针之间的转换，也不能作用包含底层const的对象。

### dynamic_cast

动态类型转换，用于将基类的指针或引用安全地转换成派生类的指针或引用（也可以向上转换），若**指针转换失败返回NULL**，若**引用返回失败抛出bad_cast异常**。只能用于含有虚函数的类（因为要通过虚函数表判断继承关系）。

```c++
Son *a;
Fa* aa = dynamic_cast<Fa*>(a);  //向上转型
```

### reinterpret_cast

在非相关的类型之间转换。

可以转化任何内置的数据类型为其他任何的数据类型，也可以转化任何指针类型为其他的类型。它甚至可以转化内置的数据类型为指针，无须考虑类型安全或者常量的情形。

```c++
class A {};
class B {};
A * a = new A;
B * b = reinterpret_cast<B *>(a);
```

*参考：[c/c++强制类型转换](https://www.cnblogs.com/yzl050819/p/6593850.html)*

## static_cast和dynamic_cast的异同点

二者都会做类型安全检查，只是static_cast在编译期进行类型检查，dynamic_cast在运行期进行类型检查。后者需要父类具备虚函数，而前者不需要。