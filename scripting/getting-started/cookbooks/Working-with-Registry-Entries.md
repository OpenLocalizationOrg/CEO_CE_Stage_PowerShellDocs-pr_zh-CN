---
title: "使用注册表项"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
ms.openlocfilehash: 24517b4a31ab2c5b92c2485fb8c6bd0e56dd2ffd
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用注册表项
注册表项是键的属性，并在这种情况下，不能直接浏览，因为我们需要执行略有不同的方法与它们一起使用时。

### 列表注册表项
有许多不同的方法来检查注册表项。 最简单方法是以获取与键关联的属性名称。 例如，若要查看的注册表项中的项名称**HKEY_LOCAL_MACHINE\\软件\\Microsoft\\Windows\\CurrentVersion**，使用**获取项目**。 注册表项中有一个属性是注册表项中的条目的列表与常规名称"属性"。 以下命令选择 Property 属性，并展开项目，以便它们显示在列表中︰

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

若要查看更容易阅读窗体中的注册表项，请使用**获取 ItemProperty**:

```
PS> Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion

PSPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows\CurrentVersion
PSParentPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows
PSChildName         : CurrentVersion
PSDrive             : HKLM
PSProvider          : Microsoft.PowerShell.Core\Registry
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
CommonFilesDir      : C:\Program Files\Common Files
ProductId           : 76487-338-1167776-22465
WallPaperDir        : C:\WINDOWS\Web\Wallpaper
MediaPath           : C:\WINDOWS\Media
ProgramFilesPath    : C:\Program Files
PF_AccessoriesName  : Accessories
(default)           :
```

键的 Windows PowerShell 相关属性都为前缀与"PS" **PSPath**、 **PSParentPath**、 **PSChildName**和**PSProvider**等。

可用于"**.**"表示法引用当前的位置。 **设置位置**可用于第一次更改为**CurrentVersion**注册表容器︰

```
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

或者，您可以使用内置的 HKLM PSDrive 与**设置位置**︰

```
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

您可以使用当前位置的"**.**"表示法列出属性，但不指定的完整路径︰

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

路径扩展工作方式相同，那样在文件系统中，以便从以下位置获取**ItemProperty**列表**HKLM:\\软件\\Microsoft\\Windows\\帮助**使用**获取 ItemProperty 的路径。\\帮助**。

### 获取单个注册表项
如果您想要检索注册表项中的特定项，您可以使用多个可能的方法之一。 此示例中查找的值中**DevicePath** **HKEY_LOCAL_MACHINE\\软件\\Microsoft\\Windows\\CurrentVersion**。

**获取 ItemProperty**使用，**路径**参数指定的密钥，名称和**Name**参数指定**DevicePath**词条的名称。

```
PS> Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath

PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

此命令返回标准的 Windows PowerShell 属性，以及**DevicePath**属性。

> [!NOTE]
> 虽然**获取 ItemProperty**进行**筛选**、**包括**和**排除**的参数，但是它们不能用于作为筛选依据属性名称。 这些参数引用注册表项，这是项目的路径 — 和不注册表项-这是项目属性。

另一种方法是使用 Reg.exe 命令行工具。 与 reg.exe 的帮助，请键入**reg.exe /？** 在命令提示符。 若要查找 DevicePath 项，请使用 reg.exe，以下命令中所示︰

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

您还可以使用**WshShell COM**对象以及查找一些注册表项，尽管这种方法不起作用与较大的二进制数据或注册表项的名称包括字符，如"\\")。 追加到的项目路径属性名称\\分隔符︰

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### 创建新的注册表项
若要添加新项名为"PowerShellPath" **CurrentVersion**键，请将**新建 ItemProperty**使用键、 输入名称和项的值的路径。 对于此示例中，我们将 Windows PowerShell 变量**$PSHome**，用于 Windows PowerShell 的存储安装目录的路径的值。

您可以使用以下命令，密钥添加新条目和命令也返回新项有关的信息︰

```
PS> New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome

PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

**PropertyType**必须是下表中的**Microsoft.Win32.RegistryValueKind**枚举成员的名称︰

|PropertyType 值|含义|
|----------------------|-----------|
|二进制|二进制数据|
|Dword 值|数字的有效 UInt32|
|ExpandString|一个字符串，可以包含动态展开的环境变量|
|MultiString|多行字符串|
|字符串|任何字符串值|
|四字|8 字节的二进制数据|

> [!NOTE]
> 您可以通过指定的**Path**参数的值数组的注册表项添加到多个位置︰

```
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

您也可以通过将**强制**参数添加到任何**新建 ItemProperty**命令覆盖预先存在的注册表项值。

### 重命名注册表项
若要重命名为"PSHome" **PowerShellPath**条目，请使用**重命名 ItemProperty**:

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

若要显示的重命名后的值，将**通过**参数添加到命令。

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### 删除注册表项
若要删除的 PSHome 和 PowerShellPath 注册表项，请使用**删除 ItemProperty**:

```
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```

