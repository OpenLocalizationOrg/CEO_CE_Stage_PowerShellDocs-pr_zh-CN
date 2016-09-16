---
title: "DSC ServiceSet 资源"
ms.date: 2016-05-23
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 798609d7e1e7d88e7a9f76f5fff12f63c6109c76
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC ServiceSet 资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0


**ServiceSet**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来管理上的目标节点的服务。 该资源是为每个服务中指定呼叫[服务资源](serviceResource.md)[复合资源](authoringResourceComposite.md)`Name`属性。

当您想要配置大量的服务到相同的状态，请使用此资源。

## 语法

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 名称| 指示服务名称。 请注意，有时这是不同的显示名称。 您可以获得服务和其当前状态与[获取服务](https://technet.microsoft.com/en-us/library/hh849804.aspx)cmdlet 的列表。|
| StartupType| 指示该服务的启动类型。 允许为此属性的值是︰**自动**、**被禁用**，和**手动**|  
| BuiltInAccount| 指示登录帐户使用的服务。 允许为此属性的值为︰**本地**、**本地系统**和**网络服务**。| 
| 状态| 指示您希望确保了该服务的状态︰**停止**或**运行**。| 
| 确保| 指示系统上是否存在服务。 将此属性设置为**不存在**以确保服务不存在。 将其设置为**演示**（默认值） 可确保目标服务存在。|
| 凭据| 指示服务资源将在下运行的帐户的凭据。 不能使用此属性和**BuiltinAccount**属性。| 
| 取决于| 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是*资源名称*和其类型是*资源类型*，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 



## 示例

以下配置启动"Windows 音频"和"远程桌面服务"的服务。

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```

