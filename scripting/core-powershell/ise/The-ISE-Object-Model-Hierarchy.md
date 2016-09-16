---
title: "ISE 对象模型的层次结构"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: bc3300e4-9c17-4f00-a621-c8867126e3b3
ms.openlocfilehash: d9ed72b42a7691f6b7509c1aefc91ada4eaad113
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# ISE 对象模型的层次结构
  本主题介绍属于的 Windows PowerShell 集成脚本环境 (ISE) 的对象的层次结构。 Windows PowerShell ISE 是包含在 Windows PowerShell 3.0 和 Windows PowerShell 4.0。 单击要将您带到定义对象的类的参考文档的对象。

##  <a name="psISE"></a> **$psISE 对象**
 **$PsISE**对象是 Windows PowerShell ISE 对象层次结构的[根对象](The-ObjectModelRoot-Object.md)。 它位于顶部的级别，使以下对象可供脚本︰

-   **[$psISE.CurrentFile](#currentfile)**

-   **[$psISE.CurrentPowerShellTab](#currentpowershelltab)**

-   **[$psISE.CurrentVisibleHorizontalTool](#CurrentVisibleHorizontalTool)**

-   **[$psISE.CurrentVisibleVerticalTool](#CurrentVisibleVerticalTool)**

-   **[$psISE.Options](#options)**

-   **[$psISE.PowerShellTabs](#powershelltabs)**

##  <a name="CurrentFile"></a> **[$psISE.CurrentFile](The-ISEFile-Object.md)**
 **$PsISE.CurrentFile**对象[ISEFile](The-ISEFile-Object.md)类的实例，使以下对象可供脚本︰

-   **[$psISE.CurrentFile.DisplayName](The-ISEFile-Object.md#Displayname)**

-   **[$psISE.CurrentFile.Editor](The-ISEEditor-Object.md)** 此对象[ISEEditor](The-ISEEditor-Object.md)类的实例，使以下对象可供脚本︰

    -   **[$psISE.CurrentFile.Editor.CanGoToMatch](The-ISEEditor-Object.md#cangotomatch)**

    -   **[CaretColumn](The-ISEEditor-Object.md#CaretColumn)**

    -   **[CaretLine](The-ISEEditor-Object.md#CaretLine)**

    -   **[$psISE.CurrentFile.Editor.CaretLineText](The-ISEEditor-Object.md#CaretLineText)**

    -   **[LineCount](The-ISEEditor-Object.md#LineCount)**

    -   **[SelectedText](The-ISEEditor-Object.md#SelectedText)**

    -   **[文本](The-ISEEditor-Object.md#Text)**

-   **[编码](The-ISEFile-Object.md#Encoding)**

-   **[FullPath](The-ISEFile-Object.md#FullPath)**

-   **[IsSaved](The-ISEFile-Object.md#IsSaved)**

-   **[IsUntitled](The-ISEFile-Object.md#IsUntitled)**

##  <a name="CurrentPowerShellTab"></a> **[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)**
 **$PsISE.CurrentPowerShellTab**对象[PowerShellTab](The-PowerShellTab-Object.md)类的实例，使以下对象可供脚本︰

-   **[$psISE.CurrentPowerShellTab.AddOnsMenu](The-ISEMenuItem-Object.md)** 此对象[ISEMenuItem](The-ISEMenuItem-Object.md)类的实例，使以下对象可供脚本︰

    -   **[$psISE.CurrentPowerShellTab.AddOnsMenu.Action](The-ISEMenuItem-Object.md#Action)**

    -   **[$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName](The-ISEMenuItem-Object.md#DisplayName)**

    -   **[$psISE.CurrentPowerShellTab.AddOnsMenu.Shortcut](The-ISEMenuItem-Object.md#Shortcut)**

    -   **[$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus](The-ISEMenuItemCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.CanInvoke](The-PowerShellTab-Object.md#CanExecute)**

-   **[$psISE.CurrentPowerShellTab.ConsolePane](The-ISEEditor-Object.md)** 此对象[ISEEditor](The-ISEEditor-Object.md)类的实例，使以下对象可供脚本︰

    -   **[$psISE.CurrentPowerShellTab.ConsolePane.CanGoToMatch](The-ISEEditor-Object.md#cangotomatch)**

    -   **[CaretColumn](The-ISEEditor-Object.md#CaretColumn)**

    -   **[CaretLine](The-ISEEditor-Object.md#CaretLine)**

    -   **[$psISE.CurrentPowerShellTab.ConsolePane.CaretLineText](The-ISEEditor-Object.md#CaretLineText)**

    -   **[LineCount](The-ISEEditor-Object.md#LineCount)**

    -   **[SelectedText](The-ISEEditor-Object.md#SelectedText)**

    -   **[文本](The-ISEEditor-Object.md#Text)**

-   **[$psISE.CurrentPowerShellTab.DisplayName](The-PowerShellTab-Object.md#Displayname)**

-   **[$psISE.CurrentPowerShellTab.ExpandedScript](The-PowerShellTab-Object.md#ExpandedScript)**

-   **[$psISE.CurrentPowerShellTab.Files](The-ISEFileCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened](The-PowerShellTab-Object.md#HorizontalAddOnToolsPaneOpened)**

-   **[$psISE.CurrentPowerShellTab.Prompt](The-PowerShellTab-Object.md#Prompt)**

-   **[$psISE.CurrentPowerShellTab.ShowCommands](The-PowerShellTab-Object.md#ShowCommands)**

-   **[$psISE.CurrentPowerShellTab.Snippets](The-ISESnippetCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.StatusText](The-PowerShellTab-Object.md#StatusText)**

-   **[$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.VerticalAddOnToolsPaneOpened](The-PowerShellTab-Object.md#VerticalAddOnToolsPaneOpened)**

-   **[$psISE.CurrentPowerShellTab.VisibleHorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.VisibleVerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)**

##  <a name="CurrentVisibleHorizontalTool"></a> **$psISE.CurrentVisibleHorizontalTool**
 **$PsISE.CurrentVisibleHorizontalTool**对象是[ISEAddOnTool](The-ISEAddOnTool-Object.md)类的实例。 指向 Windows PowerShell ISE 窗口的顶部，它表示当前停靠安装的加载项工具。 此对象使以下对象可供脚本︰

-   **[$psISE.CurrentVisibleHorizontalTool.Control](The-ISEAddOnTool-Object.md#control)**

-   **[$psISE.CurrentVisibleHorizontalTool.IsVisible](The-ISEAddOnTool-Object.md#isvisible)**

-   **[$psISE.CurrentVisibleHorizontalTool.Name](The-ISEAddOnTool-Object.md#name)**

##  <a name="CurrentVisibleVerticalTool"></a> **$psISE.CurrentVisibleVerticalTool**
 **$PsISE.CurrentVisibleHorizontalTool**对象是[ISEAddOnTool](The-ISEAddOnTool-Object.md)类的实例。 Windows PowerShell ISE 窗口的右边缘向，它表示当前停靠安装的加载项工具。 此对象使以下对象可供脚本︰

-   **[$psISE.CurrentVisibleHorizontalTool.Control](The-ISEAddOnTool-Object.md#control)**

-   **[$psISE.CurrentVisibleHorizontalTool.IsVisible](The-ISEAddOnTool-Object.md#isvisible)**

-   **[$psISE.CurrentVisibleHorizontalTool.Name](The-ISEAddOnTool-Object.md#name)**

##  <a name="Options"></a> **$psISE.Options**
 **$PsISE.Options**对象使以下对象可供脚本︰

-   **[$psISE.Options.AutoSaveMinuteInterval](The-ISEOptions-Object.md#asmi)**

-   **[$psISE.Options.ConsolePaneBackgroundColor](The-ISEOptions-Object.md#cpbc)**

-   **[$psISE.Options.ConsolePaneTextForegroundColor](The-ISEOptions-Object.md#conpfc)**

-   **[$psISE.Options.ConsolePaneTextBackgroundColor](The-ISEOptions-Object.md#conptbc)**

-   **[$psISE.Options.ConsoleTokenColors](The-ISEOptions-Object.md#contc)**

-   **[$psISE.Options.DebugBackgroundColor](The-ISEOptions-Object.md#dbc)**

-   **[$psISE.Options.DebugForegroundColor](The-ISEOptions-Object.md#dfc)**

-   **[$psISE.Options.DefaultOptions](The-ISEOptions-Object.md)**

-   **[$psISE.Options.ErrorBackgroundColor](The-ISEOptions-Object.md#ebc)**

-   **[$psISE.Options.ErrorForegroundColor](The-ISEOptions-Object.md#efc)**

-   **[$psISE.Options.FontName](The-ISEOptions-Object.md#fn)**

-   **[$psISE.Options.Fontsize](The-ISEOptions-Object.md#fs)**

-   **[$psISE.Options.IntellisenseTimeoutInSeconds](The-ISEOptions-Object.md#itis)**

-   **[$psISE.Options.MRUCount](The-ISEOptions-Object.md#mc)**

-   **[$psISE.Options.ScriptPaneBackgroundColor](The-ISEOptions-Object.md#spbc)**

-   **[$psISE.Options.ScriptPaneForegroundColor](The-ISEOptions-Object.md#spfc)**

-   **[$psISE.Options.SelectedScriptPaneState](The-ISEOptions-Object.md#ssps)**

-   **[$psISE.Options.ShowDefaultSnippets](The-ISEOptions-Object.md#sds)**

-   **[$psISE.Options.ShowIntellisenseInConsolePane](The-ISEOptions-Object.md#siicp)**

-   **[$psISE.Options.ShowIntellisenseInScriptPane](The-ISEOptions-Object.md#siisp)**

-   **[$psISE.Options.ShowLineNumbers](The-ISEOptions-Object.md#sln)**

-   **[$psISE.Options.ShowOutlining](The-ISEOptions-Object.md#so)**

-   **[$psISE.Options.ShowToolBar](The-ISEOptions-Object.md#stb)**

-   **[$psISE.Options.ShowWarningBeforeSavingOnRun](The-ISEOptions-Object.md#swbsor)**

-   **[$psISE.Options.ShowWarningForDuplicateFiles](The-ISEOptions-Object.md#swfdf)**

-   **[$psISE.Options.TokenColors](The-ISEOptions-Object.md#tc)**

-   **[$psISE.Options.UseEnterToSelectConsolePaneIntellisense](The-ISEOptions-Object.md#uetsicpi)**

-   **[$psISE.Options。 UseEnterToSelectScriptPaneIntellisense](The-ISEOptions-Object.md#uetsispi)**

-   **[$psISE.Options.UseLocalHelp](The-ISEOptions-Object.md#ulh)**

-   **[$psISE.Options.VerboseBackgroundColor](The-ISEOptions-Object.md#vbc)**

-   **[$psISE.Options.VerboseForegroundColor](The-ISEOptions-Object.md#vfc)**

-   **[$psISE.Options.WarningBackgroundColor](The-ISEOptions-Object.md#wbc)**

-   **[$psISE.Options.WarningForegroundColor](The-ISEOptions-Object.md#wfc)**

-   **[$psISE.Options.XmlTokenColors](The-ISEOptions-Object.md#xtc)**

-   **[$psISE.Options.Zoom](The-ISEOptions-Object.md#z)**

##  <a name="PowerShellTabs"></a> **[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)**
 **$PsISE.PowerShellTabs**对象是[PowerShellTabCollection](The-PowerShellTabCollection-Object.md)类的实例。 它是所有当前打开的 PowerShell 选项卡表示本地计算机上或连接在远程计算机上运行环境可用的 Windows PowerShell 的集合。 集合中的每个成员都[PowerShellTab](The-PowerShellTab-Object.md)类的实例。

## 另请参阅
 [Windows PowerShell ISE 脚本对象模型](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
 [Windows PowerShell ISE 对象模型参考](Windows-PowerShell-ISE-Object-Model-Reference.md)

