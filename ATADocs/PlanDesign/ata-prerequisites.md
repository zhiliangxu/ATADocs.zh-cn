---
# required metadata

title: ATA 先决条件 | Microsoft 高级威胁分析
description: 介绍在环境中成功部署 ATA 所要满足的要求
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 先决条件
本文介绍在环境中成功部署 ATA 所要满足的要求。

>[!NOTE]若要了解如何计划资源和容量，请参阅 [ATA 容量计划](ata-capacity-planning.md)。


ATA 由 ATA Center、ATA 网关和/或 ATA 轻型网关组成。 有关 ATA 组件的详细信息，请参阅 [ATA 体系结构](ata-architecture.md)。


[开始之前](#before-you-start)：此部分列出在开始安装 ATA 之前，应收集的信息以及要准备好的帐户和网络实体。

[ATA 中心](#ata-center-requirements)：此部分列出 ATA 中心硬件、软件要求以及需要在 ATA 中心服务器上配置的设置。

[ATA 网关](#ata-gateway-requirements)：此部分列出 ATA 网关硬件、软件要求以及需要在 ATA 网关服务器上配置的设置。

[ATA 轻型网关](#ata-lightweight-gateway-requirements)：此部分列出了 ATA 轻型网关硬件和软件要求。

[ATA 控制台](#ata-console)：此部分列出运行 ATA 控制台所要满足的浏览器要求。

![ATA 体系结构图](media/ATA-architecture-topology.jpg)

## 开始之前
本部分列出在开始安装 ATA 之前，应收集的信息以及要准备好的帐户和网络实体。


-   用户帐户和密码，两者均对要监视的域中的所有对象具有读取访问权限。

    > [!NOTE]如果你在域中的不同组织单位 (OU) 上设置了自定义 ACL，请确保所选用户对这些 OU 拥有读取权限。

-   具备网络中用于 VPN 和 Wi-Fi 的所有子网的列表，这些子网可在极短时间内（数秒或数分钟）重新分配设备间的 IP 地址。  到时你需要找出这些短期租约子网，以便 ATA 可以减少其缓存生存期来适应设备之间的快速重新分配。 有关短期租约子网配置，请参阅[安装 ATA](/advanced-threat-analytics/deploy-use/install-ata)。
-   请确保 ATA 网关或 ATA 中心上未安装 Message Analyzer 和 Wire Shark。
-    可选：用户应该对“已删除对象”容器拥有只读权限。 这样，ATA 便可以检测域中的对象批量删除。 有关配置对“已删除对象”容器的只读权限的信息，请参阅 [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx)（查看或设置对目录对象的权限）主题中的 **Changing permissions on a deleted object container**（更改对已删除对象容器的权限）部分。

-   可选：没有网络活动的用户的用户帐户。 此帐户将配置为 ATA 蜜标用户。 若要配置蜜标用户，你需要使用该用户帐户的 SID 而不是用户名。

-   可选：除了收集和分析传入和传出域控制器的网络流量以外，ATA 还可以使用 Windows 事件 4776 来进一步增强 ATA 传递哈希检测。 可以从 SIEM 接收此事件，或者通过从域控制器设置 Windows 事件转发来接收此事件。 收集的事件将为 ATA 提供更多信息，而这些信息无法通过域控制器网络流量来获得。


## ATA 中心要求
本部分列出 ATA 中心的要求。
### 常规
支持将 ATA 中心安装在运行 Windows Server 2012 R2 的服务器上。 可以在属于域或工作组的服务器上安装 ATA 中心。

支持将 ATA 中心作为虚拟机安装。 

如果将 ATA 中心作为虚拟机运行，请先关闭服务器，然后创建新的检查点以避免潜在的数据库损坏。
### 服务器规格
ATA 数据库要求你在 BIOS 中**禁用**非一致性内存访问 (NUMA)。 你的系统可能将 NUMA 识别为节点交错，此情况下必须**启用**节点交错以禁用 NUMA。 有关详细信息，请参阅 BIOS 文档。<br>
为优化性能，请将 ATA Center 的**电源选项**设置为**高性能**。<br>
要监视的域控制器数量和域控制器上的负载规定了所需的服务器规范，请参阅 [ATA 容量计划](ata-capacity-planning.md)了解详细信息。

### 时间同步
ATA Center 服务器、ATA 网关服务器和域控制器的时间必须同步，彼此间的误差不超过 5 分钟。


### 网络适配器
应具有以下内容：
-   至少 1 个网络适配器

-   2 个 IP 地址（建议但非必需）

ATA 中心与 ATA 网关之间的通信将使用端口 443 上的 SSL 进行加密。 此外，ATA 控制台将在 IIS 上运行，并在端口 443 上使用 SSL 进行保护。 建议设置**两个 IP 地址**。 ATA 中心服务将端口 443 绑定到第一个 IP 地址，IIS 将端口 443 绑定到第二个 IP 地址。

> [!NOTE]可使用具有两个不同端口的单个 IP 地址，但建议使用两个 IP 地址。

### 端口
下表列出了使 ATA 中心正常工作而最起码要打开的端口。

在此表中，IP 地址 1 绑定到 ATA Center 服务，IP 地址 2 绑定到 ATA 控制台的 IIS 服务：

|协议|Transport|Port|到/从|Direction|IP 地址|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL**（ATA 通信）|TCP|443，或可配置|ATA 网关|入站|IP 地址 1|
|**HTTP**|TCP|80|公司网络|入站|IP 地址 2|
|**HTTPS**|TCP|443|公司网络和 ATA 网关|入站|IP 地址 2|
|**SMTP**（可选）|TCP|25|SMTP 服务器|出站|IP 地址 2|
|**SMTPS**（可选）|TCP|465|SMTP 服务器|出站|IP 地址 2|
|**Syslog**（可选）|TCP|514|Syslog 服务器|出站|IP 地址 2|

### 证书
确保 ATA Center 有权访问 CRL 分发点。 如果 ATA 网关没有 Internet 访问权限，请遵循[手动导入 CRL 的过程](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx)，但注意要为整个链安装所有 CRL 分发点。

为了便于安装 ATA 中心，你可以在安装 ATA 中心的过程中安装自签名证书。 部署后，你可以将自签名证书替换为来自内部证书颁发机构的、将由 ATA 网关使用的证书。<br>
> [!NOTE]证书的提供程序类型必须是加密服务提供程序 (CSP)。


ATA 中心需要以下服务的证书：

-   Internet Information Services (IIS) – Web 服务器证书

-   ATA 中心服务 – 服务器身份验证证书

> [!NOTE]如果你要从其他计算机访问 ATA 控制台，请确保这些计算机信任 IIS 当前使用的证书，否则在转到登录页之前，会出现一个警告页，指出网站的安全证书有问题。

## ATA 网关要求
本部分列出 ATA 网关的要求。
### 常规
支持将 ATA 网关安装在运行 Windows Server 2012 R2 的服务器上。
可以在属于域或工作组的服务器上安装 ATA 网关。

在安装 ATA 网关之前，请确认是否已安装以下更新：[KB2919355](https://support.microsoft.com/en-us/kb/2919355/)。

可通过运行以下 PowerShell cmdlet 来检查：`[Get-HotFix -Id kb2919355]`

若要了解如何使用带 ATA 网关的虚拟机，请参阅[配置端口镜像](/advanced-threat-analytics/deploy-use/configure-port-mirroring)。

### 服务器规格
为了获得最佳性能，请将 ATA 网关的**电源选项**设置为**高性能**。<br>
根据传入和传出域控制器的网络流量，ATA 网关可支持监视多个域控制器。


### 时间同步
ATA Center 服务器、ATA 网关服务器和域控制器的时间必须同步，彼此间的误差不超过 5 分钟。

### 网络适配器
ATA 网关需要至少一个管理适配器和至少一个捕获适配器：

-   **管理适配器** - 用于在企业网络上通信。 此适配器应采用以下配置：

    -   包括默认网关的静态 IP 地址

    -   首选和备用 DNS 服务器

    -   **此连接的 DNS 后缀**应为每个受监视域的 DNS 域名。

        ![在高级 TCP/IP 设置中配置 DNS 后缀](media/ATA-DNS-Suffix.png)

        > [!NOTE]如果 ATA 网关是域的成员，将自动完成此配置。

-   **捕获适配器** - 用于捕获传入和传出域控制器的流量。

    > [!IMPORTANT]
    > -   将捕获适配器的端口镜像配置为域控制器网络流量的目标。 有关更多信息，请参阅[配置端口镜像](/advanced-threat-analytics/deploy-use/configure-port-mirroring)。 通常，你需要与网络或虚拟化团队合作来配置端口镜像。
    > -   为环境配置一个没有默认网关、也没有 DNS 服务器地址的静态不可路由 IP 地址。 例如 1.1.1.1/32。 这可确保捕获网络适配器可以尽量捕获最多的流量，并且管理网络适配器可用于发送和接收所需的网络流量。

### 端口
下表列出了 ATA 网关要求在管理适配器上配置的最低端口数：

|协议|Transport|Port|到/从|Direction|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP 和 UDP|389|域控制器|出站|
|安全 LDAP (LDAPS)|TCP|636|域控制器|出站|
|LDAP 到全局编录|TCP|3268|域控制器|出站|
|LDAPS 到全局编录|TCP|3269|域控制器|出站|
|Kerberos|TCP 和 UDP|88|域控制器|出站|
|Netlogon|TCP 和 UDP|445|域控制器|出站|
|Windows 时间|UDP|123|域控制器|出站|
|DNS|TCP 和 UDP|53|DNS 服务器|出站|
|基于 RPC 的 NTLM|TCP|135|网络上的所有设备|出站|
|NetBIOS|UDP|137|网络上的所有设备|出站|
|SSL|TCP|443，或采用中心服务的配置|ATA 中心：<br /><br />-   中心服务 IP 地址<br />-   IIS IP 地址|出站|
|Syslog（可选）|UDP|514|SIEM 服务器|入站|

> [!NOTE]在 ATA 网关执行解析的过程中，需要通过 ATA 网关在网络设备上打开以下入站端口。
>
> -   基于 RPC 的 NTLM
> -   NetBIOS

### 证书
确保 ATA Center 有权访问 CRL 分发点。 如果 ATA 网关未访问 Internet，请按照流程手动导入 CRL，但注意要为整个链安装所有 CRL 分发点。<br>
为了便于安装 ATA 中心，你可以在安装 ATA 中心的过程中安装自签名证书。 部署后，你可以将自签名证书替换为来自内部证书颁发机构的、将由 ATA 网关使用的证书。

> [!NOTE]
证书的提供程序类型必须是加密服务提供程序 (CSP)。<br>

需要在本地计算机存储中将支持**服务器身份验证**的证书安装在 ATA 网关的计算机存储中。 此证书必须受 ATA 中心的信任。

## ATA 轻型网关要求
本部分列出 ATA 轻型网关的要求。
### 常规
ATA 轻型网关支持在运行 Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 的域控制器上进行安装。

域控制器可以是只读域控制器 (RODC)。

域控制器不能为服务器核心。

### 服务器规格

ATA 轻型网关要求至少在域控制器上安装 2 个核心和 6 GB 的 RAM。
为优化性能，请将 ATA 轻型网关的**电源选项**设置为**高性能**。
ATA 轻型网关可在各种负载和大小的域控制器上进行部署，具体取决于域控制器的传入和传出网络流量大小，以及域控制器上安装的资源数量。

### 时间同步
ATA Center 服务器、ATA 轻型网关服务器和域控制器的时间必须同步，彼此间的误差不超过 5 分钟。
### 网络适配器
ATA 轻型网关监视所有域控制器的网络适配器上的本地流量。 <br>
在部署后，可使用 ATA 控制台来修改所监视的网络适配器。

### 端口
下表列出了 ATA 轻型网关所需的最低端口数：

|协议|Transport|Port|到/从|Direction|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP 和 UDP|53|DNS 服务器|出站|
|基于 RPC 的 NTLM|TCP|135|网络上的所有设备|出站|
|NetBIOS|UDP|137|网络上的所有设备|出站|
|SSL|TCP|443，或采用中心服务的配置|ATA 中心：<br /><br />-   中心服务 IP 地址<br />-   IIS IP 地址|出站|
|Syslog（可选）|UDP|514|SIEM 服务器|入站|

> [!NOTE]在 ATA 轻型网关执行解析的过程中，需要通过 ATA 轻型网关在网络设备上打开以下入站端口。
>
> -   基于 RPC 的 NTLM
> -   NetBIOS

### 证书
确保 ATA Center 有权访问 CRL 分发点。 如果 ATA 轻型网关未访问 Internet，请按照流程手动导入 CRL，但注意要为整个链安装所有 CRL 分发点。
为了便于安装 ATA 中心，你可以在安装 ATA 中心的过程中安装自签名证书。 部署后，可将自签名证书替换为来自内部证书颁发机构的、将由 ATA 轻型网关使用的证书。
> [!NOTE]
证书的提供程序类型必须是加密服务提供程序 (CSP)。

需要在本地计算机存储中将支持服务器身份验证的证书安装在 ATA 轻型网关的计算机存储中。 此证书必须受 ATA 中心的信任。

## ATA 控制台
通过浏览器访问 ATA 控制台，支持以下浏览器：

-   Internet Explorer 10 和更高版本

-   Google Chrome 40 及更高版本

-   最少 1700 像素的屏幕宽度分辨率

## 另请参阅

- [ATA 体系结构](ata-architecture.md)
- [安装 ATA](/advanced-threat-analytics/deploy-use/install-ata)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO4-->


