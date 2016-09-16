---
title: "从列表框中选择项目"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 327c7cc5-21d0-4ace-b151-aa1491d1d3c2
ms.openlocfilehash: 0bc566e46dcb0b5867eb2ee152677d8185a0948f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 从列表框中选择项目
使用 Windows PowerShell 3.0 和更高版本创建一个对话框，让用户能够选择项目，从列表框控件。

## 创建列表框控件，并从中选择的项目
复制，然后将以下内容粘贴到 Windows PowerShell ISE，然后将其另存为 Windows PowerShell 脚本 (.ps1)。

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form 
$form.Text = "Select a Computer"
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
$label.Text = "Please select a computer:"
$form.Controls.Add($label) 

$listBox = New-Object System.Windows.Forms.ListBox 
$listBox.Location = New-Object System.Drawing.Point(10,40) 
$listBox.Size = New-Object System.Drawing.Size(260,20) 
$listBox.Height = 80

[void] $listBox.Items.Add("atl-dc-001")
[void] $listBox.Items.Add("atl-dc-002")
[void] $listBox.Items.Add("atl-dc-003")
[void] $listBox.Items.Add("atl-dc-004")
[void] $listBox.Items.Add("atl-dc-005")
[void] $listBox.Items.Add("atl-dc-006")
[void] $listBox.Items.Add("atl-dc-007")

$form.Controls.Add($listBox) 

$form.Topmost = $True

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

该脚本首先加载两个.NET Framework 类︰ **System.Drawing**和**System.Windows.Forms**。 然后启动新实例的.NET Framework 类**System.Windows.Forms.Form**;提供一个空白窗体或可以开始添加控件的窗口。

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
```

创建窗体类实例后，此类的三个属性分配值。

-   **文本。** 这将成为窗口的标题。

-   **大小。** 这是窗体，以像素为单位的大小。 上述脚本创建的窗体 300 像素宽乘以 200 像素高。

-   **StartingPosition。** 在上述脚本情况下，此可选属性设置为**屏幕中心**。 如果您没有添加此属性，Windows 会打开该窗体时选择一个位置。 通过将**StartingPosition**设置为**屏幕中心**，您自动显示在屏幕中间的窗体加载每次。

```
$form.Text = "Select a Computer"
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

接下来，在您描述您希望用户提供的信息的窗口上提供的标签文本。 在此例中，您希望用户选择一台计算机。

```
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please select a computer:"
$form.Controls.Add($label)
```

添加控件允许用户提供您已在您的标签文本中所述的信息 （在此例中，列表框）。 有许多列表框; 之外，您可以将应用其他控件更多的控制，请参阅 MSDN 上的[System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) 。

```
$listBox = New-Object System.Windows.Forms.ListBox 
$listBox.Location = New-Object System.Drawing.Point(10,40) 
$listBox.Size = New-Object System.Drawing.Size(260,20) 
$listBox.Height = 80
```

在下一步部分中，您可以指定所需的列表框中，向用户显示的值。

> [!NOTE]
> 此脚本创建列表框只允许一个选项。 若要创建允许多个选择列表框控件，指定**SelectionMode**属性，类似于以下值︰ `$listBox.SelectionMode = "MultiExtended"`。 有关详细信息，请参阅[多选列表框](Multiple-selection-List-Boxes.md)。

```
[void] $listBox.Items.Add("atl-dc-001")
[void] $listBox.Items.Add("atl-dc-002")
[void] $listBox.Items.Add("atl-dc-003")
[void] $listBox.Items.Add("atl-dc-004")
[void] $listBox.Items.Add("atl-dc-005")
[void] $listBox.Items.Add("atl-dc-006")
[void] $listBox.Items.Add("atl-dc-007")
```

将列表框控件添加到窗体，并指示窗口打开时打开其他窗口和对话框顶部的窗体。

```
$form.Controls.Add($listBox) 
$form.Topmost = $True
```

添加以下代码将窗体显示在 Windows 中的行。

```
$result = $form.ShowDialog()
```

最后，**如果**块中的代码指示 Windows 用户从列表框中，选择一个选项，然后单击**确定**按钮或按**Enter**键后如何处理窗体。

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

## 另请参阅
[嗨脚本专家︰ 为什么没有这些 PowerShell GUI 示例工作？](http://go.microsoft.com/fwlink/?LinkId=506644)
 [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
[一周中的 Windows PowerShell 提示︰ 从列表框中选择项目](http://technet.microsoft.com/library/ff730949.aspx)

