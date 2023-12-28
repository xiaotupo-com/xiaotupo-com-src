---
sidebar_position: 6
description: C语言中的回调函数是指在函数调用时将另一个函数作为参数传递给它，从而在合适的时候调用该函数。回调函数的声明形式如下：
---

C语言中的回调函数是指在函数调用时将另一个函数作为参数传递给它，从而在合适的时候调用该函数。回调函数的声明形式如下：

```bash
返回类型 (*函数名)(参数列表);
```

其中，`*`表示函数名是一个指针，括号内的参数列表是回调函数的参数列表。例如，下面是一个回调函数的声明：

`int (*callback)(int, int);`

这个回调函数接受两个整数作为参数，并返回一个整数。在调用函数时，可以将该回调函数作为参数传递给它，例如：

```c
int add(int a, int b) {
    return a + b;
}

int multiply(int a, int b) {
    return a * b;
}

int calculate(int a, int b, int (*callback)(int, int)) {
    return callback(a, b);
}

int main() {
    int a = 10, b = 20;
    printf("Addition: %d\n", calculate(a, b, add));
    printf("Multiplication: %d\n", calculate(a, b, multiply));
    return 0;
}
```

在上面的示例中，`calculate` 函数接受两个整数和一个回调函数作为参数，并在适当的时候调用该回调函数。在 `main` 函数中，我们定义了两个回调函数 `add` 和 `multiply`，并将它们作为参数传递给 `calculate` 函数。输出结果如下：

`Addition: 30`
`Multiplication: 200`

希望这可以帮助您理解 `C` 语言中回调函数的语法格式。

该文来自必应聊天。
