---
title: "获取有关命令的信息"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: 4590982cda7cc2a50d6420306002a9e11458381d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 获取有关命令的信息
**获取命令**的 Windows PowerShell cmdlet 获取您当前的会话中可用的所有命令。 在 Windows PowerShell 提示符下键入**获取命令**时，您将看到类似于以下结果︰

```
PS> Get-Command
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
Cmdlet          Add-Member                      Add-Member [-MemberType] <PS...
...
```

此输出看起来非常类似的 Cmd.exe 帮助输出︰ 表格内部命令的摘要。 **获取命令**命令摘录中输出如上所示，每个命令，显示具有 Cmdlet 命令类型。 Cmdlet 是 Windows PowerShell 内部命令类型-向 Cmd.exe**目录**和**cd**命令和 built-ins 中例如 BASH UNIX 外壳大致对应的类型。

在**获取命令**命令的输出中，所有定义都结尾省略号 （...） 以指示 PowerShell 无法显示在可用空间中的所有内容。 Windows PowerShell 显示输出，它为文本输出格式设置，然后排列它以使数据完全放入窗口。 我们将讨论此更高版本在部分在格式化程序。

**获取命令**cmdlet 具有获取的每个 cmdlet 语法**语法**参数。 若要获取获取帮助 cmdlet 的语法，请使用以下命令︰

**获取命令获取帮助的语法**

```
Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Full] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Detailed] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Examples] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Parameter <String>] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]
```

### 显示可用的命令类型
**获取命令**命令不会列出在 Windows PowerShell 中可用的每个命令。 相反，**获取命令**命令列出当前会话中的 cmdlet。 Windows PowerShell 实际支持几种其他类型的命令。 别名、 函数和脚本也是 Windows PowerShell 命令，虽然不对其进行讨论的 Windows PowerShell 的用户指南中的详细信息。 外部文件可执行文件，或已注册的文件类型处理程序中，也被视为命令。

若要在会话中获取所有命令，请键入︰

```
Get-Command *
```

此列表中搜索路径包括外部文件，因为它可能包含数千个项目。 更多，最好查看一组缩减的命令。

要获取其他类型的本机命令，请使用**获取命令**cmdlet 的参数的**命令类型**。

> [!NOTE]
> 星号 (\*) 用于 Windows PowerShell 命令参数中的匹配的通配符。 \*表示"匹配一项或多个任意字符"。 您可以键入**获取命令\&#42;**查找字母开头的所有命令"a"。 匹配 Cmd.exe 通配符，与 Windows PowerShell 通配符将匹配一段。

若要获取命令别名，是分配给的昵称的命令，请键入︰

```
Get-Command -CommandType Alias
```

要获取当前会话中的函数，请键入︰

```
Get-Command -CommandType Function
```

若要显示在 Windows PowerShell 搜索路径的脚本，请键入︰

```
Get-Command -CommandType Script
```

