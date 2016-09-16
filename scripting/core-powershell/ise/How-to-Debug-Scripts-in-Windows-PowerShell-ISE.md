---
title: "如何调试 Windows PowerShell ISE 中的脚本"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6dc6d8f9-8978-46e9-a92f-169af37e2817
ms.openlocfilehash: d95c792be87bcc78ed1708f8917a72483718c744
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 如何调试 Windows PowerShell ISE 中的脚本
本主题介绍如何使用 Windows PowerShellÂ® 集成脚本环境 (ISE) 视觉调试功能调试脚本本地计算机上。

[如何管理断点](#bkmk_1)
[如何管理调试会话](#bkmk_2)
[如何逐、 单步执行，并移出时调试](#bkmk_3)
[如何显示在调试变量的值](#bkmk_4)

## <a name="bkmk_1"></a>如何管理断点
断点是您想要暂停，以便您可以检查变量和脚本正在运行的环境的当前状态运算脚本中的指定的位置。 一旦脚本已暂停的断点，您可以在控制台窗格来检查您的脚本状态运行命令。  您可以输出变量或运行其他命令。 您甚至可以修改对当前正在运行的脚本的上下文可见的任何变量的值。 检查您想要查看完后，您可以继续操作的脚本。

在 Windows PowerShell 调试环境中，您可以设置三种类型的断点︰

1.  **行断点**。 脚本暂停的脚本操作过程达到指定的行时

2.  **变量断点。** 指定的变量的值发生更改时，该脚本暂停。

3.  **Command 断点。** 脚本暂停只要指定的命令即将运行该脚本操作过程。 它可以包括参数以进一步筛选断点到所需的操作。 命令也可以是您创建的函数。

其中，在 Windows PowerShell ISE 调试环境中，可以通过使用菜单或键盘快捷方式设置仅行断点。 可以设置其他两种类型的断点，但通过[设置 PSBreakpoint [m2]](https://technet.microsoft.com/en-us/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) cmdlet 设置从控制台窗格。 本节介绍如何通过使用的菜单，其中可用，请在 Windows PowerShell ISE 执行调试任务和使用脚本从控制台窗格执行广泛的命令。

### 若要设置断点
仅在已保存后，可以在脚本设置断点。 右键单击您要在其中设置行断点，的行，然后单击**切换断点**。 或者，单击要设置行断点，并按**F9** ，或者单击**调试**菜单上的**切换断点**的行。

以下脚本是如何通过[设置 PSBreakpoint](https://technet.microsoft.com/en-us/library/6afd5d2c-a285-4796-8607-3cbf49471420) cmdlet，从控制台窗格中设置变量断点的示例。

```
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
set-psbreakpoint -script sample.ps1 -variable Server
```

### 列出所有断点
显示当前 Windows PowerShellÂ® 会话中的所有断点。

在**调试**菜单上，单击**列表断点**。 以下脚本是通过[获取 PSBreakpoint](https://technet.microsoft.com/en-us/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) cmdlet，您就可以列出所有断点从控制台窗格中的示例。

```
# This command lists all breakpoints in the current session. 
get-psbreakpoint
```

### 删除断点
删除断点删除它。  如果您认为可能想要以后再次使用它，请考虑[禁用](#bkmk_disable)它改为。  右键单击要删除断点的行，然后单击**切换断点**。 或单击要删除断点的行，然后单击**调试**菜单上的**切换断点**。 以下脚本是如何通过[删除 PSBreakpoint](https://technet.microsoft.com/en-us/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet 从控制台窗格中删除具有指定 ID 断点的示例。

```
# This command deletes the breakpoint with breakpoint ID 2.
remove-psbreakpoint -id 2
```

### 删除所有断点
若要删除所有断点定义在当前会话，请在**调试**菜单上，单击**都删除所有断点**。

以下脚本是如何通过[删除 PSBreakpoint](https://technet.microsoft.com/en-us/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet 从控制台窗格中删除所有断点的示例。

```
# This command deletes all of the breakpoints in the current session.
get-psbreakpoint | remove-psbreakpoint
```

### <a name="bkmk_disable"></a>禁用断点
禁用断点不会删除它。它将其关闭，直到它已启用。  若要禁用特定行断点，右键单击要禁用断点的行，然后单击**禁用断点**。 或者，单击要禁用断点，并按**F9** ，或者单击**调试**菜单上的**禁用断点**的行。 以下脚本是如何通过[禁用 PSBreakpoint](https://technet.microsoft.com/en-us/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet，从控制台窗格中删除具有指定 ID 断点的示例。

```
# This command disables the breakpoint with breakpoint ID 0.
disable-psbreakpoint -id 0
```

### 禁用所有断点
禁用断点不会删除它。它将其关闭，直到它已启用。  禁用所有断点，在当前会话，请在**调试**菜单上，单击**禁用所有断点**。 以下脚本是通过[禁用 PSBreakpoint](https://technet.microsoft.com/en-us/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet，您就可以禁用所有断点从控制台窗格中的示例。

```
# This command disables all breakpoints in the current session. 
# You can abbreviate this command as: "gbp | dbp".
get-psbreakpoint | disable-psbreakpoint
```

### 启用断点
若要启用特定断点，右键单击要启用断点的行，然后单击**启用断点**。 或者，单击要启用断点，然后按**F9**或，单击**调试**菜单上的**启用断点**的行。 以下脚本是通过[启用 PSBreakpoint](https://technet.microsoft.com/en-us/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet，您就可以启用特定断点控制台窗格中的示例。

```
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
enable-psbreakpoint -id 0, 1, 5
```

### 启用所有断点
若要启用所有断点定义在当前会话，请在**调试**菜单上，单击**都启用所有断点**。 以下脚本是通过[启用 PSBreakpoint](https://technet.microsoft.com/en-us/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet，您就可以启用从控制台窗格中的所有断点的示例。

```
# This command enables all breakpoints in the current session. 
# You can abbreviate the command by using their aliases: "gbp | ebp".
get-psbreakpoint | enable-psbreakpoint
```

## <a name="bkmk_2"></a>如何管理调试会话
在开始调试之前，必须设置一个或多个断点。 不能设置断点，除非您想要调试脚本被保存。 如何设置断点的上的说明，请参阅[如何管理断点](#bkmk_1)或[设置 PSBreakpoint](https://technet.microsoft.com/en-us/library/6afd5d2c-a285-4796-8607-3cbf49471420)。 在开始调试后，不能编辑脚本，直到您停止调试。 之前运行它时，会自动保存已设置的一个或多个断点一个脚本。

### 若要开始调试
按**F5**的工具栏上，单击**运行脚本**图标，或在**调试**菜单上单击**运行/继续**。 脚本运行直到遇到第一个断点。 它暂停那里操作，并突出显示它已暂停的行。

### 若要继续调试
按**F5**或的工具栏上，单击**运行脚本**图标，或单击**调试**菜单上的**运行/继续**或，在控制台窗格中，键入**C** ，然后按**ENTER**。 这会导致脚本继续运行到下一个断点或脚本的末尾，如果不遇到任何进一步断点。

### 若要查看调用堆栈
调用堆栈显示当前运行脚本中的位置。 如果在不同的函数调用的函数中运行脚本，然后表示在显示的输出中的其他行。 最底部行显示原始脚本和行的称为函数。 该函数和行中的另一个函数可能被称为下对齐显示。  最顶层的行显示当前设置断点的当前行的上下文。

在暂停时，若要查看当前调用堆栈，按**CTRL + SHIFT + D**或，请单击**调试**菜单上的**显示调用堆栈**或，控制台窗格中，键入**K** ，然后按**ENTER**。

### 若要停止调试
按**SHIFT F5**或，请单击**调试**菜单上的**停止调试程序**，或者，控制台窗格中，键入**Q** ，然后按**ENTER**。

## <a name="bkmk_3"></a>如何逐、 单步执行，并移出时调试
单步执行是一次运行一个语句的过程。 您可以停止在行中的代码，并检查变量和系统状态的值。 下表介绍了常见调试任务，如单步执行、 单步中，执行和单步执行。

||||
|-|-|-|
|**调试任务**|**说明**|**如何为 PowerShell ISE**|
|**单步执行**|执行当前语句，然后停在下一个语句。 如果当前语句函数或脚本的呼叫，然后为该函数或脚本调试程序步骤，否则它将停止在下一个语句。|按**F11**或，请在**调试**菜单上，单击**单步执行**或控制台窗格中，键入**S** ，然后按**ENTER**。|
|**逐过程**|执行当前语句，然后停在下一个语句。 当前语句时函数或脚本的呼叫然后调试程序执行整个函数或脚本，并在下一个语句后函数调用它停止。|按**F10**或，在**调试**菜单上，单击**逐**，或在控制台窗格中，键入**V** ，然后按**ENTER**。|
|**的步骤**|利用当前的函数和向上一级如果嵌套函数的步骤。 如果在主要正文中，为结束时，或下一个断点执行该脚本。 将执行，但不是单步执行跳过的语句。|按**SHIFT + F11**，或在**调试**菜单上，单击**步骤出**，或在控制台窗格中，键入**O** ，然后按**ENTER**。|
|**继续**|继续执行结束时，或下一个断点。 跳过的函数和调用是执行，但不是单步执行。|按**F5**或，请单击**调试**菜单上的**运行/继续**，或在控制台窗格中，键入**C** ，然后按**ENTER**。|

## <a name="bkmk_4"></a>如何在调试时显示的变量值
单步执行代码时，可以在脚本中显示变量的当前值。

### 若要显示标准变量的值
使用下列方法之一︰

-   在脚本窗格中，将鼠标悬停在要为工具提示中显示其值的变量。

-   在控制台窗格中，键入变量的名称，然后按**ENTER**。

ISE 中的所有窗格通常都是相同的范围。 因此，调试脚本时, 键入控制台窗格中的命令运行脚本作用域中。 这样，您可以使用控制台窗格查找变量的值并仅在脚本中定义的函数调用。

### 若要显示的自动变量值
您可以使用上述方法调试脚本时显示的几乎所有变量的值。 但是，这些方法不适合以下自动变量。

-   $_

-   $Input

-   $MyInvocation

-   $PSBoundParameters

-   $Args

如果您尝试以显示这些变量的任何值，您将获得该变量的值，在内部的管道中调试程序使用，不在脚本变量的值。 您可以解决此几个变量 （$_、 $Input、 $MyInvocation、 $PSBoundParameters 和 $Args） 使用下列方法︰

1.  在脚本中，将分配给新变量的自动变量的值。

2.  通过将鼠标悬停在脚本窗格中的新变量或键入新变量控制台窗格中显示的新变量的值。

例如，若要显示在脚本 $MyInvocation 变量的值，将值分配给新变量，如 $scriptname，然后将鼠标悬停在或键入要显示其值的 $scriptname 变量。

```
#In MyScript.ps1
$scriptname = $MyInvocation.MyCommand.Path

#In the Console Pane:
C:\ps-test> $scriptname
C:\ps-test\MyScript.ps1
```

## 另请参阅
[使用 Windows PowerShell ISE](Using-the-Windows-PowerShell-ISE.md)

