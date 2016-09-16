---
title: "对于使用模块 FullyQuilifiedModuleName"
author: jaimeo
contributor: vors
ms.openlocfilehash: 4bfe45ffd9f31605f87e8547c6deccafb75f25ae
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
对于使用模块 FullyQuilifiedModuleName
=========================

现在`using module`behaives PowerShell 中其他模块相关构造相同的方式。

WMF 5.0 问题
----------

* 用户无法通过某种方式来指定模块中的版本`using module`。
* 如果有相乘模块系统上可用的版本，用户将收到的错误。

WMF 5.1
----------

* 用户可以使用`ModuleSpecification`[散列表](https://msdn.microsoft.com/en-us/library/jj136290(v=vs.85).aspx)。 此哈希表具有与相同的格式 `Get-Module -FullyQualifiedName`

**示例︰** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

* Powershell 如果存在相乘模块的版本，请使用**相同的分辨率逻辑**为`Import-Module`和不错误。

* 这使得`using module`与方块`Import-Module`和`Import-DscResource`。
