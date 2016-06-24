---
# required metadata

title: 安装 ATA - 步骤 2 | Microsoft 高级威胁分析
description: 安装 ATA 时，步骤 2 的目的是帮助你在 ATA 中心服务器上配置域连接设置
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安装 ATA - 步骤 2

>[!div class="step-by-step"] [«步骤 1](install-ata-step1.md)
[步骤 3»](install-ata-step3.md)

## 步骤 2。 配置 ATA 网关的常规设置
**常规**设置选项卡中的设置适用于 ATA Center 托管的所有 ATA 网关。

若要配置常规 ATA 网关，请执行以下操作：

1.  打开 ATA 控制台并登录。 有关说明，请参阅[使用 ATA 控制台](working-with-ata-console.md)。

2.  单击“设置”图标，然后选择**配置**。

    ![ATA 网关配置设置](media/ATA-config-icon.JPG)

3.  在**常规**选项卡上的 **ATA 网关**下，输入以下信息，并单击**保存**。

    |字段|注释|
    |---------|------------|
    |**用户名**（必需）|输入只读用户名，例如 **user1**。|
    |**密码**（必需）|输入只读用户的密码，例如 **Pencil1**。 **注意：**请确保该密码正确。 如果保存了错误的密码，ATA 服务将停止在 ATA 网关服务器上运行。|
    |**域**（必需）|输入只读用户的域，例如 **contoso.com**。 **注意：**必须输入用户所在域的完整 FQDN。 例如，如果用户的帐户所在的域为 corp.contoso.com，则需输入 `corp.contoso.com` 而非 contoso.com|
    |自动更新所有 ATA 网关 |如果启用此设置，在即将发布的版本中，当你更新 ATA Center 时，所有 ATA 网关将会自动更新。|

    ![ATA 域连接设置图像](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"] [«步骤 1](install-ata-step1.md)
[步骤 3»](install-ata-step3.md)


## 另请参阅

- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [配置事件收集](configure-event-collection.md)
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO3-->


