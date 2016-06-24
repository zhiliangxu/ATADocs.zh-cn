---
# required metadata

title: 使用 ATA 检测设置 | Microsoft 高级威胁分析
description: 介绍如何配置一个使用环境不同寻常，并且其处理方式与网络中其他实体有所不同的 IP 地址和子网列表
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用 ATA 检测设置
“检测”配置页可让你配置一个使用环境不同寻常，并且其处理方式与网络中其他实体略有不同的 IP 地址和子网列表。

## 设置检测
在“检测”页上，你可以定义以下项：

-   **短期租约子网** - 如果你组织中任何子网上的 IP 地址期限极短（例如，VPN IP 地址子网或 Wi-Fi 子网），则你必须将这些 IP 地址和子网输入 ATA，以便 ATA 知道要存储计算机与这些范围中期限比其他 IP 地址更短的 IP 地址之间的关联。

-   **蜜标帐户 SID** – 这是应该没有任何网络活动的用户帐户。 此帐户将配置为 ATA 蜜标用户。 如果有人尝试使用此用户帐户，ATA 将创建可疑活动，表明出现了恶意活动。 若要配置蜜标用户，你需要使用该用户帐户的 SID 而不是用户名。

可以从以下检测中排除 IP 地址。 如果你输入其中一个列表中的 IP 地址，ATA 将从此特定类型的检测活动中排除该 IP 地址。

-   DNS 侦测 IP 地址排除

-   传递票证 IP 地址排除

## 另请参阅
- [处理可疑活动](working-with-suspicious-activities.md)
- [修改 ATA 配置](modifying-ata-configuration.md)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


