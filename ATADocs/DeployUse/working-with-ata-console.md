---
# required metadata

title: 使用 ATA 控制台 | Microsoft 高级威胁分析
description: 说明如何登录 ATA 控制台及其组件
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用 ATA 控制台

使用 ATA 控制台可以监视和响应 ATA 检测到的可疑活动。

## 启用对 ATA 控制台的访问
属于 ATA 中心服务器上本地管理员组的任何用户都有权登录到 ATA 控制台并管理 ATA 设置。
若要允许某个用户登录 ATA 控制台且无需将其指定为本地管理员，请将其添加到本地组：**Microsoft 高级威胁分析管理员**。

## 登录 ATA 控制台

1. 在 ATA Center 服务器中，单击桌面上的 **Microsoft ATA 控制台**图标，或者打开一个浏览器并浏览到 ATA 控制台。

    ![ATA 服务器图标](media/ata-server-icon.png)

    > [!NOTE] 你可以从 ATA Center 或 ATA 网关打开一个浏览器并浏览到你在安装 ATA Center 时为 ATA 控制台配置的 IP 地址。    

2.  输入你的用户名和密码，然后单击“登录”。

![ATA 登录屏幕图像](media/ATA-log-in-screen.jpg)

    > [!NOTE]
    > You have to log in with a user who is a member of the local administrator group OR of the Microsoft Advanced Threat Analytics Administrators group.

## ATA 控制台

ATA 控制台使你可以按时间顺序快速查看所有可疑活动。 你可以通过该控制台深入了解任何活动的详细信息，并根据这些活动执行操作。 控制台还显示警报和通知，以突出显示 ATA 网络问题或认为可疑的新活动。

下面是 ATA 控制台的重要元素。


### 攻击时间线

这是在你登录到 ATA 控制台时转到的默认登录页面。 默认情况下，所有未处理的可疑活动都显示在攻击时间线上。 你可以筛选攻击时间线，以显示“全部”、“未处理”、“已忽略”或“已解决”的可疑活动。 你还可以查看分配给每个活动的严重性。

![ATA 攻击时间线图像](media/attack-timeline.png)

有关详细信息，请参阅[处理可疑活动](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities)。

### 通知栏

检测到新的可疑活动时，通知栏将在右侧自动打开。 如果自从你上次登录以下发生了新的可疑活动，则当你成功登录后，将打开通知栏。 若要访问通知栏，可随时单击右侧的箭头。

![ATA 通知栏图像](media/notification-bar.png)

### 筛选面板

你可以根据“状态”和“严重性”来筛选要在攻击时间线中显示的，或者在实体配置文件可疑活动选项卡中显示的可疑活动。

### 搜索栏

菜单顶部有一个搜索栏。 你可以在 ATA 中搜索特定的用户、计算机或组。 若要试一试此功能，你可以键入关键字。

![ATA 控制台搜索图像](media/ATA-console-search.png)

### 运行状况中心

当 ATA 部署中的某个组件运行不正常时，运行状况中心将提供警报。

![ATA 运行状况中心图像](media/health-center.png)

每当你的系统遇到问题时，例如连接错误或 ATA 网关断开连接，运行状况中心图标将通过一个红点来通知你。 ![ATA 运行状况中心红点图像](media/ATA-Health-Center-Alert-red-dot.png)

你可以忽略或解决运行状况中心的警报。这些警报根据其严重性分类为“高”、“中”或“低”。 如果你解决了某个警报，但 ATA 服务检测到该警报仍未处理，该警报将自动移到“未处理”警报列表。 如果系统检测到某个警报的原因已解除（形势已好转），该警报将自动移到已解决列表。

### 用户和计算机配置文件

ATA 将为网络中的每个用户和计算机生成配置文件。 在用户配置文件中，ATA 显示常规信息，例如组成员身份、最近登录名和最近访问的资源。

![用户配置文件](media/user-profile.png)

在计算机配置文件中，ATA 显示常规信息，例如最近登录名和最近访问的资源。

![计算机配置文件](media/computer-profile.png)

ATA 提供有关以下实体（计算机、设备、用户）的附加信息：“摘要”、“活动”和“可疑活动”。

对于 ATA 无法完全解析的配置文件，它的旁边将以一个填充了一半的圆圈进行标识。


![ATA 未解析的配置文件图像](media/ATA-Unresolved-Profile.jpg)

### 微型配置文件

在控制台中存在单个实体（例如一个用户或计算机）的任意位置，如果你将鼠标悬停在该实体上，将自动打开一个微型配置文件，其中显示以下信息（如果有）：

![ATA 微型配置文件图像](media/ATA-mini-profile.jpg)

-   Name

-   图片

-   Email

-   电话

-   按严重性列出的可疑活动数



## 另请参阅
[查看 ATA 论坛！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


