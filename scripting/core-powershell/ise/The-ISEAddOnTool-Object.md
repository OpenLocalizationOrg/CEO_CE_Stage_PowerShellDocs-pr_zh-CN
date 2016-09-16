---
title: "ISEAddOnTool 对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: ce84d8bc-07ba-41f6-bdde-d6f3fddcd1e3
ms.openlocfilehash: 63ead0e423b8dd3263be16b08aa62916b01f4359
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISEAddOnTool 对象
  **ISEAddonTool**对象表示提供附加功能 toWindows PowerShell ISE 安装的加载项工具。 示例是您可以通过单击**视图**，然后**显示命令加载项**显示的**命令**工具。 此工具是然后您才能访问操作的各种可用**ISEAddOnTool**对象。

 每个加载项工具可以使用垂直窗格中或水平窗格相关联。 Windows PowerShell ISE 的右边缘停靠垂直窗格。 下边缘停靠水平窗格。

 在 Windows PowerShell ISE 中的每个 PowerShell 选项卡可以有自己的安装的加载项工具集。 请参阅[$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)和[$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)以访问可用到当前所选选项卡或任何**PowerShellTab** [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)集合对象中的对象上的相同属性的工具的集合。

## 方法
 没有 Windows PowerShell ISE 特定方法可用于此类的对象。

## 属性

###  <a name="Control"></a> 控件
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 **控件**属性提供了许多命令附加工具的详细信息的读取权限。

```
# View the properties of the Commands add-on tool.
# (assumes that it is visible in the vertical pane)
$psISE.CurrentVisibleVerticalTool.Control
HostObject                  : Microsoft.PowerShell.Host.ISE.ObjectModelRoot
Content                     :
HasContent                  :
ContentTemplate             :
ContentTemplateSelector     :
ContentStringFormat         :
BorderBrush                 :
BorderThickness             :
Background                  :
Foreground                  :
FontFamily                  :
FontSize                    :
FontStretch                 :
FontStyle                   :
FontWeight                  :
HorizontalContentAlignment  :
VerticalContentAlignment    :
TabIndex                    :
IsTabStop                   :
Padding                     :
Template                    : System.Windows.Controls.ControlTemplate
Style                       :
OverridesDefaultStyle       :
UseLayoutRounding           :
Triggers                    : {}
TemplatedParent             :
Resources                   : {System.Windows.Controls.TabItem}
DataContext                 :
BindingGroup                :
Language                    :
Name                        :
Tag                         :
InputScope                  :
ActualWidth                 : 370.75
ActualHeight                : 676.559097412109
LayoutTransform             :
Width                       :
MinWidth                    :
MaxWidth                    :
Height                      :
MinHeight                   :
MaxHeight                   :
FlowDirection               : LeftToRight
Margin                      :
HorizontalAlignment         :
VerticalAlignment           :
FocusVisualStyle            :
Cursor                      :
ForceCursor                 :
IsInitialized               : True
IsLoaded                    :
ToolTip                     :
ContextMenu                 :
Parent                      :
HasAnimatedProperties       :
InputBindings               :
CommandBindings             :
AllowDrop                   :
DesiredSize                 : 227.66,676.559097412109
IsMeasureValid              : True
IsArrangeValid              : True
RenderSize                  : 370.75,676.559097412109
RenderTransform             :
RenderTransformOrigin       :
IsMouseDirectlyOver         : False
IsMouseOver                 : False
IsStylusOver                : False
IsKeyboardFocusWithin       : False
IsMouseCaptured             :
IsMouseCaptureWithin        : False
IsStylusDirectlyOver        : False
IsStylusCaptured            :
IsStylusCaptureWithin       : False
IsKeyboardFocused           : False
IsInputMethodEnabled        :
Opacity                     :
OpacityMask                 :
BitmapEffect                :
Effect                      :
BitmapEffectInput           :
CacheMode                   :
Uid                         :
Visibility                  : Visible
ClipToBounds                : False
Clip                        :
SnapsToDevicePixels         : False
IsFocused                   :
IsEnabled                   :
IsHitTestVisible            :
IsVisible                   : True
Focusable                   :
PersistId                   : 1
IsManipulationEnabled       :
AreAnyTouchesOver           : False
AreAnyTouchesDirectlyOver   :
AreAnyTouchesCapturedWithin : False
AreAnyTouchesCaptured       :
TouchesCaptured             : {}
TouchesCapturedWithin       : {}
TouchesOver                 : {}
TouchesDirectlyOver         : {}
DependencyObjectType        : System.Windows.DependencyObjectType
IsSealed                    : False
Dispatcher                  : System.Windows.Threading.Dispatcher

```

###  <a name="IsVisible"></a> IsVisible
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 指示加载项工具是否在其已分配的窗格中当前可见的布尔属性。 如果可见，可以将**IsVisible**属性设置为**$false**若要隐藏工具，或将**IsVisible**属性设置为**$true**以使其 PowerShell 选项卡上的加载项工具可见。 请注意，加载项工具处于隐藏状态后，它将不再可访问**CurrentVisibleHorizontalTool**或**CurrentVisibleVerticalTool**对象，因此无法成为受可见该对象上使用此属性。

```
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible=$true

```

###  <a name="name"></a> 名称
  支持的 Windows PowerShell ISE 3.0 和更高版本，以及在早期版本中不存在。

 只读属性获取加载项工具的名称。

```
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.name
Commands

```

## 另请参阅
 [ISEAddOnToolCollection 对象](The-ISEAddOnToolCollection-Object.md)
 [脚本对象模型的 Windows PowerShell ISE](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md)
 [ISE 对象模型的层次结构](The-ISE-Object-Model-Hierarchy.md)

