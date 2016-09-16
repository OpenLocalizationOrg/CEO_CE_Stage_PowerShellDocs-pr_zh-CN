---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "端到端 active directory"
ms.technology: powershell
ms.openlocfilehash: 3108f5dad96ef54feb3cf559fae38812ed46849c
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 端到端-Active Directory
假设增加了您的程序的范围。
现在，您有责任将 JEA 添加到域控制器执行 Active Directory 操作。
将帮助支持人员使用 JEA 解锁帐户、 重置密码，并执行其他类似的操作。

您需要公开一组全新的到不同的一组人员的命令。
除此之外，您有多个现有 Active Directory 脚本，需要公开。
此部分将指导创作会话配置和角色功能来执行此任务。

## 先决条件
要按照本节分步，您需要的域控制器上工作。
如果您没有访问您的域控制器，不要担心。
尝试按照一起通过一些其他方案或与您熟悉的角色上工作。
如果您想要快速设置新的域控制器，请查看[创建域控制器附录](.\creating-a-domain-controller.md)。

## 使新的角色功能和会话配置的步骤

使新角色功能可能看起来令人望而生畏最初，但可以分为相当简单的步骤︰

1.  确定您需要启用的任务
2.  限制这些任务，如有必要
3.  确认他们使用 JEA
4.  将它们放入角色功能文件
5.  注册公开该角色功能会话配置

## 步骤 1︰ 确定需要公开内容
新的角色功能或会话配置之前，您需要确定所有用户将都需要执行通过 JEA 终结点，以及如何通过 PowerShell 执行这些操作。
这将涉及大量的要求收集和信息检索。
如何转有关此过程将取决于您的组织和目标。
请务必呼叫出要求收集和检索作为关键现实世界过程的一部分。
这可能是采用 JEA 最困难步骤。

