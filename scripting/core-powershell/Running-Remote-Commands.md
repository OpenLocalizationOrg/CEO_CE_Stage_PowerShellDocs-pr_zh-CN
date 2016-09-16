---
title: "运行远程命令"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 08b29a2fc00aab990f9a64b8cc18fdab7b838986
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 运行远程命令
您可以在一个或数百个单个 Windows PowerShell 命令的计算机上运行命令。 Windows PowerShell 支持使用各种技术，包括 WMI、 RPC 和 Ws-management 远程计算。

## 无需配置远程处理
许多 Windows PowerShell cmdlet 有计算机名称参数，使您可以收集数据并在一个或多个远程计算机上更改设置。 他们可以在 Windows PowerShell 支持不用任何特殊配置的所有 Windows 操作系统上使用各种通信技术和许多工作。

使用这些 cmdlet 包括︰

-   [重新启动计算机](https://technet.microsoft.com/en-us/library/dd315301.aspx)

-   [测试连接](https://technet.microsoft.com/en-us/library/dd315259.aspx)

-   [清除事件日志](https://technet.microsoft.com/en-us/library/dd347552.aspx)

-   [获取事件日志](https://technet.microsoft.com/en-us/library/dd315250.aspx)

-   [获取修补程序](https://technet.microsoft.com/en-us/library/e1ef636f-5170-4675-b564-199d9ef6f101)

-   [获取流程](https://technet.microsoft.com/en-us/library/dd347630.aspx)

-   [获取服务](https://technet.microsoft.com/en-us/library/dd347591.aspx)

-   [设置服务](https://technet.microsoft.com/en-us/library/dd315324.aspx)

-   [获取 WinEvent](https://technet.microsoft.com/en-us/library/dd315358.aspx)

-   [获取 WmiObject](https://technet.microsoft.com/en-us/library/dd315295.aspx)

通常情况下，支持远程处理，而无需特殊配置的 cmdlet 具有计算机名称的参数，并且没有参数的会话。 若要在会话中查找这些 cmdlet，请键入︰

```
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## Windows PowerShell 远程处理
Windows PowerShell 远程处理，使用 Ws-management 协议，允许您在一个或多个远程计算机上运行任何 Windows PowerShell 命令。 它可以建立持久连接、 开始 1:1 交互式会话，并在多台计算机上运行脚本。

若要使用 Windows PowerShell 远程处理，远程计算机必须配置为远程管理。 有关详细信息，包括说明，请参阅[有关远程要求](https://technet.microsoft.com/en-us/library/dd315349.aspx)。

配置 Windows PowerShell 远程处理之后，许多远程处理策略可供您。 本文档的其余部分列出只需几个它们。 有关详细信息，请参阅[有关远程](https://technet.microsoft.com/en-us/library/dd347744.aspx)和[有关远程常见问题](https://technet.microsoft.com/en-us/library/dd347744.aspx)。

### 启动交互式会话
若要开始使用单个远程计算机的交互式会话，请使用[Enter PSSession](https://technet.microsoft.com/en-us/library/dd315384.aspx) cmdlet。 例如，若要开始与 Server01 远程计算机的交互式会话，请键入︰

```
Enter-PSSession Server01
```

命令提示符更改为显示您连接到计算机的名称。 此后，可以在远程计算机上运行的任何命令提示符处键入都和结果将显示在本地计算机上。

若要结束交互式会话，请键入︰

```
Exit-PSSession
```

有关 Enter PSSession 和退出 PSSession cmdlet 的详细信息，请参阅[Enter PSSession](https://technet.microsoft.com/en-us/library/dd315384.aspx)和[退出 PSSession](https://technet.microsoft.com/en-us/library/dd315322.aspx)。

### 运行远程命令
若要在一个或多个远程计算机上运行任何命令，请使用[调用命令](https://technet.microsoft.com/en-us/library/dd347578.aspx)cmdlet。
例如，要 Server01 和 Server02 的远程计算机上运行[获取 UICulture](https://technet.microsoft.com/en-us/library/dd347742.aspx)命令，请键入︰

```
Invoke-Command -ComputerName Server01, Server02 {Get-UICulture}
```

输出将返回到您的计算机。

```
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

有关调用命令 cmdlet 的详细信息，请参阅[调用命令](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)。

### 运行脚本
若要在一个或多个远程计算机上运行脚本，请使用调用命令 cmdlet 的参数的文件路径。 打开或可访问您的本地计算机，则必须是脚本。 结果将返回到您的本地计算机。

例如，以下命令 Server01 和 Server02 的远程计算机上运行 DiskCollect.ps1 脚本。

```
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

有关调用命令 cmdlet 的详细信息，请参阅[调用命令](https://technet.microsoft.com/en-us/library/dd347578.aspx)。

### 建立永久性的连接
若要运行的一系列共享数据的相关命令，在远程计算机上创建一个会话，然后使用调用命令 cmdlet 运行在您创建的会话中的命令。 若要创建的远程会话，请使用新建 PSSession cmdlet。

例如，以下命令创建 Server01 计算机上的远程会话和其他远程会话 Server02 计算机上。 将会话对象保存在 $s 变量中。

```
$s = New-PSSession -ComputerName Server01, Server02
```

既然建立会话，您可以在其中运行任何命令。 然后，因为持久会话，您可以在一个命令中收集数据并将其用于后续命令。

例如，以下命令在 $s 变量中会话运行获取修补程序命令，并将结果保存在 $h 变量。 $H 变量创建在每个会话中 $s，但它不在本地会话。

```
Invoke-Command -Session $s {$h = Get-HotFix}
```

现在，您可以在后面的命令，如下面的一个 $h 变量中使用数据。 结果将显示在本地计算机上。

```
Invoke-Command -Session $s {$h | where {$_.installedby -ne "NTAUTHORITY\SYSTEM"}}
```

### 高级远程处理
Windows PowerShell 远程管理只需从此处开始。 通过使用安装 Windows PowerShell cmdlet，可以建立和配置远程会话同时从本地和远程结束，创建自定义和受限会话，允许用户从远程会话中导入命令在远程会话，实际隐式运行配置远程会话，以及更多的安全性。

为了便于远程配置，Windows PowerShell，请包括 WSMan 提供商。 WSMAN︰ 提供程序创建的驱动器允许您浏览本地计算机和远程计算机上的配置设置的层次结构。
有关 WSMan 提供程序的详细信息，请参阅[WSMan 提供商](https://technet.microsoft.com/en-us/library/dd819476.aspx)和  [有关 Ws-management Cmdlet](https://technet.microsoft.com/en-us/library/dd819481.aspx)，或在 Windows PowerShell 控制台中，键入"获取帮助 wsman"。

有关详细信息，请参阅︰
- [有关远程常见问题](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [注册 PSSessionConfiguration](https://technet.microsoft.com/en-us/library/dd819496.aspx)
- [导入 PSSession](https://technet.microsoft.com/en-us/library/dd347575.aspx)。 

远程处理错误的帮助，请参阅[about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx)。

## 另请参阅
- [about_Remote](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [about_Remote_FAQ](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [about_Remote_Requirements](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [about_PSSessions](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [about_WS Management_Cmdlets](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [调用命令](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)
- [导入 PSSession](https://technet.microsoft.com/en-us/library/048c115e-a6fb-4e0d-8cea-c5ca24630c9d)
- [新 PSSession](https://technet.microsoft.com/en-us/library/59452f12-a11d-4558-99ea-e6ca6ad5ffd3)
- [注册 PSSessionConfiguration](https://technet.microsoft.com/en-us/library/af68867a-d201-4b19-a1de-594015ed8a25)
- [WSMan 提供商](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

