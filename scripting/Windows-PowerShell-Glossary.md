---
title: "Windows PowerShell 词汇表"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: b0f88cbe-cb83-4912-a301-184534cb35c7
ms.openlocfilehash: 9e5bb79b0d022b85441f5f6aab2f8cce141fe9c1
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows PowerShell 词汇表


|术语|定义|
|--------|--------------|
|二进制模块|Windows PowerShell 模块其根模块是模块二进制文件 (.dll)。 二进制模块可能或不包含模块清单。|
|常见的参数|将参数添加到所有的 cmdlet 和高级功能通过 Windows PowerShell 引擎。|
|点源|在 Windows PowerShell，开始键入使用句点和命令前的一个空格命令。 在新的作用域而不是当前范围内运行命令的来源的点。 任何变量、 别名、 函数或驱动器命令创建当前范围内创建和可供用户在此命令完成。|
|动态模块|内存中仅存在一个模块。 新建模块和导入 PSSession cmdlet 创建动态模块。|
|动态参数|将参数添加到 Windows PowerShell cmdlet、 函数或在某些情况下的脚本。 Cmdlet、 函数、 提供商和脚本可以添加动态参数。|
|设置文件格式|Windows PowerShell XML 文件包含。 format.ps1xml 扩展名以及定义 Windows PowerShell 基于其.NET Framework 类型的对象的显示方式。|
|全局会话状态|包含数据的 Windows PowerShell 会话的用户可以访问会话状态。|
|主机|Windows PowerShell 引擎使用与用户进行通信界面。 例如，主机指定提示 Windows PowerShell 和用户之间的处理方式。|
|宿主应用程序|将 Windows PowerShell 引擎加载到其进程并使用它来执行操作的程序。|
|输入处理方法|作为输入接收 cmdlet 可用于处理的记录的方法。 输入的处理方法包括 BeginProcessing 方法、 ProcessRecord 方法、 EndProcessing 方法和 StopProcessing 方法。|
|清单模块|Windows PowerShell 模块具有的清单和其 ModulesToProcess 键为空。|
|模块清单|Windows PowerShell 数据文件 (.psd1)，描述模块的内容和控制如何处理模块。|
|模块会话状态|会话状态包含公钥和私钥 Windows PowerShell 模块的数据。 在此会话状态的私有数据不适用于 Windows PowerShell 会话的用户。|
|非终止错误|不会继续处理命令停止 Windows PowerShell 错误。|
|名词|后面的 Windows PowerShell cmdlet 名称连字符的单词。 名词描述的资源在其 cmdlet 作用。|
|参数集|一组可用于在相同的命令执行特定操作的参数。|
|管道|在 Windows PowerShell，以用作输入管道中下一个命令发送前面的命令的结果。|
|渠道|一系列通过管道运算符 (& #124;) 连接的命令(ASCII 124)。 每个渠道运算符作为下一步命令输入发送前面的命令的结果。|
|PSSession|创建、 管理和用户关闭 Windows PowerShell 会话的类型。|
|根模块|在模块清单中 ModuleToProcess 项中指定的模块。|
|运行空间|在 Windows PowerShell，在其中执行管道中的每个命令的操作环境。|
|脚本块|在 Windows PowerShell 的编程语言、 语句或可作为单个单元的表达式的集合。 脚本块可以接受参数和返回值。|
|脚本模块|Windows PowerShell 模块其根模块是脚本模块文件 (.psm1)。 脚本模块可能或不包含模块清单。|
|脚本模块文件|包含 Windows PowerShell 脚本文件。 脚本定义脚本模块导出的成员。 脚本模块文件具有.psm1 文件扩展名。|
|shell|用于将命令传递给操作系统的命令解释。|
|切换参数|不带参数的参数。|
|终止错误|停止处理命令 Windows PowerShell 错误。|
|事务|工时原子单位。 在事务中的工作，必须完成整个;如果事务的任何部分失败，整个事务失败。|
|文件类型|Windows PowerShell XML 文件具有.ps1xml 扩展名的和扩展的 Windows PowerShell 中的 Microsoft.NET Framework 类型的属性。|
|动词|在 Windows PowerShell cmdlet 名称前连字符的单词。 动词介绍 cmdlet 执行的操作。|
|Windows PowerShell|命令行界面和基于任务的脚本提供技术 IT 管理员全面控制和系统的自动化管理任务。|
|Windows PowerShell 命令|管线中的元素，导致要执行的操作。 Windows PowerShell 命令在键盘上键入，或者以编程方式调用。|
|Windows PowerShell 数据文件|具有.psd1 文件扩展名的文本文件。 Windows PowerShell 用于各种用途，例如存储模块清单数据和存储脚本国际化翻译的字符串数据文件。|
|Windows PowerShell 驱动器|可以直接访问数据存储虚拟驱动器。 可以通过 Windows PowerShell 提供程序定义或创建在命令行。 在命令行创建驱动器会话特定驱动器，关闭会话时将丢失。|
|Windows PowerShell 集成脚本环境 (ISE)|Windows PowerShell 宿主应用程序，使您可以运行命令以及编写、 测试和调试脚本友好的语法突出显示符合 Unicode 环境中。|
|Windows PowerShell 模块|允许您分区、 组织和抽象 Windows PowerShell 代码是自包含可重用单元。 模块可以包含 cmdlet、 提供商，函数、 变量和其他类型的可以作为单个单元导入的资源。|
|Windows PowerShell 提供商|Microsoft.NET Framework 基于程序使数据专用的数据存储在 Windows PowerShell 中可用，以便您可以查看并对其进行管理。|
|Windows PowerShell 脚本|Windows PowerShell 语言编写脚本。|
|Windows PowerShell 脚本文件|具有.ps1 扩展名的并包含在 Windows PowerShell 语言编写的脚本文件。|
|Windows PowerShell 管理单元中|定义一组 cmdlet、 提供商和可以添加到 Windows PowerShell 环境的 Microsoft.NET Framework 类型的资源。|
|Windows PowerShell 工作流|工作流是一系列编程、 已连接的步骤执行长时间运行任务或跨多个设备或托管的节点需要协调的多个步骤。 Windows PowerShell 工作流允许 IT 专业人士和开发人员创作多设备管理活动或在工作流，为工作流的单个任务的序列。 Windows PowerShell 工作流允许您适应作为工作流运行 Windows PowerShell 脚本和 XAML 文件。|

