---
title: "DSC 为 Linux nxPackage 资源的"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 31867cc7af96a3d8d527f5906d77bed5206940b4
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Linux nxPackage 资源的 DSC

**NxPackage**资源 PowerShell 需要状态配置 (DSC) 中提供了一种机制来管理包 Linux 节点上。

## 语法

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]
    
}
```

## 属性

|  属性 |  说明 | 
|---|---|
| 名称| 您要确保特定状态包的名称。| 
| 确保| 确定是否要检查是否存在包。 设置为"演示"，以确保包存在该属性。 将其设置为"无"以确保包不存在。 默认值为"演示"。|  
| PackageManager| 支持的值是"yum"、"apt，"和"zypper"。 指定要使用时安装程序包程序包管理器。 如果指定**文件路径**，则所提供的路径将用于安装程序包。 否则，将使用程序包管理器以从预配置的库中安装程序包。 如果**PackageManager**和**文件路径**都不提供，将使用系统默认程序包管理器。| 
| 文件路径| 文件路径包所在的位置| 
| PackageGroup| 如果应**$true**，**名称**为用于**PackageManager**包组的名称。 提供**文件路径**时**PacakgeGroup**无效。| 
| 参数| 将传递到包完全按照提供的参数字符串。| 
| ReturnCode| 预期返回代码。 如果实际返回代码不匹配所需的值在这里，提供配置将返回错误。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 示例

下面的示例确保使用"Yum"程序包管理器的 Linux 计算机上安装了名为"httpd"程序包。

```
Import-DSCResource -Module nx 

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```

