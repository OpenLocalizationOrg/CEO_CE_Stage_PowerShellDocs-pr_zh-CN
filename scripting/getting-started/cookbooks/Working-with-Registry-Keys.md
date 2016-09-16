---
title: "使用注册表项"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: 6af4884948c44f7f256d62d0c61f1c71b47994f3
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用注册表项
由于注册表项是 Windows PowerShell 驱动器上的项目，使用这些功能非常类似于使用的文件和文件夹。 一个重要的区别是基于注册表的 Windows PowerShell 驱动器上的每一项是容器，就像在文件系统驱动器上的文件夹。 但是，注册表项和其关联的值是该项目，而不重复的项目的属性。

### 列出所有子项的注册表项
您可以通过使用**获取 ChildItem**显示直接在注册表项中的所有项目。 显示隐藏的或系统项目中添加可选**强制**参数。 例如，此命令显示直接在 Windows PowerShell 驱动器 HKCU 项目:，它对应于 HKEY_CURRENT_USER 注册表配置单元︰

```
PS> Get-ChildItem -Path hkcu:\

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER

SKC  VC Name                           Property
---  -- ----                           --------
  2   0 AppEvents                      {}
  7  33 Console                        {ColorTable00, ColorTable01, ColorTab...
 25   1 Control Panel                  {Opened}
  0   5 Environment                    {APR_ICONV_PATH, INCLUDE, LIB, TEMP...}
  1   7 Identities                     {Last Username, Last User ...
  4   0 Keyboard Layout                {}
...
```

这些是下 HKEY_CURRENT_USER 注册表编辑器 (Regedit.exe) 中可见的顶级键。

您还可以通过指定注册表提供商的姓名后, 跟"**::**"指定此注册表路径。 注册表提供程序的完整名称是**Microsoft.PowerShell.Core\\注册表**，但这可以缩短到刚刚**注册表**。 任何以下命令将列表直接在 HKCU 下的内容︰

```
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

这些命令列出仅直接包含的项目，就像在 UNIX 外壳中使用 Cmd.exe 的**DIR**命令或**ls** 。 若要显示包含的项，您需要指定**递归**参数。 若要列出 HKCU 中的所有注册表项，请使用以下命令 （此操作可能需要很长的时间。）︰

```
Get-ChildItem -Path hkcu:\ -Recurse
```

**获取 ChildItem**可以执行复杂的筛选功能，通过其**路径**、**筛选器**，**包括**和**排除**参数，但这些参数通常基于仅名称。 您可以执行复杂的筛选通过使用**位置对象**cmdlet 基于项目的其他属性。 以下命令查找 HKCU 内的所有键︰\\有不超过一个子项，并且也具有完全四个值的软件︰

```
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### 复制键
复制已完成**复制项目**。 以下命令复制 HKLM:\\软件\\Microsoft\\Windows\\CurrentVersion 及其所有其属性设置为 HKCU:\\，创建新的密钥名为"CurrentVersion":

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

检查在注册表编辑器中，或通过使用**获取 ChildItem**此新项时，如果您将注意到，您不具有包含子项的副本中的新位置。 为了复制所有容器的内容，您需要指定**递归**参数。 若要使前面复制命令递归，您可以使用此命令︰

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

你仍然可以使用其他工具，您已经拥有可用于执行文件系统副本。 任何注册表编辑工具 — 包括 reg.exe、 regini.exe 和 regedit.exe—and 支持注册表中进行编辑 （如 WScript.Shell 和 WMI 的 StdRegProv 课堂） 的 COM 对象可以用于从 Windows PowerShell。

### 创建关键字
在注册表中创建新的密钥是简单比文件系统中创建新项目。 所有注册表项都是容器，因为不需要指定的项目类型;只需提供明确的路径，如:

```
New-Item -Path hkcu:\software_DeleteMe
```

您可以使用基于提供商的路径指定一个键︰

```
New-Item -Path Registry::HKCU_DeleteMe
```

### 删除项
删除项目在本质上的所有提供相同。 以下命令将自动删除项︰

```
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### 删除所有下特定键的键
您可以通过使用**删除项目**，删除包含的项目，但系统将提示您确认删除，如果该项目包含任何其他内容。 例如，如果我们尝试删除 HKCU:\\CurrentVersion 子项我们创建，我们可以看到此︰

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

若要删除包含的项不进行提示，请指定**-递归**参数︰

```
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

如果您想要删除所有项目内 HKCU:\\CurrentVersion，但不是 HKCU:\\CurrentVersion 本身，您可以改为使用︰

```
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```

