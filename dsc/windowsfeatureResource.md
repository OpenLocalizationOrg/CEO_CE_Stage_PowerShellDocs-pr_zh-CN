---
title: "DSC WindowsFeature 资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 98c39d11122d26502723a302ebd7ad4cff0be35d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC WindowsFeature 资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

**WindowsFeature**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来确保角色和功能添加或删除目标节点上。

## 语法

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 名称| 指示添加或删除您想要确保角色或功能的名称。 这是从[获取 WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet，而不角色或功能的显示名称__名称__属性相同。| 
| 凭据| 指明用于添加或删除角色或功能的凭据。| 
| 确保| 指示添加角色或功能。 以确保该角色或功能添加、 设置该属性为"演示"，以确保该角色或功能将被删除，将属性设为"无"。| 
| IncludeAllSubFeature| 将此属性设置为__$true__以确保所有所需的子功能与您使用__名称__属性中指定的功能的状态的状态。| 
| LogPath| 指示位置资源提供程序登录操作的日志文件的路径。| 
| 取决于| 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
| 源| 如有必要，指示要用于安装，源文件的位置。| 

## 示例
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present" 
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature  
}
```

