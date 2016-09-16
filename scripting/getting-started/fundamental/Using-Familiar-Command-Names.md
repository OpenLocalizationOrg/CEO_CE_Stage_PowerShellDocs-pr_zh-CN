---
title: "使用熟悉的命令名称"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 021e2424-c64e-4fa5-aa98-aa6405758d5d
ms.openlocfilehash: 9d112f8fb56f1cf30463a747ed19e68a3ef8a15d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用熟悉的命令名称
使用机制称为*别名*，Windows PowerShell 允许用户通过备用名称引用的命令。 别名允许其他外壳以重复使用它们已经知道在 Windows PowerShell 执行类似的操作的常见命令名称中的用户体验。 虽然我们不讨论详细的 Windows PowerShell 的别名，随着您开始使用 Windows PowerShell，但您仍然可以使用它们。

别名将在您键入的命令名称与另一个命令相关联。 例如，Windows PowerShell 具有名为清除输出窗口的**清除主机**内部函数。 如果您在命令提示符下键入**cls**或**清除**命令，将解释 Windows PowerShell，这是**清除主机**函数的别名，并运行**清除主机**函数。

此功能可帮助用户了解 Windows PowerShell。 首先，大多数 Cmd.exe 和 UNIX 用户具有大型指令的命令的用户已经知道按名称，并且虽然的 Windows PowerShell 等效可能不会产生相同的结果，但它们是关闭窗体，用户可以使用它们以执行工作而不必首先记住的 Windows PowerShell 名称中。 其次，当用户已经熟悉了另一个 shell，学习新 shell 挫折的主要源是引起"手指内存"错误。 如果您已使用 Cmd.exe 年来，当您具有完整的输出屏幕，并且想要其清理，您将 reflexively 键入**cls**命令并按 ENTER 键。 Windows PowerShell 中**清除主机**函数的别名，不只会收到错误消息"**'cls' 无法识别为 cmdlet、 函数、 操作程序或脚本文件。**" 和会留下执行不知道要清除输出。

下面是您可以使用 Windows PowerShell 内的常用 Cmd.exe 和 UNIX 命令的简短列表︰

|||||
|-|-|-|-|
|猫|dir|安装|rm|
|cd|回声|移动|rmdir|
|chdir|擦除|popd|休眠|
|清除|h|ps|排序|
|cls|历史记录|pushd|t 型|
|复制|终止|密码|类型|
|del|lp|r|编写|
|比较|ls|ren||

如果您发现自己 reflexively 使用以下命令之一，并且想要了解本机 Windows PowerShell 命令的实际名称，您可以使用**获取别名**命令︰

```
PS> Get-Alias cls

CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

若要使示例更易于阅读，Windows PowerShell 的用户指南通常避免使用别名。 但是，了解更多有关别名这早期仍可如果您正在使用的其他来源的 Windows PowerShell 代码的任意段或想要定义您自己的别名。 此部分中的其余部分将讨论标准别名以及如何定义自己的别名。

### 有关如何解读标准别名
别名上述，旨在与其他接口名称兼容性，这与 Windows PowerShell 中内置的别名通常专为赘述。 这些较短名称键入的快速，但无法读取是否您不知道他们的参考。

Windows PowerShell 尝试更加清晰明了且赘述之间有损通过提供一组标准基于常见动词和名词的简略表示法名称的别名。 这样，当您知道速记名称是可读的常见 cmdlet 的别名的一组的核心。 例如，在标准别名**获取**动词缩写为**g**，**设置**动词缩写为**s**，名词**项目**缩写为**i**、**位置**缩写为**l**，名词和名词命令缩写为**厘米**。

下面是一个简短的示例，以说明所做的工作方式。 获取和**i**组合**g**各项的来自获取项目的标准别名︰ **gi**。 为项目设置和**i**组合**s**来自设置项目的标准别名︰ **si**。 获取和**l**的**g**组合的位置，**总**来自获取位置的标准别名。 对于位置， **sl**设置和**l**组合**s**来自设置位置的标准别名。 获取和**厘米**组合**g**各的命令， **gcm**来自获取命令的标准别名。 没有设置命令 cmdlet，但如果没有，我们将能够猜测的标准别名来自**s**设置和**厘米**的命令︰ **scm**。 此外，人员熟悉 Windows PowerShell 别名遇到**scm**者将能够猜测别名指 Set 命令。

### 创建新的别名
您可以创建自己的别名使用集别名 cmdlet。 例如，以下语句创建标准 cmdlet 别名解释标准别名所述︰

```
Set-Alias -Name gi -Value Get-Item
Set-Alias -Name si -Value Set-Item
Set-Alias -Name gl -Value Get-Location
Set-Alias -Name sl -Value Set-Location
Set-Alias -Name gcm -Value Get-Command
```

内部，Windows PowerShell 使用命令在启动时，以下类似，但这些别名不是指。 如果您尝试实际执行的下列命令之一，您将收到错误说明别名不能修改。 例如︰

<pre>PS > 设置别名-名称 gi-值获取项目设置别名︰ 别名不可写入，因为别名 gi 是只读或常量，而不能写入。
在行︰ 1 char: 10 + 集别名 <<<<-名称 gi-值获取项目</pre>

