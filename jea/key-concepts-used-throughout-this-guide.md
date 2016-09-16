---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "在本指南的关键概念"
ms.technology: powershell
ms.openlocfilehash: 873ab19fdf43ec4ac41cc546aa94b64fbc607984
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 在本指南的关键概念
**对 JEA 到底是什么？**

JEA 是 PowerShell[局限终结点](http://blogs.technet.com/b/heyscriptingguy/archive/2014/03/31/introduction-to-powershell-endpoints.aspx)添加中角色定义、 虚拟帐户和许多其他改进，以使其更容易地锁定您管理的终结点的扩展。
JEA 终结点组成 PowerShell 会话的配置文件和一个或多个角色功能文件。

**什么是会话配置和角色功能的文件？**

PowerShell 会话的配置文件 (.pssc) 定义*谁*可以连接到一个 PowerShell 终结点，和*如何*将其配置。
这是您将在这里映射到特定的管理角色的用户和安全组和配置全局设置，例如虚拟帐户和抄写的策略。
特定于每台计算机，允许您控制 access 在每台计算机的基础上，如果需要的会话配置文件。

PowerShell 角色功能文件 (.psrc) 定义*哪些*属于角色的用户将能够在系统上执行。
在这里，您可以限制哪些 cmdlet、 函数、 提供商和外部的用户可能在 JEA 会话中使用的程序。
通常是通用提供服务 （DNS 管理、 1 级的技术支持人员、 只读库存审核等） 的角色的角色功能文件和属于 PowerShell 模块，轻松地在您的环境和与其他人共享它们。

**JEA 利用虚拟帐户有什么功能？**

在 PowerShell 会话的配置文件中，您可以配置 JEA 会话使用虚拟"运行"帐户。
虚拟帐户是用户的命令将在其上下文下执行特定会话中为特定连接用户旋转的一次性特权的帐户。
虚拟帐户属于本地的"管理员"安全组，默认情况下，但可以选择性地配置为只属于您指定的安全组。

**远程 PowerShell 处理**︰ PowerShell 远程处理允许您远程计算机上运行的 PowerShell 命令。
您可以对一个或多个计算机执行操作，然后使用临时或永久连接。
在此演示中，为您的本地计算机上的交互式会话与远程您。
JEA 限制通过 PowerShell 远程处理可用的功能。
有关 PowerShell 远程控制的详细信息，请运行`Get-Help about_Remote`。

**用户 RunAs**︰ 当使用 JEA，非管理员"作为运行"权限"虚拟帐户。"
虚拟帐户仅持续远程会话的持续时间。
也就是说，它创建当用户连接到的终结点，并破坏时用户结束会话。
默认情况下，虚拟帐户是本地 Administrators 组的成员。
在域控制器上，它是域管理员组的成员。
虚拟帐户是本地计算机他们创建，并没有该计算机以外的权限。
这意味着注册这些属性不在 Active Directory （分配没有 RID）。
此外，如果允许的命令/脚本尝试访问在本地计算机以外的资源，它将访问这些资源在计算机上的身份，不虚拟帐户身份信息。

**"连接"用户**︰ 连接到的 JEA 终结点以及向谁非管理员用户角色分配。
该用户运行的任何命令运行 RunAs 用户或虚拟帐户的上下文。

