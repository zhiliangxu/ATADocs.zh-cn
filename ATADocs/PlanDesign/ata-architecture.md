---
# required metadata

title: ATA 体系结构 | Microsoft 高级威胁分析
description: 介绍 Microsoft 高级威胁分析 (ATA) 的体系结构
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 体系结构
下图详细描绘了高级威胁分析的体系结构：

![ATA 体系结构拓扑图](media/ATA-architecture-topology.jpg)

ATA 可监视域控制器的网络流量，方式是通过物理或虚拟交换机将端口镜像应用到 ATA 网关，或直接在域控制器上部署 ATA 轻型网关（此操作将删除对端口镜像的要求）。 此外，ATA 可以利用 Windows 事件（直接从域控制器或 SIEM 服务器转发），并分析攻击和威胁的数据。
本部分介绍了网络和事件捕获的流程，并深入描述 ATA 的以下主要组件的功能：ATA 网关、ATA 轻型网关（其核心功能与 ATA 网关的相同），以及 ATA Center。


![ATA 流量流示意图](media/ATA-traffic-flow.jpg)

## ATA 组件
ATA 包括以下组件：

-   **ATA 中心** <br>
ATA Center 从所部署的任何 ATA 网关和/或 ATA 轻型网关接收数据。
-   **ATA 网关**<br>
ATA 网关安装在专用服务器上，该服务器使用端口镜像或网络 TAP 监视来自域控制器的流量。
-   **ATA 轻型网关**<br>
ATA 轻型网关直接安装在域控制器上并直接监视其流量，无需专用服务器或配置端口镜像。 此为 ATA 网关的替代项。

ATA 部署可由连接到所有 ATA 网关、所有 ATA 轻型网关，或这两种网关组合的单个 ATA Center 组成。


## 部署选项
可使用以下网关组合来部署 ATA：

-   **仅使用 ATA 网关** <br>
如果 ATA 部署仅包含 ATA 网关，而无任何 ATA 轻型网关，则所有域控制器均必须配置为启用到 ATA 网关的端口镜像，或者网络 TAP 必须已到位。
-   **仅使用 ATA 轻型网关**<br>
如果 ATA 部署仅包含 ATA 轻型网关，则要在每个域控制器上部署 ATA 轻型网关，且无需其他服务器或端口镜像配置。
-   **同时使用 ATA 网关和 ATA 轻型网关**<br>
如果 ATA 部署同时包含 ATA 网关和 ATA 轻型网关，则 ATA 轻型网关安装在某些域控制器上（例如，分支站点中的所有域控制器），而其他域控制器受 ATA 网关监视（例如，主数据中心中的较大域控制器）。

在所有这 3 种方案中，所有网关均将其数据发送到 ATA Center。




## ATA 中心
**ATA 中心**执行以下功能：

-   管理 ATA 网关和 ATA 轻型网关配置设置

-   从 ATA 网关和 ATA 轻型网关接收数据 

-   检测可疑活动

-   运行 ATA 行为计算机学习算法来检测异常行为

-   运行各种确定性算法，基于攻击杀伤链检测高级攻击

-   运行 ATA 控制台

-   可选：可将 ATA 中心配置为在检测到可疑活动时发送电子邮件和事件。

ATA Center 可从 ATA 网关和 ATA 轻型网关接收已分析的流量、执行分析、运行确定性检测，并运行机器学习和行为算法来了解你的网络，以便能够检测异常，在出现可疑活动时发出警告。

|||
|-|-|
|实体接收者|从所有 ATA 网关和 ATA 轻型网关接收多批实体。|
|网络活动处理器|处理每批中收到的所有网络活动。 例如，在通过可能不同的计算机执行的各种 Kerberos 步骤之间进行匹配|
|实体分析器|根据流量和事件分析所有唯一实体。 例如，ATA 在实体分析器中根据每个用户配置文件更新已登录计算机列表。|
|中心数据库|管理在数据库中写入网络活动和事件的过程。 |
|数据库|ATA 利用 MongoDB 在系统中存储所有数据：<br /><br />-   网络活动<br />-   事件活动<br />-   唯一实体<br />-   可疑活动<br />-   ATA 配置|
|检测程序|检测程序运用机器学习算法和确定性规则来查找网络中的可疑活动和异常用户行为。|
|ATA 控制台|ATA 控制台用于配置 ATA，以及监视 ATA 在网络上检测到的可疑活动。 ATA 控制台并不依赖于 ATA 中心服务，只要它能够与数据库通信，则即使该服务已停止，它也能运行。|
在决定要将多少个 ATA 中心部署到网络时，请考虑以下因素：

-   一个 ATA 中心可以监视一个 Active Directory 林。 如果你有多个 Active Directory 林，需要为每个 Active Directory 林至少配置一个 ATA 中心。

-    在非常大型的 Active Directory 部署中，单个 ATA Center 可能无法处理所有域控制器的所有流量。 在这种情况下，需要多个 ATA Center。 ATA Center 的数量应符合 [ATA 容量计划](ata-capacity-planning.md).

## ATA 网关和 ATA 轻型网关

### 网关核心功能
**ATA 网关**和**ATA 轻型网关**都具有相同的核心功能：

-   捕获并检查域控制器的网络通信（在 ATA 网关的情况下为端口镜像流量，在 ATA 轻型网关的情况下为域控制器的本地流量） 

-   从 SIEM 或 Syslog 服务器，或者使用 Windows 事件转发从域控制器接收 Windows 事件

-   从 Active Directory 域检索有关用户和计算机的数据

-   执行网络实体（用户、组和计算机）解析

-   将相关数据传输到 ATA Center

