---
# required metadata

title: 更改 ATA 配置 - 域连接密码 | Microsoft 高级威胁分析
description: 说明如何更改 ATA 网关上的域连接密码。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 更改 ATA 配置 - 域连接密码

>[!div class="step-by-step"]
[« IIS 证书](modifying-ata-config-iiscert.md)


## 更改域连接密码
如果修改域连接密码，请确保输入正确的密码。 如果密码错误，ATA 网关服务将在 ATA 网关上停止运行。

如果你怀疑 ATA 网关上已发生这种情况，则可查看 Microsoft.Tri.Gateway-Errors.log 文件中是否存在以下内容：
`The supplied credential is invalid.`

若要纠正此问题，请按以下过程操作，在 ATA 网关上对域连接密码进行更新：

1.  在 ATA 网关上打开 ATA 控制台。

2.  选择工具栏上的设置选项，然后选择**配置**.

    ![ATA 配置设置图标](media/ATA-config-icon.JPG)

3.  选择**常规**.

    ![ATA 网关更改密码图像](media/ATA-GW-change-DC-password.JPG)

4.  在**常规**下更改密码。

5.  单击“保存”.

6.  更改密码后，手动检查 ATA 网关服务是否正在 ATA 网关服务器上运行。

>[!div class="step-by-step"]
[« IIS 证书](modifying-ata-config-iiscert.md)

## 另请参阅
- [使用 ATA 控制台](working-with-ata-console.md)
- [安装 ATA](install-ata.md)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


