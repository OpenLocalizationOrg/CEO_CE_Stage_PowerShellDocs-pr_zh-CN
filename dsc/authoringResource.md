---
title: "构建自定义的 Windows PowerShell 需要状态配置资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: fe2697de322be99e9b5dfe79090fda4082a73623
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 构建自定义的 Windows PowerShell 需要状态配置资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

Windows PowerShell 需要状态配置 (DSC) 具有内置资源可用于配置您的环境。 （有关详细信息，请参阅[内置 Windows PowerShell 需要状态配置资源](builtInResource.md)）。本主题概述开发资源和与特定信息和示例的主题的链接。

## DSC 资源组件

DSC 资源是 Windows PowerShell 模块。 模块包含该资源的架构 （可配置属性的定义） 和实施工作结束后 （指定了配置的实际工时的代码）。 DSC 资源架构可以定义在 MOF 文件中，并通过脚本模块执行实施。 开始使用 PowerShell 中的类版本 5 支持，请架构和实施工作结束后可以同时定义类中。 以下主题更详细地介绍了如何创建 DSC 资源。

* [编写自定义与 MOF DSC 资源](authoringResourceMOF.md) 
* [在 C 实现 DSC 资源#](authoringResourceMofCS.md) 
* [编写自定义使用 PowerShell 类 DSC 资源](authoringResourceClass.md) 
* [复合资源︰ 作为资源使用 DSC 配置](authoringResourceComposite.md) 
* [使用资源设计器工具](authoringResourceMofDesigner.md) 

