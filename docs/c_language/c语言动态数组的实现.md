---
sidebar_position: 3
---

`Github`仓库：https://github.com/xiaotupo-com/c_learn

## 数据结构定义

```c
struct dyn_array
{
    int* array;
    int capacity;
    int size;
};

typedef struct dyn_array Dyn_arry;
```

## 初始化动态数组

```c
Dyn_array dyn_array_init(int* array, int size)
{
    // 先创建一个堆栈空间，用来作为初始动态数组的容器
    int* temp = malloc(sizeof(int) * size * 2);
    
    if (temp)
    {
        memcpy(temp, array, sizeof(int) * size);
    }
    
    Dyn_arry my_array;
    my_array.array = temp;
    my_array.capacity = size * 2;
    my_array.size = size;
    
    return my_array;
}
```

## 动态数组插入数据

```c
void dyn_array_insert(Dyn_arry* array, int var)
{
    if ((array->size) < (array->capacity))
    {
        array->array[array->size] = var;
        array->size++;
    }
    else
    {
        printf("堆空间已用完\n");
        int* temp = malloc(sizeof(int) * array->capacity * 2);
        
        if (temp)
        {
            array->capacity = array->capacity * 2;
            memcpy(temp, array->array, sizeof(int) * array->size);
            array->array = temp;
            array->array[array->size] = var;
            array->size++;
        }
    }
}
```

##  测试函数

```c
void dyn_array_test(void)
{
    Line("动态数组测试");
    Dyn_arry darray;
    int iarray[5] = {1,2,3,4,5};
    darray = dyn_array_init(iarray, 5);
    print_array_int(darray.array, darray.size);
    
    for (int i=40; i>0; i--)
    {
        dyn_array_insert(&darray, i - 6);
    }
    printf("capacity: %d\n", darray.capacity);
    print_array_int(darray.array, darray.size);
    
    printf("排序darry后的数组：\n");
    bubble_sort(darray.array, darray.size);
    print_array_int(darray.array, daray.size);
    free(darray.array);
}
```

