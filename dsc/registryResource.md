---
title: "DSC 注册表资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 4550553f31ce20fb7535655e631c913c651751e4
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 注册表资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

**注册表**资源在 Windows PowerShell 需要状态配置 (DSC) 提供了一种机制来管理注册表项和值的目标节点。

## 语法

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## 属性
|  属性  |  说明   | 
|---|---| 
| 键| 指示您希望确保特定状态的注册表项的路径。 此路径必须包括配置单元。| 
| 数值名称| 指示注册表值的名称。| 
| 确保| 指明是否存在键和值。 若要确保他们执行，请设置该属性为"演示"。 要确保它们不存在，请将属性设置为"无"。 默认值为"演示"。| 
| 强制| 如果存在指定的注册表项，__强制__将覆盖它用新值。| 
| 十六进制| 指示是否将表示为十六进制数格式的数据。 如果指定，DWORD/四字值数据显示为十六进制数格式。 对于其他类型无效。 默认值为__$false__。| 
| 取决于| 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是__资源名称__和其类型是__资源类型__，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 
| ValueData| 注册表值的数据。| 
| 值类型| 表示值的类型。 支持的类型包括︰ 
<ul><li>字符串 (REG_SZ)</li>


<li>二进制数 （注册二进制数）</li>


<li>Dword 32 位 (REG_DWORD)</li>


<li>四字 64 位 (REG_QWORD)</li>


<li>多字符串 (REG_MULTI_SZ)</li>


<li>可扩展字符串 (REG_EXPAND_SZ)</li></ul>

## 示例
```powershell
Registry RegistryExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Key = "HKEY_LOCAL_MACHINE\SOFTWARE\ExampleKey"
    ValueName = "TestValue"
    ValueData = "TestData"
}
```

