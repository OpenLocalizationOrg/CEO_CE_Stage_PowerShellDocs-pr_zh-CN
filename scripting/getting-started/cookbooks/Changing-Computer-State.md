---
title: "更改计算机状态"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 8093268b-27f8-4a49-8871-142c5cc33f01
ms.openlocfilehash: 60652b67a98179f0dab137e3360766d2e6936d81
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 更改计算机状态
若要重置 Windows PowerShell 中的计算机，请使用标准的命令行工具或 WMI 类。 尽管仅使用 Windows PowerShell 来运行该工具，则学习如何更改 Windows PowerShell 中的计算机电源状态将展示了一些有关使用 Windows PowerShell 中的外部工具的重要详细信息。

### 锁定计算机
若要锁定直接与标准可用的工具的计算机的唯一方法是在**user32.dll**调用**LockWorkstation()**函数︰

```
rundll32.exe user32.dll,LockWorkStation
```

此命令将立即锁定工作站。 使用*rundll32.exe*，运行 Windows Dll （并保存以供重复使用其库） 以运行 user32.dll，Windows 管理功能的库。

当您锁定工作站同时启用了用户快速切换，如在 Windows XP 计算机时显示用户登录屏幕，而不是当前用户的屏幕保护程序启动。

要关闭终端服务器上的特定会话，请使用**tsshutdn.exe**命令行工具。

### 关闭当前会话的日志记录
您可以使用多种不同的方法注销本地系统上的会话。 最简单方法是使用远程桌面/终端服务命令行工具**logoff.exe** (有关详细信息，请在 Windows PowerShell 提示符处，键入**注销 /？**)。 若要注销当前活动会话，请键入**注销**不带任何参数。

您还可以使用其注销选项使用**shutdown.exe**工具︰

```
shutdown.exe -l
```

第三个选项是用。 Win32_OperatingSystem 课堂具有 Win32Shutdown 方法。 调用与 0 标志方法启动注销︰

```
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

有关详细信息，并查找 Win32Shutdown 方法的其他功能，请参阅"Win32Shutdown 方法的 Win32_OperatingSystem 类"MSDN 中。

### 关闭或重新启动计算机
关闭并重新启动计算机通常是任务的相同类型。 关闭计算机的工具将通常重新启动它也 —，反之亦然。 有两个简单的选项，用于重新启动计算机从 Windows PowerShell。 使用适当的参数 Tsshutdn.exe 或 Shutdown.exe。 您可以获得用法详细的信息，从**tsshutdn.exe /？** 或**shutdown.exe /？**。

此外可以执行关闭然后重新启动使用**Win32_OperatingSystem**直接从以及 Windows PowerShell 的操作。

若要关闭计算机，使用 Win32Shutdown **1**标志。

```
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(1)
```

若要重新启动操作系统，请使用 Win32Shutdown **2**标志。

```
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(2)
```

