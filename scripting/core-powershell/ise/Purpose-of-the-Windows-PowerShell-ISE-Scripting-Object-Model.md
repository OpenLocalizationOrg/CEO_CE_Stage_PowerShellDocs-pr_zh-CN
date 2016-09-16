---
title: "Windows PowerShell ISE 脚本对象模型的用途"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: acf786c5df1555c38ade76d7ab7a6c862f96f4bd
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows PowerShell ISE 脚本对象模型的用途
  对象是与窗体和函数的 Windows PowerShell 集成脚本环境 (ISE)。 对象模型参考提供有关成员的详细信息，属性和这些对象公开的方法。 提供了示例显示如何使用脚本来直接访问这些方法和属性。 脚本对象模型轻松以下范围内的任务。

## 自定义 Windows PowerShell ISE 的外观
 您可以使用对象模型修改应用程序设置和选项。 例如，可以修改它们，如下所示︰

-   您可以更改的错误、 警告、 详细输出，颜色和调试输出。

-   您可以获得或设置命令窗格中，输出窗格和脚本窗格中的背景颜色。

-   您可以设置结果窗格中的前景色。

-   您可以为 Windows PowerShell ISE 设置的字体和字号。

-   您可以配置警告。 此设置包括多个 PowerShell 选项卡中，或在保存文件之前运行脚本文件中的时打开文件时发出警告。

-   您可以脚本窗格和输出窗格在哪里并排视图和视图之间切换脚本窗格中位于输出窗格中的位置。 您可以将命令窗格中停靠到底部或输出窗格的顶部。

## 增强 Windows PowerShell ISE 的功能
 您可以使用对象模型增强 Windows PowerShell ISE 的功能。 例如，您可以︰

-   添加和修改的 Windows PowerShell ISE 本身的实例。 例如，若要更改的菜单，可以添加新的菜单项和映射到脚本的新菜单项。

-   创建脚本，可以执行一些您可以通过使用 Windows PowerShell ISE 中的菜单命令和按钮执行的任务。 例如，您可以添加、 删除或选择一个 PowerShell 选项卡。

-   补充可以使用菜单命令和按钮执行的任务。 例如，您可以重命名 PowerShell 选项卡。

-   操作命令窗格、 输出窗格和脚本窗格中的文本缓冲区与文件关联。 例如，您可以︰

    -   获取或设置的所有文本。

    -   获取或设置所选文本。

    -   运行脚本或运行脚本的所选的部分。

    -   滚动到视图中的线条。

    -   在脱字号位置插入文本。

    -   选择文本块。

    -   获取最后一个行号。

-   执行文件操作。 例如，您可以︰

    -   打开文件，保存文件，或使用其他名称保存文件。

    -   确定文件自上次保存后是否已更改。

    -   获取文件的名称。

    -   选择文件。

## 自动执行任务
 脚本对象模型可用于创建键盘快捷方式常用操作。

## 另请参阅
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md) 
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Windows PowerShell ISE 脚本对象模型](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  
