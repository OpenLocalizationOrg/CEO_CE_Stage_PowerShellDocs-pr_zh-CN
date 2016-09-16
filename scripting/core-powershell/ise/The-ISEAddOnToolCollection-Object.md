---
title: "ISEAddOnToolCollection 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: a2c41d3306f89d7e2ab01b185b7ad8412c79975e
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISEAddOnToolCollection 对象
  **ISEAddOnToolCollection**对象是**ISEAddOnTool**对象的集合。 例如， **$psISE.CurrentPowerShellTab.VerticalAddOnTools**对象。

## 方法

### 添加\(名称、 ControlType， \[IsVisible\] \)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 向集合中添加一个新的加载项工具。 将返回新添加的加载项工具。 您运行此命令之前，必须在本地计算机上安装该加载项工具并加载程序集。

 **名称**– 字符串指定添加到 Windows PowerShell ISE 的加载项工具的显示名称。

 **ControlType** -类型指定添加的控件。

 ** \[IsVisible\] ** -可选布尔如果设置为**$true**，该加载项工具立即看到相关联的工具窗格中。

```
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)

```

### 删除\(项目 \)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 从集合中移除指定的加载项工具。

 **项目**– Microsoft.PowerShell.Host.ISE.ISEAddOnTool 指定要从 Windows PowerShell ISE 中删除的对象。

```
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)

```

### SetSelectedPowerShellTab\( psTab \)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 选择**psTab**参数指定的 PowerShell 选项卡。

 **psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab PowerShell tab 可选择。

```

      $newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"

```

### 删除\(psTab \)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 删除**psTab**参数指定的 PowerShell 选项卡。

 **psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab PowerShell 选项卡上，若要删除。

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

## 另请参阅
 [PowerShellTab 对象](The-PowerShellTab-Object.md) 
 [脚本对象模型的 Windows PowerShell ISE](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md)

  
