---
title: "PowerShell 引擎增强功能"
author: jasonsh
ms.openlocfilehash: 28e7f31e5970acd1ffb3d62b210380497a3c4992
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# PowerShell 引擎增强功能 #

已针对 PowerShell 5.1 实现核心 PowerShell 引擎的以下改进︰


## 性能 ##

改进了性能，一些重要方面︰

1. 启动
2. 管道到 ForEach 对象和位置对象之类的 cmdlet 大约是 50%更快 

某些示例改进 (resuls 可能会有所不同，具体取决于您是您的硬件): 

| 方案 | 5.0 时间 （毫秒） | 5.1 时间 （毫秒） |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | 900 | 250 |
| 首先以往 PowerShell 运行︰ `powershell -command "Unknown-Command"` | 30000 | 13000 |
| 内置命令分析缓存︰ `powershell -command "Unknown-Command"` | 7000 | 520 |
| <code>1..1000000 &#124; % { }</code> | 1400 | 750 |
  
启动与相关的一次更改可能会影响某些 （不受支持） 方案。 PowerShell 不再读取文件`$pshome\*.ps1xml`-这些文件已转换为 C# 以避免处理 xml 文件的一些文件和 cpu 开销。 文件仍然存在到支持 V2 通过并行，因此如果您更改了该文件的内容，它将没有 v5，仅 V2 任何效果。 请注意，更改这些文件的内容从未受支持的方案。

另一个可见更改是如何 PowerShell 缓存导出命令和系统安装的模块的其他信息。 上一张、 此缓存已存储在目录`$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`。 在 WMF 5.1 缓存是单个文件`$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`。
请参阅[analysis_cache.md]()更多详细信息。

从开始版本 5.1，PowerShell 是这表示不同的功能集和平台兼容性的不同版本中可用。



## 修复错误 ##

以下显著 bug 已修复︰

### 完全尊重模块自动发现 `$env:PSModulePath` ###

在 WMF3 引入了模块自动发现 （而显式导入模块调用命令时不自动加载模块）。 中的命令时引入，检查 PowerShell`$PSHome\Modules`之前使用`$env:PSModulePath`。

WMF5.1 更改此行为接受`$env:PSModulePath`完全。 这允许用户编写模块定义了提供的 PowerShell 命令 (如`Get-ChildItem`) 不自动加载和正确覆盖内置命令。

### 文件没有到较长的硬编码的重定向 `-Encoding Unicode` ###

在所有以前版本中的 PowerShell，它不可能控制文件重定向运算符，例如使用的文件编码`get-childitem > out.txt`因为 PowerShell 添加`-Encoding Unicode`。

现在，从 WMF 5.1 开始，您可以更改文件的编码重定向通过设置`$PSDefaultParameterValues`，例如

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### 固定回归中访问的成员 `System.Reflection.TypeInfo` ###

回归 WMF5 中引入中断访问的成员， `System.Reflection.RuntimeType`，例如`[int].ImplementedInterfaces`。
已在 WMF5.1 修复此错误。


### COM 对象与修复某些问题 ###

WMF5 引入新的 COM 活页夹调用方法 COM 对象和访问 COM 对象的属性。
此新活页夹显著提高了性能，但还引入了一些 bug 的已固定在 WMF5.1。

#### 参数转换未始终执行正确 ####

在下面的示例︰

```
$obj = new-object -com wscript.shell
$obj.SendKeys([char]173)
```

SendKeys 方法需要一个字符串，但 PowerShell 未转换字符为一个字符串，推迟转换为 IDispatch::Invoke，使用 VariantChangeType 进行转换，这将在本示例中导致发送"1"、"7"和"3"，而不是预期的 Volume.Mute 键的键。

#### 可枚举 COM 对象不始终正确处理 ####

PowerShell 通常枚举大多数可枚举对象，但在 WMF5 中引入回归无法实现的 COM 对象的枚举。  例如︰

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

在上面的示例中，WMF5 不当写入 Scripting.Dictionary 渠道，而不是枚举的关键值对。


### `[ordered]` 不允许内部类 ###

WMF5 引入具有验证类型串联在类中使用的类。  `[ordered]` 键入文本的外观，但不是真正的.Net 类型。  WMF5 错误报告错误的`[ordered]`类中︰

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

之前 WMF5.1，如果您有多个版本的安装的模块，则它们全部共享帮助主题中，例如 about_PSReadline，`help about_PSReadline`将返回多个与无明显的方法若要查看的真实的帮助主题。

WMF5.1 通过返回的主题的最新版本的帮助解决此问题。

获取帮助不提供指定所需的帮助哪个的版本的方法，解决方法是定位到模块目录并查看直接与您最喜爱的编辑器等工具的帮助。 
