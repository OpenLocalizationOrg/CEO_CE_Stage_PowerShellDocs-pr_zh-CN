---
title: "Linux nxUser 资源的 DSC"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 7813185313845b74e2a37dfa4ec6bb109f32f0eb
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Linux nxUser 资源的 DSC

**NxUser**资源 PowerShell 需要状态配置 (DSC) 中提供的机制管理 Linux 节点上的本地用户。

## 语法

```
nxUser <string> #ResourceName
{
    UserName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ FullName = <string> ]
    [ Description = <string> ]
    [ Password = <string> ]
    [ Disabled = <bool> ]
    [ PasswordChangeRequired = <bool> ]
    [ HomeDirectory = <string> ]
    [ Mode = <string> ]
    [ GroupID = <string> ]
    [ DependsOn = <string[]> ]

}
```

## 属性

|  属性 |  指示您希望确保特定状态的帐户名称。 | 
|---|---|
| 用户名| 指定要确保文件或目录状态的位置。| 
| 确保| 指定是否存在该帐户。 将"演示"，以确保该帐户存在该属性并将其设置为"无"以确保该帐户不存在。| 
| 全名| 包含要使用的用户帐户的完整名称的字符串。| 
| 说明| 对用户帐户的说明。| 
| 密码| 在相应的窗体的 Linux 计算机的用户密码哈希。 通常情况下，这是 salted 的 sha-256 或 sha-512 哈希。 在 Debian 和 Ubuntu Linux 上，可以使用 mkpasswd 命令生成此值。 对于其他 Linux distros，Python 的 Crypt 库的 crypt 方法可以用于生成哈希。| 
| 禁用| 指明是否启用了帐户。 将此属性设置为**$true**以确保此帐户已禁用，并将其设置为**$false**以确保它已启用。| 
| PasswordChangeRequired| 指示用户是否可以更改密码。 将此属性设置为**$true**以确保用户不能更改密码，并将其设置为**$false**以允许用户更改密码。 默认值为**$false**。 如果以前不存在的用户帐户，并且正在创建仅计算此属性。| 
| 主目录下| 用户的主目录。| 
| GroupID| 用户的主要组 ID。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先将"资源名称"，其类型是"资源类型"，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 示例

下面的示例可确保用户"monuser"存在，而是"DBusers"组的成员。

```
Import-DSCResource -Module nx 

Node $node {
nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}
 
nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"            
}
}
```