### 查找资源
下面是一组可能有进入研究资料创建 Active Directory 管理终结点的联机资源︰
-   [Active Directory PowerShell 概述](http://blogs.msdn.com/b/adpowershell/archive/2009/03/05/active-directory-powershell-overview.aspx)
-   [Active Directory PowerShell 指南 CMD](http://blogs.technet.com/b/ashleymcglone/archive/2013/01/02/free-download-cmd-to-powershell-guide-for-ad.aspx)

### 使列表
下面是一组您将从工作，此部分中的其余部分的十个操作。
保留牢记这是只需示例，您的组织要求可能会有所不同︰

|操作                                                         |PowerShell 命令                                             |
|---------------------------------------------------------------|---------------------------------------------------------------|
|解除锁定的帐户                                                 |`Unlock-ADAccount`                                             |
|密码重置                                                 |`Set-ADAccountPassword` 和 `Set-ADUser -ChangePasswordAtLogon`|
|更改用户的标题                                          |`Set-ADUser -Title`                                            |  
|查找 AD 帐户将被锁定，已禁用，处于非活动状态，等等。 |`Search-ADAccount`                                             |
|将用户添加到组                                              |`Add-ADGroupMember -Identity (with whitelist) -Members`        |
|从组中删除用户                                         |`Remove-ADGroupMember -Identity (with whitelist) -Members`     |
|启用的用户帐户                                          |`Enable-ADAccount`                                             |
|禁用用户帐户                                         |`Disable-ADAccount`                                            |

## 步骤 2︰ 根据需要限制任务

鉴于您已经有您的操作列表，您需要考虑通过每个命令的功能。
有两个重要的原因，若要执行此操作︰

1.  很容易地为用户提供比您想要更多的功能。
例如，`Set-ADUser`是一个非常强大、 灵活的命令。
您可能不想要公开所有可执行该操作可帮助支持用户。  

2.  更糟糕，则可能公开允许用户转义 JEA 的限制的命令。
如果发生这种情况，JEA 消失充当安全边界。
请请选择时要小心命令。
例如，调用表达式将允许用户运行限制的代码。
有关本主题的详细说明，请查看注意事项时限制命令部分。

查看每个命令之后, 您决定以下限制︰

1.  `Set-ADUser` 应仅允许运行与-标题参数

2.  `Add-ADGroupMember` 和`Remove-ADGroupMember`应只适用于特定组

### 步骤 3︰ 确认工作任务 JEA
实际使用这些 cmdlet 可能不是简单受限 JEA 环境中。
在其之间的其他操作，阻止用户使用变量*NoLanguage*模式下运行 JEA。
为了确保最终用户具有平滑体验，务必要检查的一些事项。

作为示例，请考虑`Set-ADAccountPassword`。
-新密码参数要求安全的字符串。
通常情况下，用户创建安全的字符串，并将其在传递作为变量 （如下所示）︰

```PowerShell
$newPassword = Read-Host -Prompt "Specify a new password" -AsSecureString
Set-ADAccountPassword -Identity mollyd -NewPassword $newPassword -Reset
```

但是， *NoLanguage*模式阻止变量的用法。
您可以通过两种方式此限制︰

1.  您可以要求用户运行的命令，而不分配变量。
这是您可以轻松地配置，但可使用端点运算符费力。
希望在每次重置密码，请键入此出？
```PowerShell
Set-ADAccountPassword -Identity mollyd -NewPassword (Read-Host -Prompt "Specify a new password" -AsSecureString) -Reset
```

2.  可以在环绕脚本或向最终用户公开函数的复杂性。
不受限制的上下文; 中运行脚本和公开的函数您可以编写使用变量和呼叫无任何问题的其他命令的功能。
此方法简化了最终用户体验、 避免错误、 减少了所需的 PowerShell 知识，并减少无意间公开多余的功能。
唯一缺点是创作和维护函数的成本。

### 预留︰ 将函数添加到您的模块
采用方法 #2，您将编写 PowerShell 函数调用`Reset-ContosoUserPassword`。
此函数正在进行重置用户密码时需要的所有内容。
在您的组织，这可能需要别致和复杂的内容。
因为这只是一个示例，你的命令只需将重置密码，然后要求用户更改登录时的密码。
我们将它放在最后一节中所做的 Contoso_AD_Module 模块中。

1. PowerShell ISE 中打开"Contoso_AD_Module.psm1"
```PowerShell
ise 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psm1'
```

2. 按 Crtl + J，以打开段菜单。

3. 键直至找到"函数"，然后按 enter。
这将显示函数超级基本框架。

4. 重命名的函数"ContosoUserPassword-重置"。  

5. 重命名的参数之一"标识"并删除第二个。

6. 将以下内容复制到该函数的正文。
```PowerShell
# Get the new password
$NewPassword = Read-Host -Prompt "Enter a new password" -AsSecureString
# Reset the password
Set-ADAccountPassword -Identity $Identity -NewPassword $NewPassword -Reset
# Require the user to reset at next logon
Set-ADUser -Identity $Identity -ChangePasswordAtLogon
```

7. 保存文件。
您应最终的外观如下所示的内容︰
```PowerShell
function Reset-ContosoUserPassword ($Identity)
{
# Get the new password
$NewPassword = Read-Host -Prompt "Enter a new password" -AsSecureString
# Reset the password
Set-ADAccountPassword -Identity $Identity -NewPassword $NewPassword -Reset
# Require the user to reset at next logon
Set-ADUser -Identity $Identity -ChangePasswordAtLogon
}
```
现在，您的用户可以只调用`Reset-ContosoUserPassword`，而不必记住要创建安全字符串内嵌的语法。

## 步骤 4︰ 编辑角色功能文件
在[功能创建角色](./role-capabilities.md#role-capability-creation)部分中，您将创建一个空白的角色功能文件。
在此部分中，将填写该文件中的值。

首先在 PowerShell ISE 打开角色功能文件。
```PowerShell
ise 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities\ADHelpDesk.psrc'
```
更新文件使用以下更改︰
```PowerShell
# OLD: VisibleCmdlets = 'Invoke-Cmdlet1', @{ Name = 'Invoke-Cmdlet2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }
VisibleCmdlets =
    'Unlock-ADAccount',
    'Search-ADAccount',
    'Enable-ADAccount',
    'Disable-ADAccount',
    @{ Name = 'Set-ADUser'; Parameters = @{ Name = 'Title'; ValidateSet = 'Manager', 'Engineer' }},
    @{ Name = 'Add-ADGroupMember'; Parameters =
        @{Name = 'Identity'; ValidateSet = 'TestGroup'},
        @{Name = 'Members'}},
    @{ Name = 'Remove-ADGroupMember'; Parameters =
        @{Name = 'Identity'; ValidateSet = 'TestGroup'},
        @{Name = 'Members'}}

# OLD: VisibleFunctions = 'Invoke-Function1', @{ Name = 'Invoke-Function2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }
VisibleFunctions = 'Reset-ContosoUserPassword'
```

有关上述注意以下几点︰
1.  PowerShell 将尝试自动加载角色功能所需的模块。
如果您发现问题无法加载模块，可能需要显式"ModulesToImport"字段中的列表模块名称。

2.  如果您不确定某个命令时 cmdlet 或函数，请运行`Get-Command`，并查看"命令类型"属性

3.  ValidatePattern 可以使用正则表达式来限制参数，如果不容易定义一组的允许的值。
不能定义 ValidatePattern 和 ValidateSet 同一个参数。

## 步骤 5︰ 注册新会话配置
接下来，您将创建一个新的会话配置文件将公开您的角色功能向"JEA_NonAdmin_HelpDesk"AD 组的成员。

首先创建和 PowerShell ISE 中打开一个新的空白会话配置文件。
```PowerShell
New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc"
ise "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc"
```
修改 PSSC 文件中的以下字段。
如果您使用自己的环境中，您应将"CONTOSO\JEA_NonAdmins_Helpdesk"替换为您自己的非管理员用户或组。
```PowerShell
# OLD: Description = ''
Description = 'An endpoint for Active Directory tasks.'

# OLD: SessionType = 'Default'
SessionType = 'RestrictedRemoteServer'

# OLD: TranscriptDirectory = 'C:\Transcripts\'
TranscriptDirectory = "C:\ProgramData\JEAConfiguration\Transcripts"

# OLD: RunAsVirtualAccount = $true
RunAsVirtualAccount = $true

# OLD: RoleDefinitions = @{ 'CONTOSO\SqlAdmins' = @{ RoleCapabilities = 'SqlAdministration' }; 'CONTOSO\ServerMonitors' = @{ VisibleCmdlets = 'Get-Process' } }
RoleDefinitions = @{ 'CONTOSO\JEA_NonAdmin_HelpDesk' = @{ RoleCapabilities =  'ADHelpDesk' }}
```
保存并注册会话配置
```PowerShell
Register-PSSessionConfiguration -Name ADHelpDesk -Path "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc"
```
## 测试出 ！
获取您的非管理员用户凭据︰
```PowerShell
$HelpDeskCred = Get-Credential
```
如果您执行[设置设置用户和组](creating-a-domain-controller.md#set-up-users-and-groups)部分中，将为凭据︰
-   用户名 ="HelpDeskUser"
-   密码 ="pa$ $w0rd"

使用非管理员凭据的 ADHelpdesk 终结点到远程︰
```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName ADHelpDesk -Credential $HelpDeskCred
```
使用设置 ADUser 来重置用户的标题。
```PowerShell
Set-ADUser -Identity OperatorUser -Title Engineer
```
验证标题已更改。
```PowerShell
Get-ADUser -Identity OperatorUser -Property Title
```
现在，使用添加 ADGroupMember 将用户添加到 TestGroup。
注意︰ 请确保您已事先创建 TestGroup。
```PowerShell
Add-ADGroupMember TestGroup -Member OperatorUser -Verbose
```
退出会话︰
```PowerShell
Exit-PSSession
```
## 关键概念
**NoLanguage 模式**︰ 当 PowerShell 处于"NoLanguage"模式，用户可能仅运行命令;用户无法使用任何语言元素。
有关详细信息，请运行`Get-Help about_Language_Modes`。

**PowerShell 函数**︰ PowerShell 函数是位的 PowerShell 调用的代码，您可以按名称。
有关详细信息，请运行`Get-Help about_Functions`。

**ValidateSet/ValidatePattern**︰ 当公开命令，可以限制为特定参数的有效参数。
ValidateSet 是特定的有效参数列表。
ValidatePattern 是该参数的参数必须匹配的正则表达式。

