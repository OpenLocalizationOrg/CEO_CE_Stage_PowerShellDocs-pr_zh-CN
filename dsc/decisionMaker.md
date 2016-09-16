---
title: "需要的决策者状态配置概述"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 0c6dd3499ed47915b190cfeb906ccafdfa43b49f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 需要的决策者状态配置概述 #

本文介绍使用 PowerShell 需要状态配置 (DSC) 的业务好处。 它不是一个技术指南。

## 什么是所需状态配置？ ##

Windows PowerShell 需要状态配置 (DSC) 是基于开放标准的 Windows 中内置配置管理平台。 DSC 非常灵活，可以在每个阶段部署生命周期 （开发、 测试、 预生产、 生产），以及扩展期间函数可靠且以一致的方式。 

DSC 围绕概念的"[配置](https://msdn.microsoft.com/en-us/powershell/dsc/configurations)"，这是与特定的特征描述环境的计算机 （"节点"） 组成的易读文档。 这些特征可以简单，只需确保启用了特定的 Windows 功能，也一样复杂的部署 SharePoint。 

DSC 也具有监视和报告在中构建。 如果系统不再符合要求，DSC 可以引发警报和更正系统的表现。 

## 使用所需的状态配置的好处 ##

配置旨在能轻松地阅读、 存储和更新。 配置只声明状态目标设备应，而不是编写说明如何将它们放在该状态。 这使得大大降低成本，以了解、 采用、 实施和维护 DSC 通过配置。 

创建配置意味着在一个位置，为"事实的单个源"捕获复杂的部署步骤。 这使得重复的部署的一组特定机的重要性低得多出错。 反过来，这使得部署更快、 更可靠。 此项服务使快速缩短复杂的部署。

配置均可通过[PowerShell 库](https://powershellgallery.com)共享。 这意味着常见方案和最佳做法可能已经存在的需要完成的工时。


## 所需的状态配置和 DevOps ##

[DevOps](http://blogs.technet.com/b/ashleymcglone/archive/2015/11/20/devops-for-n00bs-ie-windows-people.aspx)是人员、 技术和允许快速部署和迭代的文化的组合。 DSC 几点与 DevOps 设计。 有一个配置定义环境意味着开发人员可以对其配置为要求进行编码、 签入源控件，该配置和操作团队可以轻松地部署的代码，而无需穿过出错的手动流程。 

配置也是[数据驱动](https://msdn.microsoft.com/en-us/powershell/dsc/configdata)，这样使得更加轻松操作数团队来标识和更改无需开发人员参与的环境。 

## 需要状态配置和关闭-本地 ##

DSC 可以用于管理内部部署和部署关闭部署。 在部署解决方案的所需状态配置具有可用于集中管理机和其状态报告[提取服务器](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver)。 对于云解决方案，需要状态配置是可用 Windows 是可用的位置。 也有一些特定产品从 Azure 上需要状态配置，如[Azure 自动化](https://azure.microsoft.com/en-us/documentation/services/automation/)，它可集中管理报告的所需状态配置生成。 

## DSC 和兼容性 ##

尽管在 Windows Server 2012 R2 中引入了 DSC，可通过 Windows Management Framework (WMF) 程序包普通操作系统。 [PowerShell 主页](https://msdn.microsoft.com/en-us/powershell/)上，可以找到有关 WMF 的详细信息。 

DSC 也可用于管理 Linux。 有关详细信息，请参阅[linux DSC 入门](https://msdn.microsoft.com/en-us/powershell/dsc/lnxgettingstarted)

