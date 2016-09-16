---
title: "启动 Windows PowerShell 2.0 引擎"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: edafc2fa-7576-49c2-bbba-9336f4bcfc28
ms.openlocfilehash: dedd8c3192c777faac82cd87fd333fd5ab8a4ebf
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 启动 Windows PowerShell 2.0 引擎
本节介绍如何在 Windows 8.1、 Windows Server 2012 R2、 Windows 8 和 Windows Server 2012，其中包括 Windows PowerShell 2.0 引擎，并在其安装 Windows PowerShell 2.0、 Windows PowerShell 3.0 和 Windows PowerShell 4.0 其他系统上启动 Windows PowerShell 2.0 引擎。

Windows PowerShell 4.0 和 Windows PowerShell 3.0 旨在与 Windows PowerShell 2.0 向后兼容。 Cmdlet、 提供商、 单元、 模块和 for Windows PowerShell 2.0 编写的脚本运行 Windows PowerShell 4.0 和 Windows PowerShell 3.0 中未改变。 但是，由于 Microsoft.NET framework 4 运行时激活策略中的更改，Windows PowerShell 主机已 for Windows PowerShell 2.0 编写和编译与公共语言运行时 (CLR) 2.0 无法运行程序而无需在 Windows PowerShell 3.0 或 Windows PowerShell 4.0，修改与 CLR 4.0 编译。 Windows PowerShell 2.0 引擎旨在只能在一个现有的脚本或主机程序无法运行，因为它与 Windows PowerShell 4.0、 Windows PowerShell 3.0 或 Microsoft.NET Framework 4 不兼容。 这种情况下会很少出现。

需要 Windows PowerShell 2.0 引擎的许多程序自动启动它。 这些说明包括在内的出现次数较少的情况下，您需要手动启动引擎。

## 安装和启用所需的程序
在开始之前 Windows PowerShell 2.0 引擎，启用的 Windows PowerShell 2.0 引擎和 Service Pack 1 与 Microsoft.NET Framework 3.5。 有关说明，请参阅[安装 Windows PowerShell](Installing-Windows-PowerShell.md)。

系统上安装了哪些[Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881)或 Windows Management Framework 3.0 拥有所有必需的组件。 不不需要任何进一步配置。 有关安装[Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881)或 Windows Management Framework 3.0 的信息，请参阅[安装 Windows PowerShell](Installing-Windows-PowerShell.md)。

## 如何启动 Windows PowerShell 2.0 引擎
启动 Windows PowerShell 时，默认情况下启动最新版本。 若要开始使用 Windows PowerShell 2.0 引擎 Windows PowerShell，请使用 PowerShell.exe 的版本参数。 您可以在任何命令提示符处，包括 Windows PowerShell 和 Cmd.exe 运行命令。

```
PowerShell.exe -Version 2
```

## 如何开始使用 Windows PowerShell 2.0 引擎远程会话
若要在远程会话中运行 Windows PowerShell 2.0 引擎，请将 Windows PowerShell 2.0 引擎加载的远程计算机上创建会话配置 （也称为"终结点"）。 会话配置远程计算机上保存和任何授权的用户可以用于创建使用 Windows PowerShell 2.0 引擎的会话。

这是通常由系统管理员执行高级的任务。

以下过程使用**PSVersion** [Register PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) cmdlet 的参数创建使用 Windows PowerShell 2.0 引擎会话配置。 [新建 PSSessionConfigurationFile](https://technet.microsoft.com/en-us/library/5f3e3633-6e90-479c-aea9-ba45a1954866) cmdlet 的参数的**PowerShellVersion**也可用于创建会话时都会加载的 Windows PowerShell 2.0 引擎和您的配置文件可以使用**PSVersion**参数的[设置 PSSessionConfiguration](https://technet.microsoft.com/en-us/library/b21fbad3-1759-4260-b206-dcb8431cd6ea)参数更改为使用 Windows PowerShell 2.0 引擎会话配置的会话。

有关会话配置文件的详细信息，请参阅[about_Session_Configuration_Files](https://technet.microsoft.com/en-us/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8)。有关会话配置信息，包括设置和安全，请参阅[about_Session_Configurations [v4](https://technet.microsoft.com/en-us/library/a2fbe12a-350c-4d04-be50-24102824e3ab)。

#### 若要开始远程 Windows PowerShell 2.0 会话

1.  若要创建需要使用 Windows PowerShell 2.0 引擎会话配置，使用"2.0"值的**PSVersion** [Register PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) cmdlet 的参数。 在"服务器端"或接收的连接的结尾处的计算机上运行此命令。

    下面的示例命令 Server01 计算机上创建 PS2 会话配置。 若要运行此命令，启动 Windows PowerShell 4.0 或 Windows PowerShell 3.0 了**以管理员身份运行**选项。

    ```
    Register-PSSessionConfiguration -Name PS2 -PSVersion 2.0
    ```

2.  若要使用 PS2 会话配置 Server01 计算机上创建一个会话，请使用**配置名**创建远程会话，如[新建 PSSession](https://technet.microsoft.com/en-us/library/76f6628c-054c-4eda-ba7a-a6f28daaa26f) cmdlet 的 cmdlet 的参数。

    使用会话配置的会话启动时，Windows PowerShell 2.0 引擎会自动加载到会话中。

    以下命令使用 PS2 会话配置 Server01 计算机上启动会话。 命令将会话保存在 $s 变量。

    ```
    $s = New-PSSession -ComputerName Server01 -ConfigurationName PS2
    ```

## 如何开始使用 Windows PowerShell 2.0 引擎后台作业
若要开始使用 Windows PowerShell 2.0 引擎后台作业，请使用**PSVersion** [启动作业](https://technet.microsoft.com/en-us/library/2bc04935-0deb-4ec0-b856-d7290cca6442)cmdlet 的参数。

以下命令启动后台作业使用 Windows PowerShell 2.0 引擎

```
Start-Job {Get-Process} -PSVersion 2.0
```

有关背景作业的详细信息，请参阅[about_Jobs [v4]](https://technet.microsoft.com/en-us/library/7362512a-8a4e-4575-b2ea-a740e5c4f002)。

