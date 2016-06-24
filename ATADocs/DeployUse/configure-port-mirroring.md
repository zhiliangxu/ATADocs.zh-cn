---
# required metadata

title: 配置端口镜像 | Microsoft 高级威胁分析
description: 介绍端口镜像选项以及如何为 ATA 配置这些选项
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 配置端口镜像
> [!NOTE] 本文仅在部署 ATA 网关而不是 ATA 轻型网关时可提供相关帮助。 若要确定是否需要使用 ATA 网关，请参阅[为你的部署选择正确的网关](/advanced-threat-analytics/plan-design/ata-capacity-planning#Choosing-the-right-gateway-type-for-your-deployment)
 
ATA 使用的主数据源是传入和传出域控制器的网络流量的深度数据包检查。 要使 ATA 能够查看网络流量，你必须配置端口镜像，或使用网络 TAP。

对于端口镜像，请将要监视的每个域控制器的**端口镜像**配置为网络流量的**源**。 通常，你需要与网络或虚拟化团队合作来配置端口镜像。
有关详细信息，请参阅供应商的文档。

域控制器和 ATA 网关可以是物理的，也可以是虚拟的。 下面是端口镜像的常见方法和一些注意事项。 有关其他信息，请参阅交换机或虚拟化服务器产品文档。 交换机制造商可能使用不同的术语。

**交换端口分析器 (SPAN)** – 将网络流量从一个或多个交换机端口复制到同一交换机上的另一个交换机端口。 ATA 网关和域控制器都必须连接到同一个物理交换机。

**远程交换机端口分析器 (RSPAN)** – 可让你从分布在多个物理交换机上的源端口监视网络流量。 RSPAN 将源流量复制到 RSPAN 配置的 VLAN。 此 VLAN 需要中继到其他相关的交换机。 RSPAN 在第二层上运行。

**封装远程交换机端口分析器 (ERSPAN)** – 在第 3 层上运行的 Cisco 专有技术。 无需 VLAN 中继，ERSPAN 就允许你跨交换机监视流量。 ERSPAN 使用通用路由封装 (GRE) 来复制受监视的网络流量。 ATA 当前不能直接接收 ERSPAN 流量。 要使 ATA 能够处理 ERSPAN 流量，需要将一个可以解封流量的交换机或路由器配置为流量将要解封到的 ERSPAN 目标。 然后，需要将该交换机或路由器配置为使用 SPAN 或 RSPAN 向 ATA 网关转发流量。

> [!NOTE]
> 如果进行端口镜像的域控制器是通过 WAN 链路连接的，请确保该 WAN 链路可以处理 ERSPAN 流量的额外负载。

## 支持的镜像端口选项

|ATA 网关|域控制器|注意事项|
|---------------|---------------------|------------------|
|虚拟|相同主机上的虚拟设备|虚拟交换机需要支持端口镜像。<br /><br />将一个虚拟机本身移到另一台主机可能会破坏端口镜像。|
|虚拟|不同主机上的虚拟设备|确保你的虚拟交换机支持此方案。|
|虚拟|物理|需要使用专用网络适配器，否则 ATA 将看到传入和传出主机的所有流量，甚至包括它发送到 ATA 中心的流量。|
|物理|虚拟|确保你的虚拟交换机支持此方案 - 以及根据方案在物理交换机上配置的端口镜像：<br /><br />如果虚拟主机位于同一个物理交换机上，则你需要配置交换机级别的跨接。<br /><br />如果虚拟主机在不同的交换机上，则你需要配置 RSPAN 或 ERSPAN&#42;。|
|物理|相同交换机上的物理设备|物理交换机必须支持 SPAN/端口镜像。|
|物理|不同交换机上的物理设备|要求物理交换机支持 RSPAN 或 ERSPAN&#42;。|
&#42; 仅当 ATA 分析流量之前执行解封时，才支持 ERSPAN。

> [!NOTE]
> 确保域控制器与其连接到的 ATA 网关的时间同步，彼此间的误差不超过 5 分钟。

**如果你正在使用虚拟化群集：**

-   对于在包含 ATA 网关的虚拟机中的虚拟化群集上运行的每个域控制器，请在域控制器与 ATA 网关之间配置相关性。 这样，当域控制器移到群集中的另一个主机时，ATA 网关可以跟踪该域控制器。 存在多个域控制器时，这种做法非常有效。
> [!NOTE]
> 如果你的环境支持在不同主机上进行虚拟到虚拟转换 (RSPAN)，则无需担忧关联问题。
> 
-   为了确保正确选择 ATA 网关的大小以使其能够自行处理所有 DC 的监视，请尝试使用此选项：在每个虚拟化主机上安装一个虚拟机，并在每个主机上安装 ATA 网关。 将每个 ATA 网关配置为监视群集上运行的所有域控制器。 这样，即可监视运行域控制器的任何主机。

在配置端口镜像后，请先验证端口镜像是否正常工作，然后再安装 ATA 网关。

## 另请参阅
- [验证端口镜像](validate-port-mirroring.md)
- [安装 ATA](install-ata.md)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


