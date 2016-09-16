---
title: "Windows PowerShell 管理驱动器"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: bd809e38-8de9-437a-a250-f30a667d11b4
ms.openlocfilehash: 776e55de817dd200142965e19ce84bbe776fcb9d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows PowerShell 管理驱动器
*Windows PowerShell 驱动器*是您可以访问 Windows PowerShell 中的文件系统驱动器等数据存储位置。 Windows PowerShell 提供商，为您创建一些驱动器，如文件系统驱动器 （包括 c︰ 和 d:） 注册表驱动器 (HKCU︰ 和 HKLM:)，以及证书驱动器 (证书:)，并且您可以创建您自己的 Windows PowerShell 驱动器。 这些驱动器都非常有用，但它们仅在 Windows PowerShell 中可用。 您不能使用其他 Windows 工具，如文件资源管理器或 Cmd.exe 访问它们。

Windows PowerShell 将名词， **PSDrive**，用于使用 Windows PowerShell 驱动器的命令。 在您的 Windows PowerShell 会话的 Windows PowerShell 驱动器列表，请**获取 PSDrive** cmdlet。

```
PS> Get-PSDrive

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
Alias      Alias
C          FileSystem    C:\                                 ...And Settings\me
cert       Certificate   \
D          FileSystem    D:\
Env        Environment
Function   Function
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
Variable   Variable
```

在显示的驱动器与在您的系统驱动器会有所不同，但列表将类似于**获取 PSDrive**命令如上所示的输出。

文件系统驱动器是 Windows PowerShell 驱动器子集。 您可以识别文件系统驱动器通过提供商列中的文件系统项。 （Windows PowerShell 中的文件系统驱动器支持通过 Windows PowerShell 文件系统提供商。）

若要查看**获取 PSDrive** cmdlet 的语法，键入与**语法**参数**获取命令**命令︰

```
PS> Get-Command -Name Get-PSDrive -Syntax
Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

**PSProvider**参数可以显示特定的提供程序支持的 Windows PowerShell 驱动器。 例如，要显示 Windows PowerShell 文件系统提供程序支持的 Windows PowerShell 驱动器，请键入**PSProvider**参数和**文件系统**值**获取 PSDrive**命令︰

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

若要查看表示注册表键的 Windows PowerShell 驱动器，请使用**PSProvider**参数显示 Windows PowerShell 注册表提供程序支持的 Windows PowerShell 驱动器︰

<pre>PS > 获取 PSDrive-PSProvider 注册表名称提供商根 CurrentLocation......---...HKCU 注册表 HKEY_CURRENT_USER HKLM 注册表 HKEY_LOCAL_MACHINE</pre>

您还可以使用 Windows PowerShell 驱动器使用标准的位置 cmdlet:

<pre>PS > 设置位置 HKLM:\SOFTWARE PS > 推送位置。 PS \Microsoft > 获取位置路径...HKLM:\SOFTWARE\Microsoft</pre>

### 添加新的 Windows PowerShell 驱动器 (新 PSDrive)
通过使用**新建 PSDrive**命令，可以添加您自己的 Windows PowerShell 驱动器。 若要获取有关**新建 PSDrive**命令的语法，输入**语法**参数**获取命令**命令︰

```
PS> Get-Command -Name New-PSDrive -Syntax
New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

若要创建新的 Windows PowerShell 驱动器，您必须提供三个参数︰

-   （您可以使用任何有效的 Windows PowerShell 名称） 的驱动器名称

-   PSProvider （使用的文件系统位置的"文件系统"和"注册表"的注册表位置）

-   根，即，新的驱动器的根中的路径

例如，您可以创建名为"Office"映射到包含您的计算机上的 Microsoft Office 应用程序，如文件夹驱动器**c:\\Program Files\\Microsoft Office\\OFFICE11**。 若要创建驱动器，键入以下命令︰

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> 一般情况下，路径是不区分大小写。

Windows PowerShell 中的所有驱动器-由其名称跟一个冒号 （**:**） 一样，请到新的 Windows PowerShell 驱动器。

Windows PowerShell 驱动器可以使多任务变得更加简单。 例如，Windows 注册表中最重要的密钥的一些有很长的路径，使其更麻烦访问很难记住。 关键配置信息都位于下**HKEY_LOCAL_MACHINE\\软件\\Microsoft\\Windows\\CurrentVersion**。 若要查看和更改 CurrentVersion 注册表项中的项目，您可以创建所在的 Windows PowerShell 驱动器中该注册表项键入︰

<pre>PS > 新建 PSDrive-名称 cvkey-PSProvider 注册表-根 HKLM\Software\Microsoft\W indows\CurrentVersion 名称提供商根 CurrentLocation............cvkey 注册表 HKLM\Software\Microsoft\Windows\..</pre>

然后，您可以更改位置**cvkey:**驱动器就像任何其他驱动器:

`PS> cd cvkey:`

或︰

<pre>PS > 设置位置 cvkey:-通过路径...cvkey: \</pre>

新建 PsDrive cmdlet 仅与当前的 Windows PowerShell 会话中添加新的驱动器。 如果您关闭 Windows PowerShell 窗口，新的驱动器都将丢失。 若要保存的 Windows PowerShell 驱动器，导出控制台 cmdlet 用于将当前的 Windows PowerShell 会话，导出，然后使用 PowerShell.exe **PSConsoleFile**参数以将其导入。 或者，您的 Windows PowerShell 配置文件中添加新的驱动器。

### 删除 Windows PowerShell 驱动器 (删除 PSDrive)
通过**删除 PSDrive** cmdlet，您可以从 Windows PowerShell 中删除驱动器。 **删除 PSDrive** cmdlet 很容易使用;若要删除特定的 Windows PowerShell 驱动器，只需提供的 Windows PowerShell 驱动器名称。

例如，如果您添加**Office:** Windows PowerShell 驱动器，如下所示的**新建 PSDrive**主题中，您可以将其删除通过键入︰

```
PS> Remove-PSDrive -Name Office
```

若要删除**cvkey:** Windows PowerShell 驱动器，还显示在**新 PSDrive**主题中，使用以下命令︰

```
PS> Remove-PSDrive -Name cvkey
```

可以轻松地删除 Windows PowerShell 的驱动器，但在驱动器时不能将其删除。 例如︰

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

### 添加和删除驱动器外部的 Windows PowerShell
Windows PowerShell 中检测到的添加或删除 Windows，包括映射的网络驱动器、 USB 驱动器附加和通过使用**净使用**命令或从 Windows 脚本宿主 (WSH) 脚本**WScript.NetworkMapNetworkDrive**和**RemoveNetworkDrive**方法删除的驱动器中的文件系统驱动器。

