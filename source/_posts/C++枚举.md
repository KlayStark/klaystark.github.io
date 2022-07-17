---
title: C++枚举
date: 2021-6-30 14:05:18
categories: C++
tags:
---

## 枚举Enum

你有一个数值集合，你想用数字来表示他们。


默认是从0开始的。

例子：

```c++
enum Example
{
    A, B, C      //这里可以不指定值，他会默认为0，1，2
};

enum Example1
{
    A1 = 5, B2 = 7, C3      //这里也可以指定值，他会按照你给定的值递增
};

int main()
{

    Example value = B;   //给value分配值，实际上只能分配枚举里面的值
    if (value == 1)  //而这里value也就是B在枚举中是1，因为他是从0开始递增的，A是0
    {
        std::cout << "B=" << value << std::endl;
    }
    Example1 value1 = C3;
    if (value1 == 8)
    {
        std::cout << "C3=" << value1 << std::endl;
    }
    std::cin.get();
    return 0;
}
```