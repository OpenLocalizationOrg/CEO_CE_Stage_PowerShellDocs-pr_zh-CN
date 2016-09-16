---
title: "了解 Windows PowerShell 渠道"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: 34e641329388436074f2d0f05647ec4fa7efdf83
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 了解 Windows PowerShell 渠道
Windows PowerShell 管道工作几乎任意位置。 虽然您可以在屏幕上看到文本，Windows PowerShell 不管道命令之间的文本。 相反，它管道对象。

为管线表示法是类似于用在其他外壳，第一次看到因此，它可能不明显 Windows PowerShell 引入了新内容。 例如，如果您使用**传出托管**cmdlet，只需从另一个命令，输出外观强制的输出按页显示等普通文本显示在屏幕上，分为页面︰

```
PS> Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\system32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2005-10-22  11:04 PM        315 $winnt$.inf
-a---        2004-08-04   8:00 AM      68608 access.cpl
-a---        2004-08-04   8:00 AM      64512 acctres.dll
-a---        2004-08-04   8:00 AM     183808 accwiz.exe
-a---        2004-08-04   8:00 AM      61952 acelpdec.ax
-a---        2004-08-04   8:00 AM     129536 acledit.dll
-a---        2004-08-04   8:00 AM     114688 aclui.dll
-a---        2004-08-04   8:00 AM     194048 activeds.dll
-a---        2004-08-04   8:00 AM     111104 activeds.tlb
-a---        2004-08-04   8:00 AM       4096 actmovie.exe
-a---        2004-08-04   8:00 AM     101888 actxprxy.dll
-a---        2003-02-21   6:50 PM     143150 admgmt.msc
-a---        2006-01-25   3:35 PM      53760 admparse.dll
<SPACE> next page; <CR> next line; Q quit
...
```

Out-Host-分页命令是有用的管道元素，只要您有想要显示缓慢的冗长输出。 如果操作非常 CPU 密集型，将特别有用。 因为处理转移到传出托管 cmdlet 时它已准备好显示一个完整的页，cmdlet 之前在管道中暂停操作，直到输出的下一页上可用。 如果您使用 Windows 任务管理器监视 CPU 和内存使用 Windows PowerShell，您可以查看此。

运行以下命令︰**获取 ChildItem c:\\Windows-递归**。 比较到此命令 CPU 和内存使用率︰**获取 ChildItem c:\\Windows-递归 |传出托管-分页**。 在屏幕上看到的内容是文本，但这是因为需要为控制台窗口中的文本表示的对象。 这是只表示什么是真正开始往上内 Windows PowerShell。 例如，请考虑获取位置 cmdlet。 如果您的当前位置时驱动器 C 的根中，键入**获取位置**，您会看到以下输出︰

```
PS> Get-Location

Path
----
C:\
```

如果 Windows PowerShell 管道文本，发出如**获取位置命令 |传出托管**，是否能通过从**获取位置****传出托管**的字符集它们显示在屏幕上的顺序。 换言之，如果您要忽略的标题信息，**传出托管**第一次将收到字符**C**，然后字符**:**，然后字符**\\**。 **传出托管**cmdlet 不能确定什么指相关联的字符输出**获取位置**cmdlet。

而不是使用文本，让管道中的命令通信，请使用 Windows PowerShell。 从用户的角度来看，对象打包到使得更加轻松地控制的信息作为单元，一个窗体的相关的信息和提取需要的特定项目。

**获取位置**命令不会返回包含当前路径的文本。 它返回名为**PathInfo**对象包含当前路径及其他一些信息的信息的包。 **传出主机**cmdlet 然后将该**PathInfo**对象发送到屏幕上，并 Windows PowerShell 决定其格式规则在要显示的信息以及如何将其显示基于的内容。

实际上，仅在该过程，在屏幕上显示的数据的格式设置的过程的一部分的末尾添加标题信息输出**获取位置**cmdlet。 您看到的内容在屏幕上的摘要信息，不完整的对象表示形式输出。

假设可能有更多的信息输出 Windows PowerShell 命令比在控制台窗口中，我们所看到的内容显示方式可以从您检索不可见的元素吗？ 如何查看额外的数据？ 然后，如果您想要不同于一个 Windows PowerShell 格式以正常方式查看数据使用？

这一章的其余部分讨论如何发现结构的特定的 Windows PowerShell 对象，请选择特定项目和设置其格式更容易显示，以及如何将此信息发送给可选输出位置，例如文件和打印机。

