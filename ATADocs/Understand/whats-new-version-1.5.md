---
# required metadata

title: ATA 版本 1.5 中的新增功能 | Microsoft 高级威胁分析
description: 列出 ATA 版本 1.5 版中的新增功能和已知问题
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 1.5 版中的新增功能
本发行说明提供有关此版本的高级威胁分析中已知问题的信息。

## ATA 1.5 更新版中有哪些新增功能？
更新到 ATA 1.5 可在以下方面提供改进：

-   更快的检测速度

-   为 NAT（网络地址转换）设备提供增强的自动检测算法

-   为未加入域的设备提供增强的名称解析过程

-   支持在产品更新期间迁移数据

-   针对涉及数千个实体的可疑活动提供更高的 UI 响应度

-   改进了自动解决监视警报的能力

-   提供更多的性能计数器来增强监视和故障排除

## 已知问题
此版本存在以下已知问题。

### 安装新 ATA 网关失败
将 ATA 部署更新到 ATA 1.5 版之后，在安装新的 ATA 网关时，你将收到以下错误：未安装 Microsoft 高级威胁分析网关

![ATA GW 错误](media/ata-install-error.png)

<b>解决方法：</b>发送电子邮件至 <ataeval@microsoft.com> 以请求解决方法步骤。
### 部署
为“数据库数据路径”和“数据库日记路径”指定的文件夹必须为空（无文件或子文件夹）。
如果不为空，部署将无法继续。

### 从 Zip 文件安装
安装 ATA 网关时，请确保将 zip 文件中的文件解压缩到本地目录，并从该目录安装网关。 不要直接通过 zip 文件安装 ATA 网关，否则安装将会失败。

### 配置
设置 ATA 网关的配置后，首次启动 ATA 网关时，将显示“未同步”标签，直到该服务已完全启动（首次启动服务可能需要长达 10 分钟时间）。

### 网络捕获软件
在 ATA 网关上，唯一支持安装的网络捕获软件是 [Microsoft 网络监视器 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865)。 请不要安装 Microsoft 消息分析器或任何其他网络捕获软件。 安装其他软件将导致 ATA 网关无法正常运行。

### 虚拟化主机上的 KB
请不要在虚拟化主机上安装 KB 3047154。 否则，可能会导致端口镜像无法正常工作。

## 另请参阅

[将 ATA 更新到 1.5 版 - 迁移指南](ata-update-1.5-migration-guide.md)

[将 ATA 更新到 1.6 版 - 迁移指南](ata-update-1.6-migration-guide.md)

[查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


