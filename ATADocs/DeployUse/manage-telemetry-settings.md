---
# required metadata

title: 管理遥测设置 | Microsoft 高级威胁分析
description: 描述 ATA 收集的数据，并提供关闭数据收集功能所需的步骤。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 管理遥测设置
高级威胁分析 (ATA) 收集有关 ATA 的匿名遥测数据，并通过 HTTPS 连接将数据传输到 Microsoft 服务器。  Microsoft 利用该数据来改进未来版本的 ATA。

## 收集的数据
收集的匿名数据包括以下内容：

-   ATA Center 和 ATA 网关提供的性能计数器

-   来自 ATA 的许可副本的产品 ID

-   ATA 中心的部署日期

-   已部署的 ATA 网关数

-   以下匿名 Active Directory 信息：

    -   按字母顺序对域名排序时将排在首位的域的域 ID

    -   域控制器数

    -   由 ATA 通过端口镜像监视的域控制器数

    -   站点数

    -   计算机数量

    -   组数

    -   用户数

-   可疑活动 – 针对每个可疑活动收集以下匿名数据：

    （计算机名称、用户名称和 IP 地址**不**收集）

    -   可疑活动类型

    -   可疑活动 ID

    -   状态

    -   开始时间和结束时间

    -   提供的输入

### 禁用数据收集
若要停止收集遥测数据并将其发送到 Microsoft，请按以下步骤操作：

1.  登录到 ATA 控制台，单击工具栏中的三点式省略号，然后选择**关于**。

2.  取消选中“向我们发送使用情况信息，帮助我们在将来改进客户体验”所对应的框。

## 另请参阅
- [1.6 版新增功能](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


