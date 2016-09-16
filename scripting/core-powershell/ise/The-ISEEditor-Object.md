---
title: "ISEEditor 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 0101daf8-4e31-4e4c-ab89-01d95dcb8f46
ms.openlocfilehash: 93e07e255ffed1784ebb97366dc8857e8cc1e238
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISEEditor 对象
  **ISEEditor**对象是 Microsoft.PowerShell.Host.ISE.ISEEditor 类的实例。 控制台窗格是一个**ISEEditor**对象。 每个[ISEFile](The-ISEFile-Object.md)对象具有关联的**ISEEditor**对象。 下面的部分中列出的方法和**ISEEditor**对象的属性。

## 方法

### 清除\(\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 清除编辑器中的文本。

```
# Clears the text in the Console pane.
$psIse.CurrentPowerShellTab.ConsolePane.Clear()

```

### EnsureVisible\(int lineNumber\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 滚动编辑器中，以便在指定的**lineNumber**参数值对应的行可见。 如果指定的行号为 1，最后一个行号，它定义有效的行号的范围之外，它会引发异常。

 **lineNumber** 
是可见的行数。

```
# Scrolls the text in the Script pane so that the fifth line is in view. 
$psIse.CurrentFile.Editor.EnsureVisible(5)

```

### 焦点\(\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 将焦点设置为编辑器。

```
# Sets focus to the Console pane. 
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### GetLineLength\(int lineNumber \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取行的长度为整数由行号指定的行。

 **lineNumber** 
要获取长度的行号。

 **返回**
从指定的行号的行的行长度。

```
# Gets the length of the first line in the text of the Command pane. 
$psIse.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### GoToMatch\(\)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 如果编辑器对象的**CanGoToMatch**属性是**$true**，即前紧挨的左括号、 括号或大括号-脱字号时将脱字号匹配字符\(，\[，{-或右括号、 括号或大括号后立即- \)，\]，}。  插入符号位于开始字符之前或之后结束的字符。 如果**$false** **CanGoToMatch**属性，然后此方法没有任何影响。 请参阅[CanGoToMatch](#cangotomatch)。

```
# Test to see if the caret is next to a parenthesis, bracket, or brace.
```

### InsertText\(文本 \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 所选内容替换文本或插入当前位置插入符号的文本。

 **文本**-要插入的字符串文本。

 请参阅本主题后面的[脚本示例](#example)。

### 选择\(startLine，startColumn，行尾，endColumn \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 选择从**startLine**、 **startColumn**、**行尾**和**endColumn**参数的文本。

 **startLine** -整数所选内容的开始位置的行。

 **startColumn** -整数所选内容的开始位置的开始行内的列。

 **行尾**-整数所选内容的结束位置的行。

 **endColumn** -整数所选内容的结尾处的结束行内的列。

 请参阅本主题后面的[脚本示例](#example)。

### SelectCaretLine\(\)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 选择整个行的当前包含插入符号的文本。

```
# First, set the caret position on line 5.
$psIse.CurrentFile.Editor.SetCaretPosition(5,1) 
# Now select that entire line of text
$psIse.CurrentFile.Editor.SelectCaretLine()

```

### SetCaretPosition\( lineNumber，columnNumber \)
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 设置插入符号位置的行号和列数。 如果脱字号行号或插入符号的列号利用他们各自的有效范围，它会引发异常。

 **lineNumber** -脱字号行号的整数。

 **columnNumber** -脱字号列号的整数。

```
# Set the CaretPosition.
$psIse.CurrentFile.Editor.SetCaretPosition(5,1)
```

### ToggleOutliningExpansion\(\)
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 将导致所有分级显示部分以展开或折叠。

```
# Toggle the outlining expansion
$psIse.CurrentFile.Editor.ToggleOutliningExpansion()

```

## 属性

###  <a name="CanGoToMatch"></a> CanGoToMatch
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。 

 表明脱字号括号、 括号或大括号-旁边的只读布尔属性\(\)， \[\]，{}。 立即开始字符前后立即对的结束字符脱字号时，此属性值将是**$true**。 否则，它是**$false**。

```
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psIse.CurrentFile.Editor.CanGoToMatch

```

###  <a name="CaretColumn"></a> CaretColumn
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取的列号的只读属性对应于插入符号的位置。

```
# Get the CaretColumn.
$psIse.CurrentFile.Editor.CaretColumn

```

###  <a name="CaretLine"></a> CaretLine
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取包含插入符号的行数只读属性。

```
# Get the CaretLine.
$psIse.CurrentFile.Editor.CaretLine

```

###  <a name="caretlinetext"></a> CaretLineText
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 只读属性，获取完整的包含插入符号的文本行。

```
# Get all of the text on the line that contains the caret.
$psIse.CurrentFile.Editor.CaretLineText

```

###  <a name="LineCount"></a> LineCount
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取编辑器中的行数只读属性。

```
# Get the LineCount.
$psIse.CurrentFile.Editor.LineCount

```

###  <a name="SelectedText"></a> SelectedText
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 获取所选的文本编辑器中的只读属性。

 请参阅本主题后面的[脚本示例](#example)。

###  <a name="Text"></a> 文本
  支持的 Windows PowerShell ISE 2.0 和更高版本。 

 读取/写入属性来获取或设置编辑器中的文本。

 请参阅本主题后面的[脚本示例](#example)。

##  <a name="example"></a> 脚本示例

```

# This illustrates how you can use the length of a line to
# select the entire line and shows how you can make it lowercase. 
# You must run this in the Console pane. It will not run in the Script pane.
# Begin by getting a variable that points to the editor.
$myEditor=$psIse.CurrentFile.Editor
# Clear the text in the current file editor.
$myEditor.Clear()

# Make sure the file has five lines of text.
$myEditor.InsertText("LINE1 `n")
$myEditor.InsertText("LINE2 `n")
$myEditor.InsertText("LINE3 `n")
$myEditor.InsertText("LINE4 `n")
$myEditor.InsertText("LINE5 `n")

# Use the GetLineLength method to get the length of the third line. 
$endColumn= $myEditor.GetLineLength(3)
# Select the text in the first three lines.
$myEditor.Select(1,1,3,$endColumn + 1)
$selection = $myEditor.SelectedText
# Clear all the text in the editor.
$myEditor.Clear()
# Add the selected text back, but in lower case.
$myEditor.InsertText($selection.ToLower())
```

## 另请参阅
 [ISEFile 对象](The-ISEFile-Object.md) 
 [PowerShellTab 对象](The-PowerShellTab-Object.md) 
 [脚本对象模型的 Windows PowerShell ISE](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md)

  
