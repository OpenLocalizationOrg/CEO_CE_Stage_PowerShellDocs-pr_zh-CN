---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "在黑名单"
ms.technology: powershell
ms.openlocfilehash: e823cc0b130500fb7ea60e65acf27f90ad3f3802
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
### 在黑名单
玩耍与 JEA 后您可能想知道它是否能黑名单命令。
这是易于理解的请求，但不是当前计划使 JEA 原因如下︰

1.  我们设计 JEA 限制为仅他们需要执行的操作的运算符。
黑名单是相反。

2.  PowerShell 命令作者未设计 JEA 记住的 PowerShell 命令。
在 Windows Server 2016 的全新安装中，有一些关于 1520年命令立即可用。
这些命令的威胁模型中未包括的可能性，用户将运行命令为更高权限的帐户。
例如，某些命令代码注入允许通过设计 （例如添加类型和中核心 PowerShell 模块的调用命令）。
JEA 可以时发出警告公开的特定命令我们知道，但我们不重新评估了 Windows 根据新的威胁模型中的每个命令。
您必须通过 JEA 公开您了解的命令的功能。  

3.  此外，即使 JEA 阻止使用代码注入漏洞的所有命令，则恶意用户将不能执行与另一个相关命令黑名单操作不能保证。
除非您了解所有要公开的命令，它将使您无法保证某一操作不能。
在您了解要公开，哪些命令，无论他们正在使用白名单或黑名单是负担。
黑名单将公开的命令数是难以管理的因此 JEA 实现改为使用白名单。

