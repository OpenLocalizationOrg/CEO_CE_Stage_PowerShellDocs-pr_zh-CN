---
title: "WMF 5.1 （预览） 中的已知的问题"
ms.date: 2016-07-13
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
author: krishna
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 854da31929147c2886354e520c71a5f2f6f3aed7
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
#WMF 5.1 （预览） 中的已知的问题 #

> 注意︰ 此信息是初步，可能会发生更改。

##Pester
在此版本中，有两个问题，您应注意的 Nano 服务器上使用 Pester 时︰

* 进行测试，Pester 本身导致一些故障由于完整 CLR 和核心 CLR 之间的差异。 具体而言，验证方法不可用的 XmlDocument 类型。 尝试验证 nunit 输出日志架构的六个测试已知会失败。 
* 一个代码报道测试 curently 失败，因为 Nano 服务器中不存在*WindowsFeature* DSC 资源。 不过，这些故障通常误报，可以忽略。

##操作验证 

* 由于非工作日帮助 URI Microsoft.PowerShell.Operation.Validation 模块更新帮助将会失败
