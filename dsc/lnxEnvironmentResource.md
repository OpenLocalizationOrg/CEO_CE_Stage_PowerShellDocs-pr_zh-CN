---
title: "DSC 为 Linux nxEnvironment 资源的"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 0a7ab24ff278defd7fc0a80f1dbd45bfa0e16427
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 为 Linux nxEnvironment 资源的

**NxEnvironment**资源中 PowerShell 需要状态配置 (DSC) 提供机制来管理系统环境变量 Linux 节点上。

## 语法

```
nxEnvironment <string> #ResourceName
{
    Name = <string>
    [ Value = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Path = <bool> }
    [ DependsOn = <string[]> ]

}
```

## 属性

|  属性 |  说明 | 
|---|---|
| 名称| 指示您希望确保特定状态的环境变量的名称。| 
| 值| 要分配给环境变量的值。| 
| 确保| 确定是否要检查是否存在变量。 设置为"演示"，以确保该变量存在该属性。 将其设置为"无"以确保不存在的变量。 默认值为"演示"。| 
| 路径| 定义要配置的环境变量。 如果变量是**路径**变量中; 此属性设置为**$true**否则，将其设置为**$false**。 默认情况下**$false**。 如果正在配置变量是**Path**变量，通过**值**属性提供的值将追加到现有值。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 其他信息

* 如果**路径**是不存在或设置为**$false**，在中管理环境变量`/etc/environment`。 您的程序或脚本可能需要与源配置`/etc/environment`文件访问托管的环境变量。
* 如果**路径**设置为**$true**，在文件管理环境变量`/etc/profile.d/DSCenvironment.sh`。 如果不存在，则将创建此文件。 如果**确保**设置为"不存在"并设置**路径** **$true**，到现有环境变量将仅从`/etc/profile.d/DSCenvironment.sh`而不是从其他文件。

## 示例

下面的示例显示如何使用**nxEnvironment**资源以确保**TestEnvironmentVariable**存在并且具有值"测试值"。 如果不存在**TestEnvironmentVariable** ，则将创建它。

```
Import-DSCResource -Module nx 


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```


