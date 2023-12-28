---
sidebar_position: 3
title: C++ 内置函数笔记
---

在此记录一些常用的 C++ 内置函数。

## typeid(expression)

`typeid` 是 `C++` 中的关键字和 `sizeof` 类似，
```cpp
typeid(expression)
```

这个操作会返回一个定义在`<typeinfo>`里面的`const`对象，这个对象可以同其他用`typeid`获取的`const`对象进行`==`或者`!=`操作，也可以用过`.name()`来获取一个表示类型名或者是类名的以空字符结尾的字符串。例如：

```cpp
void test4(void)
{
    int * a,b;
    a = nullptr;
    b = 0;

    if (typeid(a) != typeid(b))
    {
        std::cout << "a is: " << typeid(a).name() << std::endl;
        std::cout << "b is: " << typeid(b).name() << std::endl;
    }
}
```


