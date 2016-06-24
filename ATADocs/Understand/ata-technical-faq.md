---
# required metadata

title: ATA 常见问题 | Microsoft 高级威胁分析
description: 提供有关 ATA 的常见问题列表及其相关解答。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 常见问题
本文提供有关 ATA 的常见问题列表，并提供见解与解答。


## 如何为 ATA 授权？
相关许可信息，请参阅[如何购买高级威胁分析](https://www.microsoft.com/en-us/server-cloud/products/advanced-threat-analytics/Purchasing.aspx)


## 如果 ATA 网关未无法启动，我该怎么办？
在当前错误日志中查找最新的错误（ATA 安装在“Logs”文件夹下）。
## 如何测试 ATA？
可通过执行下列操作之一来模拟可疑活动（这是一种端到端测试）：

1.  使用 Nslookup.exe 进行 DNS 侦测
2.  使用 psexec.exe 进行远程执行


需要针对受监视的域控制器远程运行，而不是从 ATA 网关上运行。

## 如何验证 Windows 事件转发？
可以在 **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** 目录中通过命令提示符下运行以下命令：

        mongo ATA --eval "printjson(db.getCollectionNames())" | find /C "NtlmEvents"`
## ATA 是否可以处理加密的流量？
将不会分析加密的流量（例如：LDAPS、IPSEC ESP）。
## ATA 是否可以使用 Kerberos Armoring？
ATA 支持启用 Kerberos Armoring（也称为灵活身份验证安全隧道 (FAST)），只不过反复传递哈希检测将不起作用。
## 我需要多少个 ATA 网关？

首先，建议在任何可支持 ATA 轻型网关的域控制器上这些网关；若要确定这一点，请参阅 [ATA 轻型网关规模](/advanced-threat-analytics/plan-design/ata-capacity-planning#ATA-Lightweight-Gateway-Sizing)。 

如果 ATA 轻型网关涵盖了所有域控制器，则无需 ATA 网关。

对于 ATA 轻型网关无法涵盖的任何域控制器，请在确定需要多少个 ATA 网关时考虑以下方面：

 - 域控制器产生的总流量大小，以及网络体系结构（目的是配置端口镜像）。 若要了解如何确定域控制器生成的流量大小，请参阅[域控制器流量估算](/advanced-threat-analytics/plan-design/ata-capacity-planning#Domain-controller-traffic-estimation)。
 - 端口镜像的操作限制（例如，每个交换机、每个数据中心、每个区域）也决定了需要多少个 ATA 网关来支持域控制器 – 每个环境都有自身的考虑因素。 

## 需要为 ATA 提供多少存储空间？
在完整的一天内，如果每秒平均产生 1000 个数据包，则、需要 0.3 GB 的存储空间。<br /><br />有关 ATA Center 规模的详细信息，请参阅 [ATA 容量计划](/advanced-threat-analytics/plan-design/ata-capacity-planning)。


## 某些帐户为何被视为是机密的？
如果某个帐户是某些机密组（例如“域管理员”）的成员，则该帐户就是机密帐户。

若要了解某个帐户为何机密，你可以查看其组成员身份，以了解它属于哪些机密组（它所属的组也可能由于其他组的关系而机密，因此，你应该执行相同的过程，直接找到级别最高的机密组）。

## 如何使用 ATA 监视虚拟域控制器？
ATA 轻型网关可涵盖大多数虚拟域控制器；若要确定 ATA 轻型网关是否适用于你的环境，请参阅 [ATA 容量计划](/advanced-threat-analytics/plan-design/ata-capacity-planning)。

如果 ATA 轻型网关无法涵盖某个虚拟域控制器，你可以按[配置端口镜像](/advanced-threat-analytics/deploy-use/configure-port-mirroring)中所述使用虚拟或物理 ATA 网关。  <br />最简单的方法是在虚拟域控制器所在的主机上创建虚拟 ATA 网关。<br />如果虚拟域控制器在主机之间移动，则你需要执行以下操作之一：

-   如果虚拟域控制器移到其他主机上，请在该主机中预配置 ATA 网关，以便从最近移动的虚拟域控制器接收流量。
-   确保将虚拟 ATA 网关与虚拟域控制器相关联，以便 ATA 网关将随着虚拟域控制器的移动而移动。
-   有些虚拟交换机可在主机之间发送流量。

## 如何备份 ATA？
需要备份 2 项信息：

-   ATA 存储的流量和事件，这可以使用任何受支持的数据库备份过程进行备份。有关详细信息，请参阅 [ATA 数据库管理](/advanced-threat-analytics/deploy-use/ata-database-management) 
-   ATA 的配置，它存储在数据库中，并且会每隔 1 小时自动备份一次。 

## ATA 可以检测哪些项目？
ATA 可检测已知的恶意攻击和技巧、安全问题以及风险。
有关 ATA 检测的完整列表，请参阅[什么是 Microsoft 高级威胁分析？](what-is-ata.md)

## 需要为 ATA 准备哪种类型的存储？
建议使用具有低延迟磁盘访问（小于 10 毫秒）的快速存储（不推荐 7200 RPM 磁盘）。 RAID 配置应支持很高的写入负荷（不推荐 RAID 5/6 及其衍生产品）。

## ATA 网关需要多少个 NIC？
ATA 网关至少需要两个网络适配器：<br>1.一个 NIC 连接到内部网络和 ATA 中心<br>2.一个 NIC 将用于通过端口镜像捕获域控制器网络流量。<br>* 这不适用于 ATA 轻型网关，因为此类网关以本机方式使用域控制器所用的全部网络适配器。

## ATA 与 SIEM 之间存在哪种集成？
ATA 与 SIEM 之间存在双向集成，如下所述：

1. 可以将 ATA 配置为在出现可疑活动时，向使用 CEF 格式的任何 SIEM 服务器发送 Syslog 警报。
2. 可以将 ATA 配置为从[这些 SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#SIEM-support) 接收 ID 为 4776 的每个 Windows 事件的 Syslog 消息。

## ATA 可以监视在 IaaS 解决方案上进行可视化的域控制器吗？

可以，ATA 轻型网关可用于监视任何 IaaS 解决方案中的域控制器。

## 该产品在本地还是在云中运行？
Microsoft 高级威胁分析是一款本地产品。

## Azure Active Directory 或本地 Active Directory 将来是否会包括该产品？
此解决方案目前是独立的产品，并未合并到 Azure Active Directory 或本地 Active Directory 中。

## 是否要编写自己的规则并创建阈值/基线？
使用 Microsoft 高级威胁分析时，无需创建规则、阈值或基线，然后进行微调。 ATA 将分析用户、设备和资源的行为以及相互之间的关系，并可以快速检测可疑活动和已知的攻击。 部署三周后，ATA 将开始检测行为可疑的活动。 另一方面，在部署后，ATA 将立即开始检测已知恶意攻击和安全问题。

## 如果我受到侵犯，Microsoft 高级威胁分析是否能够识别异常行为？
是的，即使你在受到侵犯后安装 ATA，ATA 也仍能检测到黑客的可疑活动。 ATA 不只是检测用户的行为，同时还会针对组织安全拓扑图中的其他用户执行检测。 在初始分析期间，如果攻击者的行为异常，则会将此行为标识为“异常”，同时，ATA 会不断报告异常行为。 此外，如果黑客试图盗窃其他用户凭据（例如传递票证）或者试图在一个域控制器上执行远程执行，ATA 可以检测到可疑活动。

## ATA 是否只利用 Active Directory 的流量？
除了使用深度数据包检查技术分析 Active Directory 流量以外，ATA 还可以根据 Active Directory 域服务中的信息从你的安全信息和事件管理 (SIEM) 中收集相关事件并创建实体配置文件。 如果组织配置了 Windows 事件日志转发，则 ATA 还可以从事件日志中收集事件。

## 什么是端口镜像？
端口镜像也称为 SPAN（交换端口分析器），是监视网络流量的一种方法。 启用端口镜像后，交换机会将一个端口（或整个 VLAN）上检测到的所有网络数据包的副本发送到另一个端口，然后便可在后一个端口上分析数据包。

## ATA 是否仅监视已加入域的设备？
否。 ATA 监视网络中针对 Active Directory 执行身份验证和授权请求的所有设备，包括非 Windows 设备和移动设备。

## ATA 是否会监视计算机帐户以及用户帐户？
是。 由于计算机帐户（以及任何其他实体）可用来执行恶意活动，ATA 将监视所有计算机帐户的行为以及环境中的所有其他实体。

## ATA 是否支持多域和多林？
Microsoft 高级威胁分析正式版将支持具有相同林边界的多域。 林本身是实际的“安全边界”，因此，提供多域支持可让使用 ATA 的客户 100% 覆盖其环境。

## 是否可以看到部署的总体运行状况？
是的，你可以查看部署的总体运行状况，以及与配置、连接等相关的具体问题，在发生这些问题时，系统会发出警报。


## 另请参阅
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量规划](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [配置事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [配置 Windows 事件转发](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO3-->


