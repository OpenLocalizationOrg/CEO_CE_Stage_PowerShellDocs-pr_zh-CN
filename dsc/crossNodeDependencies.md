---
title: "指定跨节点相关性"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: c99ef444027a82d3adeba6a060f60fba3a0fe530
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 指定跨节点相关性

> 适用于︰ Windows PowerShell 5.0

DSC 提供特殊资源、 **WaitForAll**、 **WaitForAny**，以及可以用于配置中指定的依赖关系其他节点上配置的**WaitForSome** 。 这些资源的行为如下所示︰

* **WaitForAll**︰ 如果指定的资源位于定义**节点名称**属性中的所有目标节点上所需状态成功。
* **WaitForAny**︰ 如果指定的资源位于至少一个**节点名称**属性中定义的目标节点上所需状态成功。
* **WaitForSome**︰ 指定**NodeCount**属性除了**节点名称**属性。 资源成功资源是否处于最小值 （由**NodeCount**指定） 定义的**节点名称**属性的节点数上所需的状态。 

## 使用 WaitForXXXX 资源

若要使用的**WaitForXXXX**资源，您可以创建资源块指定 DSC 资源和节点等待该资源类型。 然后**取决于**中使用属性任何其他资源块配置中必须等待成功**WaitForXXXX**节点中指定的条件。

例如，以下配置中，在目标节点正在等待完成**MyDC**节点上最大次数 30，与在 15 秒的时间间隔，目标节点可以加入域之前**xADDomain**资源。

```PowerShell
Configuration JoinDomain

{
    Import-DscResource -Module xComputerManagement

    Node myDomainJoinedServer
    {

        WaitForAll DC
        {
            ResourceName      = '[xADDomain]NewDomain'
            NodeName          = 'MyDC'
            RetryIntervalSec  = 15
            RetryCount        = 30
        }

        xComputer JoinDomain
        {
            Name             = 'MyPC'
            DomainName       = 'Contoso.com'
            Credential       = (Get-Credential)
            DependsOn        ='[WaitForAll]DC'
        }
    }
}
```

>**注意︰**默认情况下 WaitForXXX 资源尝试一次，然后失败。 虽然不是必需的您通常希望指定重试时间间隔和计数。

## 另请参阅
* [DSC 配置](configurations.md)
* [DSC 资源](resources.md)
* [配置本地配置管理器](metaConfig.md)

