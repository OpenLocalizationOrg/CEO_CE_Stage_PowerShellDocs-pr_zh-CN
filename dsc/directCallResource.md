---
title: "直接呼叫 DSC 资源方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 97d97a36830088d6ee1296cda5310e087fc41893
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 直接呼叫 DSC 资源方法

>适用于︰ Windows PowerShell 5.0

您可以使用[调用 DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) cmdlet 直接呼叫函数或 DSC 资源 （**获取 TargetResource**、**设置 TargetResource**和**测试 TargetResource**函数 MOF 基于资源的） 或**获取**、**设置**以及**测试**方法的类基于资源的方法。 此时可以使用第三方想要使用 DSC 资源，或作为有用工具开发资源。 

结合 metaconfiguration 属性通常用于此 cmdlet `refreshMode = 'Disabled'`，但可以无论何种**refreshMode**设置为使用它。

当调用**调用 DscResource** cmdlet，您可以指定哪种方法或函数，用于使用**方法**参数呼叫。 通过传递**属性**参数的值作为哈希表中指定的资源的属性。

下面是直接调用资源方法的示例︰

## 确保文件不含

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## 文件不含测试

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## 获取文件的内容

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

>**注意︰**不支持直接调用复合资源方法。 相反，调用基础构成复合资源的资源的方法。

## 另请参阅
- [编写自定义与 MOF DSC 资源](authoringResourceMOF.md) 
- [编写自定义使用 PowerShell 类 DSC 资源](authoringResourceClass.md)
- [调试 DSC 资源](debugResource.md)

