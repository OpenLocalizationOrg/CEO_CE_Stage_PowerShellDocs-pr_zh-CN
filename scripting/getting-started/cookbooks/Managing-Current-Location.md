---
title: "管理当前位置"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: 77960d8876a7b0bc928158a04b26735aa6be517b
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 管理当前位置
当导航文件资源管理器中的文件夹系统，您通常会有特定的工作位置-即，当前打开的文件夹。 通过单击它们，可以轻松地操作的当前文件夹中的项目。 为 Cmd.exe 之类的命令行界面，当您在同一文件夹为特定文件，您可以访问其指定相对较短名称，而无需指定该文件的完整路径。 当前目录称为工作目录。

Windows PowerShell 使用名词**位置**来引用工作目录，和实现一系列的 cmdlet，以便检查和操作您所在的位置。

### 获取您的当前位置 （获取位置）
要确定您的当前目录位置的路径，请输入**获取位置**命令︰

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> 获取位置 cmdlet 是类似于 BASH shell 中的**密码**命令。 设置位置 cmdlet 是类似于 Cmd.exe 中的**cd**命令。

### 设置您的当前位置 （设置位置）
**获取位置**命令使用**设置位置**命令。 **设置位置**命令可以指定您的位置当前目录。

```
PS> Set-Location -Path C:\Windows
```

输入命令后，您将看到您不会收到任何有关命令的效果的直接反馈。 大多数执行操作的 Windows PowerShell 命令产生或几乎没有输出，因为输出不是始终有用。 若要验证成功目录更改发生时输入**设置位置**命令，包括**-通过**参数输入**设置位置**命令时︰

```
PS> Set-Location -Path C:\Windows -PassThru
Path
----
C:\WINDOWS
```

**-通过**参数可以使用 Windows PowerShell 中的许多设置命令，用于在是没有默认输出的情况下返回结果的信息。

根据您希望在大多数 UNIX 和 Windows 命令外壳，可以指定相对于您的当前位置的方式相同的路径。 对于相对路径，标准表示法以句点 （**.**）表示您当前的文件夹，并以双写的句点 （**.**） 表示您的当前位置的父目录。

例如，如果您在**c:\\Windows**文件夹，以句点 （**.**）表示**c:\\Windows**和双句点 （**.**） 表示**c:**。 您可以通过键入到 C 盘根更改从您的当前位置︰

<pre>PS > 设置的位置的路径。 -通过路径...C:\</pre>

同样的方法适用于 Windows PowerShell 的驱动器不文件系统驱动器，如**HKLM:**。 您可以将您所在的位置设置为 HKLM\\软件通过键入注册表项︰

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

然后，您可以将目录的位置更改为父目录，这是 Windows PowerShell HKLM 的根中︰ 驱动器，通过使用相对路径︰

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

您可以键入设置位置或任何内置的 Windows PowerShell 别名用于设置位置 （cd、 chdir、 sl）。 例如︰

```
cd -Path C:\Windows
```

```
chdir -Path .. -PassThru
```

```
sl -Path HKLM:\SOFTWARE -PassThru
```

### 保存并撤回最近的位置 （推送位置和 Pop 位置）
更改位置时, 很有帮助以跟踪的其中都被和能够返回到上一个位置。 Windows PowerShell cmdlet**推送位置**创建目录路径，其中已，，您可以通过使用互补**Pop 位置**cmdlet 逐步返回通过目录路径的历史记录有序历史的记录 （"堆栈"）。

例如，Windows PowerShell 通常在用户的主目录中启动。

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> Word*堆栈*在许多编程设置，包括.NET Framework 具有特殊的含义。 物理堆栈的项目，如放到堆栈的最后一个项目是您可以关闭堆栈提取的第一个项目。 将项目添加到堆叠一般称为"延迟"堆栈的项目。 提取堆栈项目一般称为"弹出"堆栈的项目。

若要推送到堆栈，当前所在的位置，然后移动到本地设置文件夹，请键入︰

```
PS> Push-Location -Path "Local Settings"
```

您可以将推送到堆栈的 Local Settings 位置，并通过键入移动到 Temp 文件夹︰

```
PS> Push-Location -Path Temp
```

您可以验证输入**获取位置**命令更改目录︰

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

您可以通过输入**Pop 位置**命令，弹出回最近访问的目录，然后输入**获取位置**命令来验证更改︰

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

就像与**设置位置**cmdlet，您可以包含**-通过**参数输入**Pop 位置**cmdlet 来显示您输入的目录时︰

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

您还可以使用具有网络路径位置 cmdlet。 如果您有一个名为公共共享名为 FS01 的服务器，您可以通过键入更改您的位置

```
Set-Location \\FS01\Public
```

或

```
Push-Location \\FS01\Public
```

**推位置**和**设置位置**命令可用于更改位置向任何可用的驱动器。 例如，如果您有包含数据光盘驱动器号 D 与本地光盘驱动器，您可以更改位置为光盘驱动器通过输入**d 设置位置:**命令。

如果驱动器为空，您将收到以下错误消息︰

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

当您使用的命令行界面时，不方便地使用文件资源管理器以查看可用的物理驱动器。 此外，文件资源管理器将不显示您的 Windows PowerShell 驱动器全部。 Windows PowerShell 提供一组命令用于操作 Windows PowerShell 驱动器，我们将讨论这些下一步。

