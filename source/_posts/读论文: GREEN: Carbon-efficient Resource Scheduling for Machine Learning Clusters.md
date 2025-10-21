---
abbrlink: ''
author: zyuan
categories:
- - 网络科研
date: '2025-10-21T09:50:10.499349+08:00'
excerpt: 读论文: GREEN: Carbon-efficient Resource Scheduling f...
tags:
- 读论文
- DCN
- 调度器
title: '读论文: GREEN: Carbon-efficient Resource Scheduling for Machine Learning Clusters'
updated: '2025-10-21T09:51:30.494+08:00'
---
# 读论文: GREEN: Carbon-efficient Resource Scheduling for Machine Learning Clusters

## 文章摘要

> 本文探讨了在调度机器学习(ML) 作业的同时, 如何减少集群碳排放的问题, 传统 ML 主要优化作业完成时间(JCT) 未考虑其决策对于环境的影响.
> 为了解决问题, 本文提出GREEN ,  时间高效且碳高效的 ML集群调度器
> 核心是采用独特的碳感知调度算法.最小化对  JCT 的影响同时减少碳足迹
> 此外, 它利用 ML 作业的时间灵活性, 通过将工作负载转移到碳排放较低的时间段来减少碳排放.同时仍保持整体日容量
> 结果 :  GREEN 减少 41.2% 的碳足迹, 峰值功耗减少 12% , 仅仅牺牲 3.6% - 5.9 % 的时间

## 背景和动机

### ML背景

一个机器学习 (ML) 集群是一个共享环境,多个用户可以提 交训练任务,这些任务会竞争有限的资源。

管理任务队列和分配资源,其目标是优化性能指标,如作业完成时间(JCT)和资源利用率。这种设置通常被 称为机器学习即服务

1. 自适应扩展(或弹性)

   自适应扩展调度器是指根据任务加速效率动态调整资源分配(GPU 数量) , 但是自适应扩展调度器的决策,  可能导致不同的能源消耗, 影响总的功耗,

   非自适应扩展调度器 (用户告诉我要用多少 GPU), 会限制集群端的性能优化可能性
2. 模型无关

   某些调度器可能要控制超参数或者作业的先验知识. 但是这种修改任务配置, 可能会导致兼容性或者可用性的挑战.
3. 节能感知

   GPU 功耗 , 随着利用率变化.

GREEN 的设计, 体现了上面三种属性:   可扩展的、模型无关的和节能感知的。

具体而言, GREEN实现了与先前工作相当的能源和时间效率,而无需修改任务级设置,如模型超参数。这种方法保留了 GREEN在用户ML实现中的非侵入性,并确保了 GREEN与ML框架中现有的和未来的任务级优化技术的 兼容性

### 碳感知资源调度器是什么

<img src="https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020131129697.png" alt="image-20251020131129697"  />

<img src="https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020131210338.png" alt="image-20251020131210338" style="zoom: 50%;" />

> 直观感觉可以把高能耗的放到低碳强度的地方来做,  因为大模型训练时间很长

#### 碳感知的现有工作(局限性)

##### 功率和资源节流

- Google 的 CICS 在碳强度高的时期对` 集群容量施加限制`. 通过减少工作量来减少能源消耗
- 对 JCT 产生负面影响 (大)

##### 缺乏容量约数

- 不考虑作业之间的资源竞争的调度策略 ,  只考虑时间(例如CarbonScaler [8] 需要用户指定的作业截止时间,并可以使用无限的按需云资源来满足截止时间)
- 说白了, 没有考虑资源的分配策略

有的模型甚至还需要额外的用户输入, 例如预定义的作业截止时间

### 动机

#### 动机 1 : 可用资源没有被优化能源利用率的方式被分配

之前的 集群调度器只关注于 JCT 优化, 不关注能源效率问题

#### 动机 2 : 工作负载时间比较灵活 , 这一点可以用来减少碳足迹

ml 模型要用几天时间来训练, 所以对于细小的时间分配并不敏感.

### 挑战

#### 优化过程要保持集群效率

#### 优化过程中要保证资源分配.

## GREEN 概述

![image-20251020134550674](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020134550674.png)

一共 3 个器件 , 分别是 能效优化器, 碳效优化器 ,然后用MLFQ 调度, 最后用碳追踪器估算

## 碳追踪器

GREEN 是碳感知的 也监督能耗

![image-20251020135359660](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020135359660.png)

![image-20251020135414491](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020135414491.png)

![image-20251020135833417](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020135833417.png)

CIC 在线公开, 可以用历史碳强度数据, 因为一段时间内,其总是一致的.

`GREEN 的碳优化器可以优化任何模式 `

## GREEN  优化器

### 能效优化器

![image-20251020142718658](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020142718658.png)

#### 如果作业进度可用

![image-20251020144250890](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020144250890.png)

#### 如果作业进度无法获得 (用吞吐量)

![image-20251020144904844](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020144904844.png)

另外, 还有衰减因子

![image-20251020145239699](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020145239699.png)

如果后续的调度轮次, 任务的退化因子高于阈值γ,  就分配 GPU ,例如,当 γ 为 0.9 时,意味着任务的能源效率必须下降不超过 10% 才有资格进行扩展。

γ 的值会根据集群占用率和任务特 征动态调整,以防止资源分配过多或过少。此外,最大 资源上限可防止优化的任务占用所有 GPU 资源。更多 关于 GREEN 的自适应策略的细节可参考 第 6 节

### 碳足迹优化器

![image-20251020145513884](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020145513884.png)

碳因子 FOOTPRINT 这样设计有两个好处

- 跟踪任务执行的碳排放, 类似于最小达成服务算法
- 退化因子有惩罚作用, 可以让高效能任务更早完成, 提高总体作业完成时间

迁移因子  $SHIFTING_{job}$

![image-20251020150644407](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020150644407.png)

迁移因子随着 碳强度CIC 的平均值 $\bar I$ 和 job 功率的中位数 $\tilde P$ 变化, 如图 5 所示

其中 $P^*_{job}$  被缩放到$ [1 , \mu]$

![image-20251020152128758](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020152128758.png)

不同的$\mu$ 控制时间偏移的程度, 比较大的值会导致更多的作业迁移.

然后图 6 是一个分段函数的示例, 橙色线是碳强度 , 碳强度低于 $\bar I$ 的时候, shift 小于 1 , 具有更高优先级.

![image-20251020152337516](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020152337516.png)

优化器可以适应任何碳强度的变化., 因为它根据给定的 CIC 可以动态调整 $\bar I$ 和 $\tilde P$

## 整合

GREEN 的 调度算法类似多级反馈队列 (MLFQ)

![image-20251020152656789](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020152656789.png)

### 上队列利用能效(EE) 优化器, 确定分配给每个任务的资源, 确保更高效的任务获得更多资源

目标, 优化能源效率

### 下队列采用碳足迹优化器, 通过重新定位来执行峰值负载转移

![image-20251021094751137](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251021094751137.png)

## 实验

![image-20251021094812604](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251021094812604.png)

![image-20251021094856767](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251021094856767.png) ![image-20251020214228427](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020214228427.png)![image-20251020214239783](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20251020214239783.png)

$$
\text{TotalCost} = \sum_{i \in gpuTypes} gpuHours_{i} \times {costPerHour}_{i}
$$

$$
\text{Minimize} \sum_{i \in \text{gputypes}} \text{Cost}_{i} \times (\text{ProductiveGpuHours}_{i} + \text{WastedGpuHours}_{i})
$$
