---
title: "使用更改的格式命令输出视图"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 8480270797960463d438fb47dfaaa9ec297bea0e
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用更改的格式命令输出视图
Windows PowerShell 有一组的允许您控制哪些属性显示特定对象的 cmdlet。 所有 cmdlet 名称开头动词**格式**。 他们可以选择要显示的一个或多个属性。

**格式**cmdlet 是**格式范围**、**格式列表**，**表格格式**和**格式自定义**。 仅将描述此用户的指南中的**格式级**、**格式列表**和**表格格式**cmdlet。

每个格式 cmdlet 具有如果不指定要显示的特定属性，将使用的默认属性。 每个 cmdlet 也使用相同参数名称、**属性**，以指定要显示哪些的属性。 **格式范围**仅显示一个属性，因为其**属性**参数只需一个值，但**格式列表**和**表格格式**属性参数将接受属性名称的列表。

如果使用命令**获取进程-名称 powershell**添加两个 Windows PowerShell 运行，您将获得输出如下所示︰

```
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

在此部分中的其余部分，我们将探讨如何使用**格式**cmdlet 来更改此命令的输出的显示的方式。

### 使用单项目输出格式范围
**格式范围**cmdlet，默认情况下，显示对象的默认属性。 与每个对象相关联的信息将显示在一列︰

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

您还可以指定非默认属性︰

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### 控制格式范围内显示的列
使用**格式级**cmdlet，您仅可以一次显示单个属性。 这样，用于显示简单显示每行只有一个元素的列表。 若要获取的简单的列表，设置为 1 通过键入**列**参数的值︰

```
Get-Command Format-Wide -Property Name -Column 1
```

### 使用列表视图的格式列表
**格式列表**cmdlet 显示对象在表单中的列表，与标记，并在单独的行显示每个属性︰

```
PS> Get-Process -Name powershell | Format-List

Id      : 2760
Handles : 1242
CPU     : 3.03125
Name    : powershell

Id      : 3448
Handles : 328
CPU     : 1.0625
Name    : powershell
```

您可以指定所需的尽可能多的属性︰

```
PS> Get-Process -Name powershell | Format-List -Property ProcessName,FileVersion
,StartTime,Id

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:42:00
Id          : 2760

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:54:28
Id          : 3448
```

#### 通过格式列表中使用通配符获取详细的信息
**格式列表**cmdlet，您可以使用通配符作为其**属性**参数的值。 这允许您显示详细的信息。 通常情况下，对象包括信息超过了您需要这是为什么 Windows PowerShell 中不显示默认情况下的所有属性值。 若要显示所有属性的对象，请使用**格式列表-属性\&#42;**命令。 下面的命令生成输出为单个进程 60 的行︰

```
Get-Process -Name powershell | Format-List -Property *
```

**格式列表**命令可用于显示详细信息，如果您希望包含许多项目的输出的概述，虽然简单的表格视图通常会更有用。

### 为表格的输出中使用表格格式
如果没有属性名称指定要设置格式的**获取过程**命令输出中使用**表格格式**cmdlet，您将获得完全相同输出而不执行任何格式一样。 原因是流程通常显示以表格格式，大多数 Windows PowerShell 对象。

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### 改进表格格式输出 （自动调整）
虽然表格视图可用于显示了大量类似的信息，可能很难解释如果显示的数据太窄。 例如，如果您尝试显示进程路径、 ID、 名称和公司，您获取截断的输出进程路径和公司列︰

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

如果您运行的**表格格式**命令时，您可以指定**AutoSize**参数，Windows PowerShell 将计算列的宽度，根据您要显示的实际数据。 这将**路径**列可读的但是截断公司列︰

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

**设置表格格式**cmdlet 可能仍截断数据，但它将只在屏幕的结尾处执行此操作。 显示，最后一个以外的属性，指定尽可能其最长的数据元素，才能正确显示所需的大小。 您可以查看公司名称可见，但是如果交换**路径**和**公司****属性**值列表中的位置，路径会被截断。

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

**表格格式**命令假定临近属性是属性列表的开头是多重要。 使它显示最近的开头的属性会尝试完全。 如果**表格格式**命令无法显示所有属性，它将从都显示中删除某些列，并提供一个警告。 如果在列表中进行**名称**的最后一个属性，您可以看到此行为︰

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

在上面的输出中，ID 列会被截断，以使其适合该列表中，，然后堆叠的列标题。 自动调整列大小不会始终执行所需内容。

#### 环绕表格格式输出中列 （自动换行）
您可以强制漫长**设置表格格式的**数据环绕在其显示列中，通过使用**自动换行**参数。 使用单独的**自动换行**参数将一定执行您看到的内容，因为它使用默认设置，如果不指定**AutoSize**操作︰

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

使用**自动换行**参数的一个优点是，它不会不降低处理太大。 如果执行大型目录系统的递归文件列表，则可能会花费很长时间，如果您使用**AutoSize**显示第一个输出项之前，使用大量内存。

如果您未关注系统负载**AutoSize**适用于**自动换行**参数。 初始列始终分配尽可能上一行，就像在不使用**自动换行**参数指定**AutoSize**项目显示所需的宽度。 唯一的区别是最后一列将换行，如有必要︰

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

某些列可能不会显示如果指定宽列第一次，因此最好首先指定的最小的数据元素。 在下面的示例中，我们首先，指定非常宽 path 元素，然后使用环绕，甚至我们仍然丢失最终状态的**名称**列︰

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### 组织表输出 (-GroupBy)
其他有用表格输出控制参数是**GroupBy**。 表格列表再特别可能很难比较。 **GroupBy**参数组输出根据属性值。 例如，我们可以组合流程进行更容易检测，公司缺少的属性列表中的公司值︰

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```

