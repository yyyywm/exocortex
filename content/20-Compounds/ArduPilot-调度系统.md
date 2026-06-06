---
title: "ArduPilot 调度系统"
type: compound
domain: ardupilot
status: seedling
draft: true
date: "2026-06-06"
prerequisites:
  - "合作式调度"
  - "RTOS-基础"
derived_concepts: []
code_refs:
  - "sources/ardupilot/libraries/AP_Scheduler/AP_Scheduler.cpp"
  - "sources/ardupilot/libraries/AP_Scheduler/AP_Scheduler.h"
tags:
  - "ardupilot"
  - "scheduler"
---

# ArduPilot 调度系统

## 系统概述

ArduPilot 的 AP_Scheduler 是一个**合作式调度器**，负责协调飞控系统中所有任务的执行时序。它确保高优先级的控制任务（如 PID 更新）以固定频率运行，同时让低优先级的任务（如日志记录）在 CPU 空闲时执行。

## 组成模块

| 模块 | 职责 | 对应原子概念 |
|------|------|-------------|
| AP_Scheduler | 调度器核心，决定任务执行顺序 | [[合作式调度]] |
| AP_HAL | 硬件抽象层，提供时间接口 | [[HAL-设计模式]] |
| 任务表 | 注册所有需要调度的任务 | - |

## 核心机制

1. **任务注册**：每个任务在初始化时注册到调度器的任务表中，声明期望的运行频率和最大允许执行时间
2. **主循环 tick()**：调度器在主循环中被周期性调用，检查每个任务是否应该运行
3. **时间片分配**：根据任务的声明频率和实际耗时，动态调整下次执行时间

## 关键代码

```cpp
// From: sources/ardupilot/libraries/AP_Scheduler/AP_Scheduler.cpp
void AP_Scheduler::tick(void)
{
    const uint32_t now = AP_HAL::millis();
    
    for (uint8_t i = 0; i < _num_tasks; i++) {
        if (_tasks[i].tick() == 0) {
            continue;
        }
        // 执行任务...
    }
}
```

## 与知识库的关联

- 涉及原子概念：[[合作式调度]]、[[HAL-设计模式]]
- 源码解读：[[sources/ardupilot/libraries/AP_Scheduler/AP_Scheduler.cpp]]
- 可对比系统：[[FreeRTOS-任务调度]]（待创建）

## 我的理解 v1.0

> 当前理解：AP_Scheduler 是合作式调度的典型实现。它通过任务表管理所有回调函数，而不是使用操作系统线程。
> 待澄清：
> 1. `_task_time_allowed` 的具体计算逻辑
> 2. 如何处理任务超时（如果一个任务执行时间超过声明值）
> 3. 与 `fast_loop()` 的关系是什么
> 更新日期：2026-06-06
