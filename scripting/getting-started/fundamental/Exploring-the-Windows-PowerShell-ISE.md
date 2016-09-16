---
title: "浏览 Windows PowerShell ISE"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: e0d2c6e8-5126-40e7-a1e1-d1cff29fe94a
ms.openlocfilehash: 04737e77d9cea41d9633bdc49fa337cf1c841222
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 浏览 Windows PowerShell ISE
您可以使用 Windows PowerShellÂ® 集成脚本环境 (ISE) 创建、 运行和调试命令和脚本。 Windows PowerShell ISE 菜单栏、 Windows PowerShell 选项卡、 工具栏上、 脚本选项卡、 脚本窗格、 控制台窗格、 状态栏、 文本大小滑块和包含上下文相关的帮助。

> [!NOTE]
> 开头的 Windows PowerShell ISE 3.0 的命令和输出窗格已合并到单个控制台窗格。

## 菜单栏
菜单栏包含**文件**、**编辑**、**查看**、**工具**、**调试**、**加载项**和**帮助**菜单。 在菜单上的按钮允许您执行与编写和运行脚本和 Windows PowerShell ISE 中的运行命令相关的任务。 此外，[加载项工具](../../core-powershell/ise/The-ISEAddOnTool-Object.md)可能被放在菜单栏上通过使用[Windows PowerShell ISE 脚本对象模型](../../core-powershell/ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md)的脚本运行。

> [!NOTE]
> Windows PowerShell ISE 2.0，没有出现的**工具**和**加载项**菜单。

## Windows PowerShell 选项卡
Windows PowerShell 选项卡是运行 Windows PowerShell 脚本的环境。 您可以在 Windows PowerShell ISE，若要在本地计算机或远程计算机上创建单独的环境中打开新的 Windows PowerShell 选项卡。 您可能必须同时打开选项卡的 PowerShell 八个最大值。

## 工具栏
以下按钮位于工具栏上。

|按钮|函数|
|----------|------------|
|**新增功能**|将打开一个新的脚本。|
|**打开**|打开现有脚本或文件。|
|**保存**|保存脚本或文件。|
|**剪切**|剪切所选的文本，并将其复制到剪贴板。|
|**复制**|将所选的文本复制到剪贴板。|
|**粘贴**|粘贴剪贴板中的光标位置的内容。|
|**清除输出窗格**|清除输出窗格中的所有内容。|
|**撤消**|恢复已刚才执行的操作。|
|**恢复**|执行刚撤消的操作。|
|**运行脚本**|运行脚本。|
|**运行选择的内容复制**|运行脚本的所选的部分。|
|**停止执行**|停止正在运行的脚本。|
|**新的远程 PowerShell 选项卡**|创建新的 PowerShell 选项卡建立远程计算机上的会话。 对话框出现，并提示您输入所需建立远程连接的详细信息。|
|**开始 PowerShell.exe**|打开 PowerShell 控制台。|
|**显示脚本窗格顶部**|移动到显示顶部的脚本窗格。|
|**显示脚本窗格右侧**|右移脚本窗格中显示。|
|**显示最大化脚本窗格**|最大化脚本窗格。|

## 脚本选项卡
显示正在编辑的脚本的名称。 您可以单击脚本选项卡上，选择要编辑的脚本。

指向脚本选项卡时，该脚本文件的完全限定的路径显示在工具提示。

## 脚本窗格
允许您创建并运行脚本。 您可以打开、 编辑和运行脚本窗格中的现有脚本。

## 输出窗格
显示命令和脚本运行的结果。 您还可以复制并清除输出窗格中的内容。

## 命令的窗格
允许您撰写的命令。 您可以运行命令窗格中的一行命令或多行命令。 按 SHIFT + ENTER 输入一个多行的命令，每个行，然后执行多行命令的最后一个行之后按 ENTER。 命令窗格的顶部显示的提示显示当前工作目录的路径。

## 状态栏
允许您查看命令和运行脚本，是否完成。 状态栏将显示在最底部显示。 状态栏上显示所选的部分的错误消息。

## 文本大小滑块
增大或减小在屏幕上的文本的大小。

## 帮助
Windows PowerShell ISE 的帮助是 TechNet 库中在 Web 上可用。 您可以通过单击**帮助**菜单上的**Windows PowerShell ISE 帮助**或按 F1 键时光标位于脚本窗格或控制台窗格中的 cmdlet 名称以外的任何位置打开帮助。 从**帮助**菜单上还可以运行更新帮助 cmdlet，并显示命令窗口中显示所有 cmdlet 的参数，并使您可以填写易于使用窗体中的参数构造命令帮助您。

## 另请参阅
[使用 Windows PowerShell ISE](../../core-powershell/ise/Using-the-Windows-PowerShell-ISE.md)

