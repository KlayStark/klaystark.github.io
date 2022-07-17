---
title: C++运算符及其重载
date: 2021-8-05 20:15:12
categories: C++
tags:
---

运算符就是函数。

::双冒号作用域运算符

::v1 //直接引用全局变量

三目运算符：
```c++
std::string rank = s_Level > 10 ? "Master" : "Beginner"
```

箭头运算符：
```c++
Entity e;
//e.Print();
Entity* ptr = &e;
(*ptr).Print();//解引用
ptr->Print();
```

## 运算符重载
上代码。
```c++
#include <iostream>

struct Vector2 {
	float x, y;

	Vector2(float x, float y)
		:x(x),y(y){}

	Vector2 Add(const Vector2& other) const {
		return Vector2(x + other.x, y + other.y);
	}
	//重载+
	Vector2 operator+(const Vector2& other) const {
		return Add(other);
	}

	Vector2 Multiply(const Vector2& other) const {
		return Vector2(x * other.x, y * other.y);
	}
	//重载*
	Vector2 operator*(const Vector2& other) const {
		return Multiply(other);
	}

	//重载==与!=
	bool operator==(const Vector2& other) const{
		return x == other.x && y == other.y;
	}

	bool operator!=(const Vector2& other) const {
		return !(*this == other);
	}
};

//重载<<运算符
std::ostream& operator<<(std::ostream& stream, const Vector2& other) {
	stream << other.x << "," << other.y;
	return stream;
}

void Print(Vector2 v) {
		std::cout << "[" << v.x << "," << v.y << "]" << std::endl;
	}

int main() {
	Vector2 position(3.0f, 3.0f);
	Vector2 speed(0.5f, 1.0f);
	Vector2 powerup(3.5f, 4.5f);

	Vector2 result1 = position.Add(speed.Multiply(powerup));
	Vector2 result2 = position + speed * powerup;

	Print(result1);
	Print(result2);

	//重载<<运算符过后可对 Vector2 类型直接打印
	std::cout << result1 << std::endl;

	std::cout << (result1 == result2) << std::endl;
	std::cout << (result1 != result2) << std::endl;

}
```

一般地，赋值运算符重载函数的参数是函数所在类的const类型的引用。

加const是因为：

①我们不希望在这个函数中对用来进行赋值的“原版”做任何修改。

②加上const，对于const的和非const的实参，函数就能接受；如果不加，就只能接受非const的实参。

用引用是因为：

这样可以避免在函数调用时对实参的一次拷贝，提高了效率。