---
# required metadata

title: 安装 ATA | Microsoft 高级威胁分析
description: 安装 ATA 时，最后一步是配置短期租约子网和蜜标用户。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安装 ATA - 步骤 6

>[!div class="step-by-step"]
[« 步骤 5](install-ata-step5.md)

## 步骤 6. 配置短期租约子网和蜜标用户
短期租约子网是指其中的 IP 地址分配会在数秒或数分钟之内很快变化的子网。 例如，用于 VPN 的 IP 地址以及 Wi-Fi IP 地址。 若要输入在组织中使用的短期租约子网的列表，请按以下步骤操作：

1.  在 ATA 网关计算机的 ATA 控制台中，单击设置图标，然后选择**配置**。.

    ![ATA 配置设置](media/ATA-config-icon.JPG)

2.  在“检测”下，针对短期租约子网输入以下内容。 使用斜杠表示法格式输入短期租约子网（例如 `192.168.0.0/24`），然后单击加号。

3.  对于蜜标帐户 SID，请输入不会有网络活动的用户帐户的 SID，然后单击加号。 例如： `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > 若要查找用户的 SID，在 ATA 控制台中搜索该用户，然后单击**帐户信息**选项卡。 

4.  配置排除项：你可以配置需要从特定的可疑活动中排除的 IP 地址。 有关详细信息，请参阅[使用 ATA 检测设置](working-with-detection-settings.md)。

5.  单击“保存”.

![保存更改](media/ATA-VPN-Subnets.JPG)

恭喜，你已成功部署 Microsoft 高级威胁分析!

查看攻击时间线以了解检测到的可疑活动，搜索用户或计算机并查看其配置文件。

ATA 将立即启动对可疑活动进行扫描。 某些活动（如某些可疑行为活动）将不可用，直到 ATA 建立行为配置文件（最少需要三个星期）为止。


>[!div class="step-by-step"]
[« 步骤 5](install-ata-step5.md)


## 另请参阅

- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [配置事件收集](configure-event-collection.md)
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


