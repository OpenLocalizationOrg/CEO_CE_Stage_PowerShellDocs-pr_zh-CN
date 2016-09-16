---
title: "控制台改进 WMF 5.1 （预览）"
ms.date: 2016-07-13
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 574fec8e1f4948021988d8489532d7325277fed6
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 控制台改进 WMF 5.1 （预览）#

## PowerShell 控制台改进

以下进行了更改到 powershell.exe WMF 5.1 中以改进控制台体验︰

###VT100 支持

Windows 10 添加[VT100 转义序列](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx)的支持。
PowerShell 计算表格宽度时，将忽略某些 VT100 格式转义序列。

PowerShell 也格式代码来确定是否支持 VT100 中添加一个新的 API，可使用。 例如︰

```
if ($host.UI.SupportsVirtualTerminal)
{
    $esc = [char]0x1b
    "A yellow ${esc}[93mhello${esc}[0m"
}
else
{
    "A default hello"
}
```
下面是可以用于突出显示一个完整[的示例](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7)中选择字符串的匹配项。
将示例保存在一个名为文件`MatchInfo.format.ps1xml`，然后使用它，在您的配置文件或其他位置，请运行`Update-FormatData -Prepend MatchInfo.format.ps1xml`。

请注意，VT100 转义序列是仅支持开始与 Windows 10 周年纪念日的更新。不支持早期系统上。   

### 在 PSReadline Vi 模式支持

[PSReadline](https://github.com/lzybkr/PSReadLine)增加 vi 模式的支持。 若要使用 vi 模式，请运行`Set-PSReadline -EditMode vi`。

### 使用交互式输入重定向标准输入 

在早期版本中，开始使用 PowerShell`powershell -File -`时需要标准输入已重定向，并且您希望以交互方式输入命令。

与 WMF 5.1，这很难发现不再需要选项。 您可以开始 PowerShell 没有任何选项，例如`powershell`。

请注意，PSReadline 当前不支持重定向标准输入，和的重定向标准输入使用内置的命令行编辑体验非常有限，例如，箭头键不起作用。 在未来版本中提供的 PSReadline 应解决此问题。   
