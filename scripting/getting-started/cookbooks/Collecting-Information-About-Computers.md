---
title: "收集有关计算机的信息"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
ms.openlocfilehash: 4f53fb9bd096b63e23763e737dae03da2126ec56
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 收集有关计算机的信息
**获取 WmiObject**是常规系统管理任务的最重要的 cmdlet。 通过 WMI 公开的所有关键子系统设置。 此外，WMI 将数据视为一个或多个项的集合中的对象。 因为 Windows PowerShell 也适用于对象，并且包含，您可以将单个或多个对象相同的方式渠道，一般 WMI 访问可以执行一些使用很少工作的高级的任务。

下面的示例演示如何针对任意计算机使用**获取 WmiObject**收集特定信息。 带有点值 （**.**） 表示本地计算机，我们可以指定参数的**计算机名称**。 您可以指定名称或与您可以通过 WMI 到达任何计算机相关联的 IP 地址。 若要检索本地计算机有关的信息，可以忽略**-计算机名称。**

### 列表桌面设置
我们首先将本地计算机收集信息台式机的命令。

```
Get-WmiObject -Class Win32_Desktop -ComputerName .
```

这将它们是否在使用或不返回所有台式机的信息。

> [!NOTE]
> 返回由一些 WMI 类信息可以非常详细，和通常包括有关 WMI 课堂元数据。 因为大多数这些元数据属性以双下划线开头的名称，您可以筛选使用选择对象的属性。 通过使用**[a 到 z]**字母字符与指定开始的属性 * 作为属性值。 例如︰

```
Get-WmiObject -Class Win32_Desktop -ComputerName . | Select-Object -Property [a-z]*
```

若要筛选出元数据，使用管道运算符 (|) 发送获取 WmiObject 命令的结果为**选择对象的属性 [a 到 z]***。

### 列表 BIOS 信息
WMI Win32_BIOS 类返回本地计算机上的有关系统 BIOS 相当紧凑和完整信息︰

```
Get-WmiObject -Class Win32_BIOS -ComputerName .
```

### 列出的处理器信息
虽然您可能要筛选的信息，您可以通过使用 WMI 的**Win32_Processor**类，检索常规处理器信息︰

```
Get-WmiObject -Class Win32_Processor -ComputerName . | Select-Object -Property [a-z]*
```

一般说明字符串的处理器系列，您可以只返回**SystemType**属性︰

```
PS> Get-WmiObject -Class Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType
SystemType
----------
X86-based PC
```

### 列出计算机制造商和模型
计算机模型信息还会显示**Win32_ComputerSystem**。 标准显示的输出不需要任何筛选器来提供 OEM 数据︰

```
PS> Get-WmiObject -Class Win32_ComputerSystem
Domain              : WORKGROUP
Manufacturer        : Compaq Presario 06
Model               : DA243A-ABA 6415cl NA910
Name                : MyPC
PrimaryOwnerName    : Jane Doe
TotalPhysicalMemory : 804765696
```

此操作，如命令其返回直接从某些硬件的信息，请从您输出才相当于您拥有的数据。 某些信息硬件制造商未正确配置，因此可能不可用。

### 列出已安装的修补程序
您可以通过使用**Win32_QuickFixEngineering**列出所有安装的修补程序︰

```
Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName .
```

此类返回的外观如下所示的修补程序的列表︰

```
Description         : Update for Windows XP (KB910437)
FixComments         : Update
HotFixID            : KB910437
Install Date        :
InstalledBy         : Administrator
InstalledOn         : 12/16/2005
Name                :
ServicePackInEffect : SP3
Status              :
```

对于更简洁输出，您可能想要排除某些属性。 虽然您可以使用**获取-WmiObject 属性**参数来选择仅**HotFixID**，这样做这样将实际返回的详细信息，因为默认情况下显示的元数据︰

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property HotFixID
HotFixID         : KB910437
__GENUS          : 2
__CLASS          : Win32_QuickFixEngineering
__SUPERCLASS     :
__DYNASTY        :
__RELPATH        :
__PROPERTY_COUNT : 1
__DERIVATION     : {}
__SERVER         :
__NAMESPACE      :
__PATH           :
```

返回的其他数据，因为**获取 WmiObject**中的属性参数限制返回从 WMI 类实例的属性，不是对象返回到 Windows PowerShell。 若要降低输出，请使用**选择对象**︰

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property Hot
FixId | Select-Object -Property HotFixId
HotFixId
--------
KB910437
```

### 操作系统版本信息列表
**Win32_OperatingSystem**类属性包括版本和服务包信息。 显式，您可以选择仅从**Win32_OperatingSystem**获取版本信息的摘要这些属性︰

```
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

您也可以**选择对象的属性**参数使用通配符。 由于重要使用此处以**生成**或**ServicePack**开头的所有属性，我们可以缩短此到下面的窗体︰

```
PS> Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property Build*,OSType,ServicePack*

BuildNumber             : 2600
BuildType               : Uniprocessor Free
OSType                  : 18
ServicePackMajorVersion : 2
ServicePackMinorVersion : 0
```

### 列表本地用户和所有者
本地的常规用户信息 — 授权的用户数、 当前用户数，以及所有者名称 — 找不到与所选内容的**Win32_OperatingSystem**属性。 您可以显式选择要显示如下所示的属性︰

```
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

使用通配符的更多简洁版本是︰

```
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### 获取可用磁盘空间
若要查看的磁盘空间和可用空间用于本地驱动器，您可以使用 WMI Win32_LogicalDisk 类。 您需要查看 DriveType 3 的实例 — WMI 用于值固定硬盘。

```
Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName .

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 65541357568
Size         : 203912880128
VolumeName   : Local Disk

DeviceID     : Q:
DriveType    : 3
ProviderName :
FreeSpace    : 44298250240
Size         : 122934034432
VolumeName   : New Volume

Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName . | Measure-Object -Property FreeSpace,Size -Sum | Select-Object -Property Property,Sum
```

### 获取登录会话信息
您可以获得有关与用户通过 WMI Win32_LogonSession 类相关联的登录会话的常规信息︰

```
Get-WmiObject -Class Win32_LogonSession -ComputerName .
```

### 获取登录到一台计算机上的用户
您可以显示登录到使用 Win32_ComputerSystem 特定计算机系统的用户。 此命令返回仅登录到系统桌面的用户︰

```
Get-WmiObject -Class Win32_ComputerSystem -Property UserName -ComputerName .
```

### 从计算机中获取本地时间
您可以通过使用 WMI Win32_LocalTime 类检索特定计算机上当前的本地时间。 默认情况下的此类显示所有元数据，因为您可能想要筛选使用**选择对象**︰

```
PS> Get-WmiObject -Class Win32_LocalTime -ComputerName . | Select-Object -Property [a-z]*

Day          : 15
DayOfWeek    : 4
Hour         : 12
Milliseconds :
Minute       : 11
Month        : 6
Quarter      : 2
Second       : 52
WeekInMonth  : 3
Year         : 2006
```

### 显示服务状态
若要查看特定计算机上的所有服务的状态，可以在本地使用**获取服务**cmdlet 如前所述。 对于远程系统，您可以使用 WMI Win32_Service 类。 如果还可以使用**选择对象**以筛选结果**状态**、**名称**和**显示名称**，将几乎相同**获取服务**中的输出格式︰

```
Get-WmiObject -Class Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

若要允许完成偶尔服务非常长名称的名称的显示，可能想要使用**表格格式**使用**AutoSize**和**自动换行**参数，优化列的宽度，并允许长的名称，而不是被截断换行︰

```
Get-WmiObject -Class Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```

