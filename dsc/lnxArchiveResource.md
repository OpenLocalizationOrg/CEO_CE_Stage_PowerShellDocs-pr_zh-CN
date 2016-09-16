---
title: "DSC 为 Linux nxArchive 资源的"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 2edbc1d11dfc7c84369430688a8b0d773277e864
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 为 Linux nxArchive 资源的

**NxArchive**资源 PowerShell 需要状态配置 (DSC) 中提供了一种机制解压缩在特定的路径上 Linux 节点的存档 （.tar、.zip） 文件。

## 语法

```
nxArchive <string> #ResourceName
{
    SourcePath = <string>
    DestinationPath = <string>
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Force = <bool> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## 属性

|  属性 |  说明 | 
|---|---|
| 源路径| 指定存档文件的源路径。 这是.tar，.zip，或。.tar.gz 文件。 | 
| DestinationPath| 指定要确保提取存档内容的位置。| 
| 校验和| 定义要在确定是否已更新源存档时使用的类型。 值为:"ctime"，"mtime"，或"md5"。 默认值为"md5"。| 
| 强制| 某些文件操作 （如覆盖的文件或删除目录不为空） 将导致一个错误。 使用**强制**属性会覆盖这样的错误。 默认值为**$false**。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
| 确保| 确定是否检查在**目标**是否存在存档的内容。 设置为"演示"，以确保内容存在该属性。 将其设置为"无"以确保它们不存在。 默认值为"演示"。| 

## 示例

以下示例显示如何使用**nxArchive**资源以确保存档文件的内容称为`website.tar`存在并且在给定的目标位置提取。

```
Import-DSCResource -Module nx 

nxFile SyncArchiveFromWeb
{
   Ensure = "Present"
   SourcePath = “http://release.contoso.com/releases/website.tar”
   DestinationPath = "/usr/release/staging/website.tar"
   Type = "File"
   Checksum = “mtime”
}

nxArchive SyncWebDir
{
   SourcePath = “/usr/release/staging/website.tar”
   DestinationPath = “/usr/local/apache2/htdocs/”
   Force = $false
   DependsOn = "[nxFile]SyncArchiveFromWeb"
} 
```

