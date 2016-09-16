---
title: "使用资源设计器工具"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 4478806e46c9c6cdc314b1ecadd8554d6558e8f5
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用资源设计器工具

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

资源设计器工具是 cmdlet 的一套由**xDscResourceDesigner**模块公开的轻松创建 Windows PowerShell 需要状态配置 (DSC) 资源。 在此资源的 cmdlet 可帮助创建 MOF 架构、 脚本模块和新资源的目录结构。 有关 DSC 资源的详细信息，请参阅[构建自定义 Windows PowerShell 需要状态配置资源](authoringResource.md)。
在本主题中，我们将创建管理 Active Directory 用户 DSC 资源。
[安装模块](https://technet.microsoft.com/en-us/library/dn807162.aspx)cmdlet 可用于安装**xDscResourceDesigner**模块。

>**注意**︰**安装模块**包括在**PowerShellGet**模块中，包括在 PowerShell 5.0。 您可以下载**PowerShellGet**模块 PowerShell 3.0 和 4.0 [PackageManagement PowerShell 模块](https://www.microsoft.com/en-us/download/details.aspx?id=49186)的预览。

## 创建资源属性
我们需要执行的第一件事是决定将公开该资源的属性。 对于此示例中，我们将定义具有以下属性的 Active Directory 的用户。
 
参数名称说明
* **用户名**︰ 关键唯一标识的用户的属性。
* **请确保**︰ 指定的用户帐户应演示或不存在。 此参数将具有两个可能的值。
* **DomainCredential**︰ 为用户的域密码。
* **密码**︰ 允许配置，如有必要更改用户密码的用户所需的密码。

若要创建属性，我们使用**新建 xDscResourceProperty** cmdlet。 下面的 PowerShell 命令创建上述的属性。

```powershell
PS C:\> $UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
PS C:\> $Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
PS C:\> $DomainCredential = New-xDscResourceProperty –Name DomainCredential-Type PSCredential -Attribute Write
PS C:\> $Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## 创建资源

鉴于已创建的资源属性，我们可以呼叫**新建 xDscResource** cmdlet 来创建资源。 **新建 xDscResource** cmdlet 将作为参数的属性的列表。 它还会在其中创建模块的路径、 新的资源的名称和包含该模块的名称。 下面的 PowerShell 命令创建资源。

```powershell
PS C:\> New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

**新建 xDscResource** cmdlet 创建 MOF 架构主干资源脚本，您的新资源的所需的目录结构和公开新资源的模块的清单。

MOF 架构文件位于**C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**，并且其内容如下所示。

```
[ClassVersion("1.0.0.0"), FriendlyName("Demo_ADUser")]
class Demo_ADUser : OMI_BaseResource
{
[Key] string UserName;
[Write, ValueMap{"Present","Absent"}, Values{"Present","Absent"}] string Ensure;
[Write, EmbeddedInstance("MSFT_Credential")] String DomainCredential;
[Write, EmbeddedInstance("MSFT_Credential")] String Password;
};
```

资源脚本位于**C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**。 不包括要实现该资源，必须添加您自己的实际逻辑。 主干脚本的内容如下所示。

```powershell
function Get-TargetResource
{
[CmdletBinding()]
[OutputType([System.Collections.Hashtable])]
param
(
[parameter(Mandatory = $true)]
[System.String]
$UserName
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


<#
$returnValue = @{
UserName = [System.String]
Ensure = [System.String]
DomainAdminCredential = [System.Management.Automation.PSCredential]
Password = [System.Management.Automation.PSCredential]
}

$returnValue
#>
}


function Set-TargetResource
{
[CmdletBinding()]
param
(
[parameter(Mandatory = $true)]
[System.String]
$UserName,

[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[System.Management.Automation.PSCredential]
$DomainAdminCredential,

[System.Management.Automation.PSCredential]
$Password
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."

#Include this line if the resource requires a system reboot.
#$global:DSCMachineStatus = 1


}


function Test-TargetResource
{
[CmdletBinding()]
[OutputType([System.Boolean])]
param
(
[parameter(Mandatory = $true)]
[System.String]
$UserName,

[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[System.Management.Automation.PSCredential]
$DomainAdminCredential,

[System.Management.Automation.PSCredential]
$Password
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


<#
$result = [System.Boolean]

$result
#>
}


Export-ModuleMember -Function *-TargetResource
```

## 更新资源

如果您需要添加或修改的资源参数列表中，您可以呼叫**更新 xDscResource** cmdlet。 Cmdlet 使用新的参数列表更新资源。 如果您已经在资源脚本添加逻辑，它将保持不变。

例如，假设您希望用户在我们的资源的时间中包括的最后一个日志。 而不是再次完全编写资源，您可以呼叫**新建 xDscResourceProperty**以创建新的属性，然后**更新 xDscResource**呼叫，并向属性列表中添加新的属性。

```powershell
PS C:\> $lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
PS C:\> Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## 测试资源架构

资源设计器工具公开一个可用于测试手动编写 MOF 架构的有效性的更多 cmdlet。 呼叫**测试 xDscSchema** cmdlet，作为参数传递 MOF 资源架构的路径。 该 cmdlet 将输出架构中的任何错误。

### 另请参阅

#### 概念
[构建自定义的 Windows PowerShell 需要状态配置资源](authoringResource.md)

#### 其他资源
[xDscResourceDesigner 模块](https://powershellgallery.com/packages/xDscResourceDesigner)