-   从单个 ATA 网关监视多个域控制器，或者从 ATA 轻型网关监视单个域控制器。

ATA 网关可从网络中接收网络流量和 Windows 事件，并在以下主要组件中对其进行处理：

|||
|-|-|
|网络侦听器|网络侦听器负责捕获网络流量和分析流量。 这是一个 CPU 密集型任务，因此在规划 ATA 网关或 ATA 轻型网关时，检查 [ATA 先决条件](ata-prerequisites.md)尤为重要。|
|事件侦听器|事件侦听器负责捕获和分析从网络上的 SIEM 服务器转发的 Windows 事件。|
|Windows 事件日志读取器|Windows 事件日志读取器负责读取和分析从域控制器转发到 ATA 网关 Windows 事件日志的 Windows 事件。|
|网络活动转换器 | 将已分析的流量转换成 ATA 所使用的流量逻辑表示形式 (NetworkActivity)。
|实体解析器|实体解析器采用已分析的数据（网络流量和事件），并使用 Active Directory 解析数据，以查找帐户和标识信息。 然后将其与分析数据中找到的 IP 地址进行匹配。 实体解析器有效地检查数据包标头，以便分析计算机名称、属性和标识的身份验证数据包。 实体解析器将已分析的身份验证数据包与实际数据包中的数据相结合。|
|实体发送者|实体发送者负责将已分析和匹配的数据发送到 ATA 中心。|

## ATA 轻型网关功能

下述功能的工作方式有所不同，具体取决于你运行的是 ATA 网关还是 ATA 轻型网关。

-   **域同步器候选项**<br>
域同步器网关负责主动同步特定 Active Directory 域中的所有实体（类似于域控制器自身复制时使用的机制）。 从候选项列表中随机选择一个网关作为域同步器。 <br><br>
如果此同步器处于脱机状态的时间超过 30 分钟，则改选为其他候选项。 如果所有域同步器均不可用于特定域，则 ATA 将无法主动同步实体及其更改，但在所监视的流量中检测到新实体时，ATA 将被动检索这些实体。 
<br>如果域同步器均不可用，且搜索不具备任何相关流量的实体，则不会显示任何搜索结果。<br><br>
默认情况下，所有 ATA 网关都是同步器候选项。<br><br>
由于所有 ATA 轻型网关都更可能部署到分支站点和小的域控制器上，所以它们不会默认为同步器候选项。


-   **资源限制**<br>
ATA 轻型网关包括一个监视组件，该组件可计算运行它的域控制器上的可用计算和内存容量。 监视进程每隔 10 秒运行一次，并动态更新 ATA 轻型网关进程上的 CPU 和内存使用率配额，以确保在任何给定时间点，域控制器至少具有 15% 的可用计算和内存资源。<br><br>
无论域控制器上发生什么情况，此进程始终会释放资源，以确保域控制器的核心功能不受影响。<br><br>
如果此操作导致 ATA 轻型网关耗尽所有资源，则仅监视部分流量，且“运行状况”页上将显示监视警报“已删除端口镜像的网络流量”。

下表举例说明了一个域控制器，对于当前所需的较大配额而言，此控制器具有足够的可用计算资源，以便监视所有流量：

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA 轻型网关 (Microsoft.Tri.Gateway.exe)|杂项（其他进程） |ATA 轻型网关配额|正在删除的网关|
|30%|20%|10%|45%|否|

如果 Active Directory 需要更多计算，则会降低 ATA 轻型网关所需的配额。 在以下示例中，ATA 轻型网关的所需配额多于已分配的配额，并放弃一些流量（仅监视部分流量）：

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA 轻型网关 (Microsoft.Tri.Gateway.exe)|杂项（其他进程） |ATA 轻型网关配额|正在删除的网关|
|60%|15%|10%|15%|是|



## 你的网络组件
为了使用 ATA，请确保以下条件：

### 端口镜像
如果使用的是 ATA 网关，必须为要监视的域控制器设置端口镜像，并使用物理或虚拟交换机将 ATA 网关设置为目标。 还可以使用网络 TAP。 如果部分（而非全部）域控制器受到监视，则 ATA 可以工作，但检测效率将会降低。

尽管端口镜像会将所有域控制器网络流量镜像到 ATA 网关，但在这些流量中，只有极少比例的部分将经过压缩并发送到 ATA Center 进行分析。

域控制器和 ATA 网关可是物理的，也可是虚拟的；相关详细信息，请参阅[配置端口镜像](/advanced-threat-analytics/deploy-use/configure-port-mirroring)。


### 事件
若要增强 ATA 对传递哈希、暴力攻击和蜜标的检测，ATA 需要 Windows 事件日志 ID 4776。 此事件可通过两种方法之一转发到 ATA 网关：将 ATA 网关配置为侦听 SIEM 事件，或者使用 Windows 事件转发。

-   将 ATA 网关配置为侦听 SIEM 事件 <br>将 SIEM 配置为向 ATA 转发特定的 Windows 事件。 ATA 支持许多 SIEM 供应商。 相关详细信息，请参阅[配置事件集合](/advanced-threat-analytics/deploy-use/configure-event-collection)。.

-   配置 Windows 事件转发<br>让 ATA 获取事件的另一种方法是将域控制器配置为向 ATA 网关转发 Windows 事件 4776。 如果你没有 SIEM，或者你的 SIEM 当前不受 ATA 支持，则此方法特别有用。 若要深入了解 ATA 中的 Windows 事件转发，请参阅[配置 Windows 事件转发](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding).

## 另请参阅
- [ATA 先决条件](ata-prerequisites.md)
- [ATA 容量规划](ata-capacity-planning.md)
- [配置事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [配置 Windows 事件转发](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO2-->


