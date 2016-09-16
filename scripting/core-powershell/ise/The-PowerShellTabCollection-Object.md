---
title: "PowerShellTabCollection 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: 7a22642386631684bf3fd23abe762237b86f9ce6
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# PowerShellTabCollection 对象
  **PowerShellTab**集合对象是**PowerShellTab**对象的集合。 **PowerShellTab**的每个对象作为单独的运行环境。 它是 Microsoft.PowerShell.Host.ISE.PowerShellTabs 类的实例。 例如， **$psISE.PowerShellTabs**对象。

## 方法

### 添加\(\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 向集合中添加新的 PowerShell 选项卡。 将返回新添加的选项卡。

```
$NewTab=$psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab"
```

### 删除\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 删除**psTab**参数所指定的选项卡。

 **psTab** 
 PowerShell 选项卡上，若要删除。

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

### SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 选择以使其当前处于活动状态的 PowerShell 选项卡上的**psTab**参数指定的 PowerShell 选项卡。

 **psTab** 
 PowerShell tab 可选择。

```
# Save the current tab in a variable and rename it
$OldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName="Old Tab"
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab" 
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab=$oldtab
```

## 另请参阅
 [PowerShellTab 对象](The-PowerShellTab-Object.md) 
 [脚本对象模型的 Windows PowerShell ISE](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](../ise/The-ISE-Object-Model-Hierarchy.md)

  
