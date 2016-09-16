---
title: "DSC WindowsProcess 资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 7e8c0d39d4f49d09acef79d789ee54f158e465f8
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC WindowsProcess 资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

**WindowsProcess**资源在 Windows PowerShell 需要状态配置 (DSC) 提供一种机制目标节点上配置流程。

## 语法

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## 属性
|  属性  |  说明   | 
|---|---| 
| 参数| 指示字符串参数传递给为流程-是。 如果需要您可以通过多个参数将它们放在该字符串中。| 
| 路径| 该过程可执行文件路径。 如果此可执行文件 （不是完全限定的路径），DSC 资源的文件名将搜索**Path**环境变量 (`$env:Path`) 以查找可执行文件。 如果此属性的值的完全限定的路径，DSC 将不使用的**Path**环境变量以找到文件，，如果不存在该路径将引发错误。 不允许使用相对路径。| 
| 凭据| 指示过程开始的凭据。| 
| 确保| 指明是否存在该过程。 设置为"演示"，以确保该过程存在该属性。 否则，将其设置为"无"。 默认为"演示"。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法如下 ' 取决于 ="[资源类型] 资源名称"。| 
| StandardErrorPath| 指示目录路径以编写标准误差。 将覆盖任何现有文件。| 
| StandardInputPath| 指示标准输入的位置。| 
| StandardOutputPath| 指示编写标准输出的位置。 将覆盖任何现有文件。| 
| WorkingDirectory| 指示将用作过程的当前工作目录的位置。| 

