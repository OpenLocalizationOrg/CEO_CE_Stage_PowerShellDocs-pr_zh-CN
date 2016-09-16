---
title: "Windows PowerShell ISE 中的辅助功能"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: a078f9d1-dd6b-4323-b16d-0622cd993aa8
ms.openlocfilehash: b480b5cd8ec7ebafb84ee69553b2b31fc680ae8f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows PowerShell ISE 中的辅助功能
本主题介绍的 Windows PowerShell® 集成脚本环境 (ISE)，您可能会发现很有帮助的辅助功能。

* [如何更改的大小和位置控制台和脚本窗格](#bkmk_1)
* [编辑文字的键盘快捷方式](#bkmk_2)
* [键盘快捷方式运行脚本](#bkmk_3)
* [用于自定义视图的键盘快捷方式](#bkmk_4)
* [键盘快捷方式调试脚本](#bkmk_5)
* [对于 Windows PowerShell 的选项卡的键盘快捷方式](#bkmk_6)
* [启动和退出的键盘快捷方式](#bkmk_7)

Microsoft 一直致力于生产的产品和服务的每个人使用更容易。 以下主题提供有关功能、 产品和服务使残障人士的 Windows PowerShell ISE 更易于访问的信息。

Windows PowerShell ISE 支持高对比度模式。 为视觉障碍的人士，断点信息可通过用于管理断点，如[获取 PSBreakpoint](https://technet.microsoft.com/en-us/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6)和[设置 PSBreakpoint](https://technet.microsoft.com/en-us/library/6afd5d2c-a285-4796-8607-3cbf49471420)cmdlet。 有关详细信息请参阅如何[使用 Windows PowerShell ise 调试脚本](../core-powershell/ise/How-to-Debug-Scripts-in-Windows-PowerShell-ISE.md#bkmk_1)"如何管理断点"。 除了辅助功能和实用程序在 Microsoft Windows 中，以下功能使 Windows PowerShell ISE 更易于访问残障人士使用︰

-   键盘快捷方式

-   语法突出显示的表和修改使用[$psISE.Options](https://technet.microsoft.com/en-us/library/75e2a76f-f3d1-490b-ad5d-e3829946aabb)脚本对象的多个其他颜色设置的能力。

-   更改文本大小

## <a name="bkmk_1"></a>如何更改的大小和位置控制台和脚本窗格
可以使用以下步骤以更改大小和位置控制台窗格和脚本窗格。 当再次打开 Windows PowerShell ISE 时，将保留您所做的大小和位置更改。

### 若要调整大小的脚本窗格和控制台窗格

1.  暂停将指针悬停在脚本窗格和控制台窗格之间拆分线。

2.  当鼠标指针变为双向箭头时，拖动边框以更改窗格的大小。

### 若要移动的脚本窗格和控制台窗格
请执行下列操作之一︰

-   若要移动控制台窗格上方的脚本窗格中，按**CTRL + 1**的工具栏上，单击**显示脚本窗格顶部**图标，或在**视图**菜单中，单击**显示脚本窗格顶部**。

-   若要移动脚本窗格右侧的控制台窗格中，按**CTRL + 2**的工具栏上，单击**显示脚本窗格右侧**图标，或在**视图**菜单中，单击**显示脚本窗格右侧**。

-   要最大化脚本窗格中，按**CTRL + 3** ，或者，在工具栏上，单击**显示脚本窗格最大化**图标，或在**视图**菜单上，单击**显示脚本窗格最大化**。

-   最大化控制台窗格和隐藏脚本窗格上的选项卡的行的最右侧边缘，请单击**隐藏脚本窗格**图标上的，在**视图**菜单中，单击以取消选中**窗格中显示脚本**菜单选项。

-   最大化控制台窗格中，在选项卡，行的最右侧边缘上时显示脚本窗格中单击**窗格中显示脚本**图标，或在**视图**菜单上，单击以选择**窗格中显示脚本**菜单选项。

## <a name="bkmk_2"></a>编辑文字的键盘快捷方式
编辑文本时，您可以使用以下键盘快捷方式。

|操作|键盘快捷方式|在中使用|
|----------|----------------------|----------|
|**复制**|CTRL + C|脚本窗格，控制台窗格|
|**剪切**|按 CTRL + X|脚本窗格，控制台窗格|
|**在脚本查找**|CTRL + F|脚本窗格|
|**在脚本查找下一个**|F3|脚本窗格|
|**在脚本以前的查找**|SHIFT + F3|脚本窗格|
|**粘贴**|CTRL + V|脚本窗格中，控制台窗格|
|**恢复**|CTRL + Y|脚本窗格中，控制台窗格|
|**在脚本中替换**|CTRL + H|脚本窗格|
|**保存**|CTRL + S|脚本窗格|
|**选择所有**|CTRL + A|脚本窗格中，控制台窗格|
|**撤消**|CTRL + Z|脚本窗格，控制台窗格|

## <a name="bkmk_3"></a>键盘快捷方式运行脚本
在脚本窗格中运行脚本时，可以使用以下键盘快捷方式。

|操作|键盘快捷方式|
|----------|---------------------|
|**新增功能**|CTRL + N|
|**打开**|CTRL + O|
|**运行**|F5|
|**运行所选内容**|F8|
|**停止执行**|CTRL + 分页符。 上下文是明确 （当选定任何文本） 时，可以使用 CTRL + C。|
|**选项卡**（到下一个脚本）|按 CTRL + TAB**注意︰** tab 键转至下一个脚本正常工作，仅当您有一个 PowerShell 选项卡打开，或当您有多个 PowerShell 选项卡上打开，但焦点位于脚本窗格中。|
|**选项卡**（到前一节脚本）|CTRL + SHIFT + TAB**注意︰** tab 键转至前面的脚本工作时您只有一个 PowerShell 选项卡上已打开了，或如果您有多个 PowerShell 选项卡上打开，且焦点在脚本窗格中。|

## <a name="bkmk_4"></a>用于自定义视图的键盘快捷方式
可以使用以下键盘快捷方式若要自定义 Windows PowerShell ISE 中的视图。 他们已从应用程序中的所有窗格可访问。

|操作|键盘快捷方式|
|----------|---------------------|
|**转到控制台窗格**|CTRL + D|
|**转到脚本窗格**|CTRL I +|
|**显示脚本窗格**|按 CTRL + R|
|**隐藏脚本窗格**|按 CTRL + R|
||
|**上移脚本窗格**|CTRL 1 +|
|**向右移动脚本窗格**|CTRL 2 +|
|**最大化脚本窗格**|CTRL 3 +|
|**缩放**|CTRL + 加号|
|**缩小**|CTRL + 减号 （)|

## <a name="bkmk_5"></a>键盘快捷方式调试脚本
当调试脚本，您可以使用以下键盘快捷方式。

|操作|键盘快捷方式|在中使用|
|----------|---------------------|----------|
|**继续运行 /**|F5|脚本窗格中，当调试脚本|
|**单步执行**|F11|脚本窗格中，当调试脚本|
|**逐过程**|F10|脚本窗格中，当调试脚本|
|**的步骤**|SHIFT + F11|脚本窗格中，当调试脚本|
|**显示呼叫堆栈**|CTRL + SHIFT + D|脚本窗格中，当调试脚本|
|**列表断点**|CTRL + SHIFT + L|脚本窗格中，当调试脚本|
|**切换断点**|F9|脚本窗格中，当调试脚本|
|**删除所有断点**|按 CTRL + SHIFT + F9|脚本窗格中，当调试脚本|
|**停止调试程序**|SHIFT + F5|脚本窗格中，当调试脚本|

> [!NOTE]
> 您也可以使用用于 Windows PowerShell 控制台调试脚本 Windows PowerShell ISE 中的时的键盘快捷方式。 若要使用这些快捷方式，必须控制台窗格中，键入快捷方式，然后按 ENTER。

|操作|键盘快捷方式|在中使用|
|----------|---------------------|----------|
|**继续**|C|控制台窗格中，当调试脚本|
|**单步执行**|S|控制台窗格中，当调试脚本|
|**逐过程**|V|控制台窗格中，当调试脚本|
|**的步骤**|O|控制台窗格中，当调试脚本|
|**重复上一个命令**（对于单步执行或跳过）|输入|控制台窗格中，当调试脚本|
|**显示调用堆栈**|K|控制台窗格中，当调试脚本|
|**停止调试**|问︰|控制台窗格中，当调试脚本|
|**列表脚本**|L|控制台窗格中，当调试脚本|
|**显示控制台调试命令**|H 或？|控制台窗格中，当调试脚本|

## <a name="bkmk_6"></a>对于 Windows PowerShell 的选项卡的键盘快捷方式
当您使用 Windows PowerShell 选项卡时，可以使用以下键盘快捷方式。

|操作|键盘快捷方式|
|----------|---------------------|
|**关闭 PowerShell 选项卡**|CTRL + W|
|**新 PowerShell 选项卡**|CTRL + T|
|**上一个 PowerShell 选项卡**|CTRL + SHIFT + TAB。 仅当没有已在任何 PowerShell 选项卡上打开文件时，此快捷方式工作。|
|**下一个 Windows PowerShell 选项卡**|按 CTRL + TAB。 仅当没有已在任何 PowerShell 选项卡上打开文件时，此快捷方式工作。|

## <a name="bkmk_7"></a>启动和退出的键盘快捷方式
启动 Windows PowerShell 控制台 (PowerShell.exe) 或退出 Windows PowerShell ISE，您可以使用以下键盘快捷方式。

|操作|键盘快捷方式|
|----------|---------------------|
|**退出**|按 ALT + F4|
|**启动 PowerShell.exe**（Windows PowerShell 控制台）|CTRL + SHIFT + P|

## 另请参阅
[使用 Windows PowerShell ISE](../core-powershell/ise/Using-the-Windows-PowerShell-ISE.md)

