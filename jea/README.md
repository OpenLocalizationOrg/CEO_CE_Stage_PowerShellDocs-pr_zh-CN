---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "自述文件"
ms.technology: powershell
ms.openlocfilehash: b0ef4ff685b82e1a4e9ab83a45736720df7b39a2
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 刚好足够管理
只需足够管理 (JEA) 是一种安全技术，使委派管理的任何内容，可以使用 PowerShell 管理。
使用 JEA，您可以︰
- 利用虚拟执行特权的操作代表正常用户的帐户的**减少您的计算机上的管理员的数**。
- 通过指定哪些 cmdlet、 函数和外部命令可以运行的**限制用户可以执行哪些操作**。
- 显示究竟是什么"通过即时"录音具有**更好地了解您的用户正在做什么**命令在会话期间执行的用户。

**为什么这很重要？**  
请考虑 DNS 服务器位于何处共同与 Active Directory 域控制器的常见方案。
您的 DNS 管理员需要本地管理员权限以解决问题的 DNS 服务器，但是才能执行，因此，必须以使其特权"域管理员"安全组的成员。
此方法有效地使该计算机上的所有资源的 DNS 管理员控制您的整个域和访问。

在位置 JEA 下,，您可以配置获取他们完成工作，他们所需的所有命令使其都能访问您 DNS 管理员，但没有更多的角色。
这意味着您可以提供适当的访问权限来修复中毒的 DNS 缓存，而不无意中授予他们对 Active Directory 权限或浏览文件系统中，或运行有潜在危险的脚本。
更好的当 JEA 会话配置为使用一次性特权虚拟帐户，您的 DNS 管理员可以使用连接到服务器*未授权*的凭据和仍然无法运行特权的命令。

## 可用性
JEA 与 Windows Server 2016，并行开发，并通过 Windows Management Framework 更新的较旧版本的 Windows 上可用。
JEA 最新版本是以下平台上可用的︰

**Windows Server**
- 服务器 2016年技术此处 4 和更高版本
- Windows Server 2012 R2，2012 年和 2008 R2\*与安装[Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395)

**Windows 客户端**
- 安装 Windows 10 与 11 月更新 (1511)
- Windows 8.1、 8 和 7\*与安装[Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395)

\* 支持 JEA 会话中的虚拟帐户未在 Windows Server 2008 R2 或 Windows 7 上可用。


## 浏览体验指南
若要了解如何创作、 部署和使用您自己的 JEA 终结点的准备？

本指南获取您的预建的 JEA 终结点，以了解最终用户体验类似，然后将引导您完成从头开始重新创建从头端点，帮助说明概念，如会话配置和角色功能的快速入门。

1.  [简介](introduction.md)   
简要回顾为什么要留意 JEA

2.  [先决条件](prerequisites.md)  
介绍如何设置您的环境

3.  [使用 JEA](using-jea.md)  
可帮助您开始通过了解使用 JEA 的运算符体验

4.  [重新进行演示](remake-the-demo-endpoint.md)  
从头开始创建 JEA 会话配置

5.  [角色功能](role-capabilities.md)  
了解有关如何自定义的角色功能文件 JEA 功能

6.  [端到端-Active Directory](end-to-end---active-directory.md)  
进行管理 Active Directory 全新终结点

7.  [多计算机部署和维护](multi-machine-deployment-and-maintenance.md)  
了解如何部署和创作更改与缩放

8.  [在 JEA 报告](reporting-on-jea.md)  
了解如何审核报告所有 JEA 操作和基础结构

9.  附录
  - [在本指南的关键概念](key-concepts-used-throughout-this-guide.md)  
  -  [创建域控制器](creating-a-domain-controller.md)  
  -  [在黑名单](on-blacklisting.md)  
  -  [限制命令时的注意事项](considerations-when-limiting-commands.md)  
  -  [角色功能的常见错误](common-role-capability-pitfalls.md)

## 开始创作自己 JEA 终结点
可以轻松地创作 JEA 终结点--只需有 JEA 启用系统和文本编辑器 （如 PowerShell ISE)。
一个有用的提示若要开始创建使用主干文件是[`New-PSRoleCapabilityFile -Path <path>`](https://technet.microsoft.com/library/mt631422.aspx)和[`New-PSSessionConfigurationFile -Path <Path>`](https://technet.microsoft.com/library/mt631422.aspx)不带任何其他参数。
这些主干文件包含的所有适用的配置字段以及有用的注释，用于解释什么每个字段可用于。

创作 JEA 终结点更加轻松，查看[JEA 工具包帮助器](http://blogs.technet.com/b/privatecloud/archive/2015/12/20/introducing-the-updated-jea-helper-tool.aspx)提供的 GUI，您可以使用其创作会话配置和角色功能的文件。
即使支持生成角色功能基于 PowerShell 日志从您开始使用您的用户定期运行以完成工作的命令。

