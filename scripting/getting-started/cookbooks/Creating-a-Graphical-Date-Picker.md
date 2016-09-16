---
title: "创建图形的日期选取器"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 6b5349c6ac94902d5bc5859782fbc84c1d151786
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 创建图形的日期选取器
使用 Windows PowerShell 3.0 和更高版本创建一个让用户能够选择月份的一天的图形的日历样式控件的窗体。

## 创建的图形的日期选取器控件
复制，然后将以下内容粘贴到 Windows PowerShell ISE，然后将其另存为 Windows PowerShell 脚本 (.ps1)。

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object Windows.Forms.Form 

$form.Text = "Select a Date" 
$form.Size = New-Object Drawing.Size @(243,230) 
$form.StartPosition = "CenterScreen"

$calendar = New-Object System.Windows.Forms.MonthCalendar 
$calendar.ShowTodayCircle = $False
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar) 

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$form.Topmost = $True

$result = $form.ShowDialog() 

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

该脚本首先加载两个.NET Framework 类︰ **System.Drawing**和**System.Windows.Forms**。 然后启动新实例的.NET Framework 类**Windows.Forms.Form**;提供一个空白窗体或可以开始添加控件的窗口。

```
$form = New-Object Windows.Forms.Form
```

创建窗体类实例后，此类的三个属性分配值。

-   **文本。** 这将成为窗口的标题。

-   **大小。** 这是窗体，以像素为单位的大小。 上述脚本创建的窗体 243 像素宽乘以 230 像素高。

-   **StartingPosition。** 在上述脚本情况下，此可选属性设置为**屏幕中心**。 如果您没有添加此属性，Windows 会打开该窗体时选择一个位置。 通过将**StartingPosition**设置为**屏幕中心**，您自动显示在屏幕中间的窗体加载每次。

```
$form.Text = "Select a Date" 
$form.Size = New-Object Drawing.Size @(243,230) 
$form.StartPosition = "CenterScreen"
```

接下来，创建，然后再添加表单中的日历控件。 在此示例中，是不突出显示当前日期，或带圆圈。 用户可以选择仅一天在日历上一次。

```
$calendar = New-Object System.Windows.Forms.MonthCalendar 
$calendar.ShowTodayCircle = $False
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

接下来，创建窗体的**确定**按钮。 指定的大小和**确定**按钮的行为。 在本示例中，按钮的位置是从窗体的顶部边缘，165 像素，从左侧边缘的 38 像素。 按钮高度是 23 像素，而按钮长度为 75 像素。 脚本使用预定义的 Windows 窗体类型来确定按钮的行为。

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

同样，您将创建一个**取消**按钮。 **取消**按钮是从顶部，165 像素，但从窗口的左边缘 113 像素。

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

将**Topmost**属性设置为**$True**强制此窗口将打开位于其他打开的窗口和对话框顶部。

```
$form.Topmost = $True
```

添加以下代码将窗体显示在 Windows 中的行。

```
$result = $form.ShowDialog()
```

最后，**如果**块中的代码指示 Windows 用户选择某一天在日历，然后单击**确定**按钮或按**Enter**键后如何处理窗体。 Windows PowerShell 向用户显示所选的日期。

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## 另请参阅
[嗨脚本专家︰ 为什么没有这些 PowerShell GUI 示例工作？](http://go.microsoft.com/fwlink/?LinkId=506644)
 [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
[一周中的 Windows PowerShell 提示︰ 创建图形的日期选取器](http://technet.microsoft.com/library/ff730942.aspx)

