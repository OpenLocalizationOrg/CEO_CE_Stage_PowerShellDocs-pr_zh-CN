---
title: "Windows PowerShell ISE 的脚本环境的集成"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: f156b92d-0203-46d2-89c7-b4989d32e3d2
ms.openlocfilehash: 2d58a63b14ae1ef98a77ef6b9bdb9183f1f2941f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows PowerShell 集成脚本环境 (ISE)
Windows PowerShell 集成脚本环境 (ISE) 是用于 Windows PowerShell 引擎和语言的两个主机之一。 您可以与之编写、 运行和测试脚本在 Windows PowerShell 控制台中不可用的方式。 ISE 添加语法突出显示、 选项卡上完成、 IntelliSense、 可视调试和上下文相关的帮助。

ISE 允许您运行命令控制台窗格中，但它还支持可用于同时查看您的脚本和其他工具可插入 ISE 源代码的窗格。 您可以即使打开了多个脚本 windows，同时，调试脚本使用其他脚本或模块中定义的函数时是非常有帮助。

## <a name="BKMK_NEW"></a>新增功能
以下是一些已添加到最新版本的 PowerShell ISE 的功能。

### 添加了 PowerShell 3.0 （Windows Server 2012、 Windows 8）
**IntelliSense**自动完成您的命令，通过在键入时显示的匹配 cmdlet、 参数、 参数值、 文件或文件夹的菜单。

**段**是代码的短，您可以轻松地插入到脚本你编写段。 在框中包括有用的代码段的集合中，可以使用**新建代码段**cmdlet 的更多。

通过编写使用[Windows PowerShell ISE 脚本对象模型](https://technet.microsoft.com/en-us/library/dd819478.aspx)交互的代码，可以创建将功能添加到 ISE 的**加载项工具**。 这些工具可以在选项卡式窗格中显示控件或在后台不可见的方式工作。 **命令**加载项是一个很好示例附带版本 3.0 和更高版本，将显示可用的命令和其帮助的列表。

**重新启动管理器和自动保存**自动保存您的脚本每隔两分钟可帮助您避免在发生崩溃或意外重新启动您的工作丢失。

**最近使用过的列表**现在是打开文件菜单上，以使其更方便地访问最常使用的文件的一部分。

**合并控制台窗格**。 在早期版本的 ISE 没有独立的命令和输出窗格。 他们将立即合并为一个窗格的详细信息直接模仿 Windows Powershell 控制台中看到的内容。

**命令行开关**。 多个新的命令行开关为您提供更好地控制 ISE 的工作的方式。 -NoProfile 启动 ISE 不运行的配置文件脚本。 -帮助打开包含 ISE 的帮助窗口。 -mta 启动 ISE 中"多线程的单元模式"。 默认为单线程。

**编辑器的新功能**，使其更轻松地创建和读取代码︰

-   **XML 语法着色**。 ISE 编辑器现在颜色 XML 语法以相同方式为其颜色的 Windows PowerShell 代码语法。

-   **大括号匹配**。 ISEWindows PowerShell ISE 突出显示匹配的大括号，以帮助您确保您有右大括号，以匹配您打开的数量是否正确的。 使用 CTRL-\[以找到右大括号相匹配，光标位于左大括号。

-   **大纲视图**。 可以折叠或展开代码的部分，通过单击加号和减号情况下，在左页边距。 这使得更加轻松地查找您正在寻找在较长的脚本代码。

-   **拖放编辑文本**。 您可以选择文本块，并将其拖动到另一个位置以移动它。 如果按住 Ctrl 键的同时拖动而不是复制所选的文字，移动。

-   **分析错误值显示**。 Windows PowerShell 在键入时检查脚本。 如果检测到错误，它将显示在有问题的代码下红色波浪线。 当您将鼠标悬停在指定的错误时，工具提示将显示找到的问题。

-   **缩放**。 可以放大文本以使其更易于阅读或缩小以查看更大范围 ISE 窗口的右下角中使用的滑块。

-   **格式文本复制和粘贴**。 当从 ISE 复制到剪贴板、 字体、 字号和颜色信息所选文本的是包括在内。

-   **阻止所选内容**。 通过使用鼠标，脚本窗格中选择文本的同时按住 ALT 键或按**Alt + Shift + 箭头**，您可以选择的块状文本块。

### 添加 PowerShell 2.0 （Windows Server 2008 R2、 Windows 7 中
使用 PowerShell 2.0 版引入了 ISE。

## 运行 Windows PowerShell ISE 要求
ISE 是可以运行 Windows PowerShell 2.0 版的任何计算机上可用的图片或更高版本。 每个版本的 Windows 和 Windows Server 包括版本的 Windows PowerShell 和 ISE，但您可以通过安装 Windows Management Framework 升级到最晚可用资源。 运行此搜索以查找最新版本可用︰[下载](http://www.microsoft.com/en-us/search/DownloadResults.aspx?q=%22windows%20management%20framework%22%20PowerShell&sortby=Relevancy~Descending)。 请注意，任何标记为"预览"条目是预发布版的代码不是完整的功能。

> [!NOTE]
> Windows PowerShell ISE 需要图形的用户界面，因为不能在 Windows Server 的服务器核心选项来运行它。

## <a name="BKMK_LINKS"></a>另请参阅
[使用 Windows PowerShell 集成脚本环境](http://technet.microsoft.com/library/cc732148.aspx)

