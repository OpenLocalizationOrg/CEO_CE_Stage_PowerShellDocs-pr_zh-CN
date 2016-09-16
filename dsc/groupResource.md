---
title: "DSC 组资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 12c6ad6f30b4e1b67296289c927e59fd64079675
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 组资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

组资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来管理本地组目标节点上。

##语法##
```
Group [string] #ResourceName
{
    GroupName = [string]
    [ Credential = [PSCredential] ]
    [ Description = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Members = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ MembersToInclude = [string[]] ]
    [ DependsOn = [string[]] ]
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 组名称| 您要确保特定状态的组的名称。| 
| 凭据| 访问远程资源所需的凭据。 **注意**︰ 此帐户必须具有适当的 Active Directory 权限，将所有非本地帐户添加到组。否则，将发生错误。
| 说明| 组的说明。| 
| 确保| 指明是否存在组中。 设置为"无"以确保组不存在该属性。 设置以"演示"（默认值） 确保组存在。| 
| 成员| 使用此属性与指定的成员替换当前组成员身份。 此属性的值是数组的表单*域*的字符串\\*用户名*。 如果您在配置设置此属性，不要使用**MembersToExclude**或**MembersToInclude**属性。 这样做将生成一个错误。| 
| MembersToExclude| 使用此属性，若要删除现有的成员资格组的成员。 此属性的值是数组的表单*域*的字符串\\*用户名*。 如果您在配置设置此属性，请不使用**成员**属性。 这样做将生成一个错误。| 
| MembersToInclude| 使用此属性将成员添加到现有组的成员。 此属性的值是数组的表单*域*的字符串\\*用户名*。 如果您在配置设置此属性，请不使用**成员**属性。 这样做将生成一个错误。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是取决于 ="[资源类型] 资源名称"。| 

## 示例 1

下面的示例演示如何确保组名为"TestGroup"不存在。 

```powershell
Group GroupExample
{
    # This will remove TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```
## 示例 2
下面的示例演示如何添加到本地 administrators 组的 Active Directory 用户为多机实验室生成其中您已使用的 PSCredential 本地管理员帐户的一部分。 为此后还可以使用的域管理员帐户 （域升级） 我们然后需要此现有 PSCredential 转换域友好的凭据，以便我们可以将域用户添加到本地 Administrators 组的成员服务器上。

```powershell
@{
    AllNodes = @(
        @{
            NodeName = '*';
            DomainName = 'SubTest.contoso.com';
         }
     @{
            NodeName = 'Box2';
            AdminAccount = 'Admin-Dave_Alexanderson'   
      }    
    )
}
                  
$domain = $node.DomainName.split('.')[0]
$DCredential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList ("$domain\$($credential.Username)", $Credential.Password)

Group AddADUserToLocalAdminGroup
        {
            GroupName='Administrators'   
            Ensure= 'Present'             
            MembersToInclude= "$domain\$($Node.AdminAccount)"
            Credential = $dCredential    
            PsDscRunAsCredential = $DCredential
        }
```

