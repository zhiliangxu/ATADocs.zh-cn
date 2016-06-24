---
# required metadata

title: 将 ATA 更新为版本 1.5 的迁移指南 | Microsoft 高级威胁分析
description: 将 ATA 更新为版本 1.5 的过程
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 将 ATA 更新为版本 1.5 的迁移指南
更新到 ATA 1.5 可在以下方面提供改进：

-   更快的检测速度

-   为 NAT（网络地址转换）设备提供增强的自动检测算法

-   为未加入域的设备提供增强的名称解析过程

-   支持在产品更新期间迁移数据

-   针对涉及数千个实体的可疑活动提供更高的 UI 响应度

-   改进了自动解决监视警报的能力

-   提供更多的性能计数器来增强监视和故障排除

## 将 ATA 更新到版本 1.5
> [!NOTE]
> 如果你的环境中未安装 ATA，请下载包含版本 1.5 的完整版 ATA，然后按照[安装 ATA](/advanced-threat-analytics/deploy-use/install-ata) 中所述的标准安装过程.

如果你已部署 ATA 版本 1.4，则以下过程将引导你完成更新安装所要执行的步骤。

遵循以下步骤更新到 ATA 版本 1.5：

1.  [下载 1.5 更新版本](http://aka.ms/ata1_5update)
      > [!NOTE]
         也可以使用更新的完整版 ATA 来更新到版本 1.5。


2.  更新 ATA 中心

3.  下载更新的 ATA 网关程序包

4.  更新 ATA 网关

    > [!IMPORTANT]
    > 更新所有 ATA 网关以确保 ATA 正常运行。

### 步骤 1：更新 ATA 中心

1.  备份数据库：（可选）

    -   如果 ATA 中心作为虚拟机运行并且你想要创建一个检查点，请先关闭虚拟机。

    -   如果 ATA Center 在物理服务器上运行，请遵循[备份 MongoDB](https://docs.mongodb.org/manual/core/backups/) 中建议的流程.

2.  运行更新文件 Microsoft ATA Center Update.exe，然后按照屏幕上的说明安装更新。

    1.  在**欢迎**页中选择你的语言，然后单击**下一步**.

    2.  阅读最终用户许可协议；如果你接受条款，请单击相应的复选框，然后单击**下一步**.

    3.  选择是要运行完整迁移（默认设置）还是部分迁移。

        ![选择完整迁移或部分迁移](media/ATA-center-fullpartial.png)

        -   如果你选择“部分”迁移，将会删除 ATA 收集的所有网络流量以及分析的转发 Windows 事件，并且会重新学习用户行为配置文件；这至少需要三周时间。 如果磁盘空间不足，则运行“部分”迁移会很有帮助。

        -   如果运行“完整”迁移，则需要提供升级页上计算得出的额外磁盘空间，并且迁移可能需要更长时间，具体取决于网络流量。 完整迁移会保留以前收集的数据和用户行为配置文件，这意味着，ATA 不需要花费额外的时间来学习行为配置文件，并且更新后可立即检测异常行为。

3.  单击“更新”。 单击“更新”后，ATA 将保持脱机，直到更新过程完成。

4.  更新 ATA 中心后，ATA 网关将报告它们现已过时。

    ![过时的网关图像](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - 更新所有 ATA 网关以确保 ATA 正常运行。

### 步骤 2。 下载 ATA 网关安装包
在配置域连接设置之后，即可下载 ATA 网关安装包。

若要下载 ATA 网关安装包，请执行以下操作：

1.  删除以前下载的所有 ATA 网关程序包版本。

2.  在 ATA 网关计算机上打开浏览器，然后输入你在 ATA 中心为 ATA 控制台配置的 IP 地址。 当 ATA 控制台打开后，单击设置图标，然后选择**配置**.

    ![配置设置图标](media/ATA-config-icon.JPG)

3.  在**ATA 网关**选项卡中，单击**下载 ATA 网关安装程序**.

4.  将程序包保存到本地。

该 zip 文件包括以下部分：

-   ATA 网关安装程序

-   配置设置文件，其中包含连接到 ATA 中心所需的信息

### 步骤 3：更新 ATA 网关

1.  在每个 ATA 网关上，解压缩 ATA 网关程序包中的文件，然后运行 Microsoft ATA Gateway Setup 文件。

    > [!NOTE]
    > 你也可以使用此 ATA 网关程序包来安装新的 ATA 网关。

2.  以前的设置将会保留，但可能需要花费几分钟时间来重新启动服务。

3.  针对部署的所有其他 ATA 网关重复此步骤。

> [!NOTE]
> 成功更新 ATA 网关后，特定 ATA 网关过时的通知将会消失。

如果所有 ATA 网关报告它们已成功同步，并且指出有可用的更新 ATA 网关程序包的消息不再显示，则表示所有 ATA 网关已成功更新。

![更新的网关图像](media/ATA-gw-updated.png)

## 另请参阅

- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


