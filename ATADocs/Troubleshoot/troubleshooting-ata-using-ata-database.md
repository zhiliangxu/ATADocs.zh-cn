---
# required metadata

title: 使用 ATA 数据库排查 ATA 问题 | Microsoft 高级威胁分析
description: 说明如何使用 ATA 数据库来帮助解决问题 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用 ATA 数据库排查 ATA 问题
ATA 使用 MongoDB 作为其数据库。
你可以使用默认命令行或用户界面工具与数据库交互，以便执行高级任务以及进行故障排除。

## 与数据库交互
查询数据库的默认方法和最基本方法是使用 Mongo shell：

1.  打开命令行窗口，更改 MongoDB bin 文件夹的路径。 默认路径为：**C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**。

2.  运行：`mongo.exe ATA`。 确保在键入 ATA 时所有字母都大写。

|如何|语法|注意|
|-------------|----------|---------|
|检查数据库中的集合。|`show collections`|可用作端到端测试，目的是查看流量是否正写入数据库，以及 ATA 是否正接收事件 4776。|
|获取用户/计算机/组 (UniqueEntity) 的详细信息，例如用户 ID。|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|查找在特定的一天来自特定计算机的 Kerberos 身份验证流量。|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|若要获取&lt;源计算机 ID&gt;，可查询 UniqueEntity 集合，如示例所示。<br /><br />每个网络活动类型（例如 Kerberos 身份验证）都有其自己的集合（对应于 UTC 日期）。|
|查找特定的一天中与特定帐户相关的源自特定计算机的 NTLM 流量。|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|若要获取&lt;源计算机 ID&gt; 和&lt;帐户 ID&gt;，可查询 UniqueEntity 集合，如示例所示。<br /><br />每个网络活动类型（例如 NTLM 身份验证）都有其自己的集合（对应于 UTC 日期）。|
|搜索高级属性，例如帐户的活动日期。 |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|若要获取&lt;帐户 ID&gt;，可查询 UniqueEntity 集合，如示例所示。<br>显示帐户活动日期的属性名称为“ActiveDates”。 <br>
例如，你可能想要知道，帐户是否必须有至少 21 天处于活动状态，才能在其上运行异常行为机器学习算法。|
|进行高级配置更改。 在本示例中，我们将所有 ATA 网关的发送队列大小更改为 10,000。|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

下例使用上面提供的语法提供示例代码。 如果你正在调查发生在 2015/20/10 日这一天的可疑活动，并且想要详细了解“John Doe”在该天执行的 NTLM 活动，可执行以下操作：<br /><br />首先，找到“John Doe”这个 ID

`db.UniqueEntity.find({Name: "John Doe"})`<br>记下该人的 ID（通过“`_id`”值来表示）。在我们的示例中，假设该 ID 为“`123bdd24-b269-h6e1-9c72-7737as875351`”<br>然后，使用你要查找的日期（在我们的示例中为 20/10/2015）之前的最近一个日期来搜索集合。<br>然后，搜索 John Doe 的帐户 NTLM 活动： 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`
## ATA 配置文件
ATA 的配置存储在数据库的“SystemProfile”集合中。
此集合由 ATA 中心服务每隔一小时备份到名为“SystemProfile.json”的文件。 该文件位于名为“Backup”的子文件夹中。 在默认的 ATA 安装位置中，该文件位于：**C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile.json**。 

**注意**：建议在对 ATA 进行重大更改时将此文件备份到某个位置。

运行以下命令即可还原所有设置：

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## 另请参阅
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量规划](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [配置事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [配置 Windows 事件转发](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


