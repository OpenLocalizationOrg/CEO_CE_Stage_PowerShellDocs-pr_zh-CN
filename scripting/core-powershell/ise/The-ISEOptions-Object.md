---
title: "ISEOptions 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 75e2a76f-f3d1-490b-ad5d-e3829946aabb
ms.openlocfilehash: 7f9b0871d778f901afe7c6e5c0ef6b1059cc6380
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISEOptions 对象
  **ISEOptions**对象表示用于 Windows PowerShell ISE 的各种设置。 它是**Microsoft.PowerShell.Host.ISE.ISEOptions**类的实例。

 **ISEOptions**对象提供下列方法和属性。

 **方法**

-   [RestoreDefaultConsoleTokenColors()](#rdctc)

-   [RestoreDefaults()](#rd)

-   [RestoreDefaultTokenColors()](#rdtc)

-   [RestoreDefaultXmlTokenColors()](#rdxtc)

 **属性**

-   [AutoSaveMinuteInterval](#asmi)

-   [CommandPaneBackgroundColor](#cpbc)

-   [CommandPaneUp](#cpu)

-   [ConsolePaneBackgroundColor](#conpbc)

-   [ConsolePaneForegroundColor](#conpfc)

-   [ConsolePaneTextBackgroundColor](#conptbc)

-   [ConsoleTokenColors](#contc)

-   [DebugBackgroundColor](#dbc)

-   [DebugForegroundColor](#dfc)

-   [DefaultOptions](#do)

-   [ErrorBackgroundColor](#ebc)

-   [ErrorForegroundColor](#efc)

-   [字体名称](#fn)

-   [字号](#fs)

-   [IntellisenseTimeoutInSeconds](#itis)

-   [MruCount](#mc)

-   [OutputPaneBackgroundColor](#opbc)

-   [OutputPaneTextForegroundColor](#optfc)

-   [OutputPaneTextBackgroundColor](#optbc)

-   [ScriptPaneBackgroundColor](#spbc)

-   [ScriptPaneForegroundColor](#spfc)

-   [SelectedScriptPaneState](#ssps)

-   [ShowDefaultSnippets](#sds)

-   [ShowIntellisenseInConsolePane](#siicp)

-   [ShowIntellisenseInScriptPane](#siisp)

-   [ShowLineNumbers](#sln)

-   [ShowOutlining](#so)

-   [ShowToolBar](#stb)

-   [ShowWarningBeforeSavingOnRun](#swbsor)

-   [ShowWarningForDuplicateFiles](#swfdf)

-   [TokenColors](#tc)

-   [UseEnterToSelectInConsolePaneIntellisense](#uetsicpi)

-   [UseEnterToSelectInScriptPaneIntellisense](#uetsispi)

-   [UseLocalHelp](#ulh)

-   [VerboseBackgroundColor](#vbc)

-   [VerboseForegroundColor](#vfc)

-   [WarningBackgroundColor](#wbc)

-   [WarningForegroundColor](#wfc)

-   [XmlTokenColors](#xtc)

-   [缩放](#z)

## 方法

###  <a name="rdctc"></a> RestoreDefaultConsoleTokenColors\(\)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 恢复默认值控制台窗格中的标记颜色。

```
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = "red"
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

###  <a name="rd"></a> RestoreDefaults\(\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 恢复控制台窗格中的所有选项设置默认值。 它还重置的各种提供标准的复选框，以防止被再次显示邮件的警告消息的行为。

```
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = "orange"
$psISE.Options.RestoreDefaults()
```

###  <a name="rdtc"></a> RestoreDefaultTokenColors\(\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 恢复默认值脚本窗格中的标记颜色。

```
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"]="red"
$psISE.Options.RestoreDefaultTokenColors()
```

###  <a name="rdxtc"></a> RestoreDefaultXmlTokenColors\(\)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 恢复 Windows PowerShell ISE 中显示的 XML 元素的令牌颜色的默认值。 请参阅[XmlTokenColors](#xtc)。

```
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"]="red"
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## 属性

###  <a name="asmi"></a> AutoSaveMinuteInterval
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定的 Windows PowerShell ISE 通过文件自动保存操作之间的分钟数。 默认值为 2 分钟。 值为整数。

```
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

###  <a name="cpbc"></a> CommandPaneBackgroundColor
  此功能不含在 Windows PowerShell ISE 2.0 中，但已删除或重命名的 ISE 更高版本中。  更高版本，请参阅[ConsolePaneBackgroundColor](#conpbc)。

 指定命令窗格中的背景色。 它是**System.Windows.Media.Color**类的实例。

```
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = "orange"
```

###  <a name="cpu"></a> CommandPaneUp
  此功能不含在 Windows PowerShell ISE 2.0 中，但已删除或重命名的 ISE 更高版本中。

 指定是否命令窗格中位于输出窗格中的上方。

```
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true

```

###  <a name="conpbc"></a> ConsolePaneBackgroundColor
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定控制台窗格中的背景色。 它是**System.Windows.Media.Color**类的实例。

```
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = "red"
```

###  <a name="conpfc"></a> ConsolePaneForegroundColor
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定控制台窗格中的文本的前景色。

```
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = "yellow"

```

###  <a name="conptbc"></a> ConsolePaneTextBackgroundColor
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定控制台窗格中的文本的背景色。

```
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = "pink"
```

###  <a name="contc"></a> ConsoleTokenColors
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 在 Windows PowerShell ISE 控制台窗格中指定智能感知令牌的颜色。 此属性是包含标记类型和颜色控制台窗格中的名称/值对的词典对象。 若要更改的脚本窗格中的智能感知标记颜色，请参阅[TokenColors](#tc)。 重置为默认值的颜色，请参阅[RestoreDefaultConsoleTokenColors()](#rdctc)。 令牌颜色可以设置为以下︰ 属性、 命令、 CommandArgument、 与此、 批注、 GroupEnd、 GroupStart、 关键字、 行继续、 LoopLabel、 成员、 换行符、 数字、 运算符、 位置、 StatementSeparator、 字符串、 类型、 未知、 变量。

```
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = "magenta"

```

###  <a name="dbc"></a> DebugBackgroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定在控制台窗格中显示的调试文本的背景色。 它是**System.Windows.Media.Color**类的实例。

```
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor ='#0000FF'
```

###  <a name="dfc"></a> DebugForegroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定控制台窗格中显示的调试文本的前景色。 它是**System.Windows.Media.Color**类的实例。

```
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor ="yellow"
```

###  <a name="do"></a> DefaultOptions
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定用于重置方法时要使用的默认值的属性集。

```
# Displays the name of the default options. This example is from ISE 4.0.
$psISE.Options.DefaultOptions

SelectedScriptPaneState                   : Top
ShowDefaultSnippets                       : True
ShowToolBar                               : True
ShowOutlining                             : True
ShowLineNumbers                           : True
TokenColors                               : {[Attribute, #FF00BFFF], [Command, #FF0000FF], [CommandArgument, #FF8A2BE2], [CommandParameter, #FF000080]...}
ConsoleTokenColors                        : {[Attribute, #FFB0C4DE], [Command, #FFE0FFFF], [CommandArgument, #FFEE82EE], [CommandParameter, #FFFFE4B5]...}
XmlTokenColors                            : {[Comment, #FF006400], [CommentDelimiter, #FF008000], [ElementName, #FF8B0000], [MarkupExtension, #FFFF8C00]...}
DefaultOptions                            : Microsoft.PowerShell.Host.ISE.ISEOptions
FontSize                                  : 9
Zoom                                      : 100
FontName                                  : Lucida Console
ErrorForegroundColor                      : #FFFF0000
ErrorBackgroundColor                      : #00FFFFFF
WarningForegroundColor                    : #FFFF8C00
WarningBackgroundColor                    : #00FFFFFF
VerboseForegroundColor                    : #FF00FFFF
VerboseBackgroundColor                    : #00FFFFFF
DebugForegroundColor                      : #FF00FFFF
DebugBackgroundColor                      : #00FFFFFF
ConsolePaneBackgroundColor                : #FF012456
ConsolePaneTextBackgroundColor            : #FF012456
ConsolePaneForegroundColor                : #FFF5F5F5
ScriptPaneBackgroundColor                 : #FFFFFFFF
ScriptPaneForegroundColor                 : #FF000000
ShowWarningForDuplicateFiles              : True
ShowWarningBeforeSavingOnRun              : True
UseLocalHelp                              : True
AutoSaveMinuteInterval                    : 2
MruCount                                  : 10
ShowIntellisenseInConsolePane             : True
ShowIntellisenseInScriptPane              : True
UseEnterToSelectInConsolePaneIntellisense : True
UseEnterToSelectInScriptPaneIntellisense  : True
IntellisenseTimeoutInSeconds              : 3

```

###  <a name="ebc"></a> ErrorBackgroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定在控制台窗格中出现的错误文本的背景色。 它是**System.Windows.Media.Color**类的实例。

```
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor="black"
```

###  <a name="efc"></a> ErrorForegroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定控制台窗格中显示的错误文本的前景色。 它是**System.Windows.Media.Color**类的实例。

```
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor ="green"
```

###  <a name="fn"></a> 字体名称
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 在脚本窗格和控制台窗格中使用当前指定字体名称。

```
# Changes the font used in both panes.
$psISE.Options.FontName = "courier new"
```

###  <a name="fs"></a> 字号
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 为整数，指定字体大小。 在脚本窗格中，命令窗格中，输出窗格中使用。 值的有效范围是 8 到 32。

```
# Changes the font size in all panes.
$psISE.Options.FontSize = 20

```

###  <a name="itis"></a> IntellisenseTimeoutInSeconds
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定智能感知用于尝试解决当前键入的文本的秒的数。 此秒数之后, IntelliSense 超时，并使您可以继续键入。 默认值为 3 秒。 值为整数。

```
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

###  <a name="mc"></a> MruCount
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定的 Windows PowerShell ISE 跟踪，并在**文件打开**菜单的底部显示最近打开的文件数。 默认值为 10。 值为整数。

```
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

###  <a name="opbc"></a> OutputPaneBackgroundColor
  此功能不含在 Windows PowerShell ISE 2.0 中，但已删除或重命名的 ISE 更高版本中。  更高版本，请参阅[ConsolePaneBackgroundColor](#conpbc)。

 读取/写入属性来获取或设置输出窗格本身的背景色。 它是**System.Windows.Media.Color**类的实例。

```
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = "gold"

```

###  <a name="optfc"></a> OutputPaneTextForegroundColor
  此功能不含在 Windows PowerShell ISE 2.0 中，但已删除或重命名的 ISE 更高版本中。  更高版本，请参阅[ConsolePaneForegroundColor](#conpfc)。

 更改 Windows PowerShell ISE 2.0 中的结果窗格中的文本的前景色读/写属性。

```
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = "blue"

```

###  <a name="optbc"></a> OutputPaneTextBackgroundColor
  此功能不含在 Windows PowerShell ISE 2.0 中，但已删除或重命名的 ISE 更高版本中。  更高版本，请参阅[ConsolePaneTextBackgroundColor](#conptbc)。

 更改结果窗格中的文本的背景色的读/写属性。

```
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = "pink"
```

###  <a name="spbc"></a> ScriptPaneBackgroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 读取/写入属性来获取或设置文件的背景色。 它是**System.Windows.Media.Color**类的实例。

```

# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = ”yellow”

```

###  <a name="spfc"></a> ScriptPaneForegroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 读取/写入属性来获取或设置非脚本文件的前景色脚本窗格中。
若要设置脚本文件的前景色，使用[TokenColors](The-ISEOptions-Object.md#tc)属性。

```
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = "green"

```

###  <a name="ssps"></a> SelectedScriptPaneState
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 读取/写入属性来获取或设置显示在脚本窗格的位置。 字符串可以使用"最大化"、"顶部""右侧"。

```
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = "Top"
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = "Right"
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = "Maximized"

```

###  <a name="sds"></a> ShowDefaultSnippets
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定是否段的**CTRL + J**列表包含 Windows PowerShell 中包括的初学者集。 仅限用户定义的代码段设置为**$false**时， **CTRL + J**列表中显示。 默认值为**$true**。

```
# Hide the default snippets from the CTRL+J list.
$psISe.Options.ShowDefaultSnippets = $false
```

###  <a name="siicp"></a> ShowIntellisenseInConsolePane
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定是否 IntelliSense 提供语法、 参数和值的控制台窗格中的建议。 默认值为**$true**。

```
# Turn off IntelliSense in the console pane.
$psISe.Options.ShowIntellisenseInConsolePane = $false
```

###  <a name="siisp"></a> ShowIntellisenseInScriptPane
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定是否 IntelliSense 提供语法、 参数和脚本窗格中的值建议。 默认值为**$true**。

```
# Turn off IntelliSense in the Script pane.
$psISe.Options.ShowIntellisenseInScriptPane = $false
```

###  <a name="sln"></a> ShowLineNumbers
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定脚本窗格中是否显示在左边距中的行号。 默认值为**$true**。

```
# Turn off line numbers in the Script pane.
$psISe.Options.ShowLineNumbers = $false
```

###  <a name="so"></a> ShowOutlining
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定脚本窗格中是否显示在左边距旁边的代码段可展开和折叠括起来。 它们显示时，您可以单击减号\(-\)要折叠它，或单击加号的文本块旁边的图标\(+\)图标以展开的文本块。 默认值为**$true**。

```
# Turn off outlining in the Script pane.
$psISe.Options.ShowOutlining = $false
```

###  <a name="stb"></a> ShowToolBar
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定是否 ISE 工具栏显示在 Windows PowerShell ISE 窗口的顶部。 默认值为**$true**。

```
# Show the toolbar.
$psISe.Options.ShowToolBar = $true
```

###  <a name="swbsor"></a> ShowWarningBeforeSavingOnRun
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定之前运行它时自动保存脚本时是否显示一条警告消息。 默认值为**$true**。

```
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun=$true

```

###  <a name="swfdf"></a> ShowWarningForDuplicateFiles
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定不同 PowerShell 选项卡中打开同一个文件时，是否出现一条警告消息。 如果设置为**$true**，以在多个选项卡中打开同一个文件会显示此消息:"是在另一个 Windows PowerShell 选项卡中打开此文件的副本。 对此文件所做的更改将影响所有打开的副本。" 默认值为**$true**。

```
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true

```

###  <a name="tc"></a> TokenColors
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定 Windows PowerShell ISE 脚本窗格中的智能感知标记的颜色。 此属性是包含标记类型和颜色脚本窗格中的名称/值对的词典对象。 若要更改的控制台窗格中的智能感知标记颜色，请参阅[ConsoleTokenColors](#contc)。 重置为默认值的颜色，请参阅[RestoreDefaultTokenColors()](#rdtc)。 令牌颜色可以设置为以下︰ 属性、 命令、 CommandArgument、 与此、 批注、 GroupEnd、 GroupStart、 关键字、 行继续、 LoopLabel、 成员、 换行符、 数字、 运算符、 位置、 StatementSeparator、 字符串、 类型、 未知、 变量。

```
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"

```

###  <a name="uetsicpi"></a> UseEnterToSelectInConsolePaneIntellisense
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定是否可以使用 Enter 键以选择智能感知提供控制台窗格中的选项。 默认值为**$true**。

```
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense=$false

```

###  <a name="uetsispi"></a> UseEnterToSelectInScriptPaneIntellisense
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定是否可以使用 Enter 键以在脚本窗格中选择一个提供 IntelliSense 选项。 默认值为**$true**。

```
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense=$true

```

###  <a name="ulh"></a> UseLocalHelp
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定本地安装的帮助或联机 TechNet 库帮助显示时将光标放在关键字中按 F1。 如果设置为**$true**，然后弹出窗口显示内容从本地安装的帮助。 您可以通过运行安装的帮助文件`Update-Help`命令。 如果设置为**$false**，然后浏览器中打开到 TechNet 库中的页面。

```
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp=$false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp=$true

```

###  <a name="vbc"></a> VerboseBackgroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定控制台窗格中显示的详细文本的背景色。 它是**System.Windows.Media.Color**对象。

```
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

###  <a name="vfc"></a> VerboseForegroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定控制台窗格中显示的详细文本的前景色。 它是**System.Windows.Media.Color**对象。

```
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor =”yellow”
```

###  <a name="wbc"></a> WarningBackgroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 指定在控制台窗格中显示的警告文本的背景色。 它是**System.Windows.Media.Color**对象。

```
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor ='#0000FF'
```

###  <a name="wfc"></a> WarningForegroundColor
  支持的 Windows PowerShell ISE 2.0 和更高版本。

 在输出窗格中，指定警告显示的文本的前景色。 它是**System.Windows.Media.Color**对象。

```
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor =”yellow”
```

###  <a name="xtc"></a> XmlTokenColors
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定包含标记类型和显示在 Windows PowerShell ISE 的 XML 内容的颜色的名称/值对的词典对象。 令牌颜色可以设置为以下︰ 属性、 命令、 CommandArgument、 与此、 批注、 GroupEnd、 GroupStart、 关键字、 行继续、 LoopLabel、 成员、 换行符、 数字、 运算符、 位置、 StatementSeparator、 字符串、 类型、 未知、 变量。 请参阅[RestoreDefaultXmlTokenColors()](#rdxtc)。

```
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = "green"
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = "magenta"

```

###  <a name="z"></a> 缩放
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指定控制台和脚本窗格中文字的相对大小。 默认值为 100。 较小的值导致 Windows PowerShell ISE，以较大的数会导致显示较大文本时，出现小的文本。 值为整数，范围从 20 到 400。

```
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## 另请参阅
 [Windows PowerShell ISE 脚本对象模型](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md)

