---
title: "PowerShell.exe 命令行帮助"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 8a8e3a0e3d45fb0441c1bf5fd9a72e0097aafd87
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# PowerShell.exe 命令行帮助
启动 Windows PowerShell 会话。 可以使用 PowerShell.exe 从命令行中的另一种工具，如 Cmd.exe，启动 Windows PowerShell 会话，或使用它在 Windows PowerShell 命令行以开始新会话。 使用参数以自定义会话。

## 语法

```
PowerShell[.exe]
       [-EncodedCommand <Base64EncodedCommand>]
       [-ExecutionPolicy <ExecutionPolicy>]
       [-InputFormat {Text | XML}] 
       [-Mta]
       [-NoExit]
       [-NoLogo]
       [-NonInteractive] 
       [-NoProfile] 
       [-OutputFormat {Text | XML}] 
       [-PSConsoleFile <FilePath> | -Version <Windows PowerShell version>]
       [-Sta]
       [-WindowStyle <style>]
       [-File <FilePath> [<Args>]]
       [-Command { - | <script-block> [-args <arg-array>]
                     | <string> [<CommandParameters>] } ]

PowerShell[.exe] -Help | -? | /?
```

## 参数

### -EncodedCommand <Base64EncodedCommand>
接受 64 编码的字符串版本的命令。 此参数用于提交到 Windows PowerShell 需要复杂的引号或大括号的命令。

### -ExecutionPolicy <ExecutionPolicy>
将默认执行策略设置为当前会话并将其保存在 $env: PSExecutionPolicyPreference 环境变量。 此参数不会更改注册表中设置 Windows PowerShell 执行策略。 有关 Windows PowerShell 执行策略，包括有效的值的列表的信息，请参阅 about_Execution_Policies (http://go.microsoft.com/fwlink/?LinkID=135170)。

### -File <FilePath> \[<Parameters>]
运行指定的脚本在本地范围 （"点-来源"），以便函数和脚本创建的变量当前会话中可用。 输入的脚本文件路径和任何参数。 **文件**必须命令中的最后一个参数，因为所有字符都键入后**文件名参数**将被解释为后跟脚本参数和相应的值的脚本文件路径。

您可以在**文件**参数的值包括一个脚本，以及参数值的参数。 例如︰ `-File .\Get-Script.ps1 -Domain Central`

通常情况下的脚本切换参数是包含或省略。 例如，以下命令使用获取 Script.ps1 脚本文件的**所有**参数︰ `-File .\Get-Script.ps1 -All`

在出现次数较少的情况下，可能需要切换参数提供的布尔值。 **文件**参数的值中的切换参数提供一个布尔值，参数名称和值弯大括号括起来，如下所示︰ `-File .\Get-Script.ps1 {-All:$False}`

### -InputFormat {文本 |XML}
介绍数据发送到 Windows PowerShell 的格式。 有效值"文本"（文本字符串） 或"XML"（序列化 CLIXML 格式）。

### Mta
使用多线程的单元启动 Windows PowerShell。 Windows PowerShell 3.0 中引入了此参数。 在 Windows PowerShell 3.0，单线程单元 (STA) 是默认值。 在 Windows PowerShell 2.0 中，多线程的单元 (MTA) 是默认值。

### -NoExit
未运行启动命令之后退出。

### -NoLogo
隐藏启动版权标志。

### -交互式
不向用户显示交互式的提示。

### -NoProfile
不会加载 Windows PowerShell 配置文件。

### -OutputFormat {文字 |XML}
确定如何设置从 Windows PowerShell 的输出格式。 有效值"文本"（文本字符串） 或"XML"（序列化 CLIXML 格式）。

### -PSConsoleFile <FilePath>
加载指定的 Windows PowerShell 控制台文件。 输入路径和控制台文件的名称。 若要创建控制台文件，请使用 Windows PowerShell 中[导出控制台](https://technet.microsoft.com/en-us/library/4bab1c02-9e61-4aaf-9957-11d1934ef4ef)cmdlet。

### -Sta
使用单线程单元启动 Windows PowerShell。 在 Windows PowerShell 3.0，单线程单元 (STA) 是默认值。 在 Windows PowerShell 2.0 中，多线程的单元 (MTA) 是默认值。

### 版本 <Windows PowerShell Version>
启动指定的版本的 Windows PowerShell。 在系统上必须安装您指定的版本。 如果在计算机上安装 Windows PowerShell 3.0，有效的值为"2.0"和"3.0"。 默认值为"3.0"。

如果未安装 Windows PowerShell 3.0，则仅有效的值为"2.0"。 其他值将被忽略。

有关详细信息，请参阅[开始使用 Windows PowerShell [旧 MSDN]](https://technet.microsoft.com/en-us/library/69555d95-b481-43e1-86e7-b46d68b3e2dd)中的"安装 Windows PowerShell"。

### -WindowStyle <Window style>
设置会话窗口样式。 有效值为普通、 最小化、 最大化和隐藏。

### 命令
执行指定的命令 （以及任何参数），就好像它们在 Windows PowerShell 命令提示符处，键入，然后退出，除非指定 NoExit 参数。

命令的值可以是"-"，字符串。 或脚本块。 如果命令的值为"-"，从标准输入读取命令文本。

脚本块必须括在括号 （{}）。 只有当在 Windows PowerShell 运行 PowerShell.exe，您可以指定脚本块。 脚本的结果返回到父 shell 为反序列化的 XML 对象，不活动的对象。

如果命令的值为一个字符串，**命令**必须是命令中的最后一个参数，因为该命令将被解释为命令参数后键入的任何字符。

要编写一个字符串，运行 Windows PowerShell 命令，请使用格式:

```
"& {<command>}"
```

其中双引号指示字符串和调用运算符 (&) 使执行命令。

### 帮助，-？，/？
显示此消息。 Windows PowerShell 中键入 PowerShell.exe 命令时，如果在前面添加的命令参数用连字符 （-），不正斜杠 （/）。 您可以使用连字符或正斜杠 Cmd.exe 中。

> [!NOTE]
> 疑难解答注意︰ 在 Windows PowerShell 2.0 中，从开始控制台失败 Windows PowerShell 中的某些程序 0xc0000142 LastExitCode。

## 示例

```
PowerShell -PSConsoleFile sqlsnapin.psc1

PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

PowerShell -Command {Get-EventLog -LogName security}

PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```

