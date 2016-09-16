---
title: "为多个对象 ForEach 对象的重复任务"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 4b219e4499482eafa6eddf1461b74c62ba091d1a
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 重复任务，多个对象 （ForEach 对象）
**ForEach 对象**cmdlet 使用脚本块和管线当前 $_ 描述符，让您在管道中每个对象上运行的命令。 这可以用于执行一些非常复杂的任务。

这会非常有用的一种情况操作数据，以使其更有用。 例如，从 WMI Win32_LogicalDisk 类可以用于返回每个本地磁盘空间信息。 返回的数据以字节，但是，这使得难以阅读︰

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

我们可以将可用空间值转换为兆字节每个值除以 1024年两次。第一个部门后, 的数据是千字节，并且在第二个除法后兆字节。 您可以执行的 ForEach 对象脚本块中通过键入︰

```
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

很遗憾，输出是带未关联标签的数据。 因为类似 WMI 属性是只读的不能直接转换可用空间。 如果您键入此内容︰

```
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

您收到一条错误消息︰

```
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

您无法使用某些高级的技巧来重新组织数据，但更简单的方法是创建新的对象，通过**选择对象**。

