---
title: "DSC 用户资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 84ed3408cfef1dbc99f6f3147ae36be09bca67e4
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
#用户 DSC 资源#

 
>适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0


在 Windows PowerShell 需要状态配置 (DSC) 的__用户__资源提供一种机制来管理本地用户帐户上的目标节点。


##语法##

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## 属性
|  属性  |  说明   | 
|---|---| 
| 用户名| 指示您希望确保特定状态的帐户名称。| 
| 说明| 表示您想要使用的用户帐户的说明。| 
| 禁用| 指明是否已启用该帐户。 将此属性设置为__$true__以确保此帐户已禁用，并将其设置为__$false__以确保它已启用。| 
| 确保| 指明是否存在该帐户。 将"演示"，以确保该帐户存在该属性并将其设置为"无"以确保该帐户不存在。| 
| 全名| 表示您想要使用的用户帐户的完整名称的字符串。| 
| 密码| 指示您想要用于此帐户的密码。 | 
| PasswordChangeNotAllowed| 指示是否用户可以更改密码。 将此属性设置为__$true__以确保用户不能更改密码，并将其设置为__$false__以允许用户更改密码。 默认值为__$false__。| 
| PasswordChangeRequired| 指示如果用户必须在更改密码下一步登录。 如果用户必须更改密码，请将此属性设置为__$true__ 。 默认值为__$true__。| 
| PasswordNeverExpires| 指示是否的密码将过期。 以确保此帐户的密码将永远不会过期，将此属性设置为__$true__，并将其设置为__$false__如果密码过期。 默认值为__$false__。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 示例

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = “[Group]GroupExample" # Configures GroupExample first
}
```

