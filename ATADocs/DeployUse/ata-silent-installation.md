---
# required metadata

title: 无提示安装 ATA | Microsoft 高级威胁分析
description: 介绍如何无提示安装 ATA。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 无提示安装
本文提供相关说明以实现 ATA 的无提示安装。
## 先决条件

Microsoft ATA v1.6 需要安装 Microsoft .NET Framework 4.6.1。 

在安装或更新 ATA 时，.Net Framework 4.6.1 将作为 Microsoft ATA 部署的一部分自动安装。

> [!Note] 安装 .Net Framework 4.6.1 可能需要重启服务器。 在域控制器上安装 ATA 网关时，请考虑为这些域控制器计划一个维护时段。
使用 ATA 无提示安装方法时，安装程序将配置为在安装结束时自动重启服务器（如有必要）。 若要避免在安装期间重启服务器，请使用 `-NoRestart` 标志。 在安装期间需要使用 `-NoRestart` 标记和进行重启的情况下，安装程序将暂停，直到服务器重启。 若要跟踪部署进度，请监视位于 **%AppData%\Local\Temp** 的 ATA 安装程序日志.


## 安装 ATA 中心

使用以下命令安装 ATA Center：

**语法**：

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**安装选项**：

|Name|语法|强制使用无提示安装？|说明|
|-------------|----------|---------|---------|
|无提示|/quiet|是|运行安装程序，不显示任何 UI 和提示。|
|NoRestart|/norestart|否|禁止任何重启尝试。 默认情况下，将在重启前提示 UI。|
|帮助|/help|否|提供帮助和快速参考。 显示安装程序命令的正确用法，列出所有选项和行为。|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安装的参数。 必须设置为强制执行 .Net Framework 的无提示安装。|
|LicenseAccepted|--LicenseAccepted|是|指示已阅读并批准该许可证。 必须设置为无提示安装。|

**安装参数**：

|Name|语法|强制使用无提示安装？|说明|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath=“<InstallPath>”|否|设置 ATA 二进制文件的安装路径。 默认路径：C:\Program Files\Microsoft Advanced Threat Analytics\Center|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|否|设置 ATA 数据库数据文件夹的路径。 默认路径：C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|是|设置 ATA Center 服务的 IP 地址|
|CenterPort|CenterPort=<CenterPort>|是|设置 ATA Center 服务的网络端口|
|CenterCertificateThumbprint|CenterCertificateThumbprint=“<CertThumbprint>”|否|设置 ATA Center 服务的证书指纹。 此证书用于确保 ATA Center 与 ATA 网关之间的通信。 如果未设置，安装将生成自签名证书。|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|是|设置 ATA 控制台的 IP 地址|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint=”<CertThumbprint >”|否|指定 ATA 控制台的证书指纹。 此证书用于验证 ATA 控制台网站的标识。如果未指定，安装将生成自签名证书。|

**示例**：
使用默认安装路径和单个 IP 地址安装 ATA Center：

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

使用默认安装路径、两个 IP 地址，以及用户定义的证书指纹安装 ATA Center：

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## 更新 ATA 中心

使用以下命令更新 ATA Center：

**语法**：

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**安装选项**：

|Name|语法|强制使用无提示安装？|说明|
|-------------|----------|---------|---------|
|无提示|/quiet|是|运行安装程序，不显示任何 UI 和提示。|
|NoRestart|/norestart|否|禁止任何重启尝试。 默认情况下，将在重启前提示 UI。|
|帮助|/help|否|提供帮助和快速参考。 显示安装程序命令的正确用法，列出所有选项和行为。|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安装的参数。 必须设置为强制执行 .Net Framework 的无提示安装。|


更新 ATA 时，安装程序将自动检测服务器上是否安装了 ATA，且无需更新安装选项。

**示例**：
无提示更新 ATA Center。 在大型环境中，ATA Center 更新需要一段时间才能完成。 监视 ATA 日志以跟踪更新进度。

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## 无提示卸载 ATA Center

使用以下命令执行无提示卸载 ATA Center：
**语法**：

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**安装选项**：

|Name|语法|强制使用无提示卸载？|说明|
|-------------|----------|---------|---------|
|无提示|/quiet|是|运行卸载程序，不显示任何 UI 和提示。|
|“卸载”|/uninstall|是|从服务器中运行 ATA Center 的无提示卸载。|
|NoRestart|/norestart|否|禁止任何重启尝试。 默认情况下，将在重启前提示 UI。|
|帮助|/help|否|提供帮助和快速参考。 显示安装程序命令的正确用法，列出所有选项和行为。|

**安装参数**：

|Name|语法|强制使用无提示卸载？|说明|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|否|删除现有数据库中的所有文件。|

**示例**：
若要从服务器中无提示卸载 ATA Center，请删除现有的所有数据库数据：


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## ATA 网关无提示安装
使用以下命令无提示安装 ATA 网关：

**语法**：

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**安装选项**：

|Name|语法|强制使用无提示安装？|说明|
|-------------|----------|---------|---------|
|无提示|/quiet|是|运行安装程序，不显示任何 UI 和提示。|
|NoRestart|/norestart|否|禁止任何重启尝试。 默认情况下，将在重启前提示 UI。|
|帮助|/help|否|提供帮助和快速参考。 显示安装程序命令的正确用法，列出所有选项和行为。|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安装的参数。 必须设置为强制执行 .Net Framework 的无提示安装。|
|LicenseAccepted|--LicenseAccepted|是|指示已阅读并批准该许可证。 必须设置为无提示安装。|

**安装参数**：

|Name|语法|强制使用无提示安装？|说明|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint=”<CertThumbprint >”|否|设置 ATA Center 服务的证书指纹。 此证书用于确保 ATA Center 与 ATA 网关之间的通信。 如果未设置，安装将生成自签名证书。|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|是|设置用户帐户名称 (user@domain.com)，该名称用于向 ATA Center 注册 ATA 网关。|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|是|设置用户帐户密码 (user@domain.com)，该密码用于向 ATA Center 注册 ATA 网关。|

**示例**：
无提示安装 ATA 网关，并使用指定的凭据将其注册到 ATA Center ：

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## 更新 ATA 网关

使用以下命令无提示更新 ATA 网关：

**语法**：

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**安装选项**：

|Name|语法|强制使用无提示安装？|说明|
|-------------|----------|---------|---------|
|无提示|/quiet|是|运行安装程序，不显示任何 UI 和提示。|
|NoRestart|/norestart|否|禁止任何重启尝试。 默认情况下，将在重启前提示 UI。|
|帮助|/help|否|提供帮助和快速参考。 显示安装程序命令的正确用法，列出所有选项和行为。|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安装的参数。 必须设置为强制执行 .Net Framework 的无提示安装。|


**示例**：
无提示更新 ATA 网关：

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## 无提示卸载 ATA 网关

使用以下命令执行无提示卸载 ATA 网关：
**语法**：

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**安装选项**：

|Name|语法|强制使用无提示卸载？|说明|
|-------------|----------|---------|---------|
|无提示|/quiet|是|运行卸载程序，不显示任何 UI 和提示。|
|“卸载”|/uninstall|是|从服务器中运行 ATA 网关的无提示卸载。|
|NoRestart|/norestart|否|禁止任何重启尝试。 默认情况下，将在重启前提示 UI。|
|帮助|/help|否|提供帮助和快速参考。 显示安装程序命令的正确用法，列出所有选项和行为。|

**示例**：
从服务器中无提示卸载 ATA 网关：


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## 另请参阅

- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [配置事件收集](configure-event-collection.md)
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)

<!--HONumber=May16_HO1-->


