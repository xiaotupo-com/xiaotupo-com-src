---
sidebar_position: 3
description: FreeRTOS 配置文件
---

# FreeRTOS 配置文件

## configKERNEL_INTERRUPT_PRIORITY

- 用来设置RTOS内核自己的中断优先级。
- 因为RTOS内核中断不允许抢占用户使用的中断，因此这个宏一般定义为硬件最低优先级。 值可以是255(最低)到0(1?)(最高)


## configMAX_SYSCALL_INTERRUPT_PRIORITY

```c
#define configMAX_SYSCALL_INTERRUPT_PRIORITY (0x5) // 定义了受freeRTOS管理的最高优先级中断
```