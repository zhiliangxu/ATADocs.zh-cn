---
# required metadata

title: ATA 1.6 版中的新增功能 | Microsoft 高级威胁分析
description: 列出 ATA 1.6 版中的新增功能和已知问题
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

# ATA 1.6 版中的新增功能
本发行说明提供有关此版本的高级威胁分析中已知问题的信息。

## ATA 1.6 更新版中有哪些新增功能？
ATA 1.6 更新版改进了以下几个方面：

-   新增了检测功能

-   改进了现有检测

-   ATA 轻型网关

-   自动更新

-   提高了 ATA Center 性能

-   降低了存储要求

-   支持 IBM QRadar

### 新增了检测功能


- **恶意数据保护私有信息请求**数据保护 API (DPAPI) 是一种基于密码的数据保护服务。 此保护服务可供存储用户机密（例如网站密码和文件共享凭据）的各种应用程序使用。 若要处理密码丢失的情况，用户可以通过使用不涉及其密码的恢复密钥来解密受保护的数据。 在域环境中，攻击者可以在所有加入域的计算机上远程窃取恢复密钥，并使用它来解密受保护的数据。


- **网络会话枚举**侦测是高级攻击杀伤链中的一个关键阶段。 域控制器 (DC) 使用服务器消息块 (SMB) 协议，充当文件服务器以用于组策略对象分发。 作为侦测阶段的一部分，攻击者可以查询服务器上所有活动 SMB 会话的 DC，从而使其可以访问与这些 SMB 会话相关联的所有用户和 IP 地址。 SMB 会话枚举可能会被攻击者用于攻击敏感帐户，帮助他们在网络上横向移动。


- **恶意复制请求**在 Active Directory 环境中，复制会定期在域控制器之间发生。 攻击者可以伪装成 Active Directory 复制请求（有时伪装成域控制器），从而允许攻击者在无需利用更具有侵入性的技术（如卷影复制服务）的情况下即可检索在 Active Directory 中存储的数据，包括密码哈希。


- **MS11-013 漏洞检测**Kerberos 中有提升特权漏洞，这会允许伪造 Kerberos 服务票证的某些方面。 成功利用此漏洞的恶意用户或攻击者可以在域控制器上获取具有提升特权的令牌。


- **异常协议实现**通常使用一组标准的方法和协议执行身份验证请求（Kerberos 或 NTLM）。 但是，为了成功进行身份验证，请求必须仅符合一组特定的要求。 攻击者可能会在环境中以略偏离这些标准实现的方式实现这些协议。 这些偏离方式可能指示攻击者正尝试执行攻击，如密码哈希、暴力破解及其他攻击。


### 改进了现有检测
ATA 1.6 包括改进的检测逻辑，减少了现有检测的误报和漏报方案，如黄金票证、蜜标、暴力破解和远程执行。

