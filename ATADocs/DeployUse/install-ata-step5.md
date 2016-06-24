---
# required metadata

title: 安装 ATA - 步骤 5 | Microsoft 高级威胁分析
description: 安装 ATA 时，步骤 5 的目的是帮助你配置 ATA 网关的设置。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安装 ATA - 步骤 5

>[!div class="step-by-step"][«步骤 4](install-ata-step4.md)
[步骤 6»](install-ata-step6.md)


## 步骤 5. 配置 ATA 网关设置
安装 ATA 网关后，请执行以下步骤以配置 ATA 网关的设置。

1.  在 ATA 控制台中，单击**配置**，然后选择 **ATA 网关**页。

2.  输入以下信息。

  - **说明**： <br>输入 ATA 网关的说明（可选）。
  - **端口镜像域控制器 (FQDN)**（ATA 网关有此要求，对于ATA 轻型网关，则无法设置此项）： <br>输入域控制器的完整 FQDN，然后单击加号将其添加到列表中。 例如 **dc01.contoso.com**<br /><br />![FDQN 示例图像](media/ATAGWDomainController.png)

下列信息可用于你在**域控制器**列表中输入的服务器： -   其流量由 ATA 网关通过端口镜像监视的所有域控制器都必须列在**域控制器**列表中。 如果域控制器未列在“域控制器”列表中，则可能无法正常使用检测可疑活动这一功能。
-   列表中至少有一个域控制器必须是全局编录服务器。 这样 ATA 就能解析林中其他域的计算机和用户对象。

 - **捕获网络适配器**（必需）：<br>
     - 对于专用服务器上的 ATA 网关，请选择配置为目标镜像端口的网络适配器。 它们将收到镜像域控制器流量。
     - 对于 ATA 轻型网关，应选择用于与你的组织中的其他计算机进行通信的所有网络适配器。

![配置网关设置图像](media/ATA-Config-GW-Settings.jpg)

 - **域同步器候选项**<br>
任何设置为域同步器候选项的 ATA 网关都可以负责 ATA 和 Active Directory 域之间的同步。 取决于域的大小，初始同步可能需要一些时间并消耗大量资源。默认情况下，仅将 ATA 网关设置为域同步器候选项。 <br>建议禁止任何远程站点 ATA 网关成为域同步器候选项。<br>如果域控制器为只读模式，请勿将其设置为域同步器候选项。 有关详细信息，请参阅 [ATA 体系结构](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features)

> [!NOTE] 首次启动 ATA 网关服务时将需要数分钟的时间，因为它需要生成网络捕获分析程序的缓存。<br>
下次在 ATA 网关和 ATA 中心之间进行计划的同步时，配置更改就会应用到 ATA 网关。



    

3. 或者，你可以设置 [Syslog 侦听器和 Windows 事件转发集合](configure-event-collection.md)。 
4. 启用**自动更新 ATA 网关**，这样在即将发布的版本中，当你更新 ATA Center 时，将自动更新此 ATA 网关。
3.  单击“保存” 。


## 验证安装
若要验证 ATA 网关是否已成功部署，请进行下述检查：

1.  检查名为 **Microsoft 高级威胁分析网关**的服务是否正在运行。 在保存 ATA 网关设置后，可能需要几分钟时间才能启动该服务。

2.  如果该服务未启动，请查看位于下列默认文件夹“%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs”中的“Microsoft.Tri.Gateway-Errors.log”文件。

3.  查看[ATA 疑难解答](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors)获取帮助。

4.  如果这是安装的第一个 ATA 网关，则可在数分钟后登录到 ATA 控制台并打开通知窗格，只需轻扫已打开屏幕的右侧即可。 你会在控制台右侧的通知栏中看到“最近获悉的实体”列表。

5.  在桌面上单击 **Microsoft 高级威胁分析**快捷方式，以便连接到 ATA 控制台。 使用用户凭据登录，该凭据与安装 ATA 中心时所用凭据相同。
6.  在控制台的搜索栏中进行搜索，例如搜索域中的用户或组。
7.  打开性能监视器。 在“性能”树中，单击“性能监视器”，然后单击“添加计数器”旁边的加号图标。 展开 **Microsoft ATA 网关**，向下滚动到**网络侦听器 PEF 捕获的消息数/秒**，然后进行添加。 然后，确保你能在图上看到活动。

    ![添加性能计数器图像](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"][«步骤 4](install-ata-step4.md)
[步骤 6»](install-ata-step6.md)

## 另请参阅

- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [配置事件收集](configure-event-collection.md)
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO3-->


