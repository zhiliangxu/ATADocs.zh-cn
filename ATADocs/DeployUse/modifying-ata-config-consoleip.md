---
# required metadata

title: 更改 ATA 配置 - ATA 控制台 IP 地址 | Microsoft 高级威胁分析
description: 介绍如何更改 ATA 控制台的 IP 地址，该 IP 地址用于在 ATA 网关上创建 ATA 控制台的快捷方式。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 更改 ATA 配置 - ATA 控制台 IP 地址

>[!div class="step-by-step"]
[« ATA 中心证书](modifying-ata-config-centercert.md)
[IIS 证书 »](modifying-ata-config-iiscert.md)

## 更改 ATA 控制台 IP 地址
默认情况下，ATA 控制台 URL 是你在安装 ATA 中心时为 ATA 控制台选择的 IP 地址。

URL 用于以下情形：

-   安装 ATA 网关 – ATA 网关在安装以后，会自行注册到 ATA 中心。 连接到 ATA 控制台即可完成此注册过程。 如果为 ATA 控制台 URL 输入 FQDN，则需确保 ATA 网关可将该 FQDN 解析成 ATA 控制台绑定到 IIS 时使用的 IP 地址。 此外，还可以在 ATA 网关上使用该 URL 创建到 ATA 控制台的快捷方式。

-   警报 – ATA 在送出 SIEM 或电子邮件警报时，会提供可疑活动的链接。 该链接的主机部分是 ATA 控制台 URL 设置。

-   如果已安装内部证书颁发机构 (CA) 的证书，则可能需确保该 URL 与证书中的使用者名称相符，这样用户在连接到 ATA 控制台时，就不会出现警告消息。

-   如果对 ATA 控制台 URL 使用 FQDN，则可修改 IIS 用于 ATA 控制台的 IP 地址，而不会违反过去送出的警告，也不需再次重新下载 ATA 网关程序包。 只需使用新 IP 地址更新 DNS。

> [!NOTE]
> 修改 ATA 控制台 URL 以后，应先下载 ATA 网关安装程序包，然后安装新的 ATA 网关。

如需修改 IIS 用于 ATA 控制台的 IP 地址，请在 ATA 中心服务器上执行以下步骤。

1.  在 ATA 中心服务器上安装 IP 地址。

2.  打开 Internet 信息服务 (IIS) 管理器。

3.  展开服务器的名称，然后展开**站点**。.

4.  选择 Microsoft ATA 控制台站点，然后在**操作**窗格中单击**绑定**。.

    ![ATA 控制台绑定操作图像](media/ATA-console-change-IP-bindings.jpg)

5.  选择“HTTP”，然后单击“编辑”以选择新的 IP 地址。 对 **HTTPS** 执行相同的操作，选择相同的 IP 地址。

    ![编辑站点绑定图像](media/ATA-change-console-IP.jpg)

6.  在**操作**窗格的**管理网站**下单击**重启**.

7.  打开管理员命令提示符，然后键入以下命令以更新 HTTP.SYS 驱动程序：

    -   添加新的 IP 地址 - `netsh http add iplisten ipaddress=newipaddress`

    -   查看是否正在使用新地址 - `netsh http show iplisten`

    -   删除旧的 IP 地址 – `netsh http delete iplisten ipaddress=oldipaddress`

8.  如果 ATA 控制台 URL 仍在使用 IP 地址，可将 ATA 控制台 URL 更新为新的 IP 地址，然后在部署新的 ATA 网关之前，下载 ATA 网关安装程序包。

9. 如果该 ATA 控制台 URL 为 FQDN，则可使用该 FQDN 的新 IP 地址对 DNS 进行更新。

>[!div class="step-by-step"]
[« ATA 中心证书](modifying-ata-config-centercert.md)
[IIS 证书 »](modifying-ata-config-iiscert.md)


## 另请参阅
- [使用 ATA 控制台](working-with-ata-console.md)
- [安装 ATA](install-ata.md)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


