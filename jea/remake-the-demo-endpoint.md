---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "重新进行演示终结点"
ms.technology: powershell
ms.openlocfilehash: 4a56272b6f995500d443d441f5e03db85dac6f96
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 重新进行演示终结点
在此部分中，您将学习如何生成上述部分中使用的演示终结点的精确副本。
这将介绍是了解 JEA，包括 PowerShell 会话配置和角色功能所需的核心概念。

## PowerShell 会话配置
当您在上面的部分使用 JEA 时，您将开始通过运行以下命令︰

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEA_Demo -Credential $NonAdminCred
```

尽管大多数参数都一目了然，*配置名*参数可能看起来混乱最初。
指定该参数的已连接到 PowerShell 会话配置。

*PowerShell 会话配置*是别致术语 PowerShell 终结点。
这是 figurative"位置"用户连接和 PowerShell 功能访问的位置。
根据您设置会话配置，它可以提供将用户连接到不同的功能。
对于 JEA，我们使用会话配置将 PowerShell 限制为一组有限的功能，并作为特权虚拟帐户运行。

您的计算机上已有多个已注册的 PowerShell 会话配置，每个略有不同设置。
其中的大多数附带 Windows，但是"JEA_Demo"会话配置上设置[先决条件](prerequisites.md)部分。
您可以看到所有注册会话配置通过管理员 PowerShell 提示符中运行以下命令︰

```PowerShell
Get-PSSessionConfiguration
```

## PowerShell 会话的配置文件
通过注册新*PowerShell 会话的配置文件*，您可以使新会话配置。
会话配置文件包含".pssc"文件扩展名。
您可以使用新建 PSSessionConfigurationFile cmdlet 生成会话配置文件。

接下来，要创建并注册 JEA 新会话配置。

## 生成和修改 PowerShell 会话配置
运行以下命令以生成 PowerShell 会话配置"框架"文件。

```PowerShell
New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\JEADemo2.pssc"
```

> **提示︰**默认情况下，只是最常见的配置设置包括主干文件中。
> 使用`-Full`参数生成 PSSC 中包含所有适用的设置。

PowerShell ISE 或您喜爱的文本编辑器中打开的文件。

```PowerShell
ise "$env:ProgramData\JEAConfiguration\JEADemo2.pssc"
```

使用以下值 （记住要替换为您自己的非管理员安全组中） 中更新文件中的以下字段︰

```PowerShell
# OLD: SessionType = 'Default'
SessionType = 'RestrictedRemoteServer'

# OLD: TranscriptDirectory = 'C:\Transcripts\'
TranscriptDirectory = "C:\ProgramData\JEAConfiguration\Transcripts"

# OLD: # RunAsVirtualAccount = $true
RunAsVirtualAccount = $true

# OLD: RoleDefinitions = @{ 'CONTOSO\SqlAdmins' = @{ RoleCapabilities = 'SqlAdministration' }; 'CONTOSO\ServerMonitors' = @{ VisibleCmdlets = 'Get-Process' } }
RoleDefinitions = @{'CONTOSO\JEA_NonAdmin_Operator' = @{ RoleCapabilities =  'Maintenance' }}
```

下面介绍了每这些条目的平均值的︰

1.  *SessionType*字段定义预设的默认设置，可使用此终结点。
*RestrictedRemoteServer*定义远程管理所需的最小的设置。
默认情况下， *RestrictedRemoteServer*终结点将公开获取命令，获取-FormatData 选择对象，获取帮助的度量值的对象，退出-PSSession 清除主机、 和传出默认。
它将设置为*RemoteSigned*，并向*NoLanguage* *LanguageMode*的*ExecutionPolicy* 。
这些设置的最终结果是用于配置您的终结点的安全和最少的起始点。

2.  *RoleDefinitions*字段向特定组分配角色功能。
它定义哪些人可以执行哪些操作为权限的帐户。
使用此字段中，您可以指定根据组成员身份任何连接用户可用的功能。
这是 JEA 的 RBAC 功能的核心。
在此示例中，您要公开预制的"维护"RoleCapability 向"Contoso\JEA_NonAdmin_Operator"组的成员。

3.  *RunAsVirtualAccount*域指示的 PowerShell 应该"运行"虚拟帐户在此终结点。
默认情况下，虚拟帐户是内置成员管理员组中。
在域控制器上，它也是默认域管理员组的成员。
以后在本指南，您将了解如何自定义的虚拟帐户权限。

4.  *TranscriptDirectory*字段定义"放在即时"PowerShell 脚本每个远程会话后的保存位置。
这些脚本允许您检查可读的方式在每个会话采取的操作。
有关 PowerShell 脚本的详细信息，请查看此[博客文章](http://blogs.msdn.com/b/powershell/archive/2015/06/09/powershell-the-blue-team.aspx)。
注意︰ 常规 Windows 事件也捕获有关使用 PowerShell 运行的每个用户的信息。
脚本是太大更易于阅读。

最后，将更改保存到*JEADemo2.pssc*。

## 应用 PowerShell 会话配置

若要从会话配置文件创建起止工作表，您需要注册该文件。
这需要几条信息︰

1. 会话配置文件的路径。
2. 您已注册的会话配置的名称。 这是用户连接到您使用的终结点时向"配置名"参数提供的相同名称`Enter-PSSession`或`New-PSSession`。

要注册您的本地计算机上的会话配置，请运行以下命令︰

```PowerShell
Register-PSSessionConfiguration -Name 'JEADemo2' -Path "$env:ProgramData\JEAConfiguration\JEADemo2.pssc"
```

恭喜 ！ 您已经设置了您的 JEA 终结点。

## 测试您的终结点
重新运行您新的终结点，以确认运行按预期对[使用 JEA](using-jea.md)部分中列出的步骤。
请务必到提供配置名称时使用新的终结点名称 (JEADemo2) `Enter-PSSession`。

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEADemo2 -Credential $NonAdminCred
```

## 关键概念
**PowerShell 会话配置**︰ 有时称作*PowerShell 终结点*，这是 figurative"位置"用户连接和 PowerShell 功能访问的位置。
您也可以通过运行在您的系统列出已注册的会话配置`Get-PSSessionConfiguration`。
当以特定方式进行配置，PowerShell 会话配置可以调用*JEA 终结点*。

**PowerShell 会话配置文件 (.pssc)**: A 文件，当注册的请定义 PowerShell 会话配置设置。
它包含可以连接到的终结点，"运行方式"的用户角色的规范虚拟帐户，及其他内容。     

**角色定义**︰ 将用户连接到定义角色功能授予会话配置文件中的字段。
它定义*谁*可以执行*哪些*为权限的帐户。
这是 JEA 的 RBAC 功能的核心。

**SessionType**︰ 表示的会话配置默认设置的会话配置文件中的字段。
对于 JEA 终结点，这必须将设置为 RestrictedRemoteServer。

**PowerShell 脚本**︰ 包含 PowerShell 会话的"通过即时"视图的文件。
您可以设置为使用 TranscriptDirectory 域 JEA 会话生成脚本 PowerShell。
脚本的详细信息，请查看此[博客文章](https://technet.microsoft.com/en-us/magazine/ff687007.aspx)。

