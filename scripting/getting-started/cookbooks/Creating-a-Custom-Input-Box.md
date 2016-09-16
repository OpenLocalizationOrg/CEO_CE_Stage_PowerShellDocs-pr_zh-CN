---
title: "创建自定义的输入的框"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 0b12e56c-299f-40ee-afbf-d30d23ed2565
ms.openlocfilehash: 7bf80ff880fb1b357f64def1886597f613b13a10
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 创建自定义的输入的框
通过使用 Microsoft.NET Framework Windows PowerShell 3.0 和更高版本中的窗体构建功能图形的自定义输入框的脚本。

## 创建自定义的图形化输入的框
复制，然后将以下内容粘贴到 Windows PowerShell ISE，然后将其另存为 Windows PowerShell 脚本 (.ps1)。

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form 
$form.Text = "Data Entry Form"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please enter the information in the space below:"
$form.Controls.Add($label) 

$textBox = New-Object System.Windows.Forms.TextBox 
$textBox.Location = New-Object System.Drawing.Point(10,40) 
$textBox.Size = New-Object System.Drawing.Size(260,20) 
$form.Controls.Add($textBox) 

$form.Topmost = $True

$form.Add_Shown({$textBox.Select()})
$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

该脚本首先加载两个.NET Framework 类︰ **System.Drawing**和**System.Windows.Forms**。 然后启动新实例的.NET Framework 类**System.Windows.Forms.Form**;提供一个空白窗体或可以开始添加控件的窗口。

```
$form = New-Object System.Windows.Forms.Form
```

创建窗体类实例后，此类的三个属性分配值。

-   **文本。** 这将成为窗口的标题。

-   **大小。** 这是窗体，以像素为单位的大小。 上述脚本创建的窗体 300 像素宽乘以 200 像素高。

-   **StartingPosition。** 在上述脚本情况下，此可选属性设置为**屏幕中心**。 如果您没有添加此属性，Windows 会打开该窗体时选择一个位置。 通过将**StartingPosition**设置为**屏幕中心**，您自动显示在屏幕中间的窗体加载每次。

```
$form.Text = "Data Entry Form"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"
```

接下来，创建窗体的**确定**按钮。 指定的大小和**确定**按钮的行为。 在此示例中，按钮位于 120 像素从窗体的顶部边缘，并从的左边缘 75 像素。 按钮高度是 23 像素，而按钮长度为 75 像素。 脚本使用预定义的 Windows 窗体类型来确定按钮的行为。

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

同样，您将创建一个**取消**按钮。 **取消**按钮是从顶部，120 像素，但从窗口的左边缘 150 像素。

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

接下来，在您描述您希望用户提供的信息的窗口上提供的标签文本。

```
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please enter the information in the space below:"
$form.Controls.Add($label)
```

添加控件 （在此例中，将文本框），可让用户提供您已在您的标签文本中所述的信息。 有许多文本框; 之外，您可以将应用其他控件更多的控制，请参阅 MSDN 上的[System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) 。

```
$textBox = New-Object System.Windows.Forms.TextBox 
$textBox.Location = New-Object System.Drawing.Point(10,40) 
$textBox.Size = New-Object System.Drawing.Size(260,20) 
$form.Controls.Add($textBox)
```

将**Topmost**属性设置为**$True**强制此窗口将打开位于其他打开的窗口和对话框顶部。

```
$form.Topmost = $True
```

接下来，添加此行代码以激活该窗体，并将焦点设置到您创建的文本框。

```
$form.Add_Shown({$textBox.Select()})
```

添加以下代码将窗体显示在 Windows 中的行。

```
$result = $form.ShowDialog()
```

最后，**如果**块中的代码指示 Windows 用户提供文本框中的文本，然后单击**确定**按钮或按**Enter**键后如何处理窗体。

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## 另请参阅
[嗨脚本专家︰ 为什么没有这些 PowerShell GUI 示例工作？](http://go.microsoft.com/fwlink/?LinkId=506644)
 [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
[一周中的 Windows PowerShell 提示︰ 创建自定义输入框](http://technet.microsoft.com/library/ff730941.aspx)

