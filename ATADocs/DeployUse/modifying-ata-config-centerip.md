---
# required metadata

title: 更改 ATA 配置 - ATA 中心 IP 地址 | Microsoft 高级威胁分析
description: 说明如何更改 ATA 中心的 IP 地址、端口或证书。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 更改 ATA 配置 - ATA 中心 IP 地址

>[!div class="step-by-step"]
[ATA 中心证书 »](modifying-ata-config-centercert.md)

完成初始部署以后，对 ATA 中心进行修改时应格外小心。 更新 IP 地址和端口或证书时，请按以下过程操作。

## 更改 ATA 中心服务器所使用的 IP 地址
若需更改 ATA 中心 IP 地址和端口或证书，则要考虑以下因素。

ATA 网关通过本地方式存储需连接到的 ATA 中心的 IP 地址。 ATA 网关会定期连接到 ATA 中心并拉取配置更改。 更改 ATA 网关连接到 ATA 中心的方式需分两阶段进行。

-   第一阶段 – 更新你希望 ATA 中心服务使用的 IP 地址和端口。 此时 ATA 中心仍在原始 IP 地址上侦听，而下一次 ATA 网关同步其配置时，该网关会有两个用于 ATA 中心的 IP 地址。 如果能够使用原始（首个）IP 地址进行连接，ATA 网关不会尝试使用新的 IP 地址和端口。

-   第二阶段 – 在所有 ATA 网关都与已更新配置同步后，激活 ATA 中心所侦听的新 IP 地址和端口。 激活新 IP 地址后，ATA 中心服务将绑定到这个新的 IP 地址。 ATA 网关将无法连接到原始地址，现在会尝试通过第二个（新的）用于 ATA 中心的 IP 地址进行连接。 使用新的 IP 地址连接到 ATA 中心以后，ATA 网关会拉取最新的配置，会有一个适用于 ATA 中心的 IP 地址。 （重新启动该过程的情况除外。）

> [!NOTE]
> -   如果 ATA 网关在第一阶段已脱机，因此无法获得更新的配置，则需手动更新 ATA 网关上的 JSON 配置文件。
> -   如果新 IP 地址是安装在 ATA 中心服务器上的，则可在更改时从 IP 地址列表中进行选择。 不过，如果你因故无法将 IP 地址安装在 ATA 中心服务器上，则可选择自定义 IP 地址进行手动添加。 你将无法激活新 IP 地址，除非该 IP 地址已安装在服务器上。
> -   如果在激活新 IP 地址后需要部署新的 ATA 网关，则需再次下载 ATA 网关安装程序包。

1.  打开 ATA 控制台。

2.  选择工具栏上的设置选项，然后选择**配置**.

    ![ATA 配置设置图标](media/ATA-config-icon.JPG)

3.  选择**常规**.

4.  在“ATA 中心服务 IP 地址: 端口”下，选择一个现有的 IP 地址，或者先选择“添加自定义 IP 地址”，然后输入 IP 地址。

5.  单击“保存”.

6.  此时会显示一个通知，告知你多少 ATA 网关已同步到最新配置。

    ![ATA 中心已同步网关图像](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >激活新配置前，验证所有 ATA 网关是否已与最新配置同步。 在同步所有 ATA 网关之前激活新配置可能会导致 ATA 网关停止按预期方式正常运行。 如果有任何 ATA 网关没有同步，则单击“激活”时会收到此错误：
    >
    >    ![ATA 网关同步错误](media/ataGW-not-synced.png)


7.  所有 ATA 网关同步以后，单击“激活”激活新 IP 地址。

    > [!NOTE]
    > 如果输入了自定义 IP 地址，则除非你已在 ATA 中心安装 IP 地址，否则无法单击“激活”。

8.  确保在激活所做的更改以后，所有 ATA 网关都能同步其配置。 通知栏会指示有多少 ATA 网关成功同步了其配置。

>[!div class="step-by-step"]
[更改 ATA 中心证书 »](modifying-ata-config-centercert.md)


## 另请参阅
- [使用 ATA 控制台](working-with-ata-console.md)
- [安装 ATA](install-ata.md)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


