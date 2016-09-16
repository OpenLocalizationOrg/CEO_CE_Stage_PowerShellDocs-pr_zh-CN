---
title: "其他有用的脚本对象"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 0de024c9d1a5e937d7b985bbf63b1a6dc3654d4a
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 其他有用的脚本对象
  下列对象提供 Windows PowerShell ISE 中的其他脚本功能。 它们不是**$psISE**层次结构的一部分。

## 有用的脚本对象

### $psUnsupportedConsoleApplications
 存在一些限制 Windows PowerShell ISE 与控制台应用程序的交互方式。 要求用户参与自动化脚本或命令可能不起作用从 Windows PowerShell 控制台其工作的方式。 您可能希望阻止这些命令或从 Windows PowerShell ISE 命令窗格中运行脚本。 **$PsUnsupportedConsoleApplications**对象保留此类命令的列表。 如果您尝试运行此列表中的命令，您将获得一条消息，不支持。 以下脚本将某个条目添加到列表。

```
# List the unsupported commands
psUnsupportedConsoleApplications
# Add a command to this list
psUnsupportedConsoleApplications.Add(“Mycommand”)
#Show the augmented list of commands
psUnsupportedConsoleApplications

```

### $psLocalHelp
 这是维护上下文相关帮助主题和相应的本地不支持经过编译的 HTML 帮助文件中的链接之间映射的词典对象。 它用于查找特定主题的本地帮助。 您可以添加或删除此列表中的主题。 下面的代码示例显示一些示例**$psLocalHelp**中包含的键-值对。

```
# See the local help map
$psLocalHelp | Format-List

```

### 输出示例

|||
|-|-|
|键︰ 添加计算机|值︰ WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm|
|键︰ 添加内容|值︰ WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm|

 以下脚本将某个条目添加到列表中。

```
$psLocalHelp.Add("get-myNoun","c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### $psOnlineHelp
 这是维护上下文相关的帮助主题的主题标题和及其关联的外部 Url 之间映射的词典对象。 它用于在 web 上查找特定主题的帮助。 您可以添加或删除此列表中的主题。

```
$psOnlineHelp | Format-List

```

### 示例输出

|||
|-|-|
|键︰ 添加计算机|值︰ http://go.microsoft.com/fwlink/p/?LinkID=135194|
|键︰ 添加内容|值︰ http://go.microsoft.com/fwlink/p/?LinkID=113278|

 以下脚本将某个条目添加到列表中。

```
$psOnlineHelp.Add("get-myNoun","http://www.mydomain.com/MyNoun.html")
```

## 另请参阅
 [Windows PowerShell ISE 脚本对象模型](../../core-powershell/ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  
