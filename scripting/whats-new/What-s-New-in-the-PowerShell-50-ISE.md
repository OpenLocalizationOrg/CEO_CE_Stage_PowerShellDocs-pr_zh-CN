---
title: "哪些 s 中的新增功能 50 的 PowerShell ISE"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: d6b8f3710afea9b72771979c4e842b7e4b3c4c96
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 什么和 #39; 中 Windows PowerShell ISE 的新增功能
本主题介绍版本的 Windows PowerShell® 集成脚本环境 (ISE) 中引入了新的和更新功能。

## <a name="overview"></a>功能说明
Windows PowerShell ISE 是一个主机应用程序，使您能够编写、 运行和图形和直观环境中测试脚本和模块。 完成、 直观的调试、 Unicode 合规性和上下文相关帮助关键功能，如语法突出显示选项卡上提供了丰富的脚本体验。

Windows PowerShell ISE 的概述，请参阅[Windows PowerShell 集成脚本环境概述](https://technet.microsoft.com/en-us/library/3c1892c2-bf84-4cb6-af26-1f453be9e671)。

## <a name="versions"></a>Windows PowerShell ISE 中的新增功能和更改功能
下表列出了此版本的 Windows PowerShell ISE Windows PowerShell 中的新增和已更改的功能。

|功能中的功能|Windows PowerShell 4.0 ISE|Windows PowerShell 3.0 ISE|Windows PowerShell 2.0 ISE|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|**[IntelliSense](#BKMK_Intellisense)**|X|X||
|**[代码段](#bkmk_snippets)**|X|X||
|**[加载项工具](#BKMK_AddOnTools)**|X|X||
|**[重新启动管理器和自动保存](#BKMK_RestartMgr)**|X|X||
|**[控制台窗格](#BKMK_ConsolePane)**|X|X||
|**[最近使用的列表](#BKMK_MRU)**|X|X||
|**[命令行开关](#BKMK_CommandLine)**|X|X||
|**[编辑器的新增功能](#BKMK_NewEditorFeatures)**|X|X||
|**[新帮助查看器窗口](#BKMK_NewHelpViewer)**|X|X||
|**[显示命令 cmdlet](#BKMK_ShowCommand)**|X|X||

### <a name="BKMK_Intellisense"></a>IntelliSense
**添加了 ISE 3.0**

IntelliSense 是 Windows PowerShell ISE 的一部分自动完成助手功能。 IntelliSense 显示可能匹配 cmdlet、 参数、 参数值、 文件或文件夹，当您键入可单击的菜单。

**此更改添加哪些值？**

使用智能感知增加，很方便地使用 Windows PowerShell ISE 创建脚本时发现 cmdlet 和语法。 您可以使用 Windows PowerShell ISE 若要了解 Windows PowerShell，同时创建新的脚本。

**内容的工作方式？**

当您键入 cmdlet 在 Windows PowerShell ISE 3.0 或更高版本时，可滚动和可单击菜单显示时，允许您通过浏览找到并选择相应的命令。

### <a name="BKMK_Snippets"></a>代码段
**添加了 ISE 3.0**

*段*是代码的 Windows PowerShell，您可以插入到您在 Windows PowerShell ISE 中创建的脚本的一小部分。 Windows PowerShell ISE 附带一组默认的代码段。 您可以通过使用 Windows PowerShell ISE 中工作时**新建段**cmdlet 添加段。

**此更改添加哪些值？**

通过使用代码段，您可以快速收集和创建脚本来自动处理您的环境。

**内容的工作方式？**

在 Windows PowerShell 3.0 或更高版本，在**编辑**菜单上，请使用段，单击**开始段**，或按**Ctrl J**。

### <a name="BKMK_AddOnTools"></a>加载项工具
**添加了 PowerShell 3.0**

Windows PowerShell ISE 现在支持加载项工具，通过使用对象模型添加的 Windows Presentation Foundation (WPF) 控件。 加载项工具可以作为垂直或水平窗格控制台中显示。 多个加载项工具窗格中的显示为选项卡式控件。 您也可以添加或删除加载项工具所产生的非 Microsoft 方。 有关如何导入或删除加载项工具的详细信息，请参阅[Windows PowerShell ISE 操作](http://technet.microsoft.com/library/cc732148.aspx)。

**此更改添加哪些值？**

加载项允许您扩展和自定义工具，可以增强您脚本的体验，或将功能添加到 Windows PowerShell ISE 的 Windows PowerShell ISE。

**内容的工作方式？**

Windows PowerShell ISE 3.0 和更高版本附带**命令**加载项。 **命令**加载项允许您浏览 cmdlet，并访问有关 cmdlet 通过并行与**脚本**和**控制台**窗格的帮助。

通过**加载项**菜单上的**打开加载项工具网站**命令找不到其他加载项。

### <a name="BKMK_RestartMgr"></a>重新启动管理器和自动保存
**添加了 PowerShell 3.0**

Windows PowerShell ISE 现在将自动保存您打开脚本每隔两分钟在单独的位置。  如果 Windows PowerShell ISE 停止工作，或如果操作系统重新启动时，重新启动 Windows PowerShell ISE 后，它将恢复已的脚本打开上次会话，即使未保存的脚本。

若要更改的自动保存间隔，在控制台窗格中运行以下命令︰ **$psise。Options.AutoSaveMinuteInterval**。

**此更改添加哪些值？**

了解您打开脚本会自动保存在意外重新启动 Windows PowerShell ISE 内，您现在可以工作。

**内容的工作方式？**

Windows PowerShell ISE 2.0 不会保存在重新启动时自动脚本。

### <a name="BKMK_MRU"></a>最近使用的列表
**添加了 PowerShell 3.0**

Windows PowerShell ISE 现在具有最近使用的文件列表。 当您在 Windows PowerShell ISE 打开文件时，文件将添加到**文件**菜单上的最近使用列表中。

要更改最近使用的列表中的文件的默认数，请在控制台窗格中运行以下命令︰ **$psise。Options.MruCount**。

**此更改添加哪些值？**

您现在可以使用最近使用的列表轻松访问您经常使用的文件。

**内容的工作方式？**

Windows PowerShell ISE 2.0 没有最近使用的列表。

### <a name="BKMK_ConsolePane"></a>控制台窗格
**添加了 PowerShell 3.0**

单独的命令和 Windows PowerShell ISE 首次发布中提供的输出窗格具有已合并到单个控制台窗格。 控制台窗格中的功能和外观的典型的 Windows PowerShell 控制台类似，但它包括以下增强功能 （最描述了本主题中）。

-   输入文本 （不输出文本） 的语法突出显示包括 XML 语法

-   IntelliSense

-   大括号匹配

-   错误的含义

-   完整的 Unicode 支持

-   **F1**上下文相关帮助

-   **按 Ctrl + F1**上下文相关显示命令

-   复杂脚本和从右向左的支持

-   字体支持

-   缩放

-   行选择和块选择模式

-   保留在命令行时按**向上**箭头以查看历史记录控制台中键入内容

**此更改添加哪些值？**

增加了这些控制台窗格中更改提供了与控制台界面更一致的脚本体验。

**内容的工作方式？**

Windows PowerShell ISE 2.0 具有单独的命令和输出窗格。

### <a name="BKMK_CommandLine"></a>命令行开关
**添加了 PowerShell 3.0**

如果您从命令行中启动 Windows PowerShell ISE （通过键入**powershell_ise.exe**），您可以添加以下的新命令行开关。

-   *-NoProfile*︰ 不运行**$profile**启动 Windows PowerShell ISE

-   *-帮助*︰ 显示帮助窗口

-   *mta*︰ 在多线程的单元模式下启动 Windows PowerShell ISE。 Windows PowerShell ISE 的默认操作模式是单线程单元模式或*-sta*。

**此更改添加哪些值？**

这些命令行开关添加允许您控制 Windows PowerShell ISE 的运行的环境。

**内容的工作方式？**

Windows PowerShell ISE 2.0 无法识别这些命令行开关。

### <a name="BKMK_NewEditorFeatures"></a>编辑器的新增功能
**添加了 PowerShell 3.0**

其他 Windows PowerShell ISE 编辑功能包括︰

-   **XML 语法着色**Windows PowerShell ISE 现在颜色 XML 语法以相同方式为其颜色的 Windows PowerShell 语法。

-   **大括号匹配**Windows PowerShell ISE 包括括号匹配和突出显示，并且可以通过以下方式使用: (例如，使用**转到匹配项**命令或**Ctrl +]**定位右大括号，如果您有一个选定的左大括号)。

-   **大纲视图**脚本窗格支持分级显示，它允许折叠或展开代码段，通过单击加号或减号在左页边距。 您可以使用括号或**#region**和**#endregion**标记标记开头或结尾的可折叠部分。 要展开或折叠所有地区，请按**Ctrl + M**。

-   **拖放编辑文本**Windows PowerShell ISE 现在支持拖放编辑文本。 您可以选择任何文本块，并将该文本拖到编辑器或控制台来移动文本中的其他位置。 如果按住 Ctrl 键的同时拖动所选的文本，释放鼠标按钮时文本会被复制到新位置中。 在此版本的 Windows PowerShell ISE，以及早期版本的 Windows PowerShell ISE，当您拖放文件拖动到 Windows PowerShell ISE，Windows PowerShell ISE 打开文件。

-   **分析错误值显示**分析用红色下划线表示错误。 当您将鼠标悬停在指定的错误时，工具提示文本将显示在代码中找到的问题。

-   **缩放**通过使用 （在右下角的 Windows PowerShell ISE 窗口），显示比例滑块或输入控制台窗格中的命令**$psise.options.Zoom** ，可以设置的控制台的内容的缩放比例。

-   **格式文本复制和粘贴**复制到剪贴板中的 Windows PowerShell ISE 保留字体、 字号和颜色原始所选内容的信息。

-   **阻止所选内容**通过使用鼠标，脚本窗格中选择文本的同时按住 ALT 键或按**Alt + Shift + 箭头**，您可以选择文本块。

**此更改添加哪些值？**

附加的编辑功能提供更一致且功能强大的编辑环境。

**内容的工作方式？**

这些编辑的增强功能是否定的 Windows PowerShell ISE 2.0 中存在。

### <a name="BKMK_NewHelpViewer"></a>新帮助查看器窗口
**添加了 PowerShell 3.0**

如果您的光标位于 cmdlet，或突出显示 cmdlet 的一部分时按**F1** ，新帮助查看器将打开有关突出显示的 cmdlet 的上下文相关帮助。 若要显示 Windows PowerShell 有关帮助，请在控制台窗格中，键入**运算符**，然后按**F1**。

使用此功能之前，请从 Microsoft 网站下载最新版本的 Windows PowerShell 帮助主题。 下载帮助主题的最简单方法是**更新帮助**cmdlet 运行控制台窗格中，以管理员身份运行 Windows PowerShell ISE 时。

您可以更改**F1**键查找帮助。 在**工具**中/**选项**菜单中，在**常规设置**选项卡上的**其他设置**，您可以设置或清除**使用本地帮助内容，而不是联机内容**复选框。 如果选中此选项，然后客户端查找 cmdlet 位于模块文件夹中下载帮助中的帮助。  如果清除此复选框，则客户端条件查找上 cmdlet 帮助 TechNet 库中。

**此更改添加哪些值？**

上下文相关的帮助，而无需离开您的当前 cmdlet 或脚本提供了无缝学习体验。

**内容的工作方式？**

在早期版本的 Windows PowerShell ISE 中按 F1 打开本地计算机上的帮助文件。 在 Windows PowerShell ISE 3.0 和更高版本，打开一个窗口，其中包含搜索且配置 cmdlet 的帮助。 此帮助体验 for Windows PowerShell ISE 3.0 的新增功能和是 Windows PowerShell 3.0 的新增功能可更新的帮助。

### <a name="BKMK_ShowCommand"></a>显示命令 cmdlet
**添加了 PowerShell 3.0**

**显示命令**cmdlet 使您能够通过填写以图形方式来运行 cmdlet 或函数或撰写。 窗体允许用户在图形环境中使用 Windows PowerShell。 **显示命令**还将允许高级脚本专家创建快速的基于 Windows PowerShell GUI。

**此更改添加哪些值？**

通过使用 Windows PowerShell 脚本中**显示命令**，您可以向用户提供熟悉它们是图形环境。 **显示命令**还有助于介绍性的用户了解 Windows PowerShell。

**内容的工作方式？**

显示命令为新的 Windows PowerShell ISE 3.0。

## <a name="BKMK_LINKS"></a>另请参阅
有关在 Windows PowerShell 中使用 Windows PowerShell ISE 的详细信息，请参阅下面的链接。

-   [使用 Windows PowerShell 集成脚本环境](../core-powershell/ise/Using-the-Windows-PowerShell-ISE.md)

-   [在 TechNet Wiki ISE](http://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)

-   [脚本中心](http://technet.microsoft.com/scriptcenter/default)

