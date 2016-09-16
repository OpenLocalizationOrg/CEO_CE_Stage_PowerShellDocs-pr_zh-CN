---
title: "ISEFileCollection 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: 646e7f906e024785b538ab89c7f1069032ec8846
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISEFileCollection 对象
  **ISEFileCollection**对象是**ISEFile**对象的集合。 例如，$psISE.CurrentPowerShellTab.Files 集合。

## 方法

### 添加\( \[fullPath\] \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 创建并返回一个新的未命名的文件并将其添加到集合。 新创建的**IsUntitled**属性是文件的**$true**。

 ** \[fullPath\] ** -可选字符串完全指定文件的路径。 如果您包括**fullPath**参数和相对路径，或如果您使用的文件的名称，而不是完整的路径，则会生成异常。

```
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")

```

### 删除\(文件，\[强制\] \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 从当前 PowerShell 选项卡中删除指定的文件。

 **文件**– 您想要从集合中移除的字符串 ISEFile 文件。 如果尚未保存该文件，此方法引发异常。 使用**强制**切换参数强制删除未保存的文件。

 **\[强制\]**-可选布尔如果设置为**$true**，授予权限，即使它未保存在最后一次使用之后删除该文件。 默认情况下**$false**。

```
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### SetSelectedFile\( selectedFile \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 选择**selectedFile**参数所指定的文件。

 **selectedFile** – 您想要选择的 Microsoft.PowerShell.Host.ISE.ISEFile ISEFile 文件。

```

# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)

```

## 另请参阅
 [ISEFile 对象](The-ISEFile-Object.md) 
 [脚本对象模型的 Windows PowerShell ISE](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md)

  
