---
title: "ISESnippetCollection 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
ms.openlocfilehash: fa38299acf7af9ade91805e3e3c08b6bd7a89075
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISESnippetCollection 对象
  **ISESnippetCollection**对象是**ISESnippet**对象的集合。 与**PowerShellTab**对象相关联的文件集是此类的成员。 例如， **$psISE.CurrentPowerShellTab.Files**集合。

## 方法

### 加载\(FilePathName \)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 加载。 snippets.ps1xml 文件包含用户定义的代码段。 创建段的最简单方法是使用新建 IseSnippet cmdlet，自动将其存储在您的配置文件的文件夹，以便每次启动 Windows PowerShell ISE 加载。

 **FilePathName** -字符串的路径和文件名称添加到。 包含代码段定义 snippets.ps1xml 文件。

```
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) “Snippets\MySnips.snippets.ps1xml” $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)

```

## 另请参阅
 [ISESnippetObject](The-ISESnippetObject.md) 
 [脚本对象模型的 Windows PowerShell ISE](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md)

  
