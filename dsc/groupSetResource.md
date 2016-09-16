---
title: "DSC GroupSet 资源"
ms.date: 2016-05-16
keywords: "powershell，DSC，内置的资源"
description: "提供了一种机制来管理上的目标节点的本地组。"
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 6e5ea98febfe7541f35a84c37df73df580654340
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC GroupSet 资源

> 适用于︰ Windows PowerShell 的 Windows 5.0

**GroupSet**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来管理上的目标节点的本地组。 该资源是呼叫中指定的每个组的[组合资源](groupResource.md)[复合资源](authoringResourceComposite.md)`GroupName`参数。

当您想要添加和/或删除相同到多个组的成员的列表、 删除多个组中，或添加具有相同的表的多个组的成员，请使用此资源。

##语法##
```
Group [string] #ResourceName
{
    GroupName = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ MembersToInclude = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 组名称| 您要确保特定状态的组的名称。| 
| MembersToExclude| 使用此属性，若要删除现有的成员资格组的成员。 此属性的值是数组的表单*域*的字符串\\*用户名*。 如果您在配置设置此属性，请不使用**成员**属性。 这样做将生成一个错误。| 
| 凭据| 访问远程资源所需的凭据。 **注意**︰ 此帐户必须具有适当的 Active Directory 权限，将所有非本地帐户添加到组。否则，将发生错误。
| 确保| 指明是否存在组。 设置为"无"以确保组不存在该属性。 设置以"演示"（默认值） 可确保组存在。| 
| 成员| 使用此属性与指定的成员替换当前组成员身份。 此属性的值是数组的表单*域*的字符串\\*用户名*。 如果您在配置设置此属性，不要使用**MembersToExclude**或**MembersToInclude**属性。 这样做将生成一个错误。| 
| MembersToInclude| 使用此属性将成员添加到现有组的成员。 此属性的值是数组的表单*域*的字符串\\*用户名*。 如果您在配置设置此属性，请不使用**成员**属性。 这样做将生成一个错误。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是取决于 ="[资源类型] 资源名称"。| 

## 示例 1

下面的示例演示如何确保两个组名为"myGroup"和"myOtherGroup"存在。 

```powershell
configuration GroupSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {
        GroupSet GroupSetTest
        {
            GroupName        = @("myGroup", "myOtherGroup")
            Ensure           = "Present"
            MembersToInclude = @("contoso\alice", "contoso\bob")
            MembersToExclude = $("contoso\john")
            Credential       = Get-Credential
        }
    }
}
$cd = @{
    AllNodes = @(
        @{
            NodeName                    = 'localhost'
            PSDscAllowPlainTextPassword = $true
            PSDscAllowDomainUser        = $true
        }
    )
}


GroupSetTest -ConfigurationData $cd
```

>**注意︰**此示例使用简单的纯文本凭据。 有关如何进行加密的信息凭据中配置 MOF 文件，请参阅[保护 MOF 文件](secureMOF.md)。


