---
# required metadata

title: ATA 错误日志疑难解答 | Microsoft 高级威胁分析
description: 说明如何解决 ATA 中的常见错误 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 错误日志疑难解答
此部分将详细描述 ATA 部署中可能出现的错误以及解决这些问题所需的步骤。
## ATA 网关错误
|错误|描述|解决方法|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: 发生本地错误|ATA 网关无法对域控制器进行身份验证。|1.验证 DNS 服务器中是否正确配置了域控制器的 DNS 记录。 <br>2.验证 ATA 网关的时间是否与域控制器上的时间同步。|
|System.IdentityModel.Tokens.SecurityTokenValidationException: 无法验证证书链|ATA 网关无法验证 ATA Center 的证书。|1.验证是否已在 ATA 网关信任的证书颁发机构证书存储区安装了根 CA 证书。 <br>2.验证证书吊销列表 (CRL) 是否可用，以及是否可以执行证书吊销验证。|
|Microsoft.Common.ExtendedException: 无法分析生成的时间|ATA 网关无法分析从 SIEM 转发的 syslog 消息。|验证是否已将 SIEM 配置为转发采用 ATA 支持的格式之一的消息。|
|System.ServiceModel.FaultException: 验证消息安全性时出错。|ATA 网关无法对 ATA Center 进行身份验证。|验证 ATA 网关的时间是否与 ATA Center 的时间同步。|
|System.ServiceModel.EndpointNotFoundException: 无法连接到 net.tcp://center.ip.addr:443/IEntityReceiver|ATA 网关无法建立与 ATA Center 的连接。|确保网络设置正确且 ATA 网关和 ATA Center 之间的网络连接处于活动状态。|
|System.DirectoryServices.Protocols.LdapException: LDAP 服务器不可用。|ATA 网关无法查询使用 LDAP 协议的域控制器。|1.验证连接到 Active Directory 域的 ATA 使用的用户帐户具有对 Active Directory 树中所有对象的读取权限。 <br>2.确保域控制器未强制阻止 ATA 所用的用户帐户使用 LDAP 查询。|
|Microsoft.Tri.Infrastructure.ContractException: 协定异常|ATA 网关无法从 ATA Center 同步配置。|在 ATA 控制台中完成 ATA 网关的配置。|
|System.Reflection.ReflectionTypeLoadException: 无法加载一个或多个请求类型。 有关详细信息，请检索 LoaderExceptions 的属性。|ATA 网关上已安装 Message Analyzer。| 卸载 Message Analyzer。|
|错误[布局] System.OutOfMemoryException: 引发类型 “System.OutOfMemoryException” 异常。|ATA 网关内存不足。|增加域控制器上的内存量。|
|实时使用者启动失败---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: PEFNDIS 事件提供程序未准备就绪|未正确安装 PEF (Message Analyzer)。|请联系支持人员以获取解决方法。|
|安装失败，错误代码为: 0x80070652|计算机上有其他安装待处理。|等待其他安装完成，如有必要，请重启计算机。|

## ATA 控制台错误
|错误|描述|解决方法|
|-------------|----------|---------|
|HTTP 错误 500.19 - 内部服务器错误|IIS URL 重写模块无法正确安装。|卸载并重新安装 IIS URL 重写模块。<br>[下载 IIS URL 重写模块](http://go.microsoft.com/fwlink/?LinkID=615137)|

## 部署错误
|错误|描述|解决方法|
|-------------|----------|---------|
|.Net Framework 4.6.1 安装失败，错误为 0x800713ec|服务器上未安装 .Net Framework 4.6.1 的必备组件。 |在安装 ATA 之前，验证服务器上是否已安装 Windows 更新 [KB2919442](https://www.microsoft.com/en-us/download/details.aspx?id=42135) 和 [KB2919355](https://support.microsoft.com/en-us/kb/2919355)。|

![ATA .NET 安装错误图像](media/netinstallerror.png)


## 另请参阅
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量规划](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [配置事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [配置 Windows 事件转发](/advanced-threat-analytics/deploy-use/configure-event-collection#ATA_event_WEF)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


