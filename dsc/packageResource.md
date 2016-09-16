---
title: "DSC 程序包资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 4540a1b9253e69370156394476e0f5b020b0b547
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 程序包资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

**程序包**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来安装或卸载程序包，如 Windows Installer 和 setup.exe 程序包在目标节点上。

## 语法

```
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ ReturnCode = [UInt32[]] ]
}
```

## 属性
|  属性  |  说明   | 
|---|---| 
| 名称| 指示您希望确保特定状态包的名称。| 
| 路径| 指示包的所在位置的路径。| 
| 产品 Id| 指示唯一标识包的产品 ID。| 
| 参数| 列出将传递到包完全按照提供的参数的字符串。| 
| 凭据| 在远程源提供访问程序包。 此属性不用于安装程序包。 始终在本地系统安装程序包。| 
| 确保| 指明是否已安装程序包。 设置此属性为"缺少"以确保不安装包 （或卸载包，如果已安装）。 将其设置为"演示"（默认值） 以确保已安装程序包。| 
| LogPath| 指示位置以保存日志文件来安装或卸载包的提供商的完整路径。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是取决于 ="[资源类型] 资源名称"。| 
| ReturnCode| 指示预期返回代码。 如果实际返回代码不匹配所需的值在这里，提供配置将返回错误。| 

## 示例

本示例在运行.msi 安装程序位于指定的 path，具有指定的产品 id。

```powershell
Package PackageExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path  = "$Env:SystemDrive\TestFolder\TestProject.msi"
    Name = "TestPackage"
    ProductId = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
} 
```

