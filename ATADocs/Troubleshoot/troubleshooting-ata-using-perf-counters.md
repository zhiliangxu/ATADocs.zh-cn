---
# required metadata

title: 使用性能计数器排查 ATA 问题 | Microsoft 高级威胁分析
description: 介绍如何使用性能计数器来排查 ATA 问题
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用性能计数器排查 ATA 问题
ATA 性能计数器提供有关每个 ATA 组件执行情况的洞察信息。 ATA 中的组件按顺序处理数据，当出现问题时，它会产生导致流量下降的一种链式反应。 为了修复此问题，必须找出产生反作用的组件并在链的开端修复此问题。
请参阅 [ATA 体系结构](/advanced-threat-analytics/plan-design/ata-architecture)，了解内部 ATA 组件的流程。

**ATA 组件进程**：

1.  当某个组件达到其最大大小时，会阻止前一个组件向其发送更多实体。

2.  最终，前一个组件**自身**的大小会不断递增，直到阻止它前面的组件发送更多实体。

3.  发生这种问题的源头在于初始 NetworkListener 组件，当该组件不再能够转发实体时，会丢弃流量。

4. 使用性能计数器中的数据来了解每个组件的工作原理。

## ATA 网关性能计数器

此部分中的所有 ATA 网关的引用都是指 ATA 轻型网关。

你可以通过添加 ATA 网关的性能计数器来观察 ATA 网关的实时性能状态。
为此，可以打开“性能监视器”，然后添加 ATA 网关的所有计数器。 性能计数器对象的名称是：“Microsoft ATA 网关”。

![添加性能计数器图像](media/ATA-performance-counters.png)

下面要注意的主要 ATA 网关计数器列表：

|计数器|描述|Threshold|疑难解答|
|-----------|---------------|-------------|-------------------|
|NetworkListener PEF 分析程序消息数/秒|ATA 网关每秒处理的流量大小。|无阈值|帮助你了解 ATA 网关正在分析的流量大小。|
|NetworkListener PEF 删除的事件数/秒|ATA 网关每秒丢弃的流量大小。|此数字应始终为零（只可接受极短的丢包喷发）。|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。 请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|
|NetworkListener ETW 删除的事件数/秒|ATA 网关每秒丢弃的流量大小。|此数字应始终为零（只可接受极短的丢包喷发）。|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。 请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|
|NetworkActivityTranslator 消息数据 # 块大小|排队等待转换成网络活动 (NA) 的流量大小。|应小于“最大值-1”（默认最大值：100,000）|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。 请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|
|EntityResolver 活动块大小|排队等待解析的网络活动 (NA) 数量。|应小于“最大值-1”（默认最大值：10,000）|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。 请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|
|EntitySender 实体批块大小|排队等待发送到 ATA 中心的网络活动 (NA) 数量。|应小于“最大值-1”（默认最大值：1,000,000）|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。 请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|
|EntitySender 批发送时间|发送最后一个批所花费的时间。|大多数情况下应小于 1000 毫秒|检查 ATA 网关与 ATA 中心之间是否有任何网络问题。|

> [!NOTE]
> -   计时计数器以毫秒为单位。
> -   有时，使用“报告”图表类型可以更方便地监视计数器的完整列表（示例：实时监视所有计数器）

## ATA 中心性能计数器
你可以通过添加 ATA 中心的性能计数器来观察 ATA 中心的实时性能状态。

为此，可以打开“性能监视器”，然后添加 ATA 中心的所有计数器。 性能计数器对象的名称是：“Microsoft ATA 中心”。

![ATA 中心 - 添加性能计数器](media/ATA-Gateway-perf-counters.png)

下面要注意的主要 ATA 中心计数器列表：

|计数器|描述|Threshold|疑难解答|
|-----------|---------------|-------------|-------------------|
|EntityReceiver 实体批块大小|由 ATA 中心排队的实体批数。|应小于“最大值-1”（默认最大值：10,000）|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。  请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|
|NetworkActivityProcessor 网络活动块大小|排队等待处理的网络活动 (NA) 数量。|应小于“最大值-1”（默认最大值：50,000）|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。 请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|
|EntityProfiler 网络活动块大小|排队等待分析的网络活动 (NA) 数量。|应小于“最大值-1”（默认最大值：10,000）|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。 请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|
|CenterDatabase &#42; 块大小|特定类型的、排队等待写入数据库的网络活动数。|应小于“最大值-1”（默认最大值：50,000）|检查是否有任何组件达到了其最大大小，并且一直在阻止前面的组件向 NetworkListener 发送流量。 请参阅上面的 **ATA 组件进程**。<br /><br />检查 CPU 或内存是否未出现问题。|


