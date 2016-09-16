---
title: "从管线删除对象位置的对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: f616fbbc073c5e8870d7c8c55d6d2eb40fd3957c
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 从管线 （位置对象） 删除对象
Windows PowerShell 中您经常生成和更多和对象一起传递到管线比您希望。 您可以指定要使用的**格式**cmdlet，显示的特定对象的属性，但这不起作用删除整个对象从显示的问题。 您可能想要筛选管线，结束之前的对象，以便您可以在最初生成对象的子集执行操作。

Windows PowerShell 包括**位置对象**cmdlet 可使您可以测试管道中的每个对象并仅将其传递沿管线如果满足特定测试条件。 从渠道中删除不通过测试的对象。 为**位置 ObjectFilterScript**参数的值中提供的测试条件。

### 执行简单的测试位置对象
**FilterScript**的值是*脚本块*-括在括号 {} 的一个或多个 Windows PowerShell 命令的计算结果为 true 或 false。 这些脚本块非常简单，但是它们创建需要了解有关其他 Windows PowerShell 概念，比较运算符。 比较运算符来比较它的每一侧显示的项。 比较运算符开头-字符后, 跟一个名称。 基本比较运算符处理几乎任何类型的对象。 更高级的比较运算符可能仅适用于文本或数组。

> [!NOTE]
> 默认情况下，与文本一起使用时，Windows PowerShell 比较运算符不区分大小写。

由于分析注意事项、 符号 <>，，例如，= 不用作比较运算符。 相反，比较运算符组成字母。 下表列出了基本比较运算符。

|比较运算符|含义|（返回 true） 的示例|
|-----------------------|-----------|--------------------------|
|-eq|等于|1-eq 1|
|新的|不等于|1-新 2|
|-浅色|是小于|1-浅色 2|
|-le|小于或等于|1-le 2|
|-gt|大于|2-gt 1|
|-ge|大于或等于|2-ge 1|
|-如|就像 （对于文本通配符比较）|"file.doc"-如"f\*.do?"|
|-notlike|不是如 （通配符比较文本）|"file.doc"-notlike"p\*.doc"|
|-包含|包含|1,2,3-包含 1|
|-notcontains|不包含|1,2,3 4 notcontains|

位置对象脚本块使用特殊变量 $_ 指管道中当前的对象。 下面是如何工作的示例。 如果您有一列数字，并且只想返回那些小于 3，您可以使用的位置对象要作为筛选依据键入的数字︰

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### 基于对象属性进行筛选
由于 $_ 引用当前管道对象时，我们可以访问其属性，我们的测试。

作为示例，我们可以查看在 WMI Win32_SystemDriver 类。 可能有数百个系统驱动程序在特定系统，但仅可能感兴趣的系统驱动程序，如的当前正在运行的那些特定的一组。 如果您使用获取成员查看 Win32_SystemDriver 成员 (**获取 WmiObject-类 Win32_SystemDriver |Get-Member MemberType 属性**) 相关的属性是状态，并且它的值为"运行"，当驱动程序正在运行时，您将看到。 您可以筛选系统驱动程序中，选择运行只有通过键入︰

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"}
```

这仍会产生较长列表。 您可能想要筛选以仅选择驱动程序设置为自动启动，通过测试的 StartMode 值︰

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Auto"}

DisplayName : RAS Asynchronous Media Driver
Name        : AsyncMac
State       : Running
Status      : OK
Started     : True

DisplayName : Audio Stub Driver
Name        : audstub
State       : Running
Status      : OK
Started     : True
```

此为我们提供了大量不再需要因为我们知道驱动程序正在运行的信息。 实际上，我们可能需要在此时的唯一信息是名称和显示名称。 以下命令包括仅这两个属性，得到更简单的输出中︰

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Manual"} | Format-Table -Property Name,DisplayName

Name                                    DisplayName
----                                    -----------
AsyncMac                                RAS Asynchronous Media Driver
Fdc                                     Floppy Disk Controller Driver
Flpydisk                                Floppy Disk Driver
Gpc                                     Generic Packet Classifier
IpNat                                   IP Network Address Translator
mouhid                                  Mouse HID Driver
MRxDAV                                  WebDav Client Redirector
mssmbios                                Microsoft System Management BIOS Driver
```

在上面的命令，有两个位置对象元素，但他们可以在一个位置对象元素表示，使用-和逻辑运算符，如下所示︰

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq "Running") -and ($_.StartMode -eq "Manual") } | Format-Table -Property Name,DisplayName
```

在下表中列出的标准逻辑运算符。

|逻辑运算符|含义|（返回 true） 的示例|
|--------------------|-----------|--------------------------|
|-和|逻辑和;如果两个边，则，true|(1-eq-1） 和 (2-eq 2）。|
|-或|逻辑或;如果任意一侧为 true，则 true|(1-eq-1） 或 (1-eq 2）。|
|-不|逻辑非;对 true 和 false 求反|-不 (1-eq 2)|
|\!|逻辑非;对 true 和 false 求反|\!(1-eq 2)|

