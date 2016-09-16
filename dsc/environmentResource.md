---
title: "DSC 环境资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 4a51b56091aea23568674cdc7d4d4128c78b239c
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 环境资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

在 Windows PowerShell 需要状态配置 (DSC) 的__环境__资源提供了一种机制来管理系统环境变量。

## 语法
``` mof
Environment [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Path = [bool] ]
    [ DependsOn = [string[]] ]
    [ Value = [string] ]
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 名称| 指示您希望确保特定状态的环境变量的名称。| 
| 确保| 指明是否存在一个变量。 将此属性设置为__演示__创建环境变量，如果不存在或以确保它的值匹配什么通过提供的__值__属性如果变量已经存在。 将其设置为__不存在__要删除变量，如果存在。| 
| 路径| 定义要配置的环境变量。 如果变量是__路径__变量中; 此属性设置为__$true__否则，将其设置为__$false__。 默认情况下__$false__。 如果正在配置变量是__Path__变量，通过__值__属性提供的值将追加到现有值。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
| 值| 要分配给环境变量的值。| 

## 示例

下面的示例确保__TestEnvironmentVariable__演示，它具有__TestValue__的值。 如果不存在，则将创建它。

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```

