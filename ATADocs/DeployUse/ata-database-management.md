---
# required metadata

title: ATA 数据库管理 | Microsoft 高级威胁分析
description: 帮助你移动、备份或还原 ATA 数据库的过程。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 数据库管理
如果你需要移动、备份或还原 ATA 数据库，请使用以下过程来处理 MongoDB。

## 备份 ATA 数据库
请参阅[相关的 MongoDB 文档](http://docs.mongodb.org/manual/administration/backup/).

## 还原 ATA 数据库
请参阅[相关的 MongoDB 文档](http://docs.mongodb.org/manual/administration/backup/).

## 将 ATA 数据库移到另一个驱动器

1.  停止 **Microsoft 高级威胁分析中心**服务。

2.  停止 **MongoDB** 服务。

3.  打开 Mongo 配置文件，默认情况下位于：C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg。

    查找参数 `storage: dbPath`

4.  将 `dbPath` 参数中列出的文件夹移到新位置。

5.  将 mongo 配置文件中的 `dbPath` 参数更改为新的文件夹路径，然后保存并关闭该文件。

    ![修改 MongoDB 配置的图像](media/ATA-mongoDB-moveDB.png)

6.  启动 **MongoDB** 服务。

7.  打开命令提示符并运行 Mongo shell，方式是运行 `mongo.exe ATA` .

    默认情况下，mongo.exe 位于：C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin

8.  运行以下命令：`db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}}) Instead of <New DB Location>`，其中 &lt;New DB Location&gt; 是新的文件夹路径。

9.  将 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath 更新到新的文件夹路径。

9. 启动 **Microsoft 高级威胁分析中心**服务。

## 另请参阅
- [ATA 体系结构](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA 先决条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO1-->


