---
title: C++智能指针
date: 2021-7-30 20:05:18
categories: C++
tags:
---

## 智能指针的作用（使用原因）

智能指针主要解决一个内存泄露的问题，它可以自动地释放内存空间。因为它本身是一个类，当函数结束的时候会调用析构函数，并由析构函数释放内存空间。

## 四种智能指针

### unique_ptr

实现独占式拥有或严格拥有概念，保证同一时间内只有一个智能指针可以指向该对象。不能拷贝构造，但是可以移动构造和移动赋值。

```c++
//移动赋值
unique_ptr<Son> p1(new Son());
unique_ptr<Son> p2 = (std::move(p1));
```

### shared_ptr 

多个智能指针可以指向相同对象，当最后一个引用销毁时，释放内存空间。

**原理**：
使用引用计数，每当引用一次，引用计数加一，每当智能指针销毁了，引用计数就减一，当引用计数减少到0的时候就释放引用的对象。

这种引用计数的增减发生在智能指针的构造函数，拷贝构造函数，赋值操作符，析构函数中。

**成员函数**：
```
use_count 返回引用计数的个数
unique 返回是否是独占所有权( use_count 为 1)
swap 交换两个 shared_ptr 对象(即交换所拥有的对象)
reset 放弃内部对象的所有权或拥有对象的变更, 会引起原有对象的引用计数的减少
```

```c++
shared_ptr< Obj> p1(new Obj());
shared_ptr< Obj> p2 = p1;
shared_ptr< Obj> p3(p1);
p2.reset();
cout << p1.use_count() << endl;
```

### weak_ptr

用来解决shared_ptr相互引用时的死锁问题，因为shared_ptr是一种强引用的关系，智能指针直接引用对象，可能引起循环引用，从而造成内存泄漏。

解决这种状况的办法就是将两个类中的一个成员变量改为weak_ptr对象，因为weak_ptr不会增加引用计数，使得引用形不成环，最后就可以正常的释放内部的对象，不会造成内存泄漏。weak_ptr从字面意思上可以看出是一个弱指针，不是说明这个指针的能力比较弱，而是说他对他所引用的对象的所有权比较弱。

### auto_ptr (c++11已弃用)
```c++
auto_ptr< Obj> p1 (new Obj());
auto_ptr< Obj> p2;
p2 = p1;
```

此时再调用 p1就会异常，因为 auto_ptr的拷贝构造函数中把真实引用的内存指针进行的转移，也就是说 p2应引用了内存地址，而 p1引用的内存地址为空。

参考：[stl中auto_ptr,unique_ptr,shared_ptr,weak_ptr四种智能指针使用总结](https://blog.csdn.net/zsc_976529378/article/details/52250597)


## 代码

```c++
#include <iostream>
#include <string>
#include <memory>

class Entity {
public: 
    Entity() {
        std::cout << "Created Entity!" << std::endl;
    }

    ~Entity() {
        std::cout << "Destroyed Entity!" << std::endl;
    }
};

int main()
{
    {
        std::shared_ptr<Entity> e0;
        {
            std::shared_ptr<Entity> sharedEntity = std::make_shared<Entity>();
            e0 = sharedEntity;
        }
        //此时e0还未销毁
    }//当这个作用域结束时e0销毁，引用计数为0，才会调用Entity析构函数
}


```