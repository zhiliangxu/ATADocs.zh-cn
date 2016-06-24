---
# required metadata

title: 更改 ATA 配置 - ATA 中心证书 | Microsoft 高级威胁分析
description: 说明在 ATA 中心服务器上对本地计算机存储中的证书进行续订或更换所需的两阶段过程。 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 更改 ATA 配置 - ATA 中心证书

>[!div class="step-by-step"]
[« ATA 中心服务器 IP 地址](modifying-ata-config-centerip.md)
[ATA 控制台 IP 地址 »](modifying-ata-config-consoleip.md)

## 更改 ATA 中心证书
在 ATA 中心服务器上的本地计算机存储中安装新证书以后，如果该证书过期，则需续订或进行更换，此时请按如下所示的两阶段过程对证书进行更换：

-   第一阶段 – 更新你希望 ATA 中心服务使用的证书。 此时 ATA 中心服务仍绑定到原始证书。 ATA 网关在同步其配置时，可以使用两个证书进行有效的身份互证。 如果能够使用原始证书进行连接，ATA 网关不会尝试使用新的证书。

-   第二阶段 – 在所有 ATA 网关都与已更新配置同步后，即可激活 ATA 中心服务所绑定到的新证书。 激活新证书后，ATA 中心服务将绑定到该证书。 ATA 网关将无法正确地对 ATA 中心服务实施身份互证，因此会尝试对第二个证书进行身份验证。 连接到 ATA 中心服务以后，ATA 网关会拉取最新的配置，会有一个适用于 ATA 中心的证书。 （重新启动该过程的情况除外。）

> [!NOTE]
> -   如果 ATA 网关在第一阶段已脱机，因此无法获得更新的配置，则需手动更新 ATA 网关上的 JSON 配置文件。
> -   你所使用的证书必须受 ATA 网关信任。
> -   如果在激活新证书后需要部署新的 ATA 网关，则需再次下载 ATA 网关安装程序包。

1.  打开 ATA 控制台。

2.  选择工具栏上的设置选项，然后选择**配置**.

    ![ATA 配置设置图标](media/ATA-config-icon.JPG)

3.  选择 **ATA Center**。.

4.  在“证书”下，选择列表中的一个证书。

5.  单击“保存”.

6.  此时会显示一个通知，告知你多少 ATA 网关已同步到最新配置。

7.  所有 ATA 网关同步以后，单击“激活”激活新证书。
    >[!IMPORTANT]
    >激活新配置前，验证所有 ATA 网关是否已与最新配置同步。 在同步所有 ATA 网关之前激活新配置可能会导致 ATA 网关停止按预期方式正常运行。 如果有任何 ATA 网关没有同步，则单击“激活”时会收到此错误：
    >
    >    ![ATA 网关同步错误](media/ataGW-not-synced.png)

8.  确保在激活所做的更改以后，所有 ATA 网关都能同步其配置。

>[!div class="step-by-step"]
[« ATA 中心服务器 IP 地址](modifying-ata-config-centerip.md)
[ATA 控制台 IP 地址 »](modifying-ata-config-consoleip.md)

## 另请参阅
- [使用 ATA 控制台](working-with-ata-console.md)
- [安装 ATA](install-ata.md)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


