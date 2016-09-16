---
title: "DSC 服务资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 6c1dce6a3f1b801f7bdf5bf778df8033e3d76280
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 服务资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0


**服务**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来管理上的目标节点的服务。

## 语法

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 名称| 指示的服务名称。 请注意，有时这是不同的显示名称。 您可以获得服务和其当前状态与获取服务 cmdlet 的列表。| 
| BuiltInAccount| 指示登录帐户使用的服务。 允许为此属性的值为︰**本地**、**本地系统**和**网络服务**。| 
| 凭据| 指示下将运行服务的帐户的凭据。 不能使用此属性和__BuiltinAccount__属性。| 
| 取决于| 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
| StartupType| 指示该服务的启动类型。 允许为此属性的值是︰**自动**、**被禁用**，和**手动**| 
| 状态| 指示您想要确保为该服务的状态。| 
| 说明 | 指示目标服务的说明。| 
| 显示名称 | 指示目标服务的显示名称。| 
| 确保 | 指示系统上是否存在目标服务。 将此属性设置为**不存在**以确保目标服务不存在。 将其设置为**演示**（默认值） 确保目标服务存在。|
| 路径 | 指示一项新服务的二进制文件的路径。| 

## 示例

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```

