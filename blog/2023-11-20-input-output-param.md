---
slug: input-output-param
title: C语言输入参数与输出参数
authors: [xiaotupo]
tags: [C语言, 输入输出参数]
---

下面例子中 `fun1()` 函数中的 `a` 为输入型参数，`b` 为输入型参数；传值参数为输入型参数，传地址则可能为输入型参数也可能为输出型参数，如果不修改传地址参数的值则可以用 `const` 修饰。

<!-- truncate -->

```c
#include <stdio.h>

void fun1(int a, int *b)
{
    printf("a: %d\n", a);
    *b = 10;
}

int main(void)
{
   int num1 = 100;
   int num2 = 0;
   fun1(num1, &num2);
   printf("num2: %d\n", num2);
    return 0;
}
```