---
# required metadata

title: 设置 ATA 通知 | Microsoft 高级威胁分析
description: 说明如何让 ATA 在检测到可疑活动时通知你（通过电子邮件或通过 ATA 事件转发） 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 设置 ATA 通知
ATA 可以在检测到可疑活动时通知你，通知方式可以是电子邮件，也可以是 ATA 事件转发，即将事件转发到你的 SIEM/Syslog 服务器。 在选择你想要接收的通知类型之前，请[设置你的电子邮件服务器和 Syslog 服务器](setting-syslog-email-server-settings.md)。

> [!NOTE]
> -   电子邮件通知包含一个链接，将用户直接带到检测到的可疑活动。 该链接的主机名部分取自“ATA 中心”页上 ATA 控制台 URL 的设置。 默认情况下，ATA 控制台 URL 是在 ATA 中心安装过程中选择的 IP 地址。  若要配置电子邮件通知，建议使用 FQDN 作为 ATA 控制台 URL。
> -   通知会从 ATA Center 发送到 SMTP 服务器和 Syslog 服务器。

若要接收电子邮件通知，请设置以下各项：


1. 在 ATA 控制台中，选择工具栏上的设置选项，然后选择**配置**。
![ATA 配置设置图标](media/ATA-config-icon.JPG)

2. 选择**通知**。
3. 在**电子邮件通知**下，使用切换以选择应发送的通知类型：


    - 检测到新的可疑活动
    - 检测到新的运行状况问题
    - 有可用的新软件更新

4. 指定将通过电子邮件接收通知的收件人。

    [!注意：] 可疑活动电子邮件通知仅在可疑活动已产生的情况下发送。


5. 单击“保存” 。

若要接收 Syslog 通知，请设置以下各项：


1. 在 ATA 控制台中，选择工具栏上的设置选项，然后选择**配置**。
![ATA 配置设置图标](media/ATA-config-icon.JPG)

2. 选择**通知**。
3. 在 **Syslog 通知**下，使用切换以选择应发送的通知类型：


    - 检测到新的可疑活动
    - 已更新现有的可疑活动
    - 检测到新的运行状况问题
5. 单击“保存” 。
![ATA 通知设置图片](media/ATA-notification-settings.png)




## 另请参阅
[查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


