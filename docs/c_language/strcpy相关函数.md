---
sidebar_position: 4
---

在 `C` 语言中我们不能直接对 `char[]` 数组复制，要给字符数组赋值我们就需要用 `strcpy()` 系列的函数。

```c
char name[10]; // 定义一个字符数组
name = "hello,world!"; // 该行是错误的语法，C 语言不允许这样操作
```

## strcpy() 

函数原型：
`char *strcpy (char *__restrict __dest, const char *__restrict __src)`

我们可以用 `strcpy()`来给字符数组（字符串）赋值：
```c
void string_test(void)
{
    char str_1[100];
    memset(str_1, 0, sizeof(str_1));
    printf("%s\n", strcpy(str_1, "Hello,World!"));
}
```

输出：`Hello,World!`
:::tip
要注意 `strcpy()`函数的第二个参数的长度，不能大于我们定义的容器数组的大小。
另外在我们定义好数组后，最好进行初始化一下，否则数组中可以会有随机数据。
:::

## strncpy()

`strncpy()` 比 `strcpy()` 多了一个参数` n` ，`n` 指定了从第二个参数中复制指定个数的数据到第一个参数的数组中。

```c
void string_test(void)
{
    char str_1[100];
    memset(str_1, 0, sizeof(str_1));
    printf("%s\n", strncpy(str_1, "Hello,World", 5));
}
```

输出：`Hello`

## strcmp()

函数原型：
`int strcmp(const char *str1, const char *str2)`

`strcmp()` 函数的作用是判断两个字符串是否相等，返回结果为`int` 类型，返回状态：

1. 如果返回值小于`0`，则表示 `str1` 小于 `str2`。
2. 如果返回值大于 `0`，则表示 `str1` 大于 `str2`。
3. 如果返回值等于 `0`，则表示 `str1` 等于 `str2`。

```c
void strcmp_test(void)
{
    char* name = "zhangsan";
    if(strcmp(name, "zhangsa") == 0)
    {
        printf("两个字符串相等\n");
    }
    else if(strcmp(name, "zhangsan") < 0)
    {
        printf("name < 'zhangsan' \n");
    }
    else {
        printf("name > 'zhangsan' \n");
    }
}
```

## strcat()

函数原型：`char *strcat(char *dest, const char *src)`

函数作用：把 `src` 中的内容追加到 `dest` 里边。

```c
void strcat_test(void)
{
    char name[100];
    memset(name, 0, sizeof(name)); // 初始化 name

    strcat(name, "hello,"); // 项 name 中追加 "hello"字符串
    printf("%s\n", name);
    strcat(name, "world!");// 项 name 中追加 "world!"字符串
    printf("%s\n", name);
}
```

输出：

```bash
hello,
hello,world!
```

