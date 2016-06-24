---
# required metadata

title: 安装 ATA - 步骤 1 | Microsoft 高级威胁分析
description: 安装 ATA 时，第一步是下载 ATA 中心并将其安装到所选服务器。
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

# 安装 ATA - 步骤 1

>[!div class="step-by-step"]

[步骤 2 »](install-ata-step2.md)

安装过程提供了执行 ATA 1.6 的全新安装说明。 若要了解如何从早期版本更新现有的 ATA 部署，请参阅 [1.6 版本的 ATA 迁移指南](/advanced-threat-analytics/understand-explore/ata-update-1.6-migration-guide)。

> [!IMPORTANT] 开始 ATA 安装之前，请先在 ATA 中心服务器和 ATA 网关服务器上安装 KB2934520，否则需要在安装 ATA 的过程中安装该更新，并且需要重新启动。

## 步骤 1。 下载并安装 ATA 中心
确保服务器满足要求后，即可安装 ATA 中心。

在 ATA 中心服务器上执行以下步骤。

1.  从 [Microsoft 批量许可服务中心](https://www.microsoft.com/Licensing/servicecenter/default.aspx)、[TechNet 评估中心](http://www.microsoft.com/en-us/evalcenter/) 或从 [MSDN](https://msdn.microsoft.com/en-us/subscriptions/downloads) 下载 ATA。

2.  登录到计算机，在该计算机上以本地管理员组成员的用户身份安装 ATA Center。

3.  运行 **Microsoft ATA Center Setup.EXE**，然后按安装向导的要求操作。

4.  如果未安装 Microsoft.Net Framework，在开始安装时系统会提示你安装它。 系统可能会提示你在 .NET Framework 安装后重启。
5.  在**欢迎**页上，选择要用于 ATA 安装屏幕的语言，然后单击**下一步**。

6.  阅读 Microsoft 软件许可条款，如果接受这些条款，单击复选框然后单击**下一步**。

7.  建议将 ATA 设置为自动更新。 如果计算机上的 Windows 未进行此设置，你会看到**使用 Microsoft 更新帮助保护计算机安全并保持最新**屏幕。 
    ![保持 ATA 最新图片](media/ata_ms_update.png)

8. 选择**检查更新时使用 Microsoft 更新（推荐）**。 这会将 Windows 设置调整为启用其他 Microsoft 产品（包括 ATA）的更新，如下所示。 
    ![Windows 自动更新图片](media/ata_installupdatesautomatically.png)

8.  在**ATA Center 配置**页上，根据你的环境输入以下信息：

    |字段|描述|注释|
    |---------|---------------|------------|
    |安装路径|这是要安装 ATA 中心的位置。 默认情况下，该位置为 %programfiles%\Microsoft Advanced Threat Analytics\Center|保留默认值|
    |数据库数据路径|这是要放置 MongoDB 数据库文件的位置。 默认情况下，该位置为 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|将该位置更改为允许你按规模进行扩展的地方。 **注意：** <ul><li>在生产环境中，应使用有足够空间根据容量规划进行扩展的驱动器。</li><li>进行大型部署时，数据库应位于单独的物理磁盘上。</li></ul>有关规模方面的信息，请参阅 [ATA 容量规划](/advanced-threat-analytics/plan-design/ata-capacity-planning)。|
    |ATA 中心服务 IP 地址: 端口|这是可供 ATA 中心服务在其上侦听以获取来自 ATA 网关的通信的 IP 地址。<br /><br />**默认端口：**443|单击向下箭头，选择可供 ATA 中心服务使用的 IP 地址。<br /><br />ATA 中心服务的 IP 地址和端口不能与 ATA 控制台的 IP 地址和端口相同。 确保更改 ATA 控制台的端口。|
    |ATA 中心服务 SSL 证书|这是 ATA 中心服务将使用的证书。|单击密钥图标选择已安装的证书，或者勾选自签名证书（在实验室环境中部署时）。|
    |ATA 控制台 IP 地址|这是将要通过 IIS 用于 ATA 控制台的 IP 地址。|单击向下箭头，选择 ATA 控制台使用的 IP 地址。 **注意：**请记下此 IP 地址，以便从 ATA 网关访问 ATA 控制台时使用。|
    |ATA 控制台 SSL 证书|这是由 IIS 使用的证书。|单击密钥图标选择已安装的证书，或者勾选自签名证书（在实验室环境中部署时）。|

    ![ATA 中心配置图像](media/ATA-Center-Configuration.JPG)

10.  单击**安装**以安装 ATA Center 及其组件。
    以下组件是在安装 ATA 中心期间安装和配置的：

    -   Internet 信息服务 (IIS)

    -   ATA 中心服务和 ATA 控制台 IIS 站点

    -   MongoDB

    -   自定义性能监视器数据收集组

    -   自签名证书（如果在安装期间选择）

11.  安装完成后，单击“启动”连接到 ATA 控制台。
此时系统会自动将你转到**常规**设置页，以便你继续配置和部署 ATA 网关。
由于你登录到网站使用的是 IP 地址，你将收到与该证书相关的一条警告，这是正常的，此时你应该单击**继续访问此网站**。

### 验证安装

1.  查看名为 **Microsoft 高级威胁分析中心**的服务是否正在运行。
2.  在桌面上单击 **Microsoft 高级威胁分析**快捷方式，以便连接到 ATA 控制台。 使用用户凭据登录，该凭据与安装 ATA 中心时所用凭据相同。



>[!div class="step-by-step"] [«预安装](preinstall-ata.md)
[步骤 2»](install-ata-step2.md)

## 另请参阅

- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [配置事件收集](configure-event-collection.md)
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO4-->


