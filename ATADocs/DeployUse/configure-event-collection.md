---
# required metadata

title: 配置事件收集 | Microsoft 高级威胁分析
description: 介绍通过 ATA 配置事件收集时可用的选项
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 配置事件收集
若要增强检测功能，ATA 需要 Windows 事件日志 ID 4776。 此事件可通过两种方法之一转发到 ATA 网关：将 ATA 网关配置为侦听 SIEM 事件，或者[配置 Windows 事件转发](#configuring-windows-event-forwarding).

## 事件收集
除了收集和分析传入和传出域控制器的网络流量以外，ATA 还可以使用 Windows 事件 4776 来进一步增强 ATA 传递哈希检测。 可以从 SIEM 接收此事件，或者通过从域控制器设置 Windows 事件转发来接收此事件。 收集的事件将为 ATA 提供更多信息，而这些信息无法通过域控制器网络流量来获得。

### SIEM/Syslog
要使 ATA 能够使用 Syslog 服务器中的数据，你需要执行下列操作：

-   配置一个 ATA 网关服务器用于侦听和接受 SIEM/Syslog 服务器转发的事件。

-   将你的 SIEM/Syslog 服务器配置为向 ATA 网关转发特定的事件。

> [!IMPORTANT]
> -   不要将所有 Syslog 数据转发到 ATA 网关。
> -   ATA 支持来自 SIEM/Syslog 服务器的 UDP 流量。

有关如何配置为向另一台服务器转发特定事件的信息，请参阅 SIEM/Syslog 服务器的产品文档。 

### Windows 事件转发
如果你未使用 SIEM/Syslog 服务器，可将 Windows 域控制器配置为转发要由 ATA 收集和分析的 Windows 事件 ID 4776。 Windows 事件 ID 4776 提供有关 NTLM 身份验证的数据。

## 将 ATA 网关配置为侦听 SIEM 事件

1.  在 ATA 网关配置中，启用**Syslog 侦听器 UDP**.

    如下图中所述设置侦听 IP 地址。 默认端口为 514。

    ![启用 syslog 侦听器 UDP 的图像](media/ATA-enable-siem-forward-events.png)

2.  将 SIEM 或 Syslog 服务器配置为向上面所选的 IP 地址转发 Windows 事件 ID 4776。 有关配置 SIEM 的更多信息，请参阅 SIEM 联机帮助；有关每个 SIEM 服务器的具体格式化要求，请参阅技术支持选项。

### SIEM 支持
ATA 支持采用以下格式的 SIEM 事件：

#### RSA 安全分析
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Syslog 标头是可选的。

-   所有字段之间需要有“\n”字符分隔符。

-   字段依次为：

    1.  RsaSA 常量（必须显示）。

    2.  实际事件的时间戳（请确保它不是抵达 SIEM 时或者发送到 ATA 时的时间戳）。 精度最好是毫秒，这一点非常重要。

    3.  Windows 事件 ID

    4.  Windows 事件提供程序名称

    5.  Windows 事件日志名称

    6.  接收事件的计算机的名称（在本例中为 DC）

    7.  进行身份验证的用户的名称

    8.  源主机名

    9. NTLM 的结果代码

-   顺序很重要，消息中不应包含其他任何信息。

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|The domain controller attempted to validate the credentials for an account.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   必须遵守协议定义。

-   无 syslog 标头。

-   标头部分（用竖线分隔的部分）必须存在（如协议中所述）。

-   事件的 _Extension_ 部分中必须存在以下键：

    -   externalId = Windows 事件 ID

    -   rt = 实际事件的时间戳（请确保它不是抵达 SIEM 时或者发送给我们时的时间戳）。 精度最好是毫秒，这一点非常重要。

    -   cat = Windows 事件日志名称

    -   shost = 源主机名

    -   dhost = 接收事件的计算机（在本例中为 DC）

    -   duser = 进行身份验证的用户

-   _Extension_ 部分的顺序并不重要

-   这两个字段必须有一个自定义键和 keyLable：

    -   “EventSource”

    -   “Reason or Error Code” = NTLM 的结果代码

#### Splunk
&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

尝试验证帐户凭据的计算机。

身份验证包：MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

登录帐户：Administrator

源工作站：SIEM

错误代码：0x0

-   Syslog 标头是可选的。

-   所有必填字段之间有“\r\n”字符分隔符。

-   字段采用“键=值”格式。

-   以下键必须存在并且具有值：

    -   EventCode = Windows 事件 ID

    -   Logfile = Windows 事件日志名称

    -   SourceName = Windows 事件提供程序名称

    -   TimeGenerated = 实际事件的时间戳（请确保它不是抵达 SIEM 时或者发送到 ATA 时的时间戳）。 格式应与 yyyyMMddHHmmss.FFFFFF 匹配，精度最好是毫秒，这一点非常重要。

    -   ComputerName = 源主机名

    -   Message = Windows 事件中的原始事件文本

-   Message 键和值必须是 last。

-   “键=值”对的顺序并不重要。

#### QRadar
QRadar 通过代理启用事件收集。 如果使用代理来收集数据，则无需毫秒数据即可收集时间格式。 由于 ATA 要求毫秒数据，因此有必要将 QRadar 设置为使用无代理的 Windows 事件收集。 相关详细信息，请参阅 [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol")（QRadar：使用 MSRPC 协议的无代理 Windows 事件收集）.

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

所需的字段是：

- 集合的代理类型
- Windows 事件日志提供程序名称
- Windows 事件日志源
- DC 完全限定的域名
- Windows 事件 ID

TimeGenerated 是实际事件的时间戳（请确保它不是抵达 SIEM 时或者发送到 ATA 时的时间戳）。 格式应与 yyyyMMddHHmmss.FFFFFF 匹配且精度最好是毫秒，这一点非常重要。

Message 是 Windows 事件中的原始事件文本

请确保“键=值”对之间有 \t。

>[!NOTE] 不支持使用 WinCollect for Windows 事件收集。

## 配置 Windows 事件转发
如果你没有 SIEM 服务器，可以将域控制器配置为向 ATA 网关之一直接转发 Windows 事件 ID 4776。

1.  以管理员权限使用域帐户登录到所有域控制器和 ATA 网关计算机。
2. 确保连接到的所有域控制器和 ATA 网关都已加入同一个域。
3.  在每个域控制器上，在提升的命令提示符下键入以下命令：
```
winrm quickconfig
```
4.  在 ATA 网关上，在提升的命令提示符下键入以下命令：
```
wecutil qc
```
5.  在每个域控制器上的“Active Directory 用户和计算机”中，导航到“内置”文件夹并双击“事件日志读取器”组。<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
右键单击该组，然后选择“属性”。 在“成员”选项卡上，添加每个 ATA 网关的计算机帐户。
![wef_ad 事件日志读取器弹出窗口](media/wef_ad-event-log-reader-popup.png)
6.  在 ATA 网关上打开事件查看器，然后右键单击**订阅**并选择**创建订阅**.  

    a. 在“订阅类型和源计算机”下单击“选择计算机”，然后添加域控制器并测试连接。
    ![wef_subscription prop](media/wef_subscription-prop.png)

    b。 在“要收集的事件”下，单击“选择事件”。 选择“日志”，然后向下滚动并选择“安全性”。 然后，在**包括/排除事件 ID**中键入**4776**.<br>
    ![wef_4776](media/wef_4776.png)

    c. 在**更改用户帐户或配置高级设置**下，单击**高级**.
将**协议**设置为**HTTP**，将**端口**设置为**5985**.<br>
    ![wef_http](media/wef_http.png)

7.  [可选] 如果你希望轮询间隔更短，请在 ATA 网关上将订阅检测信号设置为 5 秒，以加快轮询速率。
    wecutil ss <CollectionName>/cm:custom
    wecutil ss <CollectionName> /hi:5000

8. 在 ATA 网关配置页上启用 **Windows 事件转发收集**.

> [!NOTE]
启用此设置后，ATA 网关将在“已转发事件”日志中查找域控制器向它转发的 Windows 事件。

有关详细信息，请参阅[配置计算机以转发和收集事件](https://technet.microsoft.com/en-us/library/cc748890)

## 另请参阅
- [安装 ATA](install-ata.md)
- [查看 ATA 论坛！！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


