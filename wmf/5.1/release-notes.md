---
title: "WMF 5.1 发行说明 （预览）"
ms.date: 2016-07-27
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
author: jkeithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 49a03f52535123c61646f652286ffd05bee04496
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows Management Framework (WMF) 5.1 预览发行说明 #

WMF 5.1 预览包括与 Windows Server 2016 发布的 PowerShell、 WMI、 WinRM，和软件库存和许可 (SIL) 组件。 WMF 5.1 可以安装在 Windows 7、 Windows 8.1、 Windows Server 2008 R2，2012 和 2012 R2，并通过 WMF 5.0 RTM 包括中提供了一些改进︰

- 新的 cmdlet︰ 本地用户和组;获取 ComputerInfo
- PowerShellGet 改进包括强制签名的模块，并安装 JEA 模块
- PackageManagement 添加容器，CBS 设置基于 EXE 的设置，CAB 程序包的支持
- 调试 DSC 和 PowerShell 类的改进
- 安全性增强功能包括强制实施即将从服务器中提取并使用 PowerShellGet cmdlet 时的目录签名模块
- 响应用户请求和问题的数字

**在重要笔记︰**

- **WMF 5.1 预览需要.NET Framework 46**。 安装会成功，但关键功能，如果未安装.NET 46 将失败。 [安装和配置 WMF 5.1 （预览）](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure)主题中提供的说明。 
- 这次**WMF 5.1 预览不支持生产**部署。 这被为了提供有关版中的最早的信息，并使您能够向 PowerShell 团队提供反馈。
- 可以直接通过 WMF 5.0 安装 WMF 5.1 预览。
- 它是 WMF 4.0 当前才能在 Windows 7 和 Windows Server 2008 上安装 WMF 5.1 预览所需要的已知的问题。 此要求应被删除之前的最终版本。
- 安装将来的版本的 WMF 5.1，包括 RTM 版本中，将需要卸载 WMF 5.1 预览。

