---
title: "DSC 日志资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: ac5ca96c9402aa39b7cfe4058d5721ebea9405db
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 日志资源 

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

__日志__资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来撰写邮件所需 Windows-Microsoft-状态配置/分析的事件日志。

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

注意︰ 默认情况下被启用仅 DSC 的操作日志。
分析日志将可用或可见之前，必须启用它。
请参阅以下文章。

[DSC 事件日志的位置在哪里？](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## 属性
|  属性  |  说明   | 
|---|---| 
| 消息| 指示要写入 Microsoft-Windows-Desired 状态配置/分析事件日志的邮件。| 
| 取决于 | 指示此日志消息获取写入之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 示例

下面的示例演示如何在 Microsoft-Windows-Desired 状态配置/分析的事件日志中包含一条消息。

> **注意**︰ 如果您使用此资源配置运行[测试 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) ，它将始终返回**$false**。

```powershell 
Log LogExample
{
    Message = "This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log."
} 
```

