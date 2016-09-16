---
title: "将数据使用重定向出 Cmdlet"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: b48cc5fbd5c229d0339a24402e186fe9ef69e97b
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 重定向数据出-* Cmdlet
Windows PowerShell 提供多种 cmdlet，以便您可以控制直接输出的数据。 使用这些 cmdlet 共享两个重要的特征。

首先，他们通常将数据转换为文本的一些窗体。 他们这样做，因为它们输出系统组件需要文本输入的数据。 这意味着他们需要表示为文本的对象。 因此，正如您在 Windows PowerShell 控制台窗口中看到格式文本。

第二步，使用这些 cmdlet 使用 Windows PowerShell 动词**出**，因为这些信息将从发送 Windows PowerShell 到其他位置。 **传出主机**cmdlet 也不例外: 主机窗口显示为外部 Windows PowerShell。 这是重要，因为注销 Windows PowerShell 发送数据时，它实际上将被删除。 您可以看到如果您尝试创建管线主机窗口中，为该页面数据，然后尝试设置其格式列表中，如下所示︰

```
PS> Get-Process | Out-Host -Paging | Format-List
```

您可能希望使用命令采用列表格式显示页的过程信息。 相反，它会显示默认的表格式列表︰

```
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    101       5     1076       3316    32     0.05   2888 alg
...
    618      18    39348      51108   143   211.20    740 explorer
    257       8     9752      16828    79     3.02   2560 explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

**传出主机**cmdlet 将数据发送到控制台，直接以便**格式列表**命令永远不会收到任何要设置格式。

结构此命令的正确方法是将**传出托管**cmdlet 末尾的管道如下所示。 这会导致之前正分页并显示列表中要设置格式的流程数据。

```
PS> Get-Process | Format-List | Out-Host -Paging

Id      : 2888
Handles : 101
CPU     : 0.046875
Name    : alg
...

Id      : 740
Handles : 612
CPU     : 211.703125
Name    : explorer

Id      : 2560
Handles : 257
CPU     : 3.015625
Name    : explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

这适用于所有**出**cmdlet。 **出**cmdlet 应始终显示管道的末尾。

> [!NOTE]
> 所有**出**cmdlet 呈现输出为文本，并使用格式有效控制台窗口中，包括行的长度限制。

#### 分页控制台输出 （传出托管）
默认情况下，Windows PowerShell 将数据发送到主机窗口中，是完全传出托管 cmdlet 的用途。 主要用于传出托管 cmdlet 我们如前所述是分页数据。 例如，以下命令使用传出主机页面获取命令 cmdlet 输出︰

```
PS> Get-Command | Out-Host -Paging
```

您还可以使用到页面上数据的**多个**函数。 Windows PowerShell 中**更**是函数调用**传出托管-分页**。 以下命令演示如何使用**多个**函数来获取命令的输出页面︰

```
PS> Get-Command | more
```

如果一个或多个文件名中包含多个函数的参数时，该函数将指定的文件中读取和页面到主机及其内容︰

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### 放弃输出 (传出 Null)
**传出 Null** cmdlet 旨在立即放弃收到任何输入。 这是丢弃不必要运行命令的一侧效果为您收到的数据的有用。 当键入以下命令，会从命令返回收到任何内容︰

```
PS> Get-Command | Out-Null
```

**传出 Null** cmdlet 不会丢弃错误输出。 例如，如果您输入以下命令，将显示一条消息通知您的 Windows PowerShell 无法识别的内容是 NotACommand:

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### 打印数据 （Out-打印机）
您可以通过使用**Out-打印机**cmdlet 打印数据。 如果您不提供打印机名称， **Out-打印机**cmdlet 将使用您的默认打印机。 您可以通过指定其显示名称中使用任何基于 Windows 的打印机。 存在不需要的任何类型的打印机端口映射或甚至真实物理打印机。 例如，如果您有安装 Microsoft Office 文档映像工具，您可以通过键入将数据发送图像文件中︰

```
PS> Get-Command Get-Command | Out-Printer -Name "Microsoft Office Document Image Writer"
```

#### 保存数据 （传出文件）
通过发送到一个文件，而不是控制台窗口输出**传出文件**cmdlet。 下面的命令行发送到文件的进程的列表**c:\\temp\\processlist.txt**:

```
PS> Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

使用的结果**传出文件**cmdlet 可能不适用于如果您使用传统的输出重定向到您看到的内容。 若要了解其行为，您必须在其中上下文**传出文件**cmdlet 进行操作。

默认情况下，**传出文件**cmdlet 创建 Unicode 文件。 这是最佳的默认长期运行，但它意味着该工具所期望 ASCII 文件将无法正常使用默认的输出格式。 您可以通过使用**编码**参数到 ASCII 更改默认的输出格式︰

```
PS> Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

**传出文件**格式文件内容看起来像控制台输出。 这会使输出就像在控制台窗口中，在大多数情况下是被截尾取整。 例如，如果您运行以下命令︰

```
PS> Get-Command | Out-File -FilePath c:\temp\output.txt
```

输出将如下所示︰

```
CommandType     Name                            Definition                     
-----------     ----                            ----------                     
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

要获取不强制自动换行，以匹配屏幕宽度的输出，您可以使用**宽度**参数指定线条宽度。 **宽度**为 32 位整数参数，因为它可以具有最大值是 2147483647。 键入以下命令以设置为此最大值的线条宽度︰

```
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

**传出文件**cmdlet 您想要将输出另存为将控制台上有显示时最有用。 更好地控制输出格式，您需要更多高级的工具。 我们将探讨中下一章，以及一些有关对象操作的详细信息。

