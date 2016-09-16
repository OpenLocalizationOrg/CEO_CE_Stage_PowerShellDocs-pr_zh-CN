---
title: "查看对象结构获取成员"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: 041b58f5fcfdf2225704adcb943de864c94502c1
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 查看对象结构 （获取成员）
由于对象播放 Windows PowerShell 中的角色中心，有几个本机命令设计为支持任意对象类型。 最重要的一项是**获取成员**命令。

分析命令返回的对象的最简单方法是**获取成员**cmdlet 给该命令将输出。 **获取成员**cmdlet 显示对象类型正式名称和其成员的完整列表。 有时会主要返回的元素的数目。 例如，进程对象可以具有超过 100 的成员。

若要查看的处理对象和页面输出的所有成员，以便您可以查看它的所有，请键入︰

```
PS> Get-Process | Get-Member | Out-Host -Paging
```

此命令的输出将如下所示︰

```
TypeName: System.Diagnostics.Process

Name                           MemberType     Definition
----                           ----------     ----------
Handles                        AliasProperty  Handles = Handlecount
Name                           AliasProperty  Name = ProcessName
NPM                            AliasProperty  NPM = NonpagedSystemMemorySize
PM                             AliasProperty  PM = PagedMemorySize
VM                             AliasProperty  VM = VirtualMemorySize
WS                             AliasProperty  WS = WorkingSet
add_Disposed                   Method         System.Void add_Disposed(Event...
...
```

我们可以通过筛选的元素，我们希望看到不提供此长列表中的信息更易于使用。 **获取成员**命令允许您只有成员属性的列表。 有几种形式的属性。 如果我们将**获取 MemberMemberType**参数设置为**属性**的值，则 cmdlet 显示任何类型的属性。 结果列表仍然是很长，但更易于管理︰

```
PS> Get-Process | Get-Member -MemberType Properties

   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
...
ExitCode                   Property       System.Int32 ExitCode {get;}
...
Handle                     Property       System.IntPtr Handle {get;}
...
CPU                        ScriptProperty System.Object CPU {get=$this.Total...
...
Path                       ScriptProperty System.Object Path {get=$this.Main...
...
```

> [!NOTE]
> MemberType 允许的值是 AliasProperty、 CodeProperty、 属性、 NoteProperty、 ScriptProperty、 属性、 PropertySet、 方法、 CodeMethod、 ScriptMethod、 方法、 ParameterizedProperty、 成员集，和所有。

有超过 60 流程的属性。 Windows PowerShell 通常会显示只有少量任何已知对象的属性是显示它们的原因会产生难以管理大量信息。

> [!NOTE]
> Windows PowerShell 确定如何通过使用信息存储在具有名称以结尾的 XML 文件中显示对象类型。 format.ps1xml。 对于流程对象，这些.NET System.Diagnostics.Process 对象的格式数据存储在 PowerShellCore.format.ps1xml。

如果您需要查看属性以外 Windows PowerShell 显示默认情况下，您需要自己格式输出数据。 这可以通过使用格式 cmdlet。

