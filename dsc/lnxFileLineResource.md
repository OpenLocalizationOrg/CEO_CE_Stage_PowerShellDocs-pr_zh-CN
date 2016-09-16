---
title: "DSC 为 Linux nxFileLine 资源的"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 9196129e79272d8bee717ef8a5d42fb590760a0f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Linux nxFileLine 资源的 DSC

**NxFileLine**资源 PowerShell 需要状态配置 (DSC) 中提供的机制管理上 Linux 节点的配置文件中的行。

## 语法

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## 属性

|  属性 |  说明 | 
|---|---|
| 文件路径| 管理中的行上的目标节点文件的完整路径。| 
| ContainsLine| 在文件中存在行，以确保。 如果不存在的文件中，将文件附加此行。 **ContainsLine**是必需的但可以将设置为空字符串 (ContainsLine =) 如果不需要。| 
| DoesNotContainPattern| 不应在文件中存在的线条正则表达式模式。 对于任何文件中存在的匹配此正则表达式的行，将文件从删除行。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 示例

此示例演示如何使用**nxFileLine**资源以配置`/etc/sudoers`文件，从而确保用户︰ monuser 配置为不 requiretty。

```
Import-DSCResource -Module nx 

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
} 
```

