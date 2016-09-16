---
title: "使用存储的对象变量"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: 5f37f66a34a98a4da28f4e36f115272d44ae5fc4
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用存储的对象变量
Windows PowerShell 处理对象。 Windows PowerShell，可以创建变量-实际上是命名的对象-要保留的输出以供以后使用。 如果您习惯于在其他外壳中使用变量，请记住 Windows PowerShell 变量是不是文本的对象。

变量始终指定使用初始字符 $，并可以在其名称中包含任何字母数字字符或下划线。

### 创建变量
您可以通过键入有效的变量名中创建一个变量︰

```
PS> $loc
PS>
```

这将返回无结果，因为**$loc**不具有一个值。 您可以创建一个变量，并将其分配同一个步骤中的值。 Windows PowerShell 仅创建变量，如果不存在;否则，它分配给现有变量指定的值。 若要将您的当前位置存储在变量**$loc**，请键入︰

```
$loc = Get-Location
```

当您键入以下命令，因为输出发送到 $loc.时，显示不输出 Windows PowerShell 中显示的输出的数据不否则始终直接获取发送到屏幕事实产生负面影响。 键入 $loc 将显示您的当前位置︰

```
PS> $loc

Path
----
C:\temp
```

**获取成员**可用于显示变量的内容的信息。 管道 $loc 获取成员将显示您它是**PathInfo**对象，就像获取位置的输出︰

```
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

### 操作变量
Windows PowerShell 提供用于控制变量的几个命令。 您可以通过键入看到可读窗体中的完整列表︰

```
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

除了您在您当前的 Windows PowerShell 会话中创建的变量，有几个系统定义的变量。 **删除变量**cmdlet 可用于清除所有不受 Windows PowerShell 的变量。 键入以下命令以清除所有变量︰

```
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

这将生成出现确认提示时，请参阅下文。

```
Confirm
Are you sure you want to perform this action?
Performing operation "Remove Variable" on Target "Name: Error".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):A
```

如果您运行**获取变量**cmdlet，您将看到其余的 Windows PowerShell 变量。 由于也是一个变量的 Windows PowerShell 驱动器，您也可以通过键入显示所有 Windows PowerShell 变量︰

```
Get-ChildItem variable:
```

### 使用 Cmd.exe 变量
Windows PowerShell，但不是 Cmd.exe 命令 shell 环境中运行，并且可以使用 Windows 中的任何环境中可用的相同变量。 通过名为**信纸**驱动器公开这些变量:。 您可以通过键入查看这些变量︰

```
Get-ChildItem env:
```

虽然标准变量 cmdlet 不设计为支持**环境︰**变量，您仍然可以使用它们通过指定**环境︰**前缀。 例如，若要查看的操作系统根目录下，您可以通过键入使用命令外壳**%系统根目录 %**变量从 Windows PowerShell 中︰

```
PS> $env:SystemRoot
C:\WINDOWS
```

您也可以创建和修改环境变量从 Windows PowerShell 中。 从 Windows PowerShell 访问环境变量符合 for Windows 中的其他位置的环境变量的一般规则。

