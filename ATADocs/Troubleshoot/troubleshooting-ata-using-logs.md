---
# required metadata

title: 使用 ATA 日志排查 ATA 问题 | Microsoft 高级威胁分析
description: 说明如何使用 ATA 日志来解决问题
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用 ATA 日志排查 ATA 问题
通过 ATA 日志了解每个 ATA 组件在任意给定时间点的行为。

## ATA 网关日志
此部分中的所有 ATA 网关的引用也都与 ATA 轻型网关相关。 

ATA 网关日志位于名为 **Logs** 的子文件夹中。 在默认安装位置中，该日志位于 **C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**。

ATA 网关包含以下日志：

-   **Microsoft.Tri.Gateway.log** – 此日志包含发生在 ATA 网关中的所有事项（包括解析和错误）。 其主要用途是按发生时间顺序获取所有操作的总体状态。

-   **Microsoft.Tri.Gateway-Resolution.log** – 此日志包含 ATA 网关在流量中看到的实体解析详细信息。 其主要用途是调查实体的解析问题。

-   **Microsoft.Tri.Gateway-Errors.log** – 此日志只包含 ATA 网关捕获的错误。 其主要用途是执行运行状况检查并调查需要关联到特定时间的问题。

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – 此日志将所有相似的错误和异常组合到一起，并衡量其计数。
    此文件在 ATA 网关服务每次启动时都为空，每分钟进行更新。 其主要用途是了解 ATA 网关是否存在新的错误或问题 - 由于已将错误组合到一起，因此更容易阅读和查看是否存在新的错误或问题类型。

> [!NOTE]
> 头三个日志文件的最大大小为 50 MB。 如果已经是最大大小，则会打开新的日志文件，而先前的日志文件则会重命名为“&lt;原始文件名&gt;-Archived-00000”，其中的数字在每次重命名时都会递增。

### ATA Center 日志
ATA Center 日志位于名为 **Logs** 的子文件夹中。 在默认安装位置中，该日志位于 **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**。

ATA 中心包含以下日志：

-   **Microsoft.Tri.Center.log** – 此日志包含发生在 ATA 中心的所有事项（包括检测和错误）。 其主要用途是按发生时间顺序获取所有操作的总体状态。

-   **Microsoft.Tri.Center-Detection.log** – 此日志只包含 ATA Center 的检测详细信息。 其主要用途是调查检测问题。

-   **Microsoft.Tri.Center-Errors.log** – 此日志只包含 ATA Center 捕获的错误。 其主要用途是执行运行状况检查并调查需要关联到特定时间的问题。

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – 此日志将所有相似的错误和异常组合到一起，并衡量其计数。
    此文件在 ATA 中心服务每次启动时都为空，每分钟进行更新。 其主要用途是了解 ATA Center 是否存在新的错误或问题 - 由于已将错误组合到一起，因此更容易阅读和查看是否存在新的错误或问题类型。

> [!NOTE]
> 头三个日志文件的最大大小为 50 MB。 如果已经是最大大小，则会打开新的日志文件，而先前的日志文件则会重命名为“&lt;原始文件名&gt;-Archived-00000”，其中的数字在每次重命名时都会递增。

### ATA 控制台日志
ATA 控制台日志（管理 API 日志）位于名为 **Logs** 的子文件夹中。 在默认安装位置中，该日志位于 **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Management\Logs**。

ATA 控制台包含以下日志：

-   **w3wp.log** – 此日志包含发生在管理进程 (IIS) 中的所有事项。


-   **w3wp-Errors.log** – 此日志只包含管理进程 (IIS) 捕获的错误。


-   **8e75f9f1-ExceptionStatistics.log** – 此日志将所有相似的错误和异常组合到一起，并衡量其计数。
    此文件在网关服务每次启动时都为空，每分钟进行更新。 其主要用途是了解 ATA Center 是否存在新的错误或问题 - 由于已将错误组合到一起，因此更容易阅读和查看是否存在新的错误或问题类型。

> [!NOTE]
> 头两个日志文件的最大大小为 50 MB。 如果已经是最大大小，则会打开新的日志文件，而先前的日志文件则会重命名为“&lt;原始文件名&gt;-Archived-00000”，其中的数字在每次重命名时都会递增。

### ATA 部署日志
ATA 部署日志位于安装了该产品的用户的临时目录中。 在默认安装位置中，该日志位于 **C:\Users\Administrator\AppData\Local\Temp**（或 %temp% 的上一个目录）。

ATA 中心部署日志：

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** - 此日志列出了 ATA 中心部署过程中的步骤。 其主要用途是跟踪 ATA Center 部署过程。

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** - 此日志列出了在 ATA 中心部署 MongoDB 的步骤。 其主要用途是跟踪 MongoDB 部署过程。

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** - 此日志文件列出了 ATA 中心二进制文件部署过程中的步骤。 其主要用途是跟踪 ATA Center 二进制文件的部署。

ATA 网关和 ATA 轻型网关部署日志：

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** - 此日志列出了 ATA 网关部署过程中的步骤。 其主要用途是跟踪 ATA 网关部署过程。

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** - 此日志文件列出了 ATA 网关二进制文件部署过程中的步骤。 其主要用途是跟踪 ATA 网关二进制文件的部署。

## 另请参阅
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量规划](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [配置事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [配置 Windows 事件转发](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


