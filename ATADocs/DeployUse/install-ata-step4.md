---
# required metadata

title: 安装 ATA - 步骤 4 | Microsoft 高级威胁分析
description: 安装 ATA 时，步骤 4 的目的是帮助你安装 ATA 网关。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安装 ATA - 步骤 4

>[!div class="step-by-step"]
[« 步骤 3](install-ata-step3.md)
[步骤 5 »](install-ata-step5.md)

## 步骤 4. 安装 ATA 网关

在专用服务器上安装 ATA 网关之前，请验证端口镜像是否已正确配置，以及 ATA 网关是否能看到来往于域控制器的流量。 有关详细信息，请参阅[验证端口镜像](validate-port-mirroring.md)。


> [!IMPORTANT]
> 确保 [KB2919355](http://support.microsoft.com/kb/2919355/) 已安装。  运行以下 PowerShell cmdlet 以查看修补程序是否已安装：
>
> `Get-HotFix -Id kb2919355`

在 ATA 网关服务器上执行以下步骤。

1.  从 zip 文件中提取文件。 
> [!NOTE] 直接从 zip 文件中安装将失败。

2.  在提升的命令提示符处，运行 **Microsoft ATA Gateway Setup.exe**，然后按安装向导的要求操作。

3.  在**欢迎**页中选择你的语言，然后单击**下一步**.

4.  在“ATA 网关配置”下，根据你的环境输入以下信息：

    ![ATA 网关配置图像](media/ATA-Gateway-Configuration.JPG)

    |字段|描述|注释|
    |---------|---------------|------------|
    |安装路径|这是要安装 ATA 网关的位置。 默认情况下，该位置为 %programfiles%\Microsoft Advanced Threat Analytics\Gateway|保留默认值|
    |ATA 网关服务 SSL 证书|这是 ATA 网关将使用的证书。|自签名证书仅用于实验室环境。|
    |ATA 网关注册|输入 ATA 管理员的用户名和密码。|若要将 ATA 网关注册到 ATA 中心，请输入安装过 ATA 中心的用户的用户名和密码。 该用户必须是 ATA 中心以下某个本地组的成员。<br /><br />-   管理员<br />-   Microsoft 高级威胁分析管理员**注意：**这些凭据仅用于注册，不在 ATA 中存储。|
    以下组件是在安装 ATA 网关期间安装和配置的：

    -   KB 3047154

        > [!IMPORTANT]
        > -   请勿在虚拟化主机（正在运行虚拟化的主机，在虚拟机上运行没有问题）上安装 KB 3047154。 否则，可能会导致端口镜像无法正常工作。 
        > -   请勿在 ATA 网关上安装 Message Analyzer、Wireshark 或其他网络捕获软件。 若需捕获网络流量，请安装并使用 Microsoft 网络监视器 3.4。

    -   ATA 网关服务

    -   Microsoft Visual C++ 2013 可再发行包

    -   自定义性能监视器数据收集组

5.  安装完成后，对于 ATA 网关，请单击**启动**打开你的浏览器并登录到 ATA 控制台；对于 ATA 轻型网关，请单击**完成**.


>[!div class="step-by-step"]
[« 步骤 3](install-ata-step3.md)
[步骤 5 »](install-ata-step5.md)

## 另请参阅

- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [配置事件收集](configure-event-collection.md)
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


