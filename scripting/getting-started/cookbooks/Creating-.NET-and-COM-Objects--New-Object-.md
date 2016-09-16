---
title: "创建新的.NET 和 COM 对象对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: 10302d319e1d55b6fab02bab0ee49aa0fff43f59
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 创建.NET 和 COM 对象 （新对象）
有与.NET Framework 和 COM 接口，使您可以执行许多系统管理任务的软件组件。 Windows PowerShell，可以使用这些组件，以便您不是局限于可以通过使用 cmdlet 执行的任务。 在初始版本的 Windows PowerShell cmdlet 的许多不起作用对远程计算机。 我们将演示如何通过使用.NET Framework **System.Diagnostics.EventLog**类直接从 Windows PowerShell 管理事件日志时熟悉此限制。

### 使用新对象事件日志访问
.NET Framework 类库包括一个名为可用于管理事件日志的**System.Diagnostics.EventLog**类。 **TypeName**参数中使用**新建对象**cmdlet，可以创建.NET Framework 课堂的新实例。 例如，以下命令创建的事件日志引用︰

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

虽然命令已创建的事件日志课堂实例，实例不包含任何数据。 这是因为我们未指定特定的事件日志。 您如何获得真正的事件日志？

#### 使用新对象构造函数
若要引用特定的事件日志，您需要指定日志的名称。 **新建对象**都有一个**参数列表**参数。 为值传递给此参数的参数使用选择性启动对象的方法。 该方法称为*构造函数*，因为它用于构造对象。 例如，若要获取应用程序日志的引用，指定字符串应用程序作为参数︰

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> 由于大多数.NET Framework 核心类包含在 System 命名空间中，Windows PowerShell 将自动尝试查找您指定的系统命名空间中找不到您指定的类型名称相匹配的课程。 这意味着您可以指定，而不是 System.Diagnostics.EventLog Diagnostics.EventLog。

#### 存储在变量中的对象
您可能希望存储引用的对象，以便您可以在当前 shell 中使用它。 虽然 Windows PowerShell 允许您进行大量使用管线，从而减少了需要变量，有时在变量中存储的对象的引用，可以更方便地处理这些对象。

Windows PowerShell，可以创建实际上命名对象的变量。 任何有效的 Windows PowerShell 命令的输出可以存储在变量中。 使用 $ 始终开始变量名称。 如果您想要将应用程序日志引用存储在一个名为 $AppLog 变量中，键入名称变量后, 跟一个等号，然后键入用来创建应用程序日志对象的命令︰

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

如果然后键入 $AppLog，您可以看到它包含的应用程序日志︰

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### 访问新对象远程事件日志
上一节中使用的命令目标本地计算机，则**获取事件日志**cmdlet 可以执行的操作。 若要访问远程计算机上的应用程序日志，必须作为参数提供同时日志名称和计算机名称 （或 IP 地址）。

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

现在，我们已对事件日志 $RemoteAppLog 变量中存储的引用，哪些任务可以我们对其执行？

#### 清除对象的方法与事件日志
对象通常具有可以调用来执行任务的方法。 **获取成员**可用于显示与对象相关联的方法。 以下命令并选择的输出显示一些事件日志类的方法︰

```
PS> $RemoteAppLog | Get-Member -MemberType Method

   TypeName: System.Diagnostics.EventLog

Name                      MemberType Definition
----                      ---------- ----------
...
Clear                     Method     System.Void Clear()
Close                     Method     System.Void Close()
...
GetType                   Method     System.Type GetType()
...
ModifyOverflowPolicy      Method     System.Void ModifyOverflowPolicy(Overfl...
RegisterDisplayName       Method     System.Void RegisterDisplayName(String ...
...
ToString                  Method     System.String ToString()
WriteEntry                Method     System.Void WriteEntry(String message),...
WriteEvent                Method     System.Void WriteEvent(EventInstance in...
```

若要清除事件日志，可以使用**Clear()**方法。 调用方法时，您必须始终遵循此方法名称的括号中，即使方法不需要参数。 这允许区分方法，并具有相同名称的潜在属性的 Windows PowerShell。 键入下列操作来调用**清除**方法︰

```
PS> $RemoteAppLog.Clear()
```

键入以下命令以显示日志。 您将看到事件日志已被清除，并且现在有 0 条目，而不是 262:

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### 使用新对象创建 COM 对象
**新建对象**可用于处理组件对象模型 (COM) 组件。 组件从各种库包含与 Windows 脚本宿主 (WSH) 到 ActiveX 如 Internet Explorer 中安装应用程序在大多数系统上的区域。

**新建对象**使用.NET Framework 运行时调用包装创建 COM 对象，使其具有相同.NET Framework 调用 COM 对象时的限制。 若要创建 COM 对象，您需要使用编程标识符或您想要使用的 COM 类的*进程 Id*指定**ComObject**参数。 COM 使用和确定 Progid 有哪些系统上可用的限制的完整讨论已超出此用户的指南的范围，但最已知对象，如 WSH 环境中可以使用 Windows PowerShell 内。

您可以通过指定这些 progid 创建 WSH 对象︰ **WScript.Shell**、 **WScript.Network**、 **Scripting.Dictionary**和**实例**。 以下命令创建这些对象︰

