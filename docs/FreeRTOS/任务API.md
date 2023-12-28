---
sidebar_position: 2
description: FreeRTOS 任务相关API的使用
---

# FreeRTOS 任务相关API的使用

## FreeRTOS 任务的4中状态

1. 就绪态
2. 运行态

:::tip
🛴任何时候都只有一个任务处于运行态。

🐸调度器总是在就绪态列表中选择优先级最高的任务运行。
:::
- vTaskDelayUntil()
- vTaskDelay()
- xTaskGetTickCount()
- vTaskPrioritySet() 修改任务的优先级
- void vApplicationIdleHook( void ) 空闲任务钩子函数
- uxTaskPriorityGet() 获取任务的优先级
- vTaskDelete() 删除任务
- vTaskSuspend() 挂起任务
- vTaskResume() 恢复任务到就绪态
- xTaskResumeFromISR() 中断版本