---
title: "Bug 修复在 WMF 5.1 （预览）"
ms.date: 2016-07-13
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: d851b0cc9300b9afb027fe9ceb122f246a17e418
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 错误修复在 WMF 5.1 （预览）#

## 修复错误 ##

WMF 5.1 修复以下显著错误︰

### 完全尊重模块自动发现 `$env:PSModulePath` ###

在 WMF 3 引入了模块自动发现 （而显式导入模块调用命令时不自动加载模块）。 中的命令时引入，检查 PowerShell`$PSHome\Modules`之前使用`$env:PSModulePath`。

WMF 5.1 更改此行为接受`$env:PSModulePath`完全。 这允许用户编写模块定义了提供的 PowerShell 命令 (如`Get-ChildItem`) 不自动加载和正确覆盖内置命令。

### 文件没有到较长的硬编码的重定向 `-Encoding Unicode` ###

在所有以前版本中的 PowerShell，它不可能控制文件重定向运算符，例如使用的文件编码`Get-ChildItem > out.txt`因为 PowerShell 添加`-Encoding Unicode`。

现在，从 WMF 5.1 开始，您可以更改文件的编码重定向通过设置`$PSDefaultParameterValues`:

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### 固定回归中访问的成员 `System.Reflection.TypeInfo` ###

WMF 5.0 中引入回归中断访问的成员， `System.Reflection.RuntimeType`，例如`[int].ImplementedInterfaces`。
WMF 5.1 中已修复此错误。


### COM 对象与修复某些问题 ###

WMF 5.0 引入新 COM 活页夹调用方法 COM 对象和访问 COM 对象的属性。 此新活页夹显著提高了性能，但还引入了其 WMF 5.1 修复一些错误。

#### 参数转换未始终执行正确 ####

在下面的示例︰

```
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

SendKeys 方法需要一个字符串，但 PowerShell 未转换字符为一个字符串，推迟转换为 IDispatch::Invoke，使用 VariantChangeType 进行转换，这将在本示例中导致发送"1"、"7"和"3"，而不是预期的 Volume.Mute 键的键。

#### 可枚举 COM 对象不始终正确处理 ####

PowerShell 通常枚举大多数可枚举对象，但在 WMF 5.0 引入回归无法实现的 COM 对象的枚举。  例如︰

```
function Get-COMDictionary
{
    $d = New-Object -ComObject Scripting.Dictionary
    $d.Add('a', 2)
    $d.Add('b', 2)
    return $d
}

$x = Get-COMDictionary
```

在上面的示例中，WMF 5.0 不正确，而不是枚举键/值对管道写 Scripting.Dictionary。

此更改还可以解决[问题 1752224 在连接](https://connect.microsoft.com/PowerShell/feedback/details/1752224)

### `[ordered]` 不允许内部类 ###

WMF 5.0 引入具有验证类型串联在类中使用的类。  
`[ordered]` 键入文本的外观，但不是真正的.NET 类型。 WMF 5.0 错误报告错误的`[ordered]`类中︰

```
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```


### 有关主题的多个版本的帮助不起作用 ###

之前 WMF 5.1，如果您有多个版本的安装的模块，则它们全部共享帮助主题中，例如，about_PSReadline，`help about_PSReadline`将返回多个与无明显的方法若要查看的真实的帮助主题。

WMF 5.1 通过返回的主题的最新版本的帮助解决此问题。

`Get-Help` 不提供指定所需的帮助哪个版本的方法。 若要解决此问题，导航到模块目录和查看直接与您最喜爱的编辑器等工具的帮助。 
