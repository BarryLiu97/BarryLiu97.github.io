---
title: (C\C++) auto
top: true
cover: false
toc: true
mathjax: true
summary: 关键字的用法
categories: 算法
tags:
  - C\C++
abbrlink: 13803
date: 2020-12-26 16:29:08
img:
---

## auto before C++0x

> 在C++0x之前，`auto`关键字的意义与static相对，是指自动存储的，写不写的含义都是一样的，这就导致了`auto`关键字非常的鸡肋；
>
> **PS**: auto关键字原来的含义（表示local变量）是多余而无用的——标准委员会的成员们在数百万行代码中仅仅只找到几百个用到auto关键字的地方，并且大多数出现在测试代码中，有的甚至就是一个bug。

## auto的使用方法

> C++11 赋予 auto 关键字新的含义，使用它来做自动类型推导。也就是说，使用了 auto 关键字以后，编译器会在编译期间自动推导出变量的类型，这样我们就不用手动指明变量的数据类型了。
>
> **NOTE**:`auto`类型是在<font color = red>***编译期间***</font>由编译器推导的

```cpp
auto name = value;
```

例如：

```cpp
auto n = 10;
auto f = 12.8;
auto p = &n;
auto url = "http://c.biancheng.net/cplus/";
```

下面我们来解释一下：

- 第 1 行中，10 是一个整数，默认是 int 类型，所以推导出变量 n 的类型是 int。
- 第 2 行中，12.8 是一个小数，默认是 double 类型，所以推导出变量 f 的类型是 double。
- 第 3 行中，&n 的结果是一个 int* 类型的指针，所以推导出变量 f 的类型是 int*。
- 第 4 行中，由双引号`""`包围起来的字符串是 const char* 类型，所以推导出变量 url 的类型是 const char*，也即一个常量指针。

接下来，我们再来看一下 auto 和 const 的结合：

```cpp
int  x = 0;
const  auto n = x;  //n 为 const int ，auto 被推导为 int
auto f = n;      //f 为 const int，auto 被推导为 int（const 属性被抛弃）
const auto &r1 = x;  //r1 为 const int& 类型，auto 被推导为 int
auto &r2 = r1;  //r1 为 const int& 类型，auto 被推导为 const int 类型
```

最后我们来简单总结一下 auto 与 const 结合的用法：

- 当类型不为引用时，auto 的推导结果将不保留表达式的 const 属性；
- 当类型为引用时，auto 的推导结果将保留表达式的 const 属性。

## auto 的限制

前面介绍推导规则的时候我们说过，使用 auto 的时候必须对变量进行初始化，这是 auto 的限制之一。那么，除此以外，auto 还有哪些其它的限制呢？

1. auto 不能在函数的参数中使用。

   这个应该很容易理解，我们在定义函数的时候只是对参数进行了声明，指明了参数的类型，但并没有给它赋值，只有在实际调用函数的时候才会给参数赋值；而 auto 要求必须对变量进行初始化，所以这是矛盾的。

2. auto 不能作用于类的非静态成员变量（也就是没有 static 关键字修饰的成员变量）中。

3. auto 关键字不能定义数组，比如下面的例子就是错误的：

   ```cpp
   char url[] = "http://c.biancheng.net/";
   auto  str[] = url;  //arr 为数组，所以不能使用 auto
   auto temp = url;  // auto被转化为int*
   for(auto item: temp)  // error, because temp is not a array any more.
   {
       // ...
   }
   ```

   

