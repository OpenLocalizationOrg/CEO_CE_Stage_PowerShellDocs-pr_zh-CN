---
title: "Linux nxGroup 资源的 DSC"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 2139e4462c0568c30b118ef6cb3ceef1717b52e6
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Linux nxGroup 资源的 DSC

**NxGroup**资源 PowerShell 需要状态配置 (DSC) 中提供了一种机制来管理 Linux 节点上的本地组。

## 语法

```powershell
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Members = <string[]> ]
    [ MebersToInclude = <string[]>]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}

```

## 属性

|  属性 |  说明 | 
|---|---|
| 组名称| 指定您要确保特定状态的组的名称。| 
| 确保| 确定是否要检查是否存在组中。 设置为"演示"，以确保组中存在该属性。 将其设置为"无"以确保组不存在。 默认值为"演示"。| 
| 成员| 指定表单组的成员。| 
| MembersToInclude| 指定您想要确保用户组的成员。| 
| MembersToExclude| 指定您想要确保用户不是组的成员。| 
| PreferredGroupID| 如果可能将组 id 设置为提供的值。 如果当前正在使用的组 id，则使用的下一个可用的组 id。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

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

