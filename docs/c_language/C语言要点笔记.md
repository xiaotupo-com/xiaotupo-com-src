---
sidebar_position: 2
---

该笔记主要记录一些 **C** 语言中的重要要点，比如：**数组**、**指针**、**枚举**、**结构体**等内容。

## 数组

数组是 `C` 语言中使用频率最高的数据结构，所以必须掌握数组相关的使用。

### 数组初始化

C 中数组有3中初始化方式：

1. 大括号初始化 `{0}`，但是有些编译器不支持。
2. `memset() `初始化，平台一致，推荐使用该方式。
3. `for`循环初始化，效率低下

数组如果不执行初始化动作，那么数组中的内容将是随机的，所以需要执行初始化。

在数组初始化时推荐使用 `memset()` 函数的方式，使用该函数需要包含 `string.h` 头文件。

```c
int main(void)
{
    uint8_t OLED_BUFFER[OLED_BUFFER_SIZE];
    memset(OLED_BUFFER, 8, OLED_BUFFER_SIZE);
    print_all();
}
```

### 指向数组的指针

数组的名字其实是数组中第一个值的地址，那么指向数组的指针就是指向数组第一个元素的指针。我们可以通过多种方式通过指向数组的指针来操作数组，下面列出测试代码：

```c
#include <stdio.h>
#include <string.h>

typedef unsigned char u8;
typedef unsigned int u32;

#define OUT_BR()	printf("\n")

int main(void)
{
	// 定义一个数组并初始化
	u8 array_buf[10] = { 0,1,2,3,4,5,6,7,8,9 };
	// 获取数组的长度
	int len = sizeof(array_buf) / sizeof(u8);

	// 定义一个指向数组的指针
	u8* arrayp = array_buf;

	printf("方式1：\n");
	// 遍历打印数组方式1
	for (int i = 0; i < len; i++)
	{
		printf("%d ", *(arrayp++));
	}
	OUT_BR();

	arrayp = array_buf; // 让 arrapy 重新指向 array_buf[0]
	// 遍历打印数组方式2
	printf("方式2：\n");
	for (u8 i = 0; i < len; i++)
	{
		printf("%d ", *(arrayp + i));
	}
	OUT_BR();

	// 遍历打印数组方式3
	printf("方式3：\n");
	for (u8 i = 0; i < len; i++)
	{
		printf("%d ", arrayp[i]);
	}
}
```

### 通过指向数组的指针操作数组

1. `arrayp[i]`
2. `*(arrayp + i)`
3. `*(arrayp++)`

### 通过数组名操作数组

1. `array_name[index]`
2. `*(array_name + i)`

### 数组作为函数的参数

```c
/**
  * printf 打印 u8 类型的数组
  * param arr: 指针或（数组名，arr[i])
  * param size: 数组大小或要输出几个元素
  *
*/
void print_array_u8(u8* arr, int size)
{
	for (int i = 0; i < size; i++)
	{
		printf("%d ", *(arr++));
	}
	OUT_BR();
}

void array_print_test(void)
{
	u8 a[10] = { 0,1,2,3,4,5,6,7,8,9 };

	print_array_u8(&a[3], 2); // 输出：3 4
}
```

## 格式化输出

c 语言格式化占位符如下：

- `%d` 整型输出，char 输出
- `%ld` 长整型输出
- `%o` 八进制整型输出
- `%x` 十六进制整型输出，或输出字符串的地址
- `%u` 以十进制输出 `unsigned` 型数据

### 整数格式化例子

```c
void test(void)
{
    // 格式化对齐
    int a = 123, b = 123456;
    printf("%5d\n", a);		// 默认对齐，最少5位整数，不够的使用空格替换
    printf("%05d\n", a); 	// 默认右对齐，最少5位整数，不够的使用0替换
    printf("%-5d\n", a); 	// 左对齐，最少5位整数，不够的使用空格替换
    printf("%-05d\n", a); 	// 左对齐，最少5位整数，不够的使用空格替换
    printf("%5d\n", b); 	// 超过5位全部输出
}
```

### 小数格式化例子

```c
void test(void)
{
    double af = 123.326, bf = 90.12;
    printf("%.2f\n", af); // 输出 123.33
    printf("%.3f\n", bf); // 输出 90.120
    
    printf("%4.2f\n", bf); // 输出 90.12
    printf("%7.2f\n", bf); // 输出 空格空格90.12，9前面两个空格
}
```

### 字符数组/字符串格式化

```c
void test(void)
{
    char str[30] = "hello,world";
    char s1[5] = { 'a', 'b', 'c'};
    
    printf("%s==\n", s1); // 输出 "abc=="
    printf("%2s==\n", s1); // 输出 "abc=="
    printf("%5s==\n", s1); // 输出 "  abc=="
    printf("%-5s==\n", s1); // 输出 "abc  " 从右补空格
    
    printf("%4.2s==\n", s1); // 输出 "  abc==" 从左补空格
    printf("%.2s==\n", s1); // 输出 "ab=="
    
    printf("%4.2s==\n", str); // 输出 "  he" 从左补空格
}
```

### `sprintf()` 格式化

`sprintf()` 函数可以把指定的格式打印到字符串中，例子如下：

```c
void sprintf_demo(void)
{
    char str[30];
    double a = 123.123456;
    double b = 90.12;
    sprintf(str, "a: %.2f\n", a);
    printf("%s\n", str);
    
    spirntf(str, "a: %.2f------b: %6.2f\n", a,b);
    printf("%s\n", str);
}
```

使用 `sprintf()` 要注意内存溢出的问题，要注意格式化的内容不能大于存储字符串的大小。

### `sprintf_s()` 格式化

`sprintf_s()` 是 `sprintf()`的安全版本，下面是例子：

```c
void sprintf_demo(void)
{
#define STR_LEN 30
	char str[STR_LEN];
    
    double a = 123.123456;
    double b = 90.12;
    sprintf_s(str, STR_LEN, "a: %.2f\n", a);
    printf("%s\n", str);
    
    char str_format[] = "a: %.2f------b: %6.2f\n";
    
    int str_len = sizeof(str_format);
    if (str_len < STR_LEN)
    {
        sprintf_s(str, sizeof(str), str_format, a, b);
    }
    printf("%s\n", str);
}
```

