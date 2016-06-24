---
# required metadata

title: ATA 运行状况中心 | Microsoft 高级威胁分析
description: 使用 ATA 运行状况中心可以检查 ATA 服务的工作状况，并在出现潜在问题时收到警报。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 运行状况中心
ATA 运行状况中心可让你了解 ATA 服务的执行状况，并在出现问题时发出警报。

## 使用 ATA 运行状况中心
ATA 运行状况中心通过在菜单栏中的“运行状况中心”图标上方显示警报（红点），来告诉你出现了问题。

![ATA 运行状况中心红点工具栏](media/ATA-Health-Center-Alert-red-dot.png)

### 管理 ATA 运行状况
若要检查系统的总体运行状况，请单击菜单栏中的“运行状况中心”图标 ![ATA 运行状况中心图标](media/ATA-red-dot.png)

-   对于所有未处理的警报，可通过将其设置为“已解决”或“已忽略”来进行管理。 在“警报”中，单击“未处理”，然后向下滚动到“已解决”或“已忽略”。

-   如果你解决了某个问题但 ATA 检测到该问题仍然存在，该问题将自动移回到“未处理”问题列表。 如果 ATA 检测到某个未处理的问题已得到解决，该问题将自动移到“已解决”问题列表。

-   “已忽略”问题是你不希望 ATA 继续检查的问题 - 例如，是否系统通知你出现了一个你已经知道存在的问题，并且你不打算解决该问题，但同时又不希望继续收到其相关通知，并且不希望它再次出现在“未处理”问题列表中，那么，你可以将它设置为“已忽略”。

![ATA 运行状况中心问题图像](media/ATA-Health-Issue.JPG)

## 另请参阅
- [使用 ATA 检测设置](working-with-detection-settings.md)
- [处理可疑活动](working-with-suspicious-activities.md)
- [查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


