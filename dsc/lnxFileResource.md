---
title: "Linux nxFile 资源的 DSC"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 2ba44df5dd6c91371cbbfe95d48184a4ff4a7738
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Linux nxFile 资源的 DSC

**NxFile**资源中 PowerShell 需要状态配置 (DSC) 提供机制来管理文件和 Linux 节点上的目录。

## 语法

```
nxFile <string> #ResourceName
{
    DestinationPath = <string>
    [ SourcePath = <string> ]
    [ Ensure = <string> { Absent | Present }  ]
    [ Type = <string> { directory | file | link } ]
    [ Contents = <string> ]
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Recurse = <bool> ]
    [ Force = <bool> ]
    [ Links = <string> { follow | manage } ]
    [ Group = <string> ]
    [ Mode = <string> ]
    [ Owner = <string> ]
    [ DependsOn = <string[]> ]

}
```

## 属性

|  属性 |  说明 | 
|---|---|
| DestinationPath| 指定要确保文件或目录状态的位置。| 
| 源路径| 指定要从其中复制资源文件或文件夹的路径。 此路径可能本地路径，或`http/https/ftp`URL。 远程`http/https/ftp`文件**类型**属性的值时，仅支持 Url。| 
| 确保| 确定是否要检查是否存在的文件。 设置为"演示"，以确保文件存在该属性。 将其设置为"无"以确保文件不存在。 默认值为"演示"。| 
| 类型| 指定要配置的资源的目录或文件。 设置此属性为"目录"，以指示资源是一个目录。 将其设置为"文件"，表明该资源文件。 默认值为"文件"| 
| 内容| 指定一个文件，如特定字符串的内容。| 
| 校验和| 定义用于确定两个文件都是相同的类型。 如果未指定**校验和**，只有文件或目录名称用于比较。 值为:"ctime"，"mtime"，或"md5"。| 
| 递归| 指示是否包含子目录。 此属性设置为**$true**指示您希望子目录要包括在内。 默认情况下**$false**。 **注意︰**在**类型**属性设置为目录时，此属性才有效。| 
| 强制| 某些文件操作 （如覆盖的文件或删除目录不为空） 将导致一个错误。 使用**强制**属性会覆盖这样的错误。 默认值为**$false**。| 
| 链接| 指定所需的符号链接的行为。 设置此属性"关注"按照符号链接和操作链接目标 （例如。 复制文件，而不是链接）。 设置此属性，以"管理"行事链接 （例如。 复制链接本身）。 设置此属性，以"忽略"忽略符号链接。| 
| 组| 要拥有的文件或目录的**组**的名称。| 
| 模式| 指定所需的权限的资源，以八进制数或符号表示法。 （例如，777 或 rwxrwxrwx）。 如果使用的符号表示法，不提供指示目录或文件的第一个字符。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 其他信息


Linux 和 Windows 请文本文件中使用不同换行符，默认情况下，并使用__nxFile__配置 Linux 计算机上的某些文件时，这可能会导致意外的结果。 有多种方法来避免意外的换行符引起的问题时管理 Linux 文件的内容︰

步骤 1︰ 将文件复制从远程源 （http、 https 或 ftp）︰ 使用所需的内容，创建 Linux 上的文件和阶段它可访问的网站或 ftp 服务器上将配置的节点。 与 web __nxFile__资源中定义__源路径__属性或 ftp 到的文件的 URL。

```
Import-DSCResource -Module nx
Node $Node
{
nxFile resolvConf
{
    SourcePath = "http://10.185.85.11/conf/resolv.conf"
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    
}
        
}
```


步骤 2︰ 将__$OFS__属性设置为使用 Linux 换行字符后阅读中[获取内容](https://technet.microsoft.com/en-us/library/hh849787.aspx)的 PowerShell 脚本文件内容。


```
Import-DSCResource -Module nx
Node $Node
{
$OFS = "`n"
$Contents = Get-Content C:\temp\resolv.conf

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    Contents = "$Contents"
}

}
```


步骤 3︰ 使用 PowerShell 函数 Windows 换行符替换 Linux 换行符。

```
Function LinuxString($inputStr){
    $outputStr = $inputStr.Replace("`r`n","`n")
    $ouputStr += "`n"
    Return $outputStr
}

Import-DSCResource -Module nx
Node $Node
{

$Contents = @'
search contoso.com
domain contoso.com
nameserver 10.185.85.11
'@

$Contents = LinuxString $Contents

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    Contents = $Contents
    
}
}
```

## 示例

下面的示例确保目录`/opt/mydir`存在，并且文件指定内容存在此目录。

```
Import-DSCResource -Module nx 

Node $node {
nxFile DirectoryExample
{
   Ensure = "Present"
   DestinationPath = "/opt/mydir"
   Type = "Directory"
}

nxFile FileExample
{
    Ensure = "Present"
    Destinationpath = "/opt/mydir/myfile"
    Contents=@"
#!/bin/bash`necho "hello world"`n
"@ 
    Mode = “755”
    DependsOn = "[nxFile]DirectoryExample"
} 
}
```

