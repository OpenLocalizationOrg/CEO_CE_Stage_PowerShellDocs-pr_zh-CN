---
title: "DSC WindowsFeatureSet 资源"
ms.date: 2016-05-24
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 1bb0e73a1aae6926040373e017494c2ef5e5fd3e
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC WindowsFeatureSet 资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

**WindowsFeatureSet**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来确保角色和功能添加或删除目标节点上。
该资源是对每个功能中指定呼叫[WindowsFeature 资源](windowsfeatureResource.md)[复合资源](authoringResourceComposite.md)`Name`属性。

当您想要配置多种功能，Windows 到相同的状态，请使用此资源。

## 语法

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]] 
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 名称| 添加或删除角色或您想要确保的功能的名称。 这是与[获取 WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet，**名称**属性和不显示的角色或功能的名称相同。| 
| 凭据| 用于添加或删除角色或功能的凭据。| 
| 确保| 指示是否添加角色或功能。 若要确保的角色或功能的添加、 设置设置此属性对"演示"，以确保删除角色或功能，将属性设为"无"。| 
| IncludeAllSubFeature| 将此属性设置为**$true**包含所有所需子功能与您使用**名称**属性中指定的功能。| 
| LogPath| 要登录操作的资源提供商日志文件的路径。| 
| 取决于| 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
| 源| 如有必要，指示要用于安装，源文件的位置。| 

## 示例

以下配置确保**Web 服务器**(IIS) 和**SMTP 服务器**功能和所有子功能的每个，而安装。

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        } 
    }
}
```

