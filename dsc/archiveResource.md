---
title: "DSC 存档资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 77398d26f59975469e7c752a8d7f4f8bbbe4f553
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 存档资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

存档资源在 Windows PowerShell 需要状态配置 (DSC) 提供一种机制解压缩存档 (.zip) 文件在特定的路径。

## 语法 
```MOF
Archive [string] #ResourceName
{
    Destination = [string]
    Path = [string]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Validate = [bool] ]
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| 目标| 指定要确保提取存档内容的位置。| 
| 路径| 指定存档文件的源路径。| 
| __校验和__| 定义用于确定两个文件都是相同的类型。 如果未指定__校验和__，只有文件或目录名称用于比较。 有效的值包括︰ sha-1、 sha-256、 sha-512、 createdDate、 modifiedDate，无 （默认）。 如果您指定__校验和__不__验证__，则配置将失败。| 
| 确保| 确定是否检查在__目标__是否存在存档的内容。 将此属性设置为__演示__以确保内容存在。 将其设置为__不存在__以确保它们不存在。 默认值是__演示__。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是资源名称和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
| 验证| 使用校验和属性确定存档是否匹配签名。 如果您指定校验和不验证，则配置将失败。 如果指定无校验和验证时，默认情况下使用 sha-256 校验和。| 
| 强制| 某些文件操作 （如覆盖的文件或删除目录不为空） 将导致一个错误。 使用强制属性会覆盖这样的错误。 默认值为 False。| 

## 示例

下面的示例显示如何使用存档资源以确保存在称为 Test.zip 存档文件的内容，并在给定的目标位置提取。

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
} 
```

