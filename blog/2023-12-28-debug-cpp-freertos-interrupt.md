---
slug: debug-cpp-freertos-interrupt
title: 基于C++的单片机开发中的中断函数名前要加 C 前缀
authors: [xiaotupo]
tags: [FreeRTOS,C++,中断]
---

这两天遇到一个问题就是，用C++开发单片机时遇到中断无反应的问题，怎么都无法进入中断。
<!-- truncate -->
这个是无反应的代码：

```c
void EXINT9_5_IRQHandler(void)
{
    BaseType_t xYieldRequired;
    if (exint_flag_get(EXINT_LINE_8) != RESET)
    {
        xYieldRequired = xTaskResumeFromISR(xTaskGetHandle("led_task"));
       	if (xYieldRequired == pdTRUE)
       	{
           	portYIELD_FROM_ISR(xYieldRequired);
       	} else {
           	portYIELD_FROM_ISR(NULL);
       	}
        exint_flag_clear(EXINT_LINE_8);
    }
}
```

这个是正常的代码：

```c
extern "C" void EXINT9_5_IRQHandler(void)
{
    BaseType_t xYieldRequired;
    if (exint_flag_get(EXINT_LINE_8) != RESET)
    {
        xYieldRequired = xTaskResumeFromISR(xTaskGetHandle("led_task"));
        
        if (xYieldRequired == pdTRUE)
        {
            portYIELD_FROM_ISR(xYieldRequired);
        }
        else {
            portYIELD_FROM_ISR(NULL);
        }
        exint_flag_clear(EXINT_LINE_8);
    }
}
```