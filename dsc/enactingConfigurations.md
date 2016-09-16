---
title: "制定配置"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: caa68898da4c354d711ffc7b8f2b341837beab9b
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 制定配置

>适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

有两种方法来制定 PowerShell 需要状态配置 (DSC) 配置︰ 推送模式和提取模式。

## 推送模式

![推送模式](images/Push.png "How push mode works")

推送模式下指的是积极应用到目标节点，请致电[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet 配置用户。

创建并后编译配置，您可以制定管理其推送模式中通过致电[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet，设置的配置 MOF 所在的位置的路径 cmdlet-路径参数。 例如，如果配置 MOF 位于`C:\DSC\Configurations\localhost.mof`，会将其应用到本地计算机使用以下命令︰ `Start-DscConfiguration -Path 'C:\DSC\Configurations'`

> __注意__︰ 默认情况下，DSC 运行配置作为背景作业。 以交互方式运行配置，呼叫与[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) __-等待__参数。


## 拉入模式

![拉入模式](images/Pull.png "How pull mode works")

在拉入模式提取客户端配置为从远程提取服务器获取其所需的状态配置。 同样，提取服务器已设置到主机 DSC 服务，并已配置的配置和所需的请求客户端的资源。 每个请求客户端已执行定期合规性检查配置的节点的计划的任务。 第一次触发事件时，它会导致验证配置提取客户端上的本地配置管理器 (LCM)。 如果提取客户端配置为所需，没有任何反应。 否则，则 LCM 到提取服务器以获取给定的配置发出请求。 如果提取服务器上存在该配置，它将传递初始验证检查配置传输到提取客户端，其中然后执行通过 LCM。

部署 DSC 提取服务器内部部署的详细信息，请参阅 DSC 提取服务器配置和规划指南。

如果您希望能够充分利用联机服务托管提取服务器功能，请参阅[Azure 自动化 DSC](https://azure.microsoft.com/en-us/documentation/articles/automation-dsc-overview/)服务。

以下主题介绍如何设置提取服务器和客户端︰

- [Web 提取服务器设置](pullServer.md)
- [SMB 提取服务器设置](pullServerSMB.md)
- [配置提取客户端](pullClientConfigID.md)

