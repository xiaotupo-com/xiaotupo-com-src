---
sidebar_position: 7
description: C语言中函数返回字符串的方法有四种：将字符串指针作为函数参数传入，并返回该指针。使用 malloc 函数动态分配内存,注意在主调函数中释放。返回一个静态局部变量。使用全局变量。
---

`C`语言中函数返回字符串的方法有四种：

1. 将字符串指针作为函数参数传入，并返回该指针。
2. 使用 `malloc` 函数动态分配内存，注意在主调函数中释放。
3. 返回一个静态局部变量。
4. 使用全局变量。

下面是这四种方法的详细解释：

## 将字符串指针作为函数参数传入，并返回该指针

将字符串指针作为函数参数传入，并返回该指针。典型的 `strcpy()` 函数应该就是采用的这种方法，第一个参数为指向目的字符串的指针，返回值也为这个指针。

```c
char * strcpy ( char * des, const char * source) {
    char * r= des;
    assert ( (des != NULL) && (source != NULL));
    while ( (*r++ = *source++)!= '\\0');
    return des;
}
```

## 使用 `malloc` 函数动态分配内存

使用 `malloc` 函数动态分配，但是一定要注意在主调函数中将其释放，应为 `malloc` 动态分配的内存位于堆区，而堆区的内存是要程序员自己释放的。

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

char* return_string(int a, int b)
{
    char* m = (char*)malloc(sizeof(char) * 20);
    sprintf(m, "%d+%d=%d", a, b, a + b);
    return m;
}

void function_return_string(void)
{
    char* str = return_string(12, 34);
    printf("%s\n", str);
    free(str);
}

int main(void)
{
    printf("=================== 开始测试 ===================\n");
    function_return_string();
    printf("=================== 结束测试 ===================\n");
}

```

输出：

```bash
=================== 开始测试 ===================
12+34=46
=================== 结束测试 ===================
```



## 返回一个静态局部变量。

```c
char * retstring () {
    static char name [ 10];
    strcpy (name,"张汉青");
    return name;
}
```

这种方法有一个问题：由于采用了静态局部变量（位于静态区，程序结束时由系统进行释放），这就导致，如果多次调用这个函数，下一次调用会将上一次调用的结果覆盖掉。`C`语言中的库函数，`tmpnam()` 函数、`getenv()` 函数等应该都是采用的这种方法，这也就是为什么，使用这样的函数的时候应该立即将返回结果拷贝一份的原因。

## 使用全局变量。

```c
char g_s [ 100];
char * fun () {
    strcpy (g_s, "abc ");
    return g_s;
}
```

希望这可以帮助您理解 C 语言中函数返回字符串的方法。

该文来自必应聊天，但代码部分自己做了些修改。

