---
title: "有关 Windows PowerShell"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 979654ae-7994-47f8-be43-d79e7a140143
ms.openlocfilehash: 7c2c69b128aca00235330796c1f8a46cb81a3c5f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 有关 Windows PowerShell
Windows PowerShell 旨在通过消除长期问题和添加新的功能改进的命令行和脚本环境。

## 可发现性
Windows PowerShell，可以轻松发现其功能。 例如，若要查找的 cmdlet 的查看和更改 Windows 服务列表，请键入︰

```
Get-Command *-Service
```

后发现哪些 cmdlet 完成的任务，您可以了解有关 cmdlet 使用 cmdlet 获取帮助。 例如，若要显示有关获取服务 cmdlet 的帮助，请键入︰

```
Get-Help Get-Service
```
大多数 cmdlet 发出来操作，然后呈现为显示文本的对象。 若要完全了解该 cmdlet 输出，管道获取成员 cmdlet 输出。 例如，以下命令获取服务 cmdlet 显示有关对象输出成员的信息。

```
Get-Service | Get-Member
```

## 一致性
管理系统可以是复杂的工作以及具有一致的界面工具帮助控制固有复杂程度越高。 很遗憾，命令行工具和脚本化 COM 对象都不知道其一致性。

Windows PowerShell 的一致性是其主要资产。 例如，如果您将了解如何使用排序对象 cmdlet，您可以使用该知识进行排序的任何 cmdlet 输出。 不需要了解每个 cmdlet 的不同排序例程。

此外，cmdlet 开发人员不需要设计其 cmdlet 的排序功能。 Windows PowerShell 让他们提供的基本功能并保持一致有关许多方面的界面，他们的框架。 框架消除了一些通常留给开发人员，选项，但回报，它会使开发的强大和易于使用 cmdlet 变得更加简单。

## 交互式和脚本环境
Windows PowerShell 是组合的交互式和脚本撰写环境，使您可以访问命令行工具和 COM 对象和还使您能够使用强大的.NET Framework 类库 (FCL)。

此环境改进了时 Windows 命令提示符处，其中提供了一个交互式环境与多个命令行工具。 它还改进了 Windows 脚本宿主 (WSH) 脚本，让您使用多个命令行工具和 COM 自动化的对象，但不是提供交互式环境。

通过组合访问所有这些功能，Windows PowerShell 扩展交互式用户和脚本编写人员的能力，并使系统管理更易于管理。

## 对象方向
虽然使用 Windows PowerShell 交互通过在文本中键入命令时，Windows PowerShell 基于对象，而非文字。 命令的输出是一个对象。 您可以为其输入发送到另一个命令的输出对象。 结果，Windows PowerShell 的用户遇到与其他外壳，并介绍了新的和功能强大的命令行范式提供熟悉的界面。 它扩展发送通过使您的命令发送对象，而不是文本之间的数据的概念。

## 轻松切换到脚本
Windows PowerShell 让更加轻松切换为从键入命令交互到创建和运行脚本。 在 Windows PowerShell 命令提示符发现执行某项任务的命令，您可以键入命令。 然后，您可以保存这些命令在脚本或历史记录之前将其复制到一个用于为脚本文件。

