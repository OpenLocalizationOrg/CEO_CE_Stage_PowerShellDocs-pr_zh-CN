---
title: ISESnippetObject
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: 206b3187e3634e7565141e22b12f874c0e935701
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISESnippetObject
  **ISESnippet**对象是 Microsoft.PowerShell.Host.ISE.ISESnippet 类的实例。 **$PsISE.CurrentPowerShellTab.Snippets**集合中的成员都是**ISESnippet**对象的示例。 创建段的最简单方法是使用[新建 IseSnippet 和 #91;PSITPro5_ISE & #93;](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0)cmdlet。

## 属性

###  <a name="DisplayName"></a> 作者
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 用于获取段的作者的姓名的只读属性。

```
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author

```

###  <a name="Action"></a> CodeFragment
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 获取要插入到编辑器的代码片段只读属性。

```
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment

```

###  <a name="Shortcut"></a> 快捷方式
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 获取 Windows 的只读属性键盘快捷方式菜单项。

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## 另请参阅
 [ISESnippetCollection 对象](The-ISESnippetCollection-Object.md) 
 [脚本对象模型的 Windows PowerShell ISE](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md)

  
