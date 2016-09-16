---
title: "选择对象部分选择对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 66f2927652b33371aa11db1662d3e9d28b4f5fbd
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 选择对象 （选择对象） 的某些部分
**选择对象**cmdlet 可用于创建新的自定义的 Windows PowerShell 对象包含选中从使用来创建这些对象的属性。 键入以下命令以创建新的对象，其中包含仅 Win32_LogicalDisk WMI 类的名称和可用空间属性︰

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

发出该命令之后，看不到的数据类型，但如果您在选择对象后管道获取成员的结果，您可以辨别您有新的对象，PSCustomObject 类型︰

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace| Get-Member

   TypeName: System.Management.Automation.PSCustomObject

Name        MemberType   Definition
----        ----------   ----------
Equals      Method       System.Boolean Equals(Object obj)
GetHashCode Method       System.Int32 GetHashCode()
GetType     Method       System.Type GetType()
ToString    Method       System.String ToString()
FreeSpace   NoteProperty  FreeSpace=...
Name        NoteProperty System.String Name=C:
```

选择对象有许多用途。 其中之一复制然后，您可以修改的数据。 现在，我们可以处理我们在上一节中遇到的问题。 我们可以更新可用空间的值中新创建的对象，输出将包括描述性标签︰

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```

