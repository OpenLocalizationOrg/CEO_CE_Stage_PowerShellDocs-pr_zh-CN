---
title: "了解重要的 Windows PowerShell 概念"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 3e601e38-4520-4578-a48d-b6779f1d35ee
ms.openlocfilehash: b18fbf9ac462deece2bdef6743afbda2ea194c42
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 了解重要的 Windows PowerShell 概念
Windows PowerShell 设计集成从许多不同环境的概念。 多个它们熟悉的用户体验中特定外壳或编程环境中，但很少有人将了解它们。 查看这些概念的一些提供的有用 shell 概述。

### 命令不是基于文本的
传统的命令行界面与命令不同，Windows PowerShell cmdlet 旨在处理对象的结构化的多个字符的字符串的出现在屏幕上的信息。 如果需要您可以使用的额外信息沿执行命令始终输出。 我们将讨论此文档中的深入了解此主题。

如果您已使用文本处理工具处理过去的命令行数据，您会发现，它们具有不同行为如果您尝试在 Windows PowerShell 中使用它们。 在大多数情况下，您不需要文本处理工具来提取特定信息。 可以直接使用标准的 Windows PowerShell 对象操作命令来访问数据部分。

### 命令系列是可扩展
如 Cmd.exe 接口不提供有助于您直接扩展内置命令集。 您可以创建外部 Cmd.exe，在运行的命令行工具，但这些外部工具不具有服务，如帮助集成和 Cmd.exe 不自动知道它们是有效的命令。

Windows PowerShell，称为*cmdlet* （读作命令-用于） 中的本机二进制命令可以加强 cmdlet，您可以创建和使用管理单元添加 Windows PowerShell。 Windows PowerShell*管理单元*已编译，就像任何其他界面中的二进制工具。 您可以使用它们添加到 shell，以及新的 cmdlet 的 Windows PowerShell 提供程序。

由于 Windows PowerShell 内部命令的特殊性质，我们将它们作为引用*cmdlet*。

> [!NOTE]
> Windows PowerShell 可以运行 cmdlet 以外的命令。 我们将不讨论它们的 Windows PowerShell 的用户指南中的详细信息，但它们是非常有用，若要了解有关为命令类型的类别。 Windows PowerShell 支持脚本，类似于 UNIX 外壳脚本和 Cmd.exe 批处理文件，但具有.ps1 文件扩展名。 Windows PowerShell 还使您可以创建可用于直接在界面或脚本中的内部函数。

### Windows PowerShell 控点控制台输入和显示
键入命令时，Windows PowerShell 直接始终处理命令行输入。 Windows PowerShell 也将设置屏幕看到的输出格式。 这是重要，因为它可以减少的每个 cmdlet 所需的工作，并确保可始终执行操作的 cmdlet 不管您使用的相同的方式。 如何此工具开发人员和用户简化生命周期的一个示例是命令行帮助。

传统的命令行工具有请求和显示帮助自己方案。 使用一些命令行工具**/？** 触发的帮助显示;其他人使用**-？**， **/H**，甚至**//**。 一些将在 GUI 窗口中，而不是控制台显示中显示的帮助。 某些复杂的工具，如 updater 函数应用程序，显示其帮助之前解压缩内部文件。 如果您使用了错误的参数，您键入和开始自动执行任务，可能会忽略工具。

在 Windows PowerShell 中输入命令时，您输入的所有内容是自动分析预由和处理 Windows PowerShell。 如果您使用**-？** 使用 Windows PowerShell cmdlet 的参数，则始终表示"向我显示帮助此命令"。 不需要分析命令; Cmdlet 开发人员他们只需提供帮助文本。

请务必了解即使 Windows PowerShell 中运行传统的命令行工具，可以使用 Windows PowerShell 的帮助功能。 Windows PowerShell 处理这些参数，并将结果传递给外部工具。

> [!NOTE]
> 如果 Windows PowerShell 中运行图形应用程序时，将打开应用程序窗口。 Windows PowerShell 干预仅当处理命令行输入您用品或应用程序输出返回到控制台窗口中;它不会影响应用程序的工作原理内部。

### 使用 Windows PowerShell 的一些 C# 语法
Windows PowerShell 具有语法功能和非常类似于 C# 中使用编程语言，因为 Windows PowerShell 基于.NET Framework 的关键字。 学习 Windows PowerShell 将使其更容易了解 C# 中，如果您感兴趣的语言。

如果您不是 C# 编程，则此相似性不重要。 但是，如果您已经熟悉 C#，可以使相似性学习 Windows PowerShell 变得更为轻松。

