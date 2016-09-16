---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "先决条件"
ms.technology: powershell
ms.openlocfilehash: 6cd57c2fab63d2184cb5c792b63df99dbd782235
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 先决条件

## 初始状态
在开始之前本部分，请确保︰

1. JEA 是在您的系统上可用。 查看当前支持的操作系统和所需的下载[自述文件](./README.md)。
2. 您正在试用 JEA 计算机上具有管理权限。
3. 计算机已加入域。
请参阅[创建的域控制器](#creating-a-domain-controller)部分，以快速设置服务器上的新域，如果没有一个安装。

## 启用远程 PowerShell 处理
管理与 JEA 发生通过 PowerShell 远程处理。
若要确保此已启用且已正确配置管理员 PowerShell 窗口中运行以下命令︰

```PowerShell
Enable-PSRemoting
```

如果您熟悉 PowerShell 远程处理，它将最好运行`Get-Help about_Remote`若要了解有关此重要的基本概念。

## 确定您的用户或组
若要显示 JEA 操作中，您需要标识的非管理员用户和您打算使用本指南中的组。

如果您正在使用现有域，请确定或创建一些未经授权的用户和组。
您将这些非管理员访问权限授予 JEA。
您看到的任何时候`$NonAdministrator`变量中最大的脚本，将其分配给您选定的非管理员用户或组。

如果从头开始创建新的域，则变得更为轻松。
请使用[设置设置用户和组](creating-a-domain-controller.md#set-up-users-and-groups)部分中的附录中创建非管理员用户和组。
默认值的`$NonAdministrator`将在该分区中创建的组。

## 设置维护角色功能文件
创建演示角色功能文件，我们将使用的下一节的 PowerShell 中运行以下命令。
在本指南的更高版本中，您将学习如何此文件的用途。

```PowerShell
# Fields in the role capability
$MaintenanceRoleCapabilityCreationParams = @{
    Author = 'Contoso Admin'
    CompanyName = 'Contoso'
    VisibleCmdlets = 'Restart-Service'
    FunctionDefinitions =
            @{ Name = 'Get-UserInfo'; ScriptBlock = { $PSSenderInfo } }
}

# Create the demo module, which will contain the maintenance Role Capability File
New-Item -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module" -ItemType Directory
New-ModuleManifest -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\Demo_Module.psd1"
New-Item -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities" -ItemType Directory

# Create the Role Capability file
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities\Maintenance.psrc" @MaintenanceRoleCapabilityCreationParams
```

## 创建并注册演示会话配置文件
运行以下命令以创建并注册我们将使用的下一节的演示会话配置文件。
在本指南的更高版本中，您将学习如何此文件的用途。

```PowerShell
# Determine domain
$domain = (Get-CimInstance -ClassName Win32_ComputerSystem).Domain

# Replace with your non-admin group name
$NonAdministrator = "$domain\JEA_NonAdmin_Operator"

# Specify the settings for this JEA endpoint
# Note: You will not be able to use a virtual account if you are using WMF 5.0 on Windows 7 or Windows Server 2008 R2
$JEAConfigParams = @{
    SessionType = 'RestrictedRemoteServer'
    RunAsVirtualAccount = $true
    RoleDefinitions = @{
        $NonAdministrator = @{ RoleCapabilities = 'Maintenance' }
    }
    TranscriptDirectory = "$env:ProgramData\JEAConfiguration\Transcripts"
}

# Set up a folder for the Session Configuration files
if (-not (Test-Path "$env:ProgramData\JEAConfiguration"))
{
    New-Item -Path "$env:ProgramData\JEAConfiguration" -ItemType Directory
}

# Specify the name of the JEA endpoint
$sessionName = 'JEA_Demo'

if (Get-PSSessionConfiguration -Name $sessionName -ErrorAction SilentlyContinue)
{
    Unregister-PSSessionConfiguration -Name $sessionName -ErrorAction Stop
}

New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\JEADemo.pssc" @JEAConfigParams

# Register the session configuration
Register-PSSessionConfiguration -Name $sessionName -Path "$env:ProgramData\JEAConfiguration\JEADemo.pssc"
```

## 启用日志记录 （可选） 的 PowerShell 模块
以下步骤启用系统上的所有 PowerShell 操作的日志记录。
您不需要启用此 JEA 工作，但它都将非常有用[报告 JEA 上](reporting-on-jea.md)一节中。

1. 打开本地组策略编辑器
2. 导航到"计算机配置 \windows 进一步 PowerShell"
3. 双击"打开模块日志记录"
4. 单击"启用"
5. 在选项部分中，单击"显示"模块名称旁边
6. 键入"\*"中弹出窗口。 这意味着 PowerShell 将从所有模块记录命令。
7. 单击确定，并将其应用策略

注意︰ 您还可以启用整个系统 PowerShell 抄写通过组策略。

**祝贺您，您现在已配置您的计算机具有演示终结点，并准备好开始使用 JEA ！**

