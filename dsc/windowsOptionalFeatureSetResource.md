---
title: "DSC WindowsOptionalFeatureSet 资源"
ms.date: 2016-05-24
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 1fab04dfcd4ce927bbe526b93c826cf3749a42a5
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC WindowsOptionalFeatureSet 资源

> 适用于︰ Windows PowerShell 5.0

**WindowsOptionalFeatureSet**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来确保在目标节点上启用的可选功能。 该资源是对每个功能中指定呼叫[WindowsOptionalFeature 资源](windowsOptionalFeatureResource.md)[复合资源](authoringResourceComposite.md)`Name`属性。

当您想要配置的数目相同的状态为 Windows 可选功能，请使用此资源。

## 语法

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ] 
    [ RemoveFilesOnDisable = [bool] ]  
    [ LogPath = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ DependsOn = [string[]] ]
    
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 名称| 表示启用或禁用您想要确保的功能的名称。| 
| 确保| 指定是否已启用的功能。 以确保功能已启用，请设置设置此属性对"演示"，以确保禁用功能，将属性设为"无"。|
| 源| 未实现。|
| NoWindowsUpdateCheck| 指定是否 DISM 联系人 Windows 更新 (WU) 时，搜索要启用的功能的源文件。 如果 $true，DISM 没有联系 WU。|
| RemoveFilesOnDisable| 设置为**$true**以删除时禁用这些功能与相关联的所有文件 (即，当**确保**设置为"无")。|
| 日志级别| 最大值输出日志中显示的级别。 接受的值为:"ErrorsOnly"（仅限错误记录）、"ErrorsAndWarning"（记录错误和警告），并且"ErrorsAndWarningAndInformation"（错误、 警告和调试信息记录）。|
| LogPath| 要登录操作的资源提供商日志文件的路径。| 
| 取决于| 指定配置此资源之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
 



