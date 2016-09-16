---
title: "使用 Tab 扩展"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: bb782e0834673c07527a560d04c90f1f68401089
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用 Tab 扩展
命令行外壳在加速命令条目和提供提示经常提供某种方式来自动完成长文件或命令的名称。 Windows PowerShell 允许您通过按**Tab**键填充文件的名称和 cmdlet 名称。

> [!NOTE]
> Tab 扩展由内部函数 TabExpansion 控制。 此函数可修改或重写，因为此讨论是默认的 Windows PowerShell 配置的行为的指南。

若要自动填充文件名或路径从可用选项中，键入名称的一部分，然后按**Tab**键。 Windows PowerShell 将自动扩展到发现的第一个匹配的名称。 重复按**Tab**键将循环所有可用的选项。

Cmdlet 名称的选项卡上扩展是稍有不同。 若要使用 tab 扩展的 cmdlet 名称上，键入名称 （动词） 和其后连字符的整个第的一部分。 您可以填写详细信息部分匹配的名称。 例如，如果您键入**获取 co** ，然后按**Tab**键时，Windows PowerShell 将自动扩展这给**获取命令**cmdlet （请注意它还向其标准窗体更改字母大小写）。 如果再次按**Tab**键，Windows PowerShell 替换这仅其他匹配 cmdlet 名称，**获取内容**。

您可以在同一行上重复使用 tab 扩展。 例如，您可以使用 tab 扩展**获取内容**cmdlet 的名称输入︰

```
PS> Get-Con<Tab>
```

当您按**Tab**键时，命令将扩展到︰

```
PS> Get-Content
```

您可以然后部分指定活动安装日志文件的路径和使用 tab 扩展再次︰

```
PS> Get-Content c:\windows\acts<Tab>
```

当您按**Tab**键时，命令将扩展到︰

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> 一个的选项卡上的扩展进程有限制的选项卡始终解释为尝试完成单词。 如果您复制并粘贴到 Windows PowerShell 控制台的命令示例，请确保样本不包含选项卡。如果是这样，结果将不可预测，并且几乎可以将您的预期。

