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

## 为 ATA 配置电子邮件服务器设置
ATA 可以在检测到可疑活动时向你发出通知。 若要使 ATA 能够发送电子邮件通知，必须首先配置**电子邮件服务器设置**.

1.  在 ATA 中心服务器上，单击桌面上的“Microsoft 高级威胁分析管理”图标。

2.  输入你的用户名和密码，然后单击**登录**.

3.  选择工具栏上的设置选项，然后选择**配置**.

    ![ATA 配置设置图标](media/ATA-config-icon.JPG)

4.  在**常规**选项卡中的**电子邮件服务器**下，输入下列信息：

    |字段|描述|值|
    |---------|---------------|---------|
    |SMTP 服务器终结点（必需）|输入 SMTP 服务器的 FQDN。|例如：<br />smtp.contoso.com|
    |SSL|如果 SMTP 服务器需要 SSL，则切换到 SSL。 **注意：**如果启用 SSL，则还需更改端口号。|默认值为“禁用”|
    |身份验证|如果 SMTP 服务器需要身份验证，则请启用。 **注意：**如果启用身份验证，则必须提供有权连接到 SMTP 服务器的电子邮件帐户的用户名和密码。|默认值为“禁用”|
    |发送方（必需）|输入电子邮件发送方的电子邮件地址。|例如：<br />ATA@contoso.com|
    ![ATA 电子邮件服务器设置图像](media/ATA-email-server.png)

## 为 ATA 配置 Syslog 服务器设置
ATA 可以在检测到可疑活动时通过将通知发送到 Syslog 服务器来通知你。 如果启用 Syslog 通知，则可为其设置以下内容。

1.  在配置 Syslog 通知之前，请与 SIEM 管理员一起找出以下信息：

    -   SIEM 服务器的 FQDN 或 IP 地址

    -   SIEM 服务器正在侦听的端口

    -   要使用的传输类型：UDP、TCP 或 TLS（受保护的 Syslog）

    -   发送数据时采用的格式：RFC 3164 或 5424

2.  在 ATA 中心服务器上，单击桌面上的“Microsoft 高级威胁分析管理”图标。

3.  输入你的用户名和密码，然后单击**登录**.

4.  选择工具栏上的设置选项，然后选择**配置**.

    ![ATA 配置设置图标](media/ATA-config-icon.JPG)

5.  选择 **Syslog 服务器**并输入以下信息：

    |字段|描述|
    |---------|---------------|
    |Syslog 服务器终结点|Syslog 服务器的 FQDN|
    |Transport|可以是 UDC、TCP 或 TLS（受保护的 Syslog）|
    |格式|这是将事件发送到 SIEM 服务器时 ATA 使用的格式 - RFC 5424 或 RFC 3164。|





## 另请参阅
[查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


