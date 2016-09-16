---
title: "DSC 文件资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: ba625f5130e806b3b8e14a0f6ed91fd5a1aabc54
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 文件资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

文件资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来管理文件和文件夹上的目标节点。

>**注意︰**如果**MatchSource**属性设置为**$false** （这是默认值），复制内容缓存配置应用第一次。 
>配置的后续应用程序不会检查更新的文件和/或指定**源路径**的路径中的文件夹。 如果您想要检查的更新文件和/或**源路径**中的文件夹，每次配置应用，则设置为**$true** **MatchSource** 。 

## 语法
```
File [string] #ResourceName
{
    DestinationPath = [string]
    [ Attributes = [string[]] { Archive | Hidden | ReadOnly | System }]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ Contents = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present } ] 
    [ Force = [bool] ]
    [ Recurse = [bool] ]
    [ DependsOn = [string[]] ]
    [ SourcePath = [string] ]
    [ Type = [string] { Directory | File } ] 
    [ MatchSource = [bool] ]
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| DestinationPath| 指示您希望以确保文件或目录的状态的位置。| 
| 属性| 指定目标的文件或目录属性所需的状态。| 
| 校验和| 指明用于确定两个文件都是相同的校验和类型。 如果未指定__校验和__，只有文件或目录名称用于比较。 有效的值包括︰ sha-1、 sha-256、 sha-512、 createdDate、 modifiedDate。| 
| 内容| 指定一个文件，如特定字符串的内容。| 
| 凭据| 如果需要此类访问权限，则，表示访问资源，如源文件，需要的凭据。| 
| 确保| 指明是否存在文件或目录。 设置为"无"以确保文件或目录不存在该属性。 将其设置为"演示"，以确保文件或目录存在。 默认为"演示"。| 
| 强制| 某些文件操作 （如覆盖的文件或删除目录不为空） 将导致一个错误。 使用强制属性会覆盖这样的错误。 默认值为__$false__。| 
| 递归| 指示是否包含子目录。 此属性设置为__$true__指示您希望子目录要包括在内。 默认情况下__$false__。 **注意**: 类型属性设置为目录时，此属性才有效。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
| 源路径| 指示要从中复制资源文件或文件夹的路径。| 
| 类型| 指示正在配置资源是否目录或文件。 设置此属性为"目录"，以指示资源是一个目录。 将其设置为"文件"，以指示资源文件。 默认值为"文件"。| 
| MatchSource| 如果设置为__$false__的默认值，则源 （如文件 A、 B 和 C） 上的任何文件会添加到的目标首次配置应用。 如果新的文件 (D) 添加到源，它将不会添加到的目标，即使以后重新应用配置。 如果值为__$true__，然后应用配置时，每次随后在源 （如在本示例中的文件 D） 上找到的新文件添加到的目标。 默认值为**$false**。| 

## 示例

以下示例显示如何使用文件资源以确保具有路径的目录`C:\Users\Public\Documents\DSCDemo\DemoSource`源计算机 （如"提取"服务器） 也是演示 （以及所有子目录） 上的目标节点。 此外 confirmatory 消息写入日志，完成后，并包括一个语句，以确保文件检查操作的日志记录操作之前运行。

```powershell
Configuration FileResourceDemo
{
    Node "localhost"
    {
        File DirectoryCopy
        {
            Ensure = "Present"  # You can also set Ensure to "Absent"
            Type = "Directory" # Default is "File".
            Recurse = $true # Ensure presence of subdirectories, too
            SourcePath = "C:\Users\Public\Documents\DSCDemo\DemoSource"
            DestinationPath = "C:\Users\Public\Documents\DSCDemo\DemoDestination"    
        }

        Log AfterDirectoryCopy
        {
            # The message below gets written to the Microsoft-Windows-Desired State Configuration/Analytic log
            Message = "Finished running the file resource with ID DirectoryCopy"
            DependsOn = "[File]DirectoryCopy" # This means run "DirectoryCopy" first.
        }
    }
}
```

