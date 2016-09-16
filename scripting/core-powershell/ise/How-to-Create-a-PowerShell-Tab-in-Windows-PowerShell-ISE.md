---
title: "如何在 Windows PowerShell ISE 创建 PowerShell 选项卡"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: e8ed3558549b7b73c565e1e83d524733f79604dd
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 如何在 Windows PowerShell ISE 创建 PowerShell 选项卡
在 Windows PowerShellÂ® 集成脚本环境 (ISE) 选项卡允许您同时创建和使用相同的应用程序中的多个执行环境。 每个 PowerShell 选项卡对应于单独执行环境或会话。

> [!NOTE]
> 变量、 函数和一个选项卡中创建的别名不会延续到另一个。 它们是不同的 Windows PowerShell 会话。

使用以下步骤来打开或关闭 Windows PowerShell 中的选项卡。 若要重命名选项卡上，请在 Windows PowerShell 选项卡上的脚本对象设置[DisplayName](https://technet.microsoft.com/en-us/library/a9b58556-951b-4f48-b3ae-b351b7564360#Displayname)属性。

## 若要创建和使用新的 PowerShell 选项卡
在**文件**菜单上单击**新 PowerShell 选项卡**。 为活动窗口始终打开新的 PowerShell 选项卡。 打开它们的顺序增量编号 PowerShell 选项卡。 每个选项卡是使用其自己的 Windows PowerShell 控制台窗口相关联。 您可以与自己的会话 （这仅限于 Windows PowerShell ISE 2.0 8。） 一次打开的多达 32 PowerShell 选项卡

请注意，单击工具栏上的**新建**或**打开**图标不会创建新选项卡与单独的会话。  相反，这些按钮可打开与会话的当前活动的选项卡上的新的或现有脚本文件。 您可以拥有多个脚本将每个选项卡和会话打开文件。 相关联的会话处于活动状态时，会话脚本选项卡仅显示下方的会话选项卡。

若要使 PowerShell 选项卡处于活动状态，请单击选项卡。 若要选择从处于打开状态，在**视图**菜单上的所有 PowerShell 选项卡，单击要使用 PowerShell 选项卡。

## 若要创建和使用新的远程 PowerShell 选项卡
在**文件**菜单上，单击**新的远程 PowerShell 选项卡上**建立远程计算机上的会话。 对话框出现，并提示您输入所需建立远程连接的详细信息。 远程选项卡函数一样本地 PowerShell 选项卡，但在远程计算机上运行的命令和脚本。

## 若要关闭 PowerShell 选项卡
若要关闭的选项卡上，您可以使用任何以下技巧︰

-   单击您想要关闭的选项卡。

-   在**文件**菜单上，**关闭 PowerShell 选项卡上**，单击，或关闭选项卡的活动选项卡上单击关闭按钮 (**X**)。

如果您有未保存的文件在中打开 PowerShell 选项卡，您将其关闭，提示您保存或放弃它们。 有关如何保存脚本的详细信息，请参阅[如何保存脚本](https://technet.microsoft.com/en-us/library/162f594d-efd3-4234-9960-45e56e6eadc8)。

## 另请参阅
[使用 Windows PowerShell ISE](Using-the-Windows-PowerShell-ISE.md)
[如何使用 Windows PowerShell ISE 中的控制台窗格](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)

