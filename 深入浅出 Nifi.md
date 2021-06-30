# 深入浅出 Nifi

[TOC]

## Nifi是什么

### 简介

- Apache NiFi 是一个易于使用、功能强大而且可靠的数据拉取、数据处理和分发系统，用于自动化管理系统间的数据流。
- 它支持高度可配置的指示图的数据路由、转换和系统中介逻辑，支持从多种数据源动态拉取数据。
- NiFi原来是NSA(National Security Agency [美国国家安全局])的一个项目，目前已经代码开源，是Apache基金会的顶级项目之一
- NiFi基于Web方式工作，后台在服务器上进行调度。
- 用户可以为数据处理定义为一个流程，然后进行处理，后台具有数据处理引擎、任务调度等组件。

### dataflow的挑战

- system fail
- Data access exceeds capacity to consume
- Boundary conditions are mere suggestions
- What is nosie one day become signal the next
- Systems evolve at different rates
- Compliance and security
- Continous improvment occur in production

### 特点

1. 高可用
2. 高并发
3. 错误纠察
4. 快速响应
5. 安全
6. 方便迁移

## NIFI核心概念

- Nifi 的设计理念接近于基于流的编程 Flow Based Programming。
- FlowFile：表示通过系统移动的每个对象，包含数据流的基本属性
- FlowFile Processor（处理器）：负责实际对数据流执行工作
- Connection（连接线）：负责不同处理器之间的连接，是数据的有界缓冲区
- Flow Controller（流量控制器）：管理进程使用的线程及其分配
- Process Group（过程组）：进程组是一组特定的进程及其连接，允许组合其他组件创建新组件



此设计模型也类似于seda（分阶段），带来了很多好处，有助于NiFi成为非常有效的、构建功能强大且可扩展的数据流的平台。其中一些好处包括：

- 有助于处理器有向图的可视化创建和管理
- 本质上是异步的，允许非常高的吞吐量和足够的自然缓冲
- 提供高并发的模型，开发人员不必担心并发的复杂性
- 促进内聚和松散糊合组件的开发，然后可以在其他环境中重复使用并方便单元测试
- 资源受限的连接流程中可配置connections）使得背压和压力释放等关键功能非常自然和直观
- 错误处理变得像基本逻辑一样自然，而不是粗粒度的全部捕获（catch-all）
- 数据进入和退出系统的点，以及它是如何流动的，都是容易理解和跟踪的

