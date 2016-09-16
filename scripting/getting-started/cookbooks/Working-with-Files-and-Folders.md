---
title: "处理文件和文件夹"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: be0960062182bbce161fdb26340825a7f6360382
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 处理文件和文件夹
通过 Windows PowerShell 驱动器导航和处理这些项目是类似于操作 Windows 物理磁盘驱动器上文件和文件夹。 我们将讨论如何处理特定文件和文件夹操作任务，本部分中。

### 列出所有文件和文件夹的文件夹中
通过使用**获取 ChildItem**，您可以直接在文件夹中获得的所有项目。 显示隐藏的或系统项目中添加可选**强制**参数。 例如，此命令显示 Windows PowerShell 驱动器 C （这是相同的 Windows 物理驱动器 C） 直接的内容︰

```
Get-ChildItem -Force C:\
```

命令列出了仅直接包含的项目，就像在 UNIX 外壳中使用 Cmd.exe 的**DIR**命令或**ls** 。 为了显示包含的项，您需要首先指定**-递归**以及参数。 （这可能需要很长时间才能完成）。若要列出 C 驱动器上的所有内容︰

```
Get-ChildItem -Force C:\ -Recurse
```

**获取 ChildItem**可以筛选项其**路径**、**筛选器**，**包括**和**排除**参数，但这些通常基于仅名称。 您可以执行复杂的筛选功能通过使用**位置对象**基于项目的其他属性。

以下命令的上次修改 2005 年 10 月 1 日之后，哪些方面是既不小于 1 兆字节，也不大于 10 兆字节 Program Files 文件夹内查找所有可执行文件︰

```
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt "2005-10-01") -and ($_.Length -ge 1m) -and ($_.Length -le 10m)}
```

### 复制文件和文件夹
复制已完成**复制项目**。 以下命令备份 c:\\boot.ini 到 c:\\boot.bak:

```
Copy-Item -Path c:\boot.ini -Destination c:\boot.bak
```

如果目标文件已存在，则复制尝试失败。 若要覆盖现有目标，请使用强制参数︰

```
Copy-Item -Path c:\boot.ini -Destination c:\boot.bak -Force
```

此命令正常工作，即使目标是只读的。

文件夹复制的工作方式相同。 此命令复制文件夹 c:\\temp\\test1 到新文件夹 c:\\temp\\DeleteMe 递归︰

```
Copy-Item C:\temp\test1 -Recurse c:\temp\DeleteMe
```

您还可以复制选定的项目。 以下命令复制包含 c︰ 中的任意位置的所有.txt 文件\\到 c︰ 数据\\temp\\文本︰

```
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination c:\temp\text
```

您仍然可以使用其他工具来执行文件系统副本。 XCOPY、 ROBOCOPY 和 COM 对象，如所有**实例，** Windows PowerShell 中工作。 例如，您可以使用 Windows 脚本宿主**Scripting.FileSystem COM**类备份 c:\\boot.ini 到 c:\\boot.bak:

```
(New-Object -ComObject Scripting.FileSystemObject).CopyFile("c:\boot.ini", "c:\boot.bak")
```

### 创建文件和文件夹
创建新项目的工作方式相同在所有的 Windows PowerShell 提供商。 Windows PowerShell 提供商是否具有多个项目类型 — 例如，Windows PowerShell 的文件系统提供商区分目录和文件 — 您需要首先指定项类型。

此命令创建新文件夹 c:\\temp\\新文件夹︰

```
New-Item -Path 'C:\temp\New Folder' -ItemType "directory"
```

此命令创建新的空文件 c:\\temp\\新文件夹\\file.txt

```
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType "file"
```

### 删除所有文件和文件夹的文件夹中
您可以删除包含的项目使用**删除项目**，但系统将提示您确认删除，如果该项目包含任何其他内容。 例如，如果您尝试删除文件夹 c:\\temp\\DeleteMe 包含其他项目，Windows PowerShell 提示您确认删除该文件夹之前︰

```
Remove-Item C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

如果不想将提示您为每个包含项，指定**递归**参数︰

```
Remove-Item C:\temp\DeleteMe -Recurse
```

### 为 Windows 访问驱动器映射本地文件夹
您还可以映射本地文件夹中，使用**替代**命令。 以下命令在本地 Program Files 目录中创建本地驱动器 p︰ 根︰

```
subst p: $env:programfiles
```

就像网络驱动器上，使用 Windows PowerShell 使用**替代**内映射驱动器会立即看到 Windows PowerShell shell。

### 为数组阅读文本文件
文本数据更常见的存储格式之一是文件中使用单独的行视为不同数据元素。 **获取内容**cmdlet 可用于读取整个文件在一个步骤中，如下所示︰

```
PS> Get-Content -Path C:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional"
 /noexecute=AlwaysOff /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS=" Microsoft Windows XP Professional 
with Data Execution Prevention" /noexecute=optin /fastdetect
```

**获取内容**已将从文件中读取以每行的文件内容的一个元素与数组的形式的数据。 您可以检查的**长度**，返回的内容进行确认︰

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

此命令是最有用直接获取信息导入到 Windows PowerShell 的列表。 例如，您可能 c︰ 的文件中存储的计算机名称或 IP 地址列表\\temp\\domainMembers.txt，一个文件的每一行上的姓名。 **获取内容**可用于检索文件内容，并将它们放入变量**$Computers**:

```
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

**$Computers**现在是数组，其中包含每个元素中的计算机名称。

