---
title: "Windows PowerShell 需要状态配置概述"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 2dff393684eb46aab6853010cebc76d5ca4b93a8
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows PowerShell 需要状态配置概述 

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

本主题介绍了 Windows PowerShell 中的 Windows PowerShell 需要状态配置 (DSC) 功能。 要大致了解 DSC 并查找您需要了解和使用 DSC 文档资源，您可以使用此主题。

## 功能说明
DSC 是一个新的管理平台，使部署和管理软件服务配置数据管理的环境这些服务在其中运行的 Windows PowerShell 中。

DSC 提供一组的 Windows PowerShell 语言扩展、 新的 Windows PowerShell cmdlet 和资源可用于声明方式指定希望如何您软件的环境以进行配置。 它还提供了一种方法来维持和管理现有配置。

## 实际应用
以下是在其中使用内置 DSC 资源以配置和管理自动求和中的一组计算机 （也称为目标节点） 某些示例方案︰

* 启用或禁用服务器角色和功能
* 管理注册表设置
* 管理文件和目录
* 启动、 停止和管理流程和服务
* 管理组和用户帐户
* 部署新的软件
* 管理环境变量
* 运行 Windows PowerShell 脚本
* 修复配置所具有的波动远离所需的状态
* 发现给定节点的实际配置状态

## 关键概念
DSC 是用于配置、 部署和管理系统声明性平台。 它包括三个主要组件︰

* [配置](configurations.md)是声明性 PowerShell 脚本定义并配置实例的资源。 时运行配置、 DSC （和资源通过配置调用） 将只需"使其"，确保系统位于由配置布局的状态。 DSC 配置也是幂等︰ 本地配置管理器 (LCM) 将继续确保处于任何状态配置配置机声明。
* 资源是强制性构建基块 DSC 它们编写模型子系统的各种组件和实施其更改状态的控制流。 它们驻留在 PowerShell 模块，可写入模型作为通用文件或 Windows 流程，或作为 IIS 服务器或运行在 Azure 虚拟机为特定的内容。
* 本地配置管理器 (LCM) 是的引擎依据 DSC 方便进行资源和配置之间的交互。 LCM 定期轮询系统使用控制流实现的资源以确保维护的状态由配置布局。 如果超出状态系统，则 LCM 使用更多资源内的逻辑"使其"根据配置声明。 

DSC 还包括新语言关键字、 cmdlet 和工具允许创建配置，帮助您构建 DSC 资源、 调用配置，并管理 LCM 的数目。 使用这些 cmdlet 的许多为 PSDesiredStateConfiguration 模块的一部分可在 Windows 8.1 (包括`Start-DscConfiguration`， `Set-DscLocalConfigurationManager`，和`Get-DscResource`)。 （ [PowerShell 库](https://www.powershellgallery.com/packages/xDSCResourceDesigner/)中找到） xDscResourceDesigner 是 cmdlet 的简化 DSC 资源的开发的集合。

## 另请参阅
* [DSC 配置](configurations.md)
* [DSC 资源](resources.md)
* [配置本地配置管理器](metaConfig.md)

