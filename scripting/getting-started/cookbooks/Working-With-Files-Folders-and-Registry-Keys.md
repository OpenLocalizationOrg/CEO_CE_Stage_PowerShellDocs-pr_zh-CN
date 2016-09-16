---
title: "处理文件文件夹和注册表项"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: e6cf87aa-b5f8-48d5-a75a-7cb7ecb482dc
ms.openlocfilehash: e049f49414a79b9de5c05100957ae4dba8d992ce
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 处理文件、 文件夹和注册表项
Windows PowerShell 名词**项目**引用使用 Windows PowerShell 驱动器上找到的项目。 当处理的 Windows PowerShell 文件系统提供商，**项目**可能的文件、 文件夹或 Windows PowerShell 驱动器。 列表和使用这些项目是大多数的管理设置中的关键基本任务，因此我们要讨论这些任务的详细信息。

### 枚举文件、 文件夹和注册表项 (获取 ChildItem)
由于获取从特定位置的项的集合是一个常见的任务，**获取 ChildItem** cmdlet 是专门设计返回找到如文件夹容器内的所有项目。

如果您想要返回的所有文件和文件夹直接在 c: 文件夹中包含\\Windows 中，键入︰

```
PS> Get-ChildItem -Path C:\Windows
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-16   8:10 AM          0 0.log
-a---        2005-11-29   3:16 PM         97 acc1.txt
-a---        2005-10-23  11:21 PM       3848 actsetup.log
...
```

列表类似于**Cmd.exe**或在 UNIX 命令 shell **ls**命令中输入**目录**命令时将看到的内容。

您可以通过使用**获取 ChildItem** cmdlet 的参数执行非常复杂的列表。 我们将探讨下一步出现在几个方案。 您可以通过键入看到语法**获取 ChildItem** cmdlet:

```
PS> Get-Command -Name Get-ChildItem -Syntax
```

这些参数可以是混合和匹配以获取高度自定义的输出。

#### 列出所有包含的项目 (-递归)
若要查看的项目内的 Windows 文件夹和子文件夹中所包含的任何项目，请使用**获取 ChildItem**的**递归**参数。 列表会显示任何内容的 Windows 文件夹和子文件夹中的项目中。 例如︰

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

#### 筛选依据名称 (-名称)
若要显示的项目的名称，请使用**获取 Childitem**的**名称**参数︰

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

#### 强制列表隐藏的项目 (-强制)
在文件资源管理器或 Cmd.exe 通常不可见的项目不会显示在**获取 ChildItem**命令的输出中。 若要显示隐藏的项目，请使用**获取 ChildItem****强制**参数。 例如︰

```
Get-ChildItem -Path C:\Windows -Force
```

此参数被命名强制，这是因为您可以强制覆盖**获取 ChildItem**命令的正态行为。 强制是广泛使用的参数，但它不会执行任何操作，损害系统的安全强制 cmdlet 不会以正常方式执行，操作。

#### 带通配符的匹配项名称
**获取 ChildItem**命令接受通配符中的项目列表的路径。

Windows PowerShell 引擎处理通配符匹配，因为接受通配符的所有 cmdlet 使用相同的表示法，并且具有相同的匹配行为。 Windows PowerShell 通配符表示法包括︰

-   星号 (\*) 匹配零个或多个任意字符。

-   问号 （？） 匹配一个字符。

-   左的括号 (\[) 字符以及右中括号 (]) 括起的一组要匹配的字符。

下面是通配符规范的工作方式的一些示例。

若要查找的所有文件中的基本名称完全五个字符后缀**.log**与 Windows 目录中，输入以下命令︰

```
PS> Get-ChildItem -Path C:\Windows\?????.log
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
...
-a---        2006-05-11   6:31 PM     204276 ocgen.log
-a---        2006-05-11   6:31 PM      22365 ocmsn.log
...
-a---        2005-11-11   4:55 AM         64 setup.log
-a---        2005-12-15   2:24 PM      17719 VxSDM.log
...
```

若要查找 Windows 目录中的**x**字母开头的所有文件，请键入︰

```
Get-ChildItem -Path C:\Windows\x*
```

若要查找其名称**x**或**z**开头的所有文件，请键入︰

```
Get-ChildItem -Path C:\Windows\[xz]*
```

#### 排除的项 (-排除)
您可以通过使用**排除**参数的获取 ChildItem 排除特定项目。 这允许您执行复杂的单个语句中的筛选。

例如，假设您尝试在 System32 文件夹中，查找 Windows 时间服务 DLL 和所有您仍然可以记住有关 DLL 名称是"W"开头，并且在其具有"32"。

这样的表达式**w\&#42; 32\&#42;。dll**将查找所有 Dll 满足的条件，但它还可能在其名称中返回 Windows 95 和 16 位 Windows 兼容性 dll 中包含"95"或"16"。 您可以忽略有任何这些数字在其名称中使用图案****排除**参数的文件\&#42;\[9516]\&#42;**:

<pre>PS > 获取 ChildItem-路径 C:\WINDOWS\System32\w*32*.dll-排除*[9516]*目录︰ Microsoft.PowerShell.Core\FileSystem::C:\WINDOWS\System32 模式 LastWriteTime 长度名称............----2004年-08-04 8:00 AM 174592 w32time.dll----2004年-08-04 8:00 AM 22016 w32topl.dll----2004年-08-04 8:00 AM 101888 win32spl.dll----2004年-08-04 8:00 AM 172032 wldap32.dll----2004年-08-04 8:00 AM 264192 wow32.dll----2004年-08-04 8:00 AM 82944 ws2_32.dll----2004年-08-04 8:00 AM 42496 wsnmp32.dll----2004年-08-04 8:00 AM 22528 wsock32.dll----2004年-08-04 8:00 AM 18432 wtsapi32.dll</pre>

#### 混合获取 ChildItem 参数
您可以使用多个**获取 ChildItem** cmdlet 的参数中相同的命令。 混合参数之前，请确保您了解通配符匹配。 例如，以下命令返回任何结果︰

```
PS> Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

没有任何结果，即使有两个 Windows 文件夹中的"z"以字母开头的 Dll。

没有返回结果由于我们指定通配符作为路径的一部分。 即使命令是递归，**获取 ChildItem** cmdlet 限于项目中的 Windows 文件夹包含".dll"结尾的名称。

若要指定递归搜索其名称匹配的特殊图案的文件，请使用**-包括**参数。

```
PS> Get-ChildItem -Path C:\Windows -Include *.dll -Recurse -Exclude [a-y]*.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32\Setup

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM       8261 zoneoc.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     337920 zipfldr.dll
```

