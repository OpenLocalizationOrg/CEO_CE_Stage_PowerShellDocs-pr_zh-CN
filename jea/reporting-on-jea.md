---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "在 jea 报告"
ms.technology: powershell
ms.openlocfilehash: 3e7bd2755281f491bba8a905df018fb2e1cac6ff
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 在 JEA 报告
JEA 允许非特权用户特权上下文中运行，因为日志记录和审核是非常重要。
在此部分中，我们将运行浏览您可以使用用于帮助您创建的日志记录和报告的工具。

## 报告 JEA 操作
### 即时抄写
一个以获取 PowerShell 会话中发生的情况的摘要的最快方法是键入的人员即时查看。
您看到其命令，以及这些命令，以及所有输出。
或不是，但您至少了解。
PowerShell 抄写旨在为您提供类似视图事后。

当使用会话配置中的"TranscriptDirectory"字段，PowerShell 将自动记录给定会话中执行所有操作脚本。
下面是此文档中，可以从您的会话查找脚本:"$env: ProgramData\JEAConfiguration\Transcripts"

您可以辨别的用户有关的"连接"，"运行"用户身份，脚本记录信息命令等会话，请在运行。
有关 PowerShell 抄写的详细信息，请参阅[这篇博客文章](http://blogs.msdn.com/b/powershell/archive/2015/06/09/powershell-the-blue-team.aspx)。

### PowerShell 事件日志
当您有打开的模块日志记录时，所有 PowerShell 操作也都记录在常规的 Windows 事件日志。
这是略微 messier 处理相比脚本，但它为您提供的详细信息的级别很有用。

在"PowerShell"操作日志，事件 ID 4104 将记录调用如果您已启用模块日志记录的每个命令。

### 其他事件日志
PowerShell 日志和脚本，与其他记录机制不会捕获"连接用户"。
您将需要执行其他日志和 PowerShell 日志，以匹配上执行的操作之间的一些相关。

在"Windows 远程管理"操作日志，事件 ID 193 将记录连接用户 SID 和名称，以及 RunAs 虚拟帐户 SID 与此相关帮助。
您可能还注意到 RunAs 虚拟帐户的名称，包括连接的用户的域和末尾的用户名。

## 有关 JEA 配置报告
### 获取 PSSessionConfiguration
才能准确报告您的环境的状态，请务必知道多少 JEA 终结点设置您的计算机。
`Get-PSSessionConfiguration` 只是。

### 获取 PSSessionCapability
手动报告上的任何用户通过 JEA 终结点功能会非常复杂。
您可能需要检查几个角色功能。
幸运的是，"获取 PSSessionCapability"cmdlet 执行此操作。

若要测试此出，运行以下命令以管理员身份从 PowerShell 提示符︰
```PowerShell
Get-PSSessionCapability -Username 'CONTOSO\OperatorUser' -ConfigurationName JEADemo
```

