---
# required metadata

title: 更改 ATA 配置 - IIS 证书 | Microsoft 高级威胁分析
description: 说明如何更改 IIS 用于 ATA 中心的证书。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 更改 ATA 配置 - IIS 证书

>[!div class="step-by-step"]
[« ATA 控制台 IP 地址](modifying-ata-config-consoleip.md)
[域连接密码 »](modifying-ata-config-dcpassword.md)

## 更改 IIS 证书
在控制台中，你可以选择和更改 ATA 中心服务的证书，但不能更改 IIS 使用的证书。

若要更改 IIS 使用的证书，请按以下过程操作：

> [!NOTE]
> 修改 IIS 证书以后，应先下载 ATA 网关安装程序包，然后安装新的 ATA 网关。

如需修改 IIS 用于 ATA 中心的证书，请通过 ATA 中心服务器执行以下步骤。

1.  在 ATA 中心服务器上安装新证书。

2.  打开 Internet Information Services (IIS) 管理器。

3.  展开服务器的名称，然后展开**站点**。.

4.  选择 Microsoft ATA 控制台站点，然后在**操作**窗格中单击**绑定**。.

    ![ATA 控制台绑定操作](media/ATA-console-change-IP-bindings.jpg)

5.  选择 **HTTPS**，然后单击**编辑**.

6.  在“SSL 证书”下，选择新的证书。

7.  在安装新的 ATA 网关之前，请下载 ATA 网关安装程序包。

>[!div class="step-by-step"]
[« ATA 控制台 IP 地址](modifying-ata-config-consoleip.md)
[域连接密码 »](modifying-ata-config-dcpassword.md)

## 另请参阅
- [使用 ATA 控制台](working-with-ata-console.md)
- [安装 ATA](install-ata.md)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


