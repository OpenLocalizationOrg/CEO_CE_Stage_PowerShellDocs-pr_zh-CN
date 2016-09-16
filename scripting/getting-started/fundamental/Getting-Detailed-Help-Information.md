---
title: "获取详细的帮助信息"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 4333f383d24d3673aab849b17ba3f1eafcf7b1c3
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 获取详细的帮助信息
Windows PowerShell 包括详细介绍了 Windows PowerShell 概念和 Windows PowerShell 语言的帮助主题。 还有为每个 cmdlet 和提供程序的帮助主题和许多函数和脚本帮助主题。

您可以在命令提示符显示这些帮助主题或 Microsoft TechNet 库中查看这些主题的最近已更新的版本。 Windows PowerShell，Windows PowerShell 集成脚本环境中，如托管的许多程序提供更多帮助功能，如上下文相关的帮助，并且编译帮助文件 (.chm)。

## 获取 Cmdlet 的帮助
要获取有关 Windows PowerShell cmdlet 的帮助，请使用[获取帮助 [m2]](https://technet.microsoft.com/en-us/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2) cmdlet。 例如，要用于[获取 ChildItem [m2]](https://technet.microsoft.com/en-us/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc) cmdlet 获取帮助，请键入︰

```
get-help get-childitem
```

或

```
get-childitem -?
```

您甚至可以有关获取帮助 cmdlet 获取帮助。 例如︰

```
get-help get-help
```

要在会话中获取所有 cmdlet 帮助主题的列表，请键入︰

```
get-help -category cmdlet
```

若要一次显示每个帮助主题的一页，使用**帮助**函数或**男人**其别名。 例如，要显示用于获取 ChildItem cmdlet 的帮助，请键入

```
man get-childitem
```

或

```
help get-childitem
```

若要显示有关 cmdlet 的详细的信息，函数或脚本，包括其参数和其使用，示例的说明，请使用获取帮助 cmdlet 的参数的*详细*。 例如，若要获取有关获取 ChildItem cmdlet 的详细的信息，请键入︰

```
get-help get-childitem -detailed
```

若要显示在帮助主题的所有内容，请使用*完整*获取帮助 cmdlet 的参数。 例如，要在获取 ChildItem cmdlet 的帮助主题中显示的所有内容，请键入︰

```
get-help get-childitem -full
```

若要获取有关 cmdlet 的参数的详细帮助使用获取帮助 cmdlet 的参数的*参数*。 例如，以获取详细帮助所有获取 ChildItem cmdlet，类型的参数︰

```
get-help get-childitem -parameter *
```

若要帮助主题中显示的示例，请使用获取帮助的*示例*参数。 例如，若要显示的示例仅在获取 ChildItem cmdlet 的帮助主题，请键入︰

```
get-help get-childitem -examples
```

有关如何编写您撰写的 cmdlet 的帮助主题的信息，请参阅 MSDN 中的"如何向编写 Cmdlet 帮助"主题。

## 获取概念的帮助
获取帮助 cmdlet 也会显示在 Windows PowerShell，包括有关 Windows PowerShell 语言的主题的概念主题的相关信息。 带有"关于"前缀，如 about_line_editing 开始概念的帮助主题。 （概念的主题的名称必须输入英文甚至在非英语版本的 Windows PowerShell。）

若要显示的概念的主题的列表，请键入︰

```
get-help about_*
```

若要显示特定的帮助主题，请键入主题名称，例如︰

```
get-help about_command_syntax
```

获取帮助，如*详细*、*参数*和*示例*，参数不起作用概念的帮助主题的显示屏上。

## 获取有关提供程序的帮助
获取帮助 cmdlet 显示 Windows PowerShell 提供程序的信息。 若要获取有关提供程序的帮助，请键入"获取帮助"后面跟有提供程序的名称。 例如，要注册表提供商获取帮助，请键入︰

```
get-help registry
```

要在会话中获取所有提供商的帮助主题的列表，请键入

```
get-help -category provider
```

获取帮助，如*详细*、*参数*和*示例*，参数有提供程序的帮助主题的显示屏上不起作用。

## 获取有关脚本和函数的帮助
许多脚本和 Windows PowerShell 中的函数都有帮助主题。 获取帮助 cmdlet 用于显示脚本和函数的帮助主题。

若要显示有关函数的帮助，请键入"获取帮助"的函数名后跟。 例如，要禁用 PSRemoting 函数获取帮助，请键入︰

```
get-help disable-psremoting
```

若要显示的脚本的帮助，请键入脚本文件的完全限定的路径。 如果该脚本位于 Path 环境变量中列出的路径，可以忽略命令中的路径。

例如，如果您有一个脚本您 c︰ 中名为"TestScript.ps1"\\PS 测试目录，以显示帮助主题的脚本，类型︰

```
get-help c:\ps-test\TestScript.ps1
```

用于显示帮助信息，如*详细*、*完整*、*示例*和*参数*，cmdlet 的参数适合脚本帮助和函数的帮助，也。 但是，当您显示所有的帮助，请键入"获取帮助\*"、 函数的帮助和脚本不会显示。

有关编写您的函数和脚本的帮助主题的信息，请参阅[about_Functions [m2]](https://technet.microsoft.com/en-us/library/61d40692-5300-4de9-a9b5-bae31815e105)、 [about_Scripts](https://technet.microsoft.com/en-us/library/7dc08334-dcfe-450b-b949-0554855623af)和[about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)。

## 联机获取帮助
如果您已连接到 Internet，之一以获取帮助的最佳方法是查看联机帮助主题。 联机主题可以很容易地更新，因为它们是可能会提供最新内容。

若要获取联机帮助，请尝试*联机*获取帮助 cmdlet 的参数。 获取帮助 cmdlet 的参数的*联机*工作仅适用于 cmdlet 帮助、 函数的帮助和脚本帮助。 您无法使用与*联机*参数概念 （关于） 主题或提供程序的帮助主题。 此外，由于此功能是可选的它不起作用为每个 cmdlet、 函数或脚本帮助主题。

不过，所有的帮助主题，附带有 Windows PowerShell，包括提供程序的帮助和帮助主题 （关于） 概念部分提供了联机[Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116)的 Microsoft TechNet 库。

要使用*联机*获取帮助 cmdlet 的参数，请使用以下命令格式。

```
get-help <command-name> -online
```

例如，要获取有关获取 ChildItem cmdlet 的帮助主题的联机版本，请键入︰

```
get-help get-childitem -online
```

如果可用的帮助主题的联机版本，则它将默认浏览器中打开。

如果联机帮助受支持的帮助主题，您还可以查看帮助主题的 Internet 地址 (URL)。 Internet 地址显示在帮助主题的相关链接部分。

例如，若要查看的 URL 添加计算机 cmdlet 的联机版本，请键入︰

```
get-help add-computer
```

主题的相关链接部分中的第一行如下所示。

```
Online version: http://go.microsoft.com/fwlink/?LinkID=135194
```

有关如何为您的帮助主题提供联机支持信息，请参阅[about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)，并了解"向编写 Cmdlet 帮助"([http://go.microsoft.com/fwlink/?LinkID=123415](http://go.microsoft.com/fwlink/?LinkID=123415)) MSDN （Microsoft 开发人员网络） 库中。

## 另请参阅
[about_Functions [m2]](https://technet.microsoft.com/en-us/library/61d40692-5300-4de9-a9b5-bae31815e105)
[about_Scripts](https://technet.microsoft.com/en-us/library/7dc08334-dcfe-450b-b949-0554855623af)
[about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)
[获取帮助 [m2]](https://technet.microsoft.com/en-us/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2)

