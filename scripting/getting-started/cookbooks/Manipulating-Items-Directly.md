---
title: "直接操作项"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: f462f195e1128cd67be8073fe0755b5158fee970
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 直接操作项
您在 Windows PowerShell 驱动器中，例如文件和文件夹中的文件系统驱动器，注册表项中的 Windows PowerShell 注册表驱动器，请参阅元素 Windows PowerShell 中称为*项目*。 项目使用这些 cmdlet 有名词**项目**在其名称。

输出**获取-命令-名词项目**命令显示有九个 Windows PowerShell 项目 cmdlet。

```
PS> Get-Command -Noun Item

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Clear-Item                      Clear-Item [-Path] <String[]...
Cmdlet          Copy-Item                       Copy-Item [-Path] <String[]>...
Cmdlet          Get-Item                        Get-Item [-Path] <String[]> ...
Cmdlet          Invoke-Item                     Invoke-Item [-Path] <String[...
Cmdlet          Move-Item                       Move-Item [-Path] <String[]>...
Cmdlet          New-Item                        New-Item [-Path] <String[]> ...
Cmdlet          Remove-Item                     Remove-Item [-Path] <String[...
Cmdlet          Rename-Item                     Rename-Item [-Path] <String>...
Cmdlet          Set-Item                        Set-Item [-Path] <String[]> ...
```

### 创建新项目 （新项目）
若要在文件系统中创建新项目，请使用**新建项目**cmdlet。 包括的项，路径与**Path**参数和参数值"文件"或"目录"的**项类型**。

例如，若要创建新的目录命名为"c: New.Directory"in\\Temp 目录中，键入︰

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

若要创建文件时，更改到"文件"的**项类型**参数的值。 例如，若要创建名为"file1.txt"New.Directory 目录中的文件，请键入︰

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

您可以使用同样的方法创建一个新的注册表项。 实际上，注册表项就越容易创建，因为在 Windows 注册表中的唯一项目类型是关键。 （注册表项是项目*属性*）。例如，若要创建名为"_Test"CurrentVersion 子项中的键，键入︰

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

键入时注册表路径，请务必在 HKLM 的 Windows PowerShell 驱动器名称中包含冒号 （**:**）︰ 和 HKCU:。 无冒号，Windows PowerShell 无法识别路径中的驱动器名称。

### 为什么注册表值不是项目
**获取 ChildItem** cmdlet 用于查找注册表项中的项目，将永远不会看到实际注册表项或相应的值。

例如，注册表项**HKEY_LOCAL_MACHINE\\软件\\Microsoft\\Windows\\CurrentVersion\\运行**通常包含表示系统启动时运行的应用程序的几个注册表项。

但是，当使用**获取 ChildItem**查找中项的子项目时，您将看到所有是密钥的**OptionalComponents**子项︰

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run
   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

尽管它会很方便地将视为项目的注册表项，不能以确保它是唯一的方式来指定注册表项的路径。 路径表示法不区分名为**运行**并在**运行**子项**（默认）**注册表项的注册表子项。 此外，因为注册表项名称可以包含反斜杠字符 (**\\**)，如果注册表项的项目，然后您可以使用路径表示法来区分注册表项名为**Windows\\CurrentVersion\\运行**从位于该路径的子项。

### 重命名现有项目 （重命名项目）
若要更改的文件或文件夹的名称，使用**重命名项目**cmdlet。 以下命令更改为**fileOne.txt** **file1.txt**文件的名称。

```
PS> Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

**重命名项目**cmdlet 可以更改的名称的文件或文件夹，但是不能将项目移。 以下命令将失败，因为它试图将文件从 New.Directory 目录移到 Temp 目录。

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### 移动项目 （移动项目）
若要移动的文件或文件夹，请使用**移动项目**cmdlet。

例如，以下命令移动 c︰ 从 New.Directory 目录\\到 C 盘根临时目录。 若要验证该项目被移动，包括**通过****移动项目**cmdlet 的参数。 不**通过**，**移动项目**cmdlet 不显示任何结果。

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### 复制项目 （复制项目）
如果您熟悉其他外壳中的复制操作，您可能会发现特殊的 Windows PowerShell cmdlet**复制项目**的行为。 当将项目从一个位置复制到另一个中时，复制项目不默认情况下复制其内容。

例如，如果您将复制**New.Directory**目录从 c︰ 驱动器到 c:\\临时目录，命令成功，但不是会复制 New.Directory 目录中的文件。

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp
```

如果显示的内容**c:\\temp\\New.Directory**，您将找到它包含任何文件︰

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

为什么无法**复制项目**cmdlet 将内容复制到新位置？

**复制项目**cmdlet 被可通用;不只是为了复制文件和文件夹。 此外，即使复制文件和文件夹，您可能希望复制仅容器而不是在其中的项目。

要复制所有文件夹的内容，请在命令中包括**递归****复制项目**cmdlet 的参数。 如果您已复制不其内容的目录，添加**强制**参数，以便您可以覆盖清空文件夹。

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp -Recurse -Force -Passthru
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18   1:53 PM            New.Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

### 删除项目 （删除项目）
若要删除的文件和文件夹，请使用**删除项目**cmdlet。 Windows PowerShell cmdlet，如**删除项目**，可以进行重大、 是不可逆的更改将经常提示确认时输入其命令。 例如，如果您尝试删除**New.Directory**文件夹，您将会提示您确认命令，因为文件夹包含文件︰

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

为****是的默认响应，因为若要删除的文件夹和文件，请按**Enter**键。 若要不确认删除该文件夹，请使用**-递归**参数。

```
PS> Remove-Item C:\temp\New.Directory -Recurse
```

### 执行项 （调用项目）
Windows PowerShell 使用**调用项目**cmdlet 执行默认操作的文件或文件夹。 此默认操作取决于注册表; 中的默认应用程序处理就像双击文件资源管理器中的项目是相同的效果。

例如，假设您运行以下命令︰

```
PS> Invoke-Item C:\WINDOWS
```

位于 c︰ 在浏览器窗口\\窗口显示，就像了双击 c:\\Windows 文件夹。

如果您调用**boot.ini 之前 Windows Vista 系统上**︰

```
PS> Invoke-Item C:\boot.ini
```

与记事本关联的.ini 文件类型时，如果在记事本中打开 boot.ini 文件。

