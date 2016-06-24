---
# required metadata

title: 将 ATA 更新为版本 1.6 的迁移指南 | Microsoft 高级威胁分析
description: 将 ATA 更新为版本 1.6 的过程
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

# 将 ATA 更新为版本 1.6 的迁移指南
ATA 1.6 更新版改进了以下几个方面：

-   新增了检测功能

-   改进了现有检测

-   ATA 轻型网关

-   自动更新

-   提高了 ATA Center 性能

-   降低了存储要求

-   支持 IBM QRadar

## 将 ATA 更新到版本 1.6
> [!NOTE]如果你的环境中未安装 ATA，请下载包含版本 1.6 的完整版 ATA，然后遵循[安装 ATA](/advanced-threat-analytics/deploy-use/install-ata) 中所述的标准安装过程。

如果你已部署 ATA 1.5 版本，则以下过程将引导你完成更新部署所要执行的步骤。

> [!NOTE] 不能直接在 ATA 1.4 版之上安装 ATA 1.6 版。 你必须首先安装 ATA 1.5 版。 如果你未安装 ATA 1.5 而无意尝试安装 ATA 1.6，则会产生报错，提示 **你的计算机上已安装有更新版本。** 请先卸载计算机上保留的 ATA 1.6 版的残留文件（即使安装失败，ATA 1.6 残留文件也会产生），然后再安装 ATA 1.5 版。

遵循以下步骤更新到 ATA 版本 1.6：

1. 更新过程之前，请确保遵循[更新到 ATA 1.6 版时迁移失败](whats-new-version-1.6#Migration-failure-when-updating-from-ATA-1.5)处理的过程
2. 请确保具有所需的可用空间来完成更新。 可执行就绪状态检查安装来估计所需多少可用空间，然后在分配必要磁盘空间后重新更新。 升级将至少使用数据库大小的 2%，有关详细信息请参阅 [ATA 容量计划](/advanced-threat-analytics/plan-design/ata-capacity-planning)。
1.  [下载 1.6 更新版本](http://www.microsoft.com/en-us/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
在此版本中，安装 ATA 的新部署和升级现有部署将使用相同的安装文件 (Microsoft ATA Center Setup.exe)。

2.  更新 ATA 中心

3.  下载更新的 ATA 网关程序包

4.  更新 ATA 网关

    > [!IMPORTANT] 更新所有 ATA 网关以确保 ATA 正常运行。

### 步骤 1：更新 ATA 中心

1.  备份数据库：（可选）

    -   如果 ATA 中心作为虚拟机运行并且你想要创建一个检查点，请先关闭虚拟机。

    -   如果 ATA 中心在物理服务器上运行，请遵循[备份 MongoDB](https://docs.mongodb.org/manual/core/backups/) 中建议的过程。

2.  运行安装文件 Microsoft ATA Center Setup.exe，然后按照屏幕上的说明安装更新。

    1.  ATA 1.6 要求安装 .Net Framework 4.6.1。 如果尚未安装，ATA 安装将在安装期间一并安装 .Net Framework 4.6.1<br>
    > [!NOTE]安装 .Net Framework 4.6.1 可能需要重启服务器。 必须先重启服务器，才可继续安装 ATA。
5.  在“欢迎”页中选择语言，然后单击“下一步”。

    6.  阅读最终用户许可协议，如果接受相关条款，请单击“下一步”。

    7.  现可借助用于 ATA 的 Microsoft 更新来保持最新状态。  在“Microsoft 更新”页中，选择**检查更新时使用 Microsoft 更新(推荐)**。
    ![保持 ATA 最新图片](media/ata_ms_update.png)这会将 Windows 设置调整为启用其他 Microsoft 产品（包括 ATA）的更新，如下所示。 
     ![Windows 自动更新图片](media/ata_installupdatesautomatically.png)

    8.  安装开始前，ATA 将执行就绪状态检查。 查看检查结果，以确保已成功配置先决条件且至少具有最小的磁盘空间量。 
    ![ATA 就绪状态检查图像](media/ata_install_readinesschecks.png)

    3.  单击“更新”。 单击“更新”后，ATA 将保持脱机，直到更新过程完成。

4.  更新 ATA 中心后，ATA 网关将报告它们现已过时。

    ![过时的网关图像](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - 更新所有 ATA 网关以确保 ATA 正常运行。

### 步骤 2。 下载 ATA 网关安装包
在配置域连接设置之后，即可下载 ATA 网关安装包。

若要下载 ATA 网关安装包，请执行以下操作：

1.  删除以前下载的所有 ATA 网关程序包版本。

2.  在 ATA 网关计算机上打开浏览器，然后输入你在 ATA 中心为 ATA 控制台配置的 IP 地址。 当 ATA 控制台打开后，单击设置图标，然后选择“配置”。

    ![配置设置图标](media/ATA-config-icon.JPG)

3.  在“ATA 网关”选项卡中，单击“下载 ATA 网关安装程序”。

4.  将程序包保存到本地。

该 zip 文件包括以下部分：

-   ATA 网关安装程序

-   配置设置文件，其中包含连接到 ATA 中心所需的信息

### 步骤 3：更新 ATA 网关

1.  在每个 ATA 网关上，解压缩 ATA 网关程序包中的文件，然后运行 **Microsoft ATA Gateway Setup.exe** 文件

    > [!NOTE]你也可以使用此 ATA 网关程序包来安装新的 ATA 网关。

2.  以前的设置将会保留，但可能需要花费几分钟时间来重启服务。

3.  针对部署的所有其他 ATA 网关重复此步骤。

> [!NOTE]成功更新 ATA 网关后，将删除特定 ATA 网关的过时通知。

如果所有 ATA 网关报告它们已成功同步，并且指出有可用的更新 ATA 网关程序包的消息不再显示，则表示所有 ATA 网关已成功更新。

![更新的网关图像](media/ATA-gw-updated.png)


## 另请参阅

- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


