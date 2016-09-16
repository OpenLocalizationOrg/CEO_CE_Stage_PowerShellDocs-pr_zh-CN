---
title: "新的方案和 WMF 5.1 （预览） 中的功能"
ms.date: 2016-07-13
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 92a4657e90c197cbd7d1b11f778809a860092596
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 新方案和 WMF 5.1 （预览） 中的功能 #

> 注意︰ 此信息是初步，可能会发生更改。

## PowerShell 版本 ##
从开始版本 5.1，PowerShell 是这表示不同的功能集和平台兼容性的不同版本中可用。

- **桌面版︰**在.NET Framework 内置并提供与脚本和模块设定 PowerShell 的 Windows Server 核心如和 Windows 台式机的完整资源消耗版本上运行的版本兼容性。
- **核心版︰**基于.NET 核心，并提供与脚本和定位版本的 Windows，如 Nano Server 和 Windows IoT 缩减资源消耗版本上运行的 PowerShell 模块的兼容性。

**了解有关使用 PowerShell 版本**
- [确定运行 PowerShell 版本]()
- [声明模块到特定 PowerShell 版本的兼容性]()
- [获取模块按筛选结果 CompatiblePSEditions]()
- [防止执行脚本，除非是兼容的 PowerShell 版本上运行]()

## 目录 Cmdlet  

已添加了两个新 cmdlet 中[Microsoft.PowerShell.Security](https://technet.microsoft.com/en-us/library/hh847877.aspx)模块中。这些生成和验证 Windows 目录文件。  

###新 FileCatalog 
--------------------------------

新 FileCatalog Windows 目录为创建文件的文件夹和文件。 此目录文件包含指定路径中的所有文件哈希。 用户可以分发一的组以及表示这些文件夹的相应目录文件的文件夹。 此信息很有用来验证是否目录创建时间后的文件夹进行任何更改。    

```PowerShell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
支持的目录版本 1 和 2。 版本 1 使用 SHA1 哈希算法来创建文件哈希;第 2 版使用 SHA256。 在*Windows Server 2008 R2*或*Windows 7*上不支持目录版本 2。 在*Windows 8*、 *Windows Server 2012*和更高版本操作系统上，应使用目录版本 2。  

![](../images/NewFileCatalog.jpg)

这将创建目录文件。 

![](../images/CatalogFile1.jpg)  

![](../images/CatalogFile2.jpg) 

若要验证的目录文件 (在上面的示例 Pester.cat) 完整性，登录使用[设置 AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet。   


###测试 FileCatalog 
--------------------------------

测试 FileCatalog 验证目录表示一组文件夹。 

```PowerShell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

此 cmdlet 比较所有文件哈希和是*磁盘*上的*目录*中找到其相对的路径。 如果检测到任何文件哈希和路径，则返回的状态为*ValidationFailed*之间的不匹配。 用户可以通过使用检索所有此类信息*-详细*参数。 它还显示*签名*属性，它相当于调用[获取 AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) cmdlet 目录文件中的目录的签名状态。 用户可以跳过任何文件验证期间通过使用*-FilesToSkip*参数。 


## 模块分析缓存 ##
从开始 WMF 5.1，PowerShell 提供控制有关模块，如它导出的命令的缓存数据使用的文件。

默认情况下，在文件中存储此缓存`${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`。
缓存搜索命令时在启动时通常读取并写入后台线程上一段时间后模块导入。

若要更改缓存的默认位置，请设置`$env:PSModuleAnalysisCachePath`环境变量，然后再开始 PowerShell。 对此环境变量的更改仅会影响子流程。 值应名称 PowerShell 有权创建和写入文件的完整路径 （包括文件名）。 要禁用文件缓存，请将该值设置为无效的位置，例如︰

```PowerShell
$env:PSModuleAnalysisCachePath = 'nul'
```

此设置无效的设备的路径。 如果 PowerShell 无法写入路径，不会返回错误，但您可以查看错误报告使用追踪︰

```PowerShell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

编写出缓存时, 将检查 PowerShell 不再存在以避免不必要地大缓存的模块。
有时这些检查都不需要，在这种情况下您可以将其关闭通过设置︰

```PowerShell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

设置此环境变量将会立即生效当前进程中。

##指定模块版本

WMF 5.1 中`using module`行为 PowerShell 中其他模块相关构造相同的方式。 以前，您必须无法指定特定模块版本;如果存在多个版本，这会导致错误。


在 WMF 5.1:

* 您可以使用`ModuleSpecification`[哈希表](https://msdn.microsoft.com/en-us/library/jj136290(v=vs.85).aspx)。 此哈希表具有相同的格式为`Get-Module -FullyQualifiedName`。

**示例︰** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

* PowerShell 如果存在多个版本的模块，请使用**相同的分辨率逻辑**为`Import-Module`并不会返回错误--相同的行为`Import-Module`和`Import-DscResource`。


##改进 Pester
在 WMF 5.1 使用 PowerShell Pester 附带的版本进行了更新从 3.3.5 到 3.4.0，添加了提交 https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e，对于 Pester Nano 服务器上启用更好的行为。 

您可以通过检查 ChangeLog.md 文件在查看版本 3.3.5 到 3.4.0 中的更改︰ https://github.com/pester/Pester/blob/master/CHANGELOG.md
