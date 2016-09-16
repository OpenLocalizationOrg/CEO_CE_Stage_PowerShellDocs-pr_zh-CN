---
title: "DSC ProcessSet 资源"
ms.date: 2016-05-23
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: f9754be3f803d3232189985faa41fb209bfcfe46
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC WindowsProcess 资源

> 适用于︰ Windows PowerShell 5.0

**ProcessSet**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来在目标节点上配置流程。 该资源是为每个组中指定呼叫[WindowsProcess 资源](windowsProcessResource.md)[复合资源](authoringResourceComposite.md)`GroupName`参数。

## 语法

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ StandardOutputPath = [string] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]   
    [ WorkingDirectory = [string] ]
    [ DependsOn = [string[]] ]
}
```

## 属性
|  属性  |  说明   | 
|---|---| 
| 参数| 一个字符串，包含参数传递给为流程-是。 如果您需要通过多个参数，则此字符串中的所有将它们。| 
| 路径| 处理可执行文件的路径。 以下是可执行文件 （不完全限定的路径） 的名称，如果 DSC 资源将搜索**Path**环境变量 (`$env:Path`) 以查找文件。 如果此属性的值是完全限定的路径，DSC 将不使用**Path**环境变量以查找的文件，如果任何路径不存在，将引发错误。 不允许使用相对路径。| 
| 凭据| 指示过程开始的凭据。| 
| 确保| 指定是否存在流程。 设置为"演示"，以确保该过程存在该属性。 否则，将其设置为"无"。 默认为"演示"。| 
| StandardErrorPath| 流程写入标准误差的路径。 将覆盖任何现有文件。| 
| StandardInputPath| 流程从中接收标准输入流。| 
| StandardOutputPath| 流程写入标准输出文件的路径。 将覆盖任何现有文件。| 
| WorkingDirectory| 为当前工作目录用于进程位置。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是**资源名称**和其类型是**_ResourceType**，使用此属性的语法如下 ' 取决于 ="[资源类型] 资源名称"。| 

