---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "常见的角色功能错误"
ms.technology: powershell
ms.openlocfilehash: df4a6bb1243cf610b6b1be11718ba3a4909bc554
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
### 角色功能的常见错误
您可能遇到的一些常见缺陷到您转到此过程自己。
下面介绍了如何识别并解决这些问题时修改或创建新的终结点的快速指南︰

#### 函数与 Cmdlet
PowerShell 中编写的 PowerShell 命令是 PowerShell 函数。
编写一样专用的.NET 类 PowerShell Cmdlet 的 PowerShell 命令。
您可以通过运行检查命令类型`Get-Command`。

#### VisibleProviders
您将需要公开您的命令需要任何提供商。
最常用的文件系统提供商，但您可能还需要公开其他人，如注册表提供程序。
提供商的简介，请查看此[嗨，脚本专家博客文章](http://blogs.technet.com/b/heyscriptingguy/archive/2015/04/20/find-and-use-windows-powershell-providers.aspx)。
通常公开提供商-时要小心，它是更好地定义您自己处理比以直接公开提供程序 JEA 会话中的基础提供程序的函数。
这种方式，您仍允许用户处理文件，注册表项，等等，但保留控制**哪些**文件，他们可以使用自定义验证逻辑处理注册表项。