> [!NOTE]
> -   计时计数器以毫秒为单位
> -   有时，使用“报告”图表类型可以更方便地监视计数器的完整列表（示例：实时监视所有计数器）。

## 操作系统计数器
以下为要注意的主要操作系统计数器列表：

|计数器|描述|Threshold|疑难解答|
|-----------|---------------|-------------|-------------------|
|Processor(_Total)\% Processor Time|处理器执行非空闲线程所用时间的百分比。|平均值小于 80%|检查是否有特定的进程花费的处理器时间超过了预期。<br /><br />添加更多处理器。<br /><br />减少每个服务器的流量大小。<br /><br />虚拟服务器上的“Processor(_Total)\% Processor Time”计数器可能不太准确，在这种情况下，测量处理器能力不足的更准确方法是通过“System\Processor Queue Length”计数器。|
|System\Context Switches/sec|从该处的所有处理器都从一个线程都切换到另一个综合的速率。|小于 5000 个&#42; 核心（物理核心）|检查是否有特定的进程花费的处理器时间超过了预期。<br /><br />添加更多处理器。<br /><br />减少每个服务器的流量大小。<br /><br />虚拟服务器上的“Processor(_Total)\% Processor Time”计数器可能不太准确，在这种情况下，测量处理器能力不足的更准确方法是通过“System\Processor Queue Length”计数器。|
|System\Processor Queue Length|已准备好执行并等待调度的线程数。|小于 5 个&#42; 核心（物理核心）|检查是否有特定的进程花费的处理器时间超过了预期。<br /><br />添加更多处理器。<br /><br />减少每个服务器的流量大小。<br /><br />虚拟服务器上的“Processor(_Total)\% Processor Time”计数器可能不太准确，在这种情况下，测量处理器能力不足的更准确方法是通过“System\Processor Queue Length”计数器。|
|Memory\Available MBytes|可用于分配的物理内存 (RAM) 量。|应大于 512|检查是否有特定的进程花费的物理内存量超过了预期。<br /><br />增大物理内存量。<br /><br />减少每个服务器的流量大小。|
|LogicalDisk(&#42;)\Avg. Disk sec/Read|从磁盘读取数据发生的平均延迟（你应选择数据库驱动器作为实例）。|应小于 10 毫秒|检查是否有特定的进程占用数据库驱动器的时间超过了预期。<br /><br />如果此驱动器可以提供当前工作负荷，并且延迟小于 10 毫秒，请咨询你的存储团队/供应商。 可以使用磁盘利用率计数器确定当前工作负荷。|
|LogicalDisk(&#42;)\Avg. Disk sec/Write 性能计数器的收集规则|向磁盘写入数据发生的平均延迟（你应选择数据库驱动器作为实例）。|应小于 10 毫秒|检查是否有特定的进程占用数据库驱动器的时间超过了预期。<br /><br />如果此驱动器可以提供当前工作负荷，并且延迟小于 10 毫秒，请咨询你的存储团队/供应商。 可以使用磁盘利用率计数器确定当前工作负荷。|
|\LogicalDisk(&#42;)\Disk Reads/sec|向磁盘执行读取操作的速率。|无阈值|磁盘利用率计数器可以在排查存储延迟问题时添加洞察信息。|
|\LogicalDisk(&#42;)\Disk Read Bytes/sec|每秒从磁盘读取的字节数。|无阈值|磁盘利用率计数器可以在排查存储延迟问题时添加洞察信息。|
|\LogicalDisk(&#42;)\Disk Writes/sec|向磁盘执行写入操作的速率。|无阈值|磁盘利用率计数器（可以在排查存储延迟问题时添加洞察信息）|
|\LogicalDisk(&#42;)\Disk Write Bytes/sec|每秒向磁盘写入的字节数。|无阈值|磁盘利用率计数器可以在排查存储延迟问题时添加洞察信息。|

## 另请参阅
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量规划](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [配置事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [配置 Windows 事件转发](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


