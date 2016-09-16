---
title: "PowerShellTab 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: f9818c0ca9c8e415525aad2d577a912562b00ce2
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# PowerShellTab 对象
  **PowerShellTab**对象表示 Windows PowerShell 运行时环境。

## 方法

###  <a name="invoke"></a> 调用\(脚本 \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 在 PowerShell 选项卡中运行给定的脚本。

> [!NOTE]
>  此方法仅适用于其他 PowerShell 选项卡上，不在运行它 PowerShell 选项卡。 它不返回任何对象或值。 如果代码修改任何变量，这些更改保留在依据调用该命令选项卡。

 **脚本**-System.Management.Automation.ScriptBlock 或字符串以运行该脚本块。

```
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psise.PowerShellTabs[1].Invoke({dir})
```

### InvokeSynchronous\(脚本， \[useNewScope\]，等效 \)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 在 PowerShell 选项卡中运行给定的脚本。

> [!NOTE]
>  此方法仅适用于其他 PowerShell 选项卡上，不在运行它 PowerShell 选项卡。 运行该脚本块，并从脚本返回任何值返回到运行环境从中调用命令。 如果命令需要更长时间运行比**millesecondsTimeout**值指定，然后命令处理的异常失败:"操作已超时。"

 **脚本**-System.Management.Automation.ScriptBlock 或字符串以运行该脚本块。

 ** \[useNewScope\] ** -可选 boolean 值，默认为**$true** 
如果设置为**$true**，则新范围创建要在其中运行的命令。 它不修改指定命令 PowerShell 选项卡上的运行时环境。

 **\[等效\]**- **500**到默认的可选整数。
如果在指定的时间内未完成命令，然后命令生成**TimeoutException**处理该邮件"操作已超时。"

```
# create a new PowerShell tab and then switch back to the first
$PSise.PowerShellTabs.Add()
$psISE.PowerShellTabs.SetSelectedPowerShellTab($psISE.PowerShellTabs[0]) 

# Invoke a simple command on the other tab, in its own scope
$psISE.PowerShellTabs[1].InvokeSynchronous('$x=1',$false)
# You can switch to the other tab and type “$x” to see that the value is saved there.

# This example sets a value in the other tab (in a different scope) 
# and returns it through the pipeline to this tab to store in $a
$a=$psISE.PowerShellTabs[1].InvokeSynchronous('$z=3;$z') 
$a

# This example runs a command that takes longer than the allowed timeout value
# and measures how long it runs so that you can see the impact
measure-command {$psISE.PowerShellTabs[1].InvokeSynchronous("sleep 10",$false,5000)}

```

## 属性

###  <a name="AddOnsMenu"></a> AddOnsMenu
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取 PowerShell 选项卡的加载项菜单上只读属性。

```
# Clear the Add-ons menu if one exists.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
# Create an AddOns menu with an accessor.
# Note the use of "_"  as opposed to the "&" for mapping to the fast key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")
# Show the Add-ons menu on the current PowerShell tab.
$psISE.CurrentPowerShellTab.AddOnsMenu
```

###  <a name="CanExecute"></a> CanInvoke
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 只读布尔值属性，如果可以使用[调用 （脚本）](#invoke)方法调用脚本返回**$true**值。

```
# CanInvoke will be false if the PowerShell
# tab is running a script that takes a while, and you
# check its properties from another PowerShell tab. It is
# always false if checked on the current PowerShell tab. 
# Manually create a second PowerShell tab before running this script.
# Return to the first tab and type
$secondTab = $psise.PowerShellTabs[1] 
$secondTab.CanInvoke 
$secondTab.Invoke({sleep 20})
$secondTab.CanInvoke

```

###  <a name="Commandpane"></a> Consolepane
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。  在 Windows PowerShell ISE 2.0 这是名为**CommandPane**。

 用于获取控制台窗格[编辑器](../ise/The-ISEEditor-Object.md)对象的只读属性。

```
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane

```

###  <a name="Displayname"></a> 显示名称
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 读写属性来获取或设置 PowerShell 选项卡显示的文本。 默认情况下，命名选项卡的"PowerShell #"、 # 表示数字的位置。

```
$newTab = $psise.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

###  <a name="ExpandedScript"></a> ExpandedScript
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 读写布尔值属性，确定是展开还是隐藏脚本窗格。

```
# Toggle the expanded script property to see its effect.
$PSise.CurrentPowerShellTab.ExpandedScript=!$PSise.CurrentPowerShellTab.ExpandedScript

```

###  <a name="Files"></a> 文件
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取[集合的脚本文件](../ise/The-ISEFileCollection-Object.md)的只读属性是在 PowerShell 选项卡中打开。

```
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb" 
# Gets the line count
$newFile.Editor.LineCount
```

###  <a name="Output"></a> 输出
  此功能不含在 Windows PowerShell ISE 2.0 中，但已删除或重命名的 ISE 更高版本中。  在更高版本的 Windows PowerShell ISE 中，您可以使用相同的目的**ConsolePane**对象。

 用于获取当前[编辑器](../ise/The-ISEEditor-Object.md)的结果窗格中的只读属性。

```
# Clears the text in the Output pane.
$psise.CurrentPowerShellTab.output.clear()
```

###  <a name="Prompt"></a> 提示
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取当前提示文本只读属性。 注意︰**提示**函数可以通过用户的配置文件。 如果结果为简单的字符串之外，则此属性返回执行任何操作。

```
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

###  <a name="ShowCommands"></a> ShowCommands
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 指示当前如果显示命令窗格中的读写属性。

```
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $True
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands=$True}
```

###  <a name="StatusText"></a> StatusText
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取**PowerShellTab**状态文字只读属性。

```
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

###  <a name="HorizontalAddOnToolsPaneOpened"></a> HorizontalAddOnToolsPaneOpened
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 只读属性指示是否为当前打开的水平的加载项工具窗格。

```
# Gets the current state of the horizontal Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

###  <a name="VerticalAddOnToolsPaneOpened"></a> **VerticalAddOnToolsPaneOpened**
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 指示垂直加载项是否工具窗格中的只读属性当前已打开。

```
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands=$True
# Gets the current state of the vertical Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## 另请参阅
 [PowerShellTabCollection 对象](The-PowerShellTabCollection-Object.md) 
 [脚本对象模型的 Windows PowerShell ISE](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](../ise/The-ISE-Object-Model-Hierarchy.md)

  
