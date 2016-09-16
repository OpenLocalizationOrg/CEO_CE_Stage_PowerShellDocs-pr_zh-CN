---
title: "控制台体验的增强功能"
author: jasonsh
ms.openlocfilehash: 60aaaead1dd307f2cbfeb48106e8c642f4b8165d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
>注意︰ 提供建议的描述性标题和简短说明

## PowerShell 控制台增强功能

以下进行了更改到 powershell.exe 以改进控制台体验︰

1. VT100 支持

Windows 10 添加[VT100 转义序列](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx)的支持。
PowerShell 计算表格宽度时，将忽略某些 VT100 格式转义序列。

PowerShell 也格式代码来确定是否支持 VT100 中添加一个新的 api，可使用。  例如︰

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
将示例保存在一个名为文件`MatchInfo.format.ps1xml`，则使用它，在您的配置文件或其他位置，请运行`Update-FormatData -Prepend MatchInfo.format.ps1xml`。

请注意，仅支持 VT100 转义序列开头 Aniversary 更新到 Windows 10 早期系统上不支持。   

2. 在 PSReadline Vi 模式支持

[PSReadline](https://github.com/lzybkr/PSReadLine)增加 vi 模式的支持。 若要使用 vi 模式，请运行`Set-PSReadline -EditMode vi`。

3. 带交互式输入重定向标准输入 

在早期版本中，开始使用 PowerShell`powershell -File -`时需要标准输入已重定向，并且您希望以交互方式输入命令。

通过 WMF 5.1，这很难发现选项不再有必要，您可以开始 powershell 没有任何选项，例如`powershell`。

请注意，PSReadline 不目前不支持重定向标准输入，并编辑使用重定向标准输入体验的内置命令行是非常有限，例如箭头键不起作用。  在未来版本中提供的 PSReadline 应解决此问题。   