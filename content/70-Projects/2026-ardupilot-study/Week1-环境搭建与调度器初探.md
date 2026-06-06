---
title: "Week1：环境搭建与调度器初探"
type: project
date: "2026-06-06"
project: "2026-ardupilot-study"
week: 1
draft: false
tags:
  - "ardupilot"
  - "weekly"
---

# Week1：环境搭建与调度器初探

## 本周目标

1. [x] 搭建 Exocortex 笔记系统
2. [x] 克隆 ArduPilot 源码
3. [x] 理解 AP_Scheduler 的基本架构

## 学习笔记

### 合作式调度

创建了第一条原子概念笔记：[[合作式调度]]

核心认识：ArduPilot 没有使用传统 RTOS，而是自己实现了合作式调度器。这简化了设计，但也要求每个任务必须在合理时间内完成。

### AP_Scheduler 架构

创建了复合系统笔记：[[ArduPilot-调度系统]]

## 代码发现

AP_Scheduler 的主入口是 `tick()` 函数，它遍历任务表，判断每个任务是否应该执行。

## 遇到的问题

| 问题 | 解决状态 | 备注 |
|------|----------|------|
| Quartz 初始化网络失败 | 待解决 | GitHub 访问不稳定，后续再配 |
| 子模块下载慢 | 进行中 | ArduPilot 仓库较大 |

## 下周计划

1. 精读 AP_Scheduler.cpp 源码，理解任务注册机制
2. 跟踪一次实际的 tick() 执行流程
3. 理解 `_task_time_allowed` 的计算逻辑

## 相关笔记

- [[合作式调度]]
- [[ArduPilot-调度系统]]