### ATA 轻型网关
此版本的 ATA 引入了 ATA 网关的新部署选项，它允许直接在域控制器上安装 ATA 网关。 此部署选项将删除 ATA 网关的非关键功能，并引入基于 DC 上的可用资源的动态资源管理，从而确保 DC 的现有操作不受影响。 ATA 轻型网关可以减少 ATA 部署的成本。 同时，它还可简化分支站点中的部署，在分支站点中，用于设置端口镜像的硬件资源容量有限或不可用。
有关 ATA 轻型网关的详细信息，请参阅 [ATA 体系结构](/advanced-threat-analytics/plan-design/ata-architecture#ata-gateway-and-ata-lightweight-gateway)

有关部署注意事项以及选择正确的网关类型的详细信息，请参阅 [ATA 容量规划](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment)


### 自动更新
从 1.6 版开始，将可以使用 Microsoft 更新来更新 ATA Center。 此外，ATA 网关现在可以使用其到 ATA Center 的标准通信信道进行自动更新。
### 提高了 ATA Center 性能
此版本减轻了数据库负载并提供了运行所有检测的更高效方法，使单个 ATA Center 能够监视更多域控制器。

### 降低了存储要求
ATA 1.6 版对运行 ATA 数据库的存储空间要求明显降低，现在所需的存储空间仅为以前版本的 20%。

### 支持 IBM QRadar
除了以前支持的 SIEM 解决方案外，ATA 现在还可以从 IBM 的 QRadar SIEM 解决方案接收事件。

## 已知问题
此版本存在以下已知问题。

### 未能识别手动移动数据库中的新路径

部署中的数据库路径为手动移动，ATA 部署不会为更新使用新的数据库路径。 这可能会导致以下问题：


- ATA 可能会使用 ATA Center 的系统驱动器中的所有可用空间，而不会定期删除旧的网络活动。


- 将 ATA 更新到 1.6 版可能无法通过更新前就绪状态检查，如下图所示。
    ![未通过就绪状态检查](media/ata_failed_readinesschecks.png)
    >[!Important]
将 ATA 更新到 1.6 版之前，请用正确的数据库路径更新以下注册表项：  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`

### 从 ATA 1.5 更新时迁移失败
当更新到 ATA 1.6 时，更新过程可能会失败，错误代码如下：

![将 ATA 更新到 1.6 出现的错误](http://i.imgur.com/QrLSApr.png)如果你看到此错误，请在如下位置查看部署日志：**C:\Users\<User>\AppData\Local\Temp**，并查找以下异常：

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

你也可能会看到此错误：System.ArgumentNullException: 值不能为 null。
    
如果看到上述任一错误，请运行以下解决方法。

**解决方法**： 

1.  将文件夹“data_old”移到一个临时文件夹（通常位于 %ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin）。
2.  卸载 ATA Center v1.5，并删除所有数据库数据。
![卸载 ATA 1.5](http://i.imgur.com/x4nJycx.png)
3.  重新安装 ATA Center v1.5。 确保使用的配置与之前的 ATA 1.5 安装相同（证书、IP 地址和 DB 路径等）。
4.  按以下顺序停止这些服务：
    1.  Microsoft 高级威胁分析中心
    2.  MongoDB
5.  将 MongoDB 数据库文件替换为“data_old”文件夹中的文件。
6.  按以下顺序启动这些服务：
    1.  MongoDB
    2.  Microsoft 高级威胁分析中心
7.  查看日志以验证该产品的当前运行是否错误。
8.  [下载](http://aka.ms/ataremoveduplicateprofiles "下载")“RemoveDuplicateProfiles.exe”工具，然后将其复制到主安装路径 (%ProgramFiles%\Microsoft Advanced Threat Analytics\Center)
9.  从提升的命令提示符处，运行“RemoveDuplicateProfiles.exe”并等待，直到成功完成。
10. 从此处开始：...\Microsoft Advanced Threat Analytics\Center\MongoDB\bin 目录：**Mongo ATA**，键入下列命令：

    db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![升级解决方法](http://i.imgur.com/Nj99X2f.png)

这应会返回 WriteResult({ "nRemoved" : XX })，其中“XX”是已删除的可疑活动的数目。 如果数字大于 0，将退出命令提示符，并继续升级过程。


### Net Framework 4.6.1 需要重启服务器

在某些情况下，安装 .Net Framework 4.6.1 可能需要重启服务器。 请注意，在 **Microsoft 高级威胁分析中心安装**对话框中单击“确定”将自动重启服务器。 如果想在安装前规划一个维护时段，当在域控制器中安装 ATA 轻型网关时，这一点尤其重要。
    ![重启 .NeT Framework](media/ata-net-framework-restart.png)

### 不能再迁移的历史记录网络活动
此版本 ATA 提供了改进的检测引擎，使检测更准确并减少了许多误报的情况，尤其减少了对传递哈希的误报。
新增和改进的检测引擎利用内联检测技术，允许在无需访问历史网络活动的情况下启用检测，从而大大提高了 ATA Center 的性能。 这也意味着在更新过程中不再需要迁移历史记录网络活动。
ATA 更新过程会将数据导出到 `<Center Installation Path>\Migration` 作为 JSON 文件，以防你想要以后进行调查。

## 另请参阅
[查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

[将 ATA 更新到 1.6 版 - 迁移指南](ata-update-1.6-migration-guide.md)

<!--HONumber=May16_HO4-->


