---
title: "学习 Windows PowerShell 名称"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: b4d0fd22-8298-4ee6-82ae-9b6f2907c986
ms.openlocfilehash: 6bd3c3d9b9f05f8ea633ee23fdce7608e985abd7
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 学习 Windows PowerShell 名称
学习名称的命令和命令参数是大量时间投资的大多数命令行界面。 问题得到，有很少模式，以便了解的唯一方法是通过记住每个命令，您需要定期使用的每个参数。

当您使用的新建命令或参数，您通常不能使用您已经知道;您需要查找并了解新的名称。 如果您看一下如何接口增长从一小组的增量内容的工具的功能，很容易看到非标准的结构为什么。 使用命令名称特别是，这可能看起来逻辑由于每个命令是一个单独的工具，但没有更好的方法处理命令名称。

内置大多数命令管理操作系统或应用程序，例如服务或进程的元素。 命令有多种，也可能不适合一系列的名称。 例如，Windows 系统上您可以使用**净开始时间**和**净停止**命令启动和停止服务。 没有另一种更加通用的服务控件工具具有完全不同的名称， **sc**，不适合**净**服务命令的命名模式的 Windows。 为流程管理 Windows 具有**任务列表**列出进程和的**taskkill**命令终止进程。

采用参数的命令具有不规则参数规范。 不能使用**开始净**命令远程计算机上启动服务。 **Sc**命令将启动一项服务的远程计算机上，但若要指定远程计算机，您必须使用双反斜杠其名称前缀。 例如，要在名为 DC01 的远程计算机上启动后台处理程序服务，需要键入**sc \\\\DC01 开始打印后台处理程序**。 向列表 DC01 上运行的任务，您需要使用**/S** （适用于"系统"） 参数，并提供名称 DC01 不带反斜杠，如下所示︰**任务列表 /S DC01**。

虽然有服务和流程之间的重要技术区别，它们是具有明确定义的生命周期的计算机上的管理元素的两个示例。 您可能想要启动或停止服务或进程，或获取所有当前运行服务或进程的列表。 换言之，虽然服务和流程是不同的操作，我们在一项服务或流程执行的操作通常是概念相同。 此外，可能使我们通过指定参数自定义操作的选项可能会概念上类似。

Windows PowerShell 利用这些相似性减少不同的名称，您需要知道了解和使用 cmdlet 数目。

### 若要降低命令记忆的 Cmdlet 使用动词名词名称
Windows PowerShell 使用"动词名词"命名系统，其中每个 cmdlet 名称包含标准动词与特定名词断字。 Windows PowerShell 谓词不是始终英语谓词，但它们 express Windows PowerShell 中的特定操作。 名词非常相似任何语言的名词，它们描述特定类型的一些重要系统管理中的对象。 很容易地展示如何以下两个部分名称减少学习投入看动词和名词的几个示例。

名词较低的限制，但它们应始终描述命令作用于。 Windows PowerShell 具有**获取流程**、**停止处理**、**获取服务**和**停止服务**之类的命令。

对于两个名词和两个谓词，一致性不简化学习过多。 如果您看一组标准的 10 个动词和 10 的名词，您可以仅 20 单词理解，但是，这些单词可用于形成 100 不同命令名称。

通常情况下，您可以识别命令用途阅读它的名称，并通常明显是什么名称应使用新的命令。 例如，计算机关闭命令可能会**停止计算机**。 列出所有计算机网络上的命令可能**获取计算机**。 获取的系统日期的命令是**获取日期**。

您可以列出所有命令，包括与特定动词**-动词****获取命令**（我们将讨论的详细信息下一步部分中**获取命令**） 的参数。 例如，若要查看所有使用动词**获取**的 cmdlet，请键入︰

```
PS> Get-Command -Verb Get
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Acl                         Get-Acl [[-Path] <String[]>]...
Cmdlet          Get-Alias                       Get-Alias [[-Name] <String[]...
Cmdlet          Get-AuthenticodeSignature       Get-AuthenticodeSignature [-...
Cmdlet          Get-ChildItem                   Get-ChildItem [[-Path] <Stri...
...
```

**-名词**参数是变得更为有用，因为它允许您查看一系列的影响相同类型的对象的命令。 例如，如果您想要查看哪些命令可用于管理服务，键入以下命令︰

```
PS> Get-Command -Noun Service
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Service                     Get-Service [[-Name] <String...
Cmdlet          New-Service                     New-Service [-Name] <String>...
Cmdlet          Restart-Service                 Restart-Service [-Name] <Str...
Cmdlet          Resume-Service                  Resume-Service [-Name] <Stri...
Cmdlet          Set-Service                     Set-Service [-Name] <String>...
Cmdlet          Start-Service                   Start-Service [-Name] <Strin...
Cmdlet          Stop-Service                    Stop-Service [-Name] <String...
Cmdlet          Suspend-Service                 Suspend-Service [-Name] <Str... 
...
```

命令不一定 cmdlet，只是因为它具有动词名词命名方案。 本机用于 Windows PowerShell 命令不 cmdlet，但有动词名词名称，例如，清除控制台窗口中，清除主机的命令。 清除主机命令是实际内部函数，您可以看到对它如果运行获取命令︰

```
PS> Get-Command -Name Clear-Host

CommandType     Name                            Definition
-----------     ----                            ----------
Function        Clear-Host                      $spaceType = [System.Managem...
```

### Cmdlet 使用标准的参数
如前所述，传统的命令行界面中使用的命令不通常具有一致的参数名。 有时参数没有名称根本。 此时，它们通常是单字符或缩写词，可以快速类型，但不是为新用户轻松地理解。

与大多数其他传统的命令行接口不同 Windows PowerShell 直接处理参数，并使用此直接访问开发人员指南以及参数标准化参数名。 尽管这不保证每个 cmdlet 始终将符合标准，它会鼓励它。

> [!NOTE]
> 参数名称必须始终-时使用它们，以允许 Windows PowerShell 清楚地将其标识为参数预置它们。 在**获取-命令-名称清除主机**示例中，参数的名称是**名称**，但它以-**名称**输入。

以下是一些一般特征的标准参数名称和用法。

#### 帮助参数 （？）
当您指定**-？** 不执行任何 cmdlet，cmdlet 的参数。 相反，Windows PowerShell 显示帮助 cmdlet。

#### 常见的参数
Windows PowerShell 具有多个参数，称为*公共参数*。 这些参数由使用 Windows PowerShell 引擎，只要由 cmdlet，因为它们将总是相同的行为。 常见的参数是**WhatIf**、**确认**、**详细**、**调试**、**发出警告**， **ErrorAction**、 **ErrorVariable**、 **OutVariable**和**OutBuffer**。

#### 建议的参数
Windows PowerShell 核心 cmdlet 使用标准类似的参数的名称。 虽然不强制参数名使用，则使用量鼓励标准化明确的指导。

例如，指南建议命名为**计算机名称**，而不是服务器、 主机、 系统、 节点或其他常见的可选单词按名称引用使用计算机的参数。 重要的建议的参数名称包括**强制**、**排除**，**包括**、**层通过**、**路径**和**区分大小写**。

