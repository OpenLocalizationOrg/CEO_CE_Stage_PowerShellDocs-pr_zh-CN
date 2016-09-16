---
title: "DSC WindowsOptionalFeature 资源"
ms.date: 2016-05-24
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 26d140d68760ec92b3b6cbc31d0735eaaf671d9c
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC WindowsOptionalFeature 资源

> 适用于︰ Windows PowerShell 5.0

**WindowsOptionalFeature**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来确保在目标节点上启用的可选功能。

## 语法

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 名称| 表示启用或禁用您想要确保功能的名称。| 
| 确保| 指定是否已启用该功能。 以确保该功能已启用、 设置"演示"，以确保该功能已禁用此属性将属性设为"无"。|
| 源| 未实现。|
| NoWindowsUpdateCheck| 指定是否 DISM 联系人 Windows 更新 (WU) 时，搜索要启用的功能的源文件。 如果 $true，DISM 没有联系 WU。|
| RemoveFilesOnDisable| 设置为**$true**以删除它被禁用该功能与相关联的所有文件 (即，当**确保**设置为"无")。|
| 日志级别| 最大值输出日志中显示的级别。 接受的值为: （仅限错误记录）"ErrorsOnly"、"ErrorsAndWarning"（记录错误和警告），并且"ErrorsAndWarningAndInformation"（错误、 警告和调试信息记录）。|
| LogPath| 要登录操作的资源提供商日志文件的路径。| 
| 取决于| 指定配置此资源之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
 



