---
title: "ISEFile 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: abd8680607e1f57c2883ccb5dc11d2a2c2f937bd
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISEFile 对象
  **ISEFile**对象表示在 Windows PowerShellÂ® 集成脚本环境 (ISE) 的文件。 它是 Microsoft.PowerShell.Host.ISE.ISEFile 类的实例。 本主题列出其成员方法和成员属性。 **$PsISE.CurrentFile**和文件集合中 PowerShell 选项卡上的文件是 Microsoft.PowerShell.Host.ISE.ISEFile 类的所有实例。

## 方法

###  <a name="save-override"></a> 保存\( \[saveEncoding\] \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 将文件保存到磁盘。

 ** \[saveEncoding\] ** -可选[System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) 
可选的字符编码参数要用于保存的文件。 默认值为**UTF8**。

 **异常**
 -   **System.IO.IOException**︰ 无法保存该文件。

```
# Save the file using the default encoding (UTF8)
$psIse.CurrentFile.Save()

# Save the file as ASCII.
$psIse.CurrentFile.Save( [System.Text.Encoding]::ASCII )

# Gets the current encoding.
$myfile=$psIse.CurrentFile
$myfile.Encoding

```

###  <a name="saveas"></a> 另存为\(filename， \[saveEncoding\]\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 使用指定的文件名保存文件和编码。

 **文件名**-字符串要用于保存文件的名称。

 ** \[saveEncoding\] ** -可选[System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) 
可选的字符编码要用于保存文件的参数。 默认值为**UTF8**。

 **异常**
 -   **System.ArgumentNullException**: **filename**参数为 null。

-   **System.ArgumentException**: **filename**参数为空。

-   **System.IO.IOException**︰ 无法保存该文件。

```
# Save the file with a full path and name. 
$fullpath = "c:\temp\newname.txt"
$psIse.CurrentFile.SaveAs($fullPath) 
# Save the file with a full path and name and explicitly as UTF8. 
$psIse.CurrentFile.SaveAs( $fullPath, [System.Text.Encoding]::UTF8 )

```

## 属性

###  <a name="Displayname"></a> 显示名称
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 用于获取包含此文件的显示名称的字符串的只读属性。 在编辑器顶部的**文件**选项卡上显示名称。 星号状态\(\*\)末尾的名称指示的文件具有未保存的更改。

```
# Shows the display name of the file.
$psIse.CurrentFile.DisplayName

```

###  <a name="Editor"></a> 编辑器
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取[编辑器对象](The-ISEEditor-Object.md)的只读属性用于指定的文件。

```
# Gets the editor and the text.
$psIse.CurrentFile.Editor.Text

```

###  <a name="Encoding"></a> 编码
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取原始文件编码只读属性。 这是**System.Text.Encoding**对象。

```
# Shows the encoding for the file. 
$psIse.CurrentFile.Encoding

```

###  <a name="FullPath"></a> FullPath
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取指定打开的文件的完整路径的字符串只读属性。

```
# Shows the full path for the file. 
$psIse.CurrentFile.FullPath

```

###  <a name="IsSaved"></a> IsSaved
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 只读布尔属性返回**$true**如果上次修改后保存该文件。

```
# Determines whether the file has been saved since it was last modified.
$myfile=$psIse.CurrentFile
$myfile.IsSaved

```

###  <a name="IsUntitled"></a> IsUntitled
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 如果文件从未给定标题，则返回**$true**只读属性。

```
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled

```

## 另请参阅
 [ISEFileCollectionObject](The-ISEFileCollection-Object.md) 
 [脚本对象模型的 Windows PowerShell ISE](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md)

  
