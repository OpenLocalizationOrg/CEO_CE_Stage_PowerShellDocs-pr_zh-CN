---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "角色功能"
ms.technology: powershell
ms.openlocfilehash: d5f6311d74e47f2fa1a93909c244cddf114b0229
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 角色功能

## 概述
在上面的部分中，您将学习"RoleDefinitions"字段定义所属的组有权访问哪些角色功能。
您可能有疑惑，"有哪些角色功能？"
此部分将回答该问题。  

## PowerShell 角色功能简介
PowerShell 角色功能定义用户可在 JEA 终结点"内容"。
他们将详细介绍白名单中可见的命令、 可见的应用程序等之类的内容。
由文件扩展名为".psrc"定义角色功能。

## 角色功能内容
我们将通过检查并修改使用以前的演示角色功能文件开始。
假设您已在您的环境中部署会话配置，但您已获得您需要向用户更改公开的功能的反馈。
运算符需要重新启动计算机的能力，他们也希望将能够获取有关网络设置的信息。
此外，安全小组具有告诉您不带任何限制允许用户运行"重新启动服务"不可接受。
您需要限制运算符可以重新启动的服务。

要使这些更改，请首先以管理员身份运行 PowerShell ISE，并打开以下文件︰

```
C:\Program Files\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities\Maintenance.psrc
```

现在查找和更新文件中的以下行︰

```PowerShell
# OLD: VisibleCmdlets = 'Restart-Service'
VisibleCmdlets = 'Restart-Computer',
                 @{
                     Name = 'Restart-Service'
                     Parameters = @{ Name = 'Name'; ValidateSet = 'Spooler' }
                 },
                 'NetTCPIP\Get-*'

# OLD: VisibleExternalCommands = 'Item1', 'Item2'
VisibleExternalCommands = 'C:\Windows\system32\ipconfig.exe'
```

这将包含一些有趣的示例︰

1.  具有受限重新启动服务，以便运算符将只能使用重新启动 Service 与-名称参数，以及它们只允许作为该参数的参数提供"后台处理程序"。
如果您愿意，也可能会限制使用正则表达式使用"ValidatePattern"而不是"ValidateSet"的参数。

2.  已公开与"获取"谓词 NetTCPIP 模块中的所有命令。
"获取"命令通常不更改系统状态，因为这是相对安全的操作。
谈话，它是强烈鼓励到密切 examinine 您通过 JEA 公开的每个命令。

3.  已公开使用 VisibleExternalCommands 可执行文件 (ipconfig)。
您还可以公开与此字段的完整 PowerShell 脚本。
请务必始终提供外部命令以确保未改为执行类似的命名 （和潜在恶意） 程序放置在用户的路径的完整路径。

保存该文件，然后连接到再次以确认所做的更改有效的演示终结点。

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEADemo2 -Credential $NonAdminCred
Get-Command
```
仅修改角色功能文件，因为您不需要重新注册会话配置。
当用户连接，PowerShell 将自动查找您已更新的角色功能。
由于角色功能会加载会话启动时，现有会话不受角色功能文件的更新。

现在，确认，您可以通过使用-WhatIf 参数运行重新启动计算机，（除非你实际上想要重新启动计算机） 来重新启动计算机。

```PowerShell
Restart-Computer -WhatIf
```

确认您可以运行"ipconfig"

```PowerShell
ipconfig
```

并最后，确认，请重新启动服务仅适用于后台处理程序服务。

```PowerShell
Restart-Service Spooler # This should work
Restart-Service WSearch # This should fail
```

退出完毕后的会话。

```PowerShell
Exit-PSSession
```

## 角色功能创建
在下一步部分中，您将创建 AD 帮助桌面用户 JEA 终结点。
若要准备，我们将创建一个空白的角色功能文件，为该分区填充。
为了解决会话启动时，必须内有效的 PowerShell 模块的"RoleCapabilities"文件夹内创建角色功能。

PowerShell 模块是实际上 PowerShell 功能包。
它们可以包含 PowerShell 函数、 cmdlet、 DSC 资源、 角色功能等。
您可以通过运行查找有关模块的信息`Get-Help about_Modules`PowerShell 控制台中。

若要使用空白角色功能文件创建一个新的 PowerShell 模块，请运行以下命令︰  

```PowerShell
# Create a new folder for the module.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module' -ItemType Directory

# Add a module manifest to contain metadata for this module.
New-ModuleManifest -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psd1' -RootModule Contoso_AD_Module.psm1

# Create a blank script module. You'll use this for custom functions in the next section.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psm1' -ItemType File

# Create a RoleCapabilities folder in the Contoso_AD_Module folder. PowerShell expects Role Capabilities to be located in a "RoleCapabilities" folder within a module.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities' -ItemType Directory

# Create a blank Role Capability in your RoleCapabilities folder. Running this command without any additional parameters just creates a blank template.
New-PSRoleCapabilityFile -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities\ADHelpDesk.psrc'
```

祝贺您，您已创建了空白的角色功能文件。
将在下一节中使用它。

## 关键概念
**角色功能 (.psrc)**: 用户可以在 JEA 终结点执行"内容"定义的文件。
它详细说明白名单等可见命令、 可见控制台应用程序等内容。
为了让 PowerShell 检测角色的功能，您必须将它们放有效 PowerShell 模块中的"RoleCapabilities"文件夹中。

**PowerShell 模块**︰ PowerShell 功能包。
它可以包含 PowerShell 函数、 cmdlet、 DSC 资源、 角色功能等。
为了会自动加载，PowerShell 模块必须位于下路径中`$env:PSModulePath`。

