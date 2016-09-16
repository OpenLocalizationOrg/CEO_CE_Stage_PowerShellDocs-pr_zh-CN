---
title: "ISEMenuItemCollection 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7e9a128d955508c2b5b6429d59d8d7e32c631cdb
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISEMenuItemCollection 对象
  **ISEMenuItemCollection**对象是**ISEMenuItem**对象的集合。 它是 Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection 类的实例。 示例是用于自定义**加载项**菜单中 Windows PowerShellÂ® 集成脚本环境 (ISE) 的**$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus**对象。

## 方法

### 添加\(字符串 DisplayName，System.Management.Automation.ScriptBlock 操作 System.Windows.Input.KeyGesture 快捷方式 \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 将菜单项添加到集合。

 **DisplayName** 
添加菜单上的显示名称。

 **操作**
 **System.Management.Automation.ScriptBlock**对象用于指定与此菜单项相关联的操作。

 **快捷方式**
操作的键盘快捷方式。

 **返回**
 ISEMenuItem 刚添加的对象。

```
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
```

### 清除\(\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 从菜单项中删除所有子菜单。

```
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

```

## 另请参阅
 [ISEMenuItem 对象](The-ISEMenuItem-Object.md) 
 [脚本对象模型的 Windows PowerShell ISE](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md)

  
