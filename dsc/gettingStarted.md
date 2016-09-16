---
title: "PowerShell 入门所需的状态配置"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 3a59f76919c0a63f269ca587d358020825412be4
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# PowerShell 入门所需的状态配置 #

本文介绍如何开始创建 PowerShell 需要状态配置文档并将其应用到计算机。 它假定基本熟悉 PowerShell cmdlet、 模块和函数。 


## 创建配置 ##

[**配置**](https://msdn.microsoft.com/en-us/powershell/dsc/configurations)是描述环境的文档。 环境包含"**节点**"，这通常是虚拟或物理计算机。 

配置可以来自各种窗体中。 创建新的配置的最简单方法是创建.ps1 （PowerShell 脚本） 文件。 若要执行此操作，打开您选择的编辑器。 PowerShell ISE 是很好的选择，因为它理解 DSC 本身。 保存为 PS1 下列操作︰

```powershell
configuration MyFirstConfiguration
{
    Import-DscResource -Name WindowsFeature

    Node localhost
    {
        WindowsFeature IIS
        {
            Name = "IIS"

        }
        
    }

}
```
## 配置的组成部分 ##
**配置**是已添加到 PowerShell 4.0 关键字。 表示一种特殊的 PowerShell 函数需要状态配置使用它。 在本示例中，该函数名为 myFirstConfiguration。 

下一行是类似于导入模块导入语句。 它将在以后讨论。

"节点"定义起作用，此配置的计算机名称。 虽然此配置本地编辑，但配置可以问候远程节点，并将其配置。 

节点可以是计算机名称或 IP 地址。 在单个配置文档中，您可以拥有多个节点。 使用[配置数据](https://msdn.microsoft.com/en-us/powershell/dsc/configdata)，您也可以将应用于多个节点的相同配置。 在此例中，则节点是"主机"-意味着本地计算机。 

下一个项目是[**资源**](https://msdn.microsoft.com/en-us/powershell/dsc/resources)。 资源是配置的构建基块。 每个资源是定义实施逻辑的计算机上的单个方面的模块。 您可以通过 PowerShell 中运行**获取 DscResource**来查看您的计算机上的每个资源。 资源必须在本地计算机上，然后才可以使用在**导入 DscResource**位于此配置的第二行与配置导入。 

**制定配置**

如果上面的脚本保存并运行，将不生成任何输出。 这是因为配置只需函数，并且上述脚本已定义的函数，但尚未运行它。 定义函数后，必须调用它︰
```powershell
myFirstConfiguration
```

配置函数执行时，验证配置有效。 应有没有语法错误、 资源应拥有所有必需参数定义，并执行之前应导入的所有资源。

一旦执行配置，它将创建一个文件夹，与包含**配置的名称。MOF 文件**中配置每个节点。 。MOF 文件是一种基于标准的管理格式 PowerShell DSC 用于通过网络通信。

制定配置︰
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration
```
这将创建的 PowerShell 作业会与在配置节点并配置它们。 若要查看作业的输出，请使用-等待。 
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration -Wait
```

