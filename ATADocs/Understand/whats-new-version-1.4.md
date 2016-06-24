---
# required metadata

title: ATA 版本 1.4 中的新增功能 | Microsoft 高级威胁分析
description: 列出 ATA 版本 1.4 版中的新增功能和已知问题
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 版本 1.4 中的新增功能
本发行说明提供高级威胁分析版本 1.4 中已知问题的信息。

## 此版本有哪些新增功能？

-   支持使用 Windows 事件转发 (WEF) 将事件直接从域控制器发送到 ATA 网关。

-   通过组合 DPI（深度数据包检查）和 Windows 事件日志，针对企业资源提供传递哈希检测增强。

-   在检测能力和可见性方面，增强了对未加入域的设备和非 Windows 设备的支持。

-   改进了性能，支持在每个 ATA 网关上发送更多流量。

-   改进了性能，支持在每个 ATA 中心使用更多的 ATA 网关。

-   添加了可将计算机名称与 IP 地址进行匹配的新自动名称解析过程 – 这种独特的功能可在调查过程中节省宝贵的时间，并安全分析师提供有力的证据

-   改进了从用户收集输入信息的能力，可自动微调检测过程。

-   自动检测 NAT 设备。

-   当域控制器不可访问时自动故障转移。

-   系统运行状况监视和通知现在提供部署的总体运行状况以及与配置和连接相关的具体问题。

-   可以洞察实体运行所在的站点和位置。

-   多域支持。

-   支持单标签域 (SLD)。

-   支持修改 ATA 网关和 ATA 中心的 IP 地址与证书。

-   通过遥测来帮助改进客户体验。

## 已知问题
此版本存在以下已知问题。

### 网络捕获软件
在 ATA 网关上，唯一支持安装的网络捕获软件是 [Microsoft 网络监视器 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865)。 请不要安装 Microsoft 消息分析器或任何其他网络捕获软件。 安装其他软件将导致 ATA 网关无法正常运行。

### 从 Zip 文件安装
安装 ATA 网关时，请确保将 zip 文件中的文件解压缩到本地目录，并从该目录安装网关。 不要直接通过 zip 文件安装 ATA 网关，否则安装将会失败。

### 卸载以前的 ATA 版本
如果你安装了以前版本的 ATA、公共预览版或个人预览版，必须先卸载 ATA 中心和 ATA 网关，然后再安装此 ATA 版本。

此外，必须删除数据库文件和日志文件。 以前版本的 ATA 中的数据库与 ATA GA 版本不兼容。

当你尝试卸载 ATA 中心或 ATA 网关时，如果打开的是 ATA 安装程序而不是卸载程序，则你需要添加以下注册表项，然后再次卸载 ATA。

**ATA 中心**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   添加一个名为 `InstallationPath`、值为 `C:\Program Files\Microsoft Advanced Threat Analytics\Center` 的新字符串值。 这是默认的安装文件夹。 如果你更改了安装文件夹，请输入安装 ATA 的路径。

    ![ATA 中心安装路径的注册表编辑器](media/ATA-uninstall-center-bug.jpg)

**ATA 网关**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   添加一个名为 `InstallationPath`、值为 `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway` 的新字符串值。 这是默认的安装文件夹。  如果你更改了安装文件夹，请输入安装 ATA 的路径。

    ![ATA 网关安装路径的注册表编辑器](media/ATA-GW-uninstall-bug.jpg)

卸载后，删除 ATA 中心和 ATA 网关上的安装文件夹。  如果你在独立的文件夹中安装了数据库，请删除 ATA 中心上的数据库文件夹。

### 运行状况警报 - ATA 网关断开连接
如果你有多个 ATA 网关并出现了“ATA 网关断开连接”警报，将只会在一个 ATA 网关上自动解决警报，其他网关上的警报将处于“未处理”状态。 你必须手动确认 ATA 网关已启动并且服务正在运行，然后手动解决该警报。

### 虚拟化主机上的 KB
请不要在虚拟化主机上安装 KB 3047154。 否则，可能会导致端口镜像无法正常工作。

## 另请参阅

[将 ATA 更新到 1.6 版 - 迁移指南](ata-update-1.6-migration-guide.md)

[查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

<!--HONumber=May16_HO3-->