```
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

尽管大多数这些类由 Windows PowerShell 中可用的其他方法，例如创建快捷方式的一些任务是功能的仍然易于使用 WSH 类执行。

### 使用 WScript.Shell 创建桌面快捷方式
可以快速执行与 COM 对象的一个任务创建快捷方式。 假设您要创建快捷方式在桌面上链接到主文件夹 Windows powershell。 需要首先创建**WScript.Shell**，我们将存储在变量名为**$WshShell**的引用︰

```
$WshShell = New-Object -ComObject WScript.Shell
```

获取成员处理 COM 对象，以便您可以通过键入查看对象的成员︰

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

**获取成员**具有可选**InputObject**参数可以使用，而不是管道为**获取成员**提供输入。 您将获得相同的输出如上所示如果改为使用命令**获取成员 InputObject $WshShell**。 如果您使用**InputObject**，它会将视为单个项目的其参数。 这意味着，如果您在变量中有多个对象，**获取成员**将其视为对象的数组。 例如︰

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

**WScript.Shell CreateShortcut**方法接受一个参数，要创建的快捷方式文件的路径。 我们可以在桌面上的完整路径中键入，但没有简便的方法。 桌面通常表示名桌面为当前用户的主文件夹内的文件夹。 Windows PowerShell 具有变量**$Home**包含此文件夹的路径。 我们可以通过使用此变量，指定主文件夹的路径，然后添加桌面文件夹的名称和名称的快捷方式若要创建通过键入︰

```
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

当您使用如下所示在双引号内的变量名时，Windows PowerShell 尝试替换匹配的值。 如果您使用单引号，Windows PowerShell 不会尝试替换变量的值。 例如，请尝试键入以下命令︰

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

现在，我们有一个名为**$lnk**包含新的快捷方式引用变量。 如果您想要查看其成员，可以先将其传送到**获取成员**。 下面的输出显示的成员，我们需要使用完成创建我们的快捷方式︰

<pre>PS > $lnk |获取成员 TypeName: System.__ComObject# {f935dc23-1cf0-11d0-adb9-00c04fd58a0b} 名称 MemberType 定义...---......保存 void 保存 （） 的方法...目标路径属性字符串目标路径 （) {获取} {set}...</pre>

我们需要指定**目标路径**，即 Windows PowerShell 的应用程序文件夹，然后将快捷方式**$lnk**保存调用**保存**的方法。 Windows PowerShell 应用程序的文件夹路径存储在变量**$PSHome**，以便我们可以通过键入来执行此操作︰

<pre>$lnk。目标路径 = $PSHome $lnk。Save （)</pre>

### 使用 Windows PowerShell 从 Internet Explorer
可以通过使用自动化许多应用程序 （包括 Microsoft Office 系列应用程序和 Internet Explorer） Internet Explorer 演示的一些典型方法和参与使用基于 COM 应用程序的问题。

您可以通过指定 Internet Explorer 加载项程序 Id， **InternetExplorer.Application**创建 Internet Explorer 实例︰

```
$ie = New-Object -ComObject InternetExplorer.Application
```

此命令启动 Internet Explorer 中，但不会使其可见。 如果您键入时获取过程，您可以看到名为 iexplore 进程正在运行。 实际上，如果退出 Windows PowerShell，进程将继续运行。 您必须重新启动计算机或使用任务管理器等工具结束 iexplore 流程。

> [!NOTE]
> 作为单独的过程，通常称为*ActiveX 可执行文件*，启动的 COM 对象可能或启动时可能不会显示用户界面窗口。 如果他们创建窗口但不能进行其可见，如 Internet Explorer，通常会将焦点移动到 Windows 桌面，您必须此窗口中可见，要与之进行交互。

通过键入**$ie |获取成员**，您可以查看属性和方法适用于 Internet Explorer。 若要查看 Internet Explorer 窗口中，将可见属性设置为 $true，键入︰

```
$ie.Visible = $true
```

可以使用导航方法然后导航到特定的 Web 地址︰

```
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

使用 Internet Explorer 对象模型的其他成员，很可能从网页检索文本内容。 以下命令将显示在正文中的当前网页的 HTML 文本︰

```
$ie.Document.Body.InnerText
```

若要关闭 Internet Explorer 从 PowerShell 内，呼叫其 Quit() 方法︰

```
$ie.Quit()
```

这将强制其关闭。 Ie 变量 $ 不再包含为有效引用，即使它仍然看起来 COM 对象。 如果您尝试使用它，您将收到自动化错误︰

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

您可以的删除 ie 剩余引用的命令，如 $ = $null，或通过键入变量中完全删除︰

```
Remove-Variable ie
```

> [!NOTE]
> ActiveX 可执行文件是否退出或继续运行时删除引用某个没有公共标准。 如应用程序是否可见，是否正在编辑的文档运行，但甚至是否 Windows PowerShell 仍在运行的情况下，根据应用程序，也可能不退出。 因此，您应为您想要使用 Windows PowerShell 中可执行每个 ActiveX 测试终止行为。

### 获取有关.NET Framework 包装 COM 对象的警告
在某些情况下，COM 对象可能有相关联的.NET Framework*运行时可调用包装*或 RCW，，这将使用**新对象**。 由于 RCW 的行为可能不同于普通 COM 对象的行为，**新建对象**具有**严格**参数 RCW 访问有关向您发出警告。 如果您指定的**严格**参数，然后创建使用 RCW COM 对象时，您将收到一条警告消息︰

```
PS> $xl = New-Object -ComObject Excel.Application -Strict
New-Object : The object written to the pipeline is an instance of the type "Mic
rosoft.Office.Interop.Excel.ApplicationClass" from the component's primary inte
rop assembly. If this type exposes different members than the IDispatch members
, scripts written to work with this object might not work if the primary intero
p assembly is not installed.
At line:1 char:17
+ $xl = New-Object  <<<< -ComObject Excel.Application -Strict
```

虽然仍创建对象时，将警告它不是标准的 COM 对象。

