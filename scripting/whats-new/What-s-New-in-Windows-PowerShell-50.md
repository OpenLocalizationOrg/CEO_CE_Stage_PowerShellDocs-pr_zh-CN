---
title: "哪些 s Windows PowerShell 50 中的新增功能"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 1476722e-947e-425d-a86c-50037488dc6e
ms.openlocfilehash: 2a38012830e0f4ab92710b1e70cb4be9a2aedd65
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 什么和 #39; s Windows PowerShell 中的新增功能
Windows PowerShell® 5.0 包含重大扩展其使用，提高其可用性，允许您控制和管理基于 Windows 的环境，更轻松地和全面的新功能。

Windows PowerShell 5.0 向后兼容。 Cmdlet、 提供商、 模块、 单元、 脚本、 函数和通常设计的 Windows PowerShell 4.0、 Windows PowerShell 3.0 和 Windows PowerShell 2.0 的配置文件工作 Windows PowerShell 5.0 而无需更改。

默认情况下，在 Windows Server® 2016年技术预览版和 Windows 10® 上安装 Windows PowerShell 5.0。 若要在 Windows Server 2012 R2、 Windows 8.1 企业级、 或 Windows 8.1 Pro 安装 Windows PowerShell 5.0，请下载并安装[Windows Management Framework 5.0](http://aka.ms/wmf5download)。 请务必阅读下载详细信息，并安装 Windows Management Framework 5.0 之前满足所有的系统要求。

## 本主题中

-   [Windows PowerShell 4.0 DSC KB 3000850 中的更新](#BKMK_3000850)

-   [Windows PowerShell 5.0 中的新增功能](#BKMK_new50)

-   [Windows PowerShell 4.0 中的新增功能](#BKMK_wps4)

-   [Windows PowerShell 3.0 的新增功能](#BKMK_wps3)

## <a name="BKMK_3000850"></a>在 2014 年 11 月的 Windows PowerShell 4.0 更新来更新总成型任务 (KB 3000850)
[2014 年 11 月 Windows RT 8.1、 Windows 8.1 和 Windows Server 2012 R2 的累积更新](https://support.microsoft.com/kb/3000850/)(KB 3000850) 中提供了许多更新和改进到 Windows PowerShell 需要状态配置 (DSC) 在 Windows PowerShell 4.0。 您可以确定是否 KB 3000850 安装在您的系统通过运行`Get-Hotfix -Id KB3000850`Windows PowerShell 中。

-   更新现有 cmdlet [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx)模块中

    -   [获取 DscResource](http://technet.microsoft.com/library/dn521625.aspx)是更快地 （尤其是在 ISE)。

    -   [开始 DscConfiguration](http://technet.microsoft.com/library/dn521623.aspx)有一个新的参数，-UseExisting，其重新应用最后一个已应用的配置。

    -   [开始 DscConfiguration](http://technet.microsoft.com/library/dn521623.aspx) -已固定强制。

    -   [获取 DscLocalConfigurationManager](http://technet.microsoft.com/library/dn407378.aspx)显示更多有用信息引擎状态。

    -   [测试 DscConfiguration](http://technet.microsoft.com/library/dn407382.aspx)现在返回 True 或 False 及计算机名称。

    -   [新建 DscChecksum](http://technet.microsoft.com/library/dn521622.aspx)现在支持 UNC 路径。

-   [PSDesiredStateConfiguration](http://technet.microsoft.com/library/dn391651(v=wps.640).aspx)模块中的新 cmdlet

    -   [更新 DscConfiguration](http://technet.microsoft.com/library/mt143541(v=wps.630).aspx)︰ 执行点播拉服务器检查。

    -   [停止 DscConfiguration](http://technet.microsoft.com/library/mt143542(v=wps.630).aspx)︰ 停止正在运行的配置。

    -   [删除 DscConfigurationDocument](http://technet.microsoft.com/library/mt143544(v=wps.630).aspx)︰ 使您可以在不同阶段 （挂起、 上一张、 或当前） 删除配置文档。

-   语言增强功能

    -   取决于现在支持复合资源。

    -   取决于现在支持资源实例名称中的数字。

    -   不再计算结果为空的节点表达式引发错误。

    -   已固定的节点表达式的计算结果为空时出现错误。

    -   在 Windows PowerShell 控制台工作配置现在调用配置。

-   提取模式增强功能

    -   拉入模式中现在支持所有 ZIP 文件。

    -   **AllowModuleOverwrite**现在可以正常工作。

-   关于复原能力改进

    -   新**DebugMode**允许您重新加载资源模块。

    -   如果配置失败，pending.mof 文件未被删除。

    -   现在在 metaconfiguration 设置已损坏时更具弹性本地配置管理器 (LCM)。

-   诊断改进

    -   LCM 将计时器设置为不同的设置比您指定时，将显示警告。

    -   错误日志文件现在包含调用堆栈的 Windows PowerShell 资源。

-   改进灵活性

    -   LocalConfigurationManager 资源具有新的属性， **ActionAfterReboot**。

        -   ContinueConfiguration （默认值）︰ 目标节点重新启动后自动恢复配置。

        -   StopConfiguration︰ 不会自动继续配置后重新启动节点。

    -   现在可以比抽取操作或与之相反更频繁地发生一致性运行。

    -   版本控制支持︰ DSC 现在可以在较新的客户端 （附带[WMF 5.0](http://aka.ms/wmf5download)） 可以识别生成的文档。

-   错误保护改进

    -   配置应用之前，现在强制实施模块版本。

    -   **DebugPreference**现在已正确设置获取、 设置或测试 TargetResource 呼叫中。

-   处理改进的凭据

    -   现在使用证书，如果指定**证书**和**PSDscAllowPlainTextPassword** 。

    -   即使对于获取 TargetResource 解密凭据。

    -   加密和解密 Metaconfiguration 凭据。

    -   当嵌入对象，现在被解密 PSCredentials。

-   内置资源改进

    -   程序包资源

        -   不能再安装错误的包 (从本地或 web 源)。

        -   现在支持 HTTPS。

    -   没有为 HTTPS[程序包资源](http://technet.microsoft.com/library/dn282132.aspx)中现在支持。

    -   [存档资源](http://technet.microsoft.com/library/dn249917.aspx)现在支持凭据。

## <a name="BKMK_new50"></a>Windows PowerShell 5.0 中的新增功能

-   [Windows PowerShell 中的新增功能](#BKMK_newcore)

-   [Windows PowerShell 需要状态配置中的新增功能](#BKMK_newDSC)

-   [Windows PowerShell ISE 中的新增功能](#BKMK_newISE)

-   [Windows PowerShell Web 服务中的新增功能](#BKMK_newOData)

-   [在 Windows PowerShell 5.0 显著 bug 修复](#BKMK_5bugfix)

### <a name="BKMK_newcore"></a>Windows PowerShell 中的新增功能

-   在 Windows PowerShell 5.0 中启动，您还可以开发通过使用类，使用正式的语法和语义类似于其他面向对象的编程语言。 已为 Windows PowerShell 的语言支持的新功能**类**、**枚举**，以及其他关键字。 有关使用类别的详细信息，请参阅 about_Classes。

-   Windows PowerShell 5.0 引入了新的结构化信息流可用于传输脚本及其呼叫者 （或宿主环境） 之间的结构化的数据。 您现在可以使用写入主机发出到信息流输出。 信息流也适用于 PowerShell.Streams、 作业、 计划的作业和工作流。 以下功能支持信息流。

    -   新的写入信息 cmdlet，允许您指定 Windows PowerShell 命令信息流数据的处理方式。 编写主机是包装写入信息。 编写信息也是受支持的工作流活动。

    -   两个新常见参数，InformationVariable 和 InformationAction，让您确定信息流从命令的显示方式。 有效值 InformationAction 是 SilentlyContinue、 停止、 继续、 查询、 忽略或挂起，与正在默认 SilentlyContinue。 InformationVariable 指定字符串作为要写入主机数据从命令保存到一个变量的名称。

    -   新的首选项变量 InformationPreference，指定中的 Windows PowerShell 会话的信息流数据默认首选项。 默认值为 SilentlyContinue。

    -   添加了两个新工作流常见参数，PSInformation 和 InformationAction。

    -   使用表格格式命令时，表格的列现在自动通过计算通过流数据，第一个除了格式。

-   在与[Microsoft 研究](http://research.microsoft.com/)进行协作，添加新的 cmdlet，ConvertFrom 字符串。 ConvertFrom 字符串允许您提取和分析从文本字符串的内容的结构化的对象。 有关详细信息，请参阅 ConvertFrom 字符串。

-   新的转换字符串 cmdlet 自动设置格式文本基于您提供的示例参数中的示例。

-   新的模块，Microsoft.PowerShell.Archive，包括 cmdlet 可让您压缩文件和文件夹到存档 （也称为 zip 压缩） 文件、 从现有的 ZIP 文件中提取文件和使用较新版本的之内压缩的文件进行更新 ZIP 文件。

-   新的模块，PackageManagement，允许您发现并在 Internet 上安装软件程序包。 PackageManagement （以前称为 OneGet） 模块是一个管理器或 （也称为包提供商） 的现有程序包经理的复用器统一的单一的 Windows PowerShell 界面 Windows 程序包管理。

-   新的模块，PowerShellGet，允许您查找、 安装、 发布和更新模块和 DSC 资源上的[PowerShell 库](http://www.powershellgallery.com/)中，或内部模块存储库中，您可以通过运行 Register PSRepository cmdlet 设置。

-   已添加的新语言关键字**隐藏**，以指定成员 （属性或方法） 不显示默认情况下，在结果中获取成员 (除非添加-强制参数)。 属性或已标记为隐藏的方法也不会显示在 IntelliSense 结果中，除非该成员应可见，则的上下文中例如，自动变量 $这应显示隐藏的成员时的类方法。

-   新建项目、 删除项目和获取 ChildItem 已经增强了支持创建和管理[符号链接](http://en.wikipedia.org/wiki/Symbolic_link)。 新建项目**的项类型**参数接受新值， **SymbolicLink**。 现在可以通过运行新建项目 cmdlet 单一线条创建符号链接。

-   获取 ChildItem 还具有新-深度参数，以及-递归参数中用于限制递归。 例如，获取 ChildItem-递归-竖 2 返回结果从当前文件夹的所有子文件夹中当前文件夹，并在子文件夹的所有文件夹。

-   复制项现在可以复制文件或文件夹从一个 Windows PowerShell 会话，这意味着您可以将文件复制到已连接到远程计算机 （包括计算机运行的[Nano 服务器](http://blogs.technet.com/b/windowsserver/archive/2015/04/08/microsoft-announces-nano-server-for-modern-apps-and-cloud.aspx)，，因此没有其他界面） 的会话。 若要复制的文件，指定 PSSession Id 为新-FromSession 和-ToSession 参数的值并添加-路径和 – 目标指定原点路径和目标，请分别。 例如，复制项目-路径 c:\\myfile.txt 文件-ToSession $s-目标 d:\\destinationFolder。

-   Windows PowerShell 抄写经过改进，以将应用于所有托管应用程序 （如 Windows PowerShell ISE) 除了控制台主机 (**powershell.exe**)。 可以通过启用**开启 PowerShell 抄写**组策略设置，管理模板 /windows 组件/Windows PowerShell 中找到配置抄写选项 （包括使整个系统脚本）。

-   新的详细的脚本跟踪功能允许您启用详细的跟踪和分析系统上的 Windows PowerShell 脚本使用。 启用详细的脚本跟踪后，Windows PowerShell 的 Windows 事件跟踪 (ETW) 事件日志， **Microsoft Windows-PowerShell/运营**登录所有脚本块。

-   在 Windows PowerShell 5.0 中启动，新的加密邮件语法 cmdlet 支持加密和解密的内容使用密码保护的邮件[RFC5652](http://tools.ietf.org/html/rfc5652)所述 IETF 标准格式。 已给[Microsoft.PowerShell.Security](http://technet.microsoft.com/library/hh849807.aspx)模块获取 CmsMessage、 保护-CmsMessage 和撤消 CmsMessage cmdlet。

-   在[Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx)模块，获取运行空间、 调试运行空间，获取 RunspaceDebug、 启用-RunspaceDebug 禁用-RunspaceDebug 新 cmdlet 允许您设置调试选项卡上的运行空间，以及如何启动和停止调试上运行空间。 调试任意运行空间 — 即不是 Windows PowerShell 控制台或 Windows PowerShell ISE 会话的默认运行空间的运行空间 — Windows PowerShell 允许您设置断点，在脚本，并添加断点停止运行，直到您可以将附加调试程序调试运行空间脚本从该脚本。 对任意运行空间的嵌套调试支持已添加到 Windows PowerShell 脚本调试程序的运行空间。

-   新的格式十六进制 cmdlet 已添加到[Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx)模块。 格式十六进制允许您查看十六进制格式的文本或二进制数据。

-   获取剪贴板和设置剪贴板 cmdlet 已添加到[Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx)模块中。他们减少传输到和 Windows PowerShell 会话的内容。 剪贴板 cmdlet 支持图像、 音频文件，文件列表和文本。

-   新的 cmdlet，清除-RecycleBin 已添加到[Microsoft.PowerShell.Management](http://technet.microsoft.com/library/hh849827(v=wps.640).aspx)模块中。此 cmdlet 清空回收站中的硬盘驱动器，其中包括外部驱动器。 默认情况下，您会提示您确认清除 RecycleBin 命令，因为该 cmdlet 的 ConfirmImpact 属性设置为 ConfirmImpact.High。

-   新 cmdlet，新建-TemporaryFile，可以创建一个临时文件作为脚本的一部分。 默认情况下，在创建新的临时文件```C:\Users\<user name>\AppData\Local\Temp```。

-   Out-File、 添加内容和设置内容 cmdlet 现在有一个新的-NoNewline 参数后输出忽略新行。

-   新建 Guid cmdlet 利用.NET Framework Guid 类生成 GUID，如果您正在撰写的脚本或 DSC 资源非常有用。

-   由于文件版本信息可以误导，尤其是后修补文件，新的 FileVersionRaw 和 ProductVersionRaw 脚本属性可用于 FileInfo 对象。 例如，您可以运行以下命令以显示 powershell.exe，这些属性的值 $pid 其中包含进程 ID 运行的 Windows PowerShell 会话︰  ```Get-Process -Id $pid -FileVersionInfo | Format-List *version* -Force```

-   新 cmdlet Enter PSHostProcess 和退出 PSHostProcess 可让您调试从当前进程正在运行的 Windows PowerShell 控制台中单独的流程中的 Windows PowerShell 脚本。 运行 Enter-PSHostProcess 以输入，或将文件附加到，特定进程 ID，然后再运行获取运行空间返回活动过程中的运行空间。 运行退出-PSHostProcess 的过程分离，当您完成调试流程中的脚本。

-   新的等待调试程序 cmdlet 已添加到[Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx)模块。 您可以运行等待调试程序运行脚本中的下一个语句之前停止调试程序中的脚本。

-   Windows PowerShell 工作流调试程序现在支持命令或选项卡上完成，并可以调试工作流的嵌套的函数。 现在，您可以按**Ctrl + 符**输入调试程序中运行脚本、 本地和远程会话和工作流脚本中。

-   调试作业 cmdlet 已添加到[Microsoft.PowerShell.Core](http://technet.microsoft.com/library/hh849695.aspx)模块为 Windows PowerShell 工作流、 背景和运行在远程会话中的作业调试运行作业脚本。

-   已添加了新的状态，AtBreakpoint，用于 Windows PowerShell 作业。 AtBreakpoint 状态适用当作业运行时包括设置断点一个脚本和脚本具有断点。 调试断点处停止作业后，您必须通过运行调试作业 cmdlet 调试作业。

-   Windows PowerShell 5.0 实现中 $PSModulePath 所在的文件夹中的单个 Windows PowerShell 模块的多个版本的支持。 RequiredVersion 属性已添加到 ModuleSpecification 类以帮助您获取所需的版本的模块;此属性是互斥与 ModuleVersion 属性。 获取模块的 FullyQualifiedName 参数的值的一部分，现在支持 RequiredVersion 导入模块和删除模块 cmdlet。

-   现在，您可以通过运行测试 ModuleManifest cmdlet 执行模块版本验证。

-   获取命令 cmdlet 的结果现在显示版本列中。新的版本属性已添加到 CommandInfo 类。 获取命令显示来自多个版本相同的模块的命令。 版本属性也是组成部分的 CmdletInfo 派生类︰ CmdletInfo 和 ApplicationInfo。

-   获取命令都有一个新的参数，-ShowCommandInfo，返回为 PSObjects ShowCommand 信息。 这是通过使用 Windows PowerShell 远程 Windows PowerShell ISE 中运行显示命令时特别有用的功能。 -ShowCommandInfo 参数将替换现有获取 SerializedCommand 函数 Microsoft.PowerShell.Utility 模块中的获取 SerializedCommand 脚本，但是仍可供支持普通脚本。

-   新的获取 ItemPropertyValue cmdlet，您可以不使用点表示法获取属性的值。 例如，在较早版本的 Windows PowerShell 中，您可以运行以下命令以获得 PowerShellEngine 注册表项的应用程序基属性的值︰ **(获取 ItemProperty-路径 HKLM:\\软件\\Microsoft\\PowerShell\\3\\PowerShellEngine-名称 ApplicationBase)。ApplicationBase**。 在 Windows PowerShell 5.0 中启动，您可以运行**获取 ItemPropertyValue-路径 HKLM:\\软件\\Microsoft\\PowerShell\\3\\PowerShellEngine-名称 ApplicationBase**。

-   Windows PowerShell 控制台现在使用语法突出显示，就像在 Windows PowerShell ISE 一样。

-   新的 NetworkSwitch 模块包含 cmdlet，使您能够适用于 Windows Server 2012 R2 徽标认证的网络开关的虚拟 LAN (VLAN) 与基本 2 层网络切换端口配置切换。

-   FullyQualifiedName 参数已添加到导入模块和删除模块 cmdlet，以支持存储多个版本的单个模块。

-   保存帮助、 更新帮助、 导入 PSSession、 导出-PSSession 和获取命令有新的参数，FullyQualifiedModule，类型 ModuleSpecification。 添加此参数指定的完全限定名称的模块。

-   已更新到 5.0 **$PSVersionTable.PSVersion**的值。

### <a name="BKMK_newDSC"></a>Windows PowerShell 需要状态配置中的新增功能

-   Windows PowerShell 语言增强功能使您可以通过使用类定义 Windows PowerShell 需要状态配置 (DSC) 资源。 导入 DscResource 现在是正确的动态关键字;Windows PowerShell 分析指定的模块根模块中，搜索包含 DscResource 属性的类。 您现在可以使用类定义 DSC 资源，在哪些两者均不检查 MOF 文件也 DSCResource 子文件夹模块文件夹中的，不是必需的。 Windows PowerShell 模块文件可以包含多个 DSC 资源类。

-   新的参数，ThrottleLimit，已添加到以下 cmdlet PSDesiredStateConfiguration 模块中。 添加使用 ThrottleLimit 参数指定的目标计算机或设备的所需命令正常工作，同时数。

    -   获取 DscConfiguration

    -   获取 DscConfigurationStatus

    -   获取 DscLocalConfigurationManager

    -   还原 DscConfiguration

    -   测试 DscConfiguration

    -   比较 DscConfiguration

    -   发布 DscConfiguration

    -   设置 DscLocalConfigurationManager

    -   开始 DscConfiguration

    -   更新 DscConfiguration

-   通过集中 DSC 错误报告，丰富的错误消息是不只记录事件日志，但是它可以发送到更高版本的分析的中心位置。 可以使用此中心位置存储在其环境中的任何服务器发生的 DSC 配置错误。 报表服务器定义元配置中后，所有错误发送到报表服务器，然后存储数据库中。 您可以设置此功能，无论配置目标节点中提取从提取服务器配置。

-   改进的创作的 Windows PowerShell ISE 轻松 DSC 资源。 您现在可以执行以下。

    -   通过在块中的一个空行中输入**Ctrl + 空格键**列表**配置**或**节点**块中的所有 DSC 资源。

    -   **枚举**类型的资源属性的自动完成。

    -   DSC 资源，基于配置中的其他资源实例的**取决于**属性的自动完成。

    -   改进的选项卡上完成的资源属性值。

-   现在，用户可以通过添加到节点块**PSDscRunAsCredential**属性运行下一组指定的凭据的资源。 例如，PSDscRunAsCredential = 获取凭据 Contoso\\DscUser。 此功能可用于创建运行 Windows Installer 和可执行安装程序、 访问每个用户注册表配置单元，或执行其他任务的当前用户上下文之外的配置。

-   32 位 （x86） 支持添加了**配置**关键字。

-   Windows PowerShell 现在包含与 DSC 配置，通过添加定义的自定义帮助的支持\[CmdletBinding()] 生成的配置函数。

-   新**DscLocalConfigurationManager**属性指定为元-配置用于配置 DSC 本地配置管理器配置块。 此属性限制配置到包含该配置 DSC 本地配置管理器的项目。 在处理期间，此配置生成\*。 meta.mof 文件，然后将发送到适当的目标节点通过运行设置 DscLocalConfigurationManager cmdlet。

-   在 Windows PowerShell 5.0 现在允许部分配置。 您可以为在段落中的节点提供配置文档。 对于接收的配置文档的多个片段节点，节点的本地配置管理器必须首先设置，以指定预期的片段

-   跨计算机同步是在 Windows PowerShell 5.0 DSC 中的新增功能。 使用内置的 WaitFor\*资源 （**WaitForAll**、 **WaitForAny**和**WaitForSome**），现在您可以指定相关性跨计算机过程配置运行时，不外部业务流程。 这些资源提供通过 Ws-man 协议使用 CIM 连接到节点同步。 配置可以等待若要更改的另一台计算机特定的资源状态。

-   只需足够管理 (JEA)、 新的委派安全功能，利用 DSC 并约束的 Windows PowerShell 运行空间帮助安全企业数据丢失或受损员工，通过从是否有意或无意。 JEA，包括您可以在何处下载 xJEA DSC 资源，有关详细信息，请参阅[只需足够管理，Step by Step](http://blogs.technet.com/b/privatecloud/archive/2014/05/14/just-enough-administration-step-by-step.aspx)。

-   以下新 cmdlet 已添加到 PSDesiredStateConfiguration 模块。

    -   新的获取 DscConfigurationStatus cmdlet 从目标节点获取更高级别的配置状态信息。 您可以获得状态的最后一个或所有配置。

    -   新的比较 DscConfiguration cmdlet 之间的比较的实际状态的一个或多个目标节点与指定的配置。

    -   新的发布 DscConfiguration cmdlet 配置 MOF 文件复制到目标节点，但不适用于配置。 在下一步的一致性阶段中，或运行更新 DscConfiguration cmdlet 应用配置。

    -   新的测试 DscConfiguration cmdlet 允许您验证结果配置匹配所需的配置，如配置匹配所需的配置或 False，如果实际配置与所需的配置不匹配，则返回真。

    -   新的更新 DscConfiguration cmdlet 强制配置进行处理。 如果本地配置管理器在拉入模式，cmdlet 获取配置从提取服务器应用之前。

### <a name="BKMK_newISE"></a>Windows PowerShell ISE 中的新增功能

-   您现在可以编辑通过运行 Enter-PSSession 存储您想要编辑的文件的计算机上启动远程会话，然后运行的 Windows PowerShell ISE 的本地副本中的文件和远程 Windows PowerShell 脚本**PSEdit <path and file name on the remote computer> **。 此功能可以简化编辑存储在 Windows Server，Windows PowerShell ISE 不能在其中运行的服务器核心安装选项的 Windows PowerShell 文件。

-   在 Windows PowerShell ISE，现在支持开始脚本 cmdlet。

-   您现在可以调试在 Windows PowerShell ISE 远程脚本。

-   新的菜单命令**全部中断**(Ctrl + B) 分成用于本地和远程运行脚本。

### <a name="BKMK_newOData"></a>Windows PowerShell Web 服务 （管理 OData IIS 扩展） 中的新增功能

-   在 Windows PowerShell 5.0 中启动，您可以生成一组的 Windows PowerShell cmdlet 基于给定的 OData 终结点，通过导出 ODataEndpointProxy cmdlet，找到新的[Microsoft.PowerShell.OdataUtils](http://technet.microsoft.com/library/dn818507(v=wps.640).aspx)模块中运行公开的功能。

### <a name="BKMK_5bugfix"></a>在 Windows PowerShell 5.0 显著 bug 修复

-   Windows PowerShell 5.0 包括新的 COM 实现，当您正在使用 COM 对象提供显著的性能改进。 效果的视频演示，请参阅[Com_Perf_Improvements](http://1drv.ms/1qu3UPZ)。

-   对第一个选项卡上完成中的 Windows PowerShell 会话，几乎 500 ms 缩短选项卡上完成时间进行了重大性能改进。

## <a name="BKMK_wps4"></a>Windows PowerShell 4.0 中的新增功能
Windows PowerShell 4.0 向后兼容。 Cmdlet、 提供商、 模块、 单元、 脚本、 函数和设计的 Windows PowerShell 3.0 和 Windows PowerShell 2.0 的配置文件在工作 Windows PowerShell 4.0 而无需更改。

默认情况下，在 WindowsÂ® 8.1 和 Windows Server 2012 R2 上安装 Windows PowerShell 4.0。 若要在 Windows 7 SP1，或 Windows Server 2008 R2 上安装 Windows PowerShell 4.0，请下载并安装[Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)。 请务必阅读下载详细信息，并安装 Windows Management Framework 4.0 之前满足所有的系统要求。

-   [Windows PowerShell 中的新增功能](#BKMK_core)

-   [在 Windows PowerShell 集成脚本环境 (ISE) 的新增功能](#BKMK_ise)

-   [Windows PowerShell 工作流中的新增功能](#BKMK_workflow)

-   [Windows PowerShell Web 服务中的新增功能](#BKMK_psws)

-   [Windows PowerShell Web Access 中的新增功能](#BKMK_powwa)

-   [在 Windows PowerShell 4.0 显著 bug 修复](#BKMK_bugs)

Windows PowerShell 4.0 包括以下新功能。

### <a name="BKMK_core"></a>Windows PowerShell 中的新增功能

-   **Windows PowerShell 所需状态配置**(DSC) 是启用的部署和管理软件服务配置数据的 Windows PowerShell 4.0 和这些服务在其中运行的环境中的新管理系统。 DSC 有关的详细信息，请参阅[开始使用 Windows PowerShell 需要状态配置](https://technet.microsoft.com/en-us/library/c134aa32-b085-4656-9a89-955d8ff768d0)。

-   **保存帮助**现在允许您存储在远程计算机安装的模块的帮助。 您可以使用保存帮助下载来自 Internet 连接的客户端 （在其未安装的所有帮助您要为其模块一定），帮助模块，然后复制到远程共享的文件夹或不具有 Internet 访问远程计算机已保存的帮助。

-   Windows PowerShell 调试程序已增强以允许调试 Windows PowerShell 工作流，以及在远程计算机运行的脚本。 现在可以从 Windows PowerShell 命令行或 Windows PowerShell ISE 的脚本级别调试 Windows PowerShell 工作流。 Windows PowerShell 脚本，包括脚本工作流，可以立即调试切换远程会话。 远程调试会话将保留在 Windows PowerShell 远程会话断开了连接，然后以后重新连接。

-   **注册 ScheduledJob**和**设置 ScheduledJob** **RunNow**参数不需要使用**触发器**参数设置立即开始日期和时间作业。

-   **调用 RestMethod**和**调用 WebRequest**现在可以通过使用页眉参数设置的所有标题。 虽然此参数始终存在，它是导致异常或错误的 web cmdlet 的几个参数之一。

-   **获取模块**都有一个新的参数， **FullyQualifiedName**，类型的**ModuleSpecification\[]**。 获取模块的**FullyQualifiedName**参数现在可以通过使用模块的名称、 版本和其 GUID （可选） 指定模块。

-   在 Windows Server 2012 R2 上执行默认的策略设置为**RemoteSigned**。 在 Windows 8.1 上没有更改默认设置。

-   在 Windows PowerShell 4.0 中启动，支持使用动态方法名称的方法调用。 您可以使用变量存储方法名称，然后通过致电变量动态调用方法。

-   当**PSElapsedTimeoutSec**工作流常见参数指定超时时间已过不再删除异步工作流作业。

-   新的参数， **RepeatIndefinitely**，已添加到**新建 JobTrigger**和**设置 JobTrigger** cmdlet。 此不再需要的值，指定要无限期重复运行安排的作业的**RepetitionDuration**参数的**TimeSpan.MaxValue**值。

-   **通过**参数已添加到**启用 JobTrigger**和**禁用 JobTrigger** cmdlet。 通过参数︰ 显示任何对象，创建或修改您的命令。

-   现在，用于指定工作组中**添加计算机**和**删除计算机**cmdlet 的参数名是一致。 现在，这两个 cmdlet 使用参数**工作组名**。

-   已添加了新的公共参数， **PipelineVariable**。 PipelineVariable 允许您存储输送的命令 （或输送命令的一部分） 的结果为可以在后面的管道传递变量。

-   现在支持使用方法语法筛选的集合。 这意味着您可以通过使用简化的语法，类似于 Where() 或位置对象，格式设置为方法调用中现在筛选对象的集合。 下面是一个示例: （获取进程）.where ({$_。Name-匹配 powershell})

-   **获取流程**cmdlet 具有新的开关参数**IncludeUserName**。

-   已添加了新的 cmdlet，**获取 FileHash**，返回中指定文件的多种格式之一的文件哈希。

-   在 Windows PowerShell 4.0 中，如果模块中其清单，使用**DefaultCommandPrefix**密钥或者用户与**前缀**参数，模块导入模块的**ExportedCommands**属性显示的命令前缀的模块。 当您运行命令通过使用模块限定的语法，ModuleName\\按钮，命令名称必须包括前缀。

-   已更新到 4.0 **$PSVersionTable.PSVersion**的值。

-   **Where()**运算符行为已更改。 `Collection.Where('property –match name')` 接受的格式的字符串表达式`"Property –CompareOperator Value"`不再支持。 但是， **Where()**运算符接受的格式将脚本块; 的字符串表达式仍然支持此功能。

### <a name="BKMK_ise"></a>在 Windows PowerShell 集成脚本环境 (ISE) 的新增功能

-   Windows PowerShell ISE 支持 Windows PowerShell 工作流调试和远程脚本调试。

-   IntelliSense 支持添加了用于 Windows PowerShell 需要状态配置供应商和配置。

### <a name="BKMK_workflow"></a>Windows PowerShell 工作流中的新增功能

-   支持已添加了新的**PipelineVariable**公共参数迭代管线，如所使用的系统中心控制器; 上下文中对也就是说，只需从左到右，而不是运行命令的管道交错运行使用流式处理。

-   参数绑定具有显著增强处理外部选项卡上完成方案，如当前运行空间中不存在的命令。

-   自定义容器活动的支持已添加到 Windows PowerShell 工作流。 如果活动参数属于类型**活动**，**活动\[]**— 或是活动的常规集 — 和用户提供的脚本块作为参数，然后 Windows PowerShell 工作流将转换 XAML，与普通的 Windows PowerShell 脚本到工作流编译的脚本块。

-   后崩溃，Windows PowerShell 工作流自动重新连接到托管节点。

-   您现在可以限制**Foreach-并行**活动语句通过使用**ThrottleLimit**属性。

-   **ErrorAction**公共参数具有新无效值，则**挂起**，是专为工作流。

-   工作流终结点现在自动关闭如果有没有活动会话、 没有正在进行的作业，以及任何未完成的作业。 此功能，从而节约充当工作流服务器上，在满足自动关闭条件时的计算机上的资源。

### <a name="BKMK_psws"></a>Windows PowerShell Web 服务中的新增功能

-   Windows PowerShell Web 服务 (PSWS，也称为管理 OData IIS 扩展)，时出现错误时 cmdlet 正在运行，更详细的错误消息将返回到呼叫者。 此外，错误代码遵循[Windows Azure REST API 错误代码的准则](http://msdn.microsoft.com/library/windowsazure/dd179357.aspx)。

-   端点可以立即定义 API 版本，以及实施使用特定的 API 版本。 当客户端和服务器之间出现版本不匹配时，则显示错误的到客户端和服务器。

-   管理调度架构的简化了自动生成架构中的任何缺少的字段的值。 生成发生，很有帮助的起始点，即使调度架构不存在。

-   在 PSWS 处理类型进行了改进支持通过 Windows PowerShell 中**PSTypeConverter**到同样行为使用默认构造函数，比其他构造函数的类型。 这允许您与 PSWS 使用复杂的类型。

-   PSWS 现在允许运行查询时展开关联的实例。 二进制内容 （如图像，音频或视频） 越多，传输成本非常重要，和最好传输二进制数据，但不编码。 PSWS 用于命名的资源流转接不编码。 命名的资源流是**Edm.Stream**类型实体的属性。 每个命名的资源流具有单独 URI 获取或更新操作。

-   OData 操作现在提供了一种机制来调用非 CRUD （创建、 读取、 更新和删除） 上资源的方法。 您可以通过将 HTTP 发送请求发送到定义操作的 URI 调用操作。 操作参数定义文章请求正文中。

-   若要使用 Windows Azure 准则一致，可简化的所有 Url。 更改包括在**密钥为段**允许单个键以表示为段。 请注意使用多个关键值的引用为之前需要在括号记数法，逗号分隔的值。

-   此版本的 PSWS 之前, 仅方式来执行创建、 更新或删除操作是调用文章，放置，或在顶级资源上删除。 新建在此版本的 PSWS，包含资源操作让用户同时做到相同资源更少直接，就像包含这些资源即将达到实现相同结果。

### <a name="BKMK_powwa"></a>Windows PowerShell Web Access 中的新增功能

-   您可以断开并重新连接到基于 web 的 Windows PowerShell Web Access 控制台中的现有会话。 基于 web 的控制台中的**保存**按钮允许您断开与会话，而不删除它，然后重新连接到会话另一个时间。

-   在登录页面上，可以显示默认参数。 若要显示默认参数，配置一个名为**web.config**文件中的登录页面的**可选的连接设置**区域中显示的设置的所有值。 您可以使用**web.config**文件配置第二次或备用的一组凭据除外的所有可选的连接设置。

-   在 Windows Server 2012 R2，可以用于 Windows PowerShell Web 访问远程管理授权规则。 **添加 PswaAuthorizationRule**和**测试 PswaAuthorizationRule** cmdlet 现在包括使管理员能够从远程计算机或 Windows PowerShell Web Access 会话中管理授权规则的凭据参数。

-   现在可以为每个会话中使用新的浏览器选项卡上的单个浏览器会话中的多个 Windows PowerShell Web Access 会话。 您不再需要打开一个新的浏览器会话连接到基于 web 的 Windows PowerShell 控制台中新的会话。

### <a name="BKMK_bugs"></a>在 Windows PowerShell 4.0 显著 bug 修复

-   **获取计数器**现在可以返回计数器包含法语版本的 Windows 中撇号字符。

-   现在，您可以查看**GetType**方法反序列化的对象。

-   **#Requires**语句现在允许用户需要管理员访问权限，如果需要。

-   **导入 Csv** cmdlet 现在将忽略空白的行。

-   已修复 Windows PowerShell ISE 其中使用太多内存，当您运行的**调用 WebRequest**命令时出现问题。

-   **获取模块**现在显示在**版本**列中的模块版本。

-   删除项递归现在在按预期子文件夹中删除项目。

-   **UserName**属性已添加到**获取流程**输出对象。

-   现在，**调用 RestMethod** cmdlet 返回所有可用的结果。

-   **添加成员**立即生效上哈希表，即使未访问哈希表。

-   **选择对象-展开**不再失败或生成异常，如果该属性的值为空。

-   现在可以在与其他对象从获取**计算机名称**属性的命令管道中使用**获取流程**。

-   **ConvertTo Json**和**ConvertFrom Json**现在可以接受条款双引号引起来，并且现在可本地化其错误消息。

-   **获取作业**现在可返回任何已完成的计划的作业，即使是在新会话。

-   安装和使用 Windows PowerShell 4.0 在**文件系统**提供商卸载 Vhd 问题已解决。 Windows PowerShell 现在能够时装载同一会话中检测到新的驱动器。

-   您不再需要显式加载**ScheduledJob**或**工作流**模块，以使用其作业类型。

-   导入定义嵌套工作流; 的工作流的过程进行了性能改进此过程现在更快。

## <a name="BKMK_wps3"></a>Windows PowerShell 3.0 的新增功能
Windows PowerShell 3.0 包括以下新功能。

-   [Windows PowerShell 工作流](#BKMK_Workflow)

-   [Windows PowerShell Web Access](#BKMK_WebAccess)

-   [Windows PowerShell ISE 的新增功能](#BKMK_ISE)

-   [Microsoft.NET Framework 4.0 的支持](#BKMK_NET4)

-   [Windows 预安装环境的支持](#BKMK_WinPE)

-   [断开连接的会话](#BKMK_Disconnected)

-   [强大的会话连接](#BKMK_Robust)

-   [可更新的帮助系统](#BKMK_UpHelp)

-   [增强的联机帮助](#BKMK_Online)

-   [CIM 集成](#BKMK_CIM)

-   [会话配置文件](#BKMK_ConfigFile)

-   [计划的作业和任务计划程序集成](#BKMK_ScheduledJob)

-   [Windows PowerShell 语言增强功能](#BKMK_Lang)

-   [新的核心 Cmdlet](#BKMK_Core)

-   [对现有核心 Cmdlet 和提供商的改进](#BKMK_Prov)

-   [远程模块导入和发现](#BKMK_REM)

-   [增强的选项卡上完成](#BKMK_TAB)

-   [模块自动加载](#BKMK_AutoLoad)

-   [模块体验的改进](#BKMK_MOD)

-   [简化的命令发现](#BKMK_SIMPLE)

-   [改进的日志记录、 诊断和组策略支持](#BKMK_LOG)

-   [格式和输出改进](#BKMK_OUT)

-   [增强的控制台主机体验](#BKMK_HOST)

-   [新的 Cmdlet 和托管 Api](#BKMK_API)

-   [改进了性能](#BKMK_PERF)

-   [RunAs 和共享的主机支持](#BKMK_RUNAS)

-   [特殊字符处理改进](#BKMK_CHAR)

### <a name="BKMK_Workflow"></a>Windows PowerShell 工作流
Windows PowerShellÂ® 工作流将 Windows PowerShell 的 Windows Workflow Foundation 强大。 可以在 XAML 或 Windows PowerShell 语言编写工作流和运行它们，就像将运行 cmdlet。 [获取命令](https://technet.microsoft.com/en-us/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad)cmdlet 获取 workflw 命令，并[获取帮助](https://technet.microsoft.com/en-us/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a)cmdlet 获取帮助的工作流。

工作流是长时间运行，可重复、 频繁、 可并行化、 中断、 suspendable，且可重启的 multicomputer 管理活动的序列。 可以从有意或意外中断，例如网络中断、 Windows 重新启动计算机或停电继续工作流。

工作流也是可移植;他们可以导出为或从 XAML 文件导入。 您可以编写自定义会话配置文档，以便由用户委派或附属运行工作流中的工作流或活动。

下面是 Windows PowerShell 工作流的好处

-   **已排序、 长时间运行的任务的自动化。**

-   **远程监控长时间运行的任务**。 在任何时候都可见状态和进度的活动。

-   **Multicomputer 管理。** 同时在数百个托管节点上运行为工作流的任务。 Windows PowerShell 工作流包含常见管理参数，如**PSComputerName**，启用多台计算机管理方案的内置库。

-   **单个任务执行复杂的流程。** 您可以组合到单个工作流实现的整个的端到端方案的相关的脚本。

-   **持续。**: 工作流保存 （或检查指向） 定义其作者，因此您可以继续工作流中保留的最后一个任务 （或检查点），而不是重新启动工作流从头开始的特定位置。

-   **可靠性。** 自动的故障恢复。 工作流在计划和非计划重新启动后仍然存在。 可以暂停工作流执行，然后继续在最后一个持续点的工作流。 工作流作者可以指定特定活动上托管的一个或多个节点在失败的情况下重新运行。

-   **能够断开连接，请重新连接，并在断开连接的会话中运行。** 用户可以连接和断开与工作流服务器，而是继续运行工作流。 您可以注销客户端计算机或重新启动客户端计算机并监控工作流执行从另一台计算机，而不会中断工作流。

-   **日程安排。** 可以像任何 Windows PowerShell cmdlet 或脚本安排工作流任务。

-   **工作流和连接限制。** 执行工作流和与节点的连接可以被阻止，从而使可伸缩性和高可用性方案。

### <a name="BKMK_WebAccess"></a>Windows PowerShell Web Access
Windows PowerShellÂ® Web Access 是 Windows Server 2012 功能可允许用户在基于 web 的控制台运行 Windows PowerShell 命令和脚本。 Windows PowerShell、 远程管理软件或浏览器插件安装不需要使用基于 web 的控制台的设备。 所需的所有已正确配置的 Windows PowerShell Web Access 网关和客户端设备浏览器支持 JavaScript® 并接受 cookie。

有关详细信息，请参阅[部署 Windows PowerShell Web Access](http://go.microsoft.com/fwlink/p/?LinkID=221050)。

### <a name="BKMK_ISE"></a>Windows PowerShell ISE 的新增功能
Windows PowerShell 3.0，Windows PowerShellÂ® 集成脚本环境 (ISE) 有许多新的功能，包括智能感知、 显示命令窗口、 统一的控制台窗格、 段、 括号匹配、 展开折叠节、 自动保存、 最近的项目列表、 丰富的副本，块复制和完全支持编写 Windows PowerShell 脚本工作流。 有关详细信息，请参阅[about_Windows_PowerShell_ISE [v3]](https://technet.microsoft.com/en-us/library/dfa54d47-60c6-4fff-8197-c747e8d411bb)。

### <a name="BKMK_NET4"></a>Microsoft.NET Framework 4 的支持
Windows PowerShell 是生成针对公共语言运行时 4.0。 Cmdlet、 脚本和工作流作者可以使用新的 Microsoft.NET Framework 4 类中 Windows PowerShell 与功能，包括应用程序兼容性和部署、 管理扩展性框架、 并行计算、 网络、 Windows Communication Foundation 和 Windows Workflow Foundation。

### <a name="BKMK_WinPE"></a>Windows 预安装环境的支持
Windows PowerShell 3.0 是 Windows 预安装环境 (Windows PE) 4.0 Windows 8 的可选组件。 Windows PE 是启动具有没有操作系统和准备 Windows 安装的计算机使用最少操作系统。 Windows PE 可以用于的分区和格式设置硬盘、 磁盘图像复制到计算机，并从网络共享启动 Windows 安装程序。 Windows PowerShell 3.0 可在 Windows PE 管理部署、 诊断和恢复方案。

### <a name="BKMK_Disconnected"></a>断开连接的会话
在 Windows PowerShell 3.0 开始，请在远程计算机上保存持续用户管理会话 ("PSSessions") 使用新建 PSSession cmdlet 您创建的。 他们将不再依赖于会话创建它们。

而不会中断会话中运行的命令，可以立即断开与会话。 您可以关闭会话并关闭您的计算机。 更高版本，您可以重新连接到会话从不同的会话相同或不同计算机上。

[获取 PSSession](https://technet.microsoft.com/en-us/library/b2b10531-d0df-4746-b877-e75c09955cb6) cmdlet 的参数的**计算机名称**现在获取所有用户的会话的连接到计算机，即使在另一台计算机上的不同会话中启动。 您可以连接到会话、 获取命令的结果、 开始新的命令，然后断开与会话。

添加了新的 cmdlet 来支持断开连接会话功能，包括[断开 PSSession](https://technet.microsoft.com/en-us/library/f8f95111-612f-4cba-9098-77904b0473d8)、[连接 PSSession](https://technet.microsoft.com/en-us/library/b803dd29-f208-4079-80d4-db04d778f060)，以及接收-PSSession 和新的参数已添加到管理 PSSessions，如[调用命令](https://technet.microsoft.com/en-us/library/906b4b41-7da8-4330-9363-e7164e5e6970)cmdlet 的**InDisconnectedSession**参数的 cmdlet。

仅当计算机在这两个源表 （"客户"） 和终止 （"服务器"） 的连接的结束正在运行的 Windows PowerShell 3.0 支持断开连接会话功能。

### <a name="BKMK_Robust"></a>强大的会话连接
Windows PowerShell 3.0 检测意外的损失的客户端和服务器之间的连接，并尝试重新建立连接，并自动继续执行。 如果无法在指定的时间重新建立客户端 / 服务器连接，通知用户并断开会话。 在尝试重新连接，Windows PowerShell 向用户提供连续的反馈。

如果由使用 InvokeCommand 启动断开连接的会话，Windows PowerShell 创建断开连接的会话，以使其更轻松地重新连接并继续执行作业。

这些功能提供更多可靠且可恢复的远程处理体验，并允许用户执行长时间运行需要强大的会话，如工作流的任务。

### <a name="BKMK_UpHelp"></a>可更新的帮助系统
现在，您可以下载最新的帮助文件的 cmdlet 模块中。 [更新帮助](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)cmdlet 标识的最新的帮助文件、 从 Internet 下载它们，解压缩其、 验证，并在正确的语言特定目录模块安装它们。

若要使用的最新的帮助文件，只需键入`Get-Help`。 您不需要重新启动 Windows 或 Windows PowerShell。 若要更新的模块 $pshome 目录中的帮助，请使用"以管理员身份运行"选项启动 Windows PowerShell。

若要支持不具有 Internet 访问权的用户和用户防火墙后面，新[保存帮助](https://technet.microsoft.com/en-us/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa)cmdlet 将帮助文件下载到文件系统目录，例如文件共享。 用户可以使用[更新帮助](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)cmdlet 可更新的帮助文件的文件共享。

您可以使用[更新帮助](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)cmdlet 所有更新的帮助文件或特定的模块中所有支持 UI 区域性。 您甚至可以放在您的 Windows PowerShell 配置文件的[更新帮助](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)命令。 默认情况下，Windows PowerShell 不超过每天一次下载模块的帮助文件。

Windows 8 和 Windows Server 2012 模块不包括帮助文件。 若要下载最新的帮助文件，请键入`Update-Help`。 有关详细信息，请键入`Get-Help`（无参数） 或查看[about_Updatable_Help](https://technet.microsoft.com/en-us/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe)。

在计算机上未安装 cmdlet 的帮助文件时，[获取帮助](https://technet.microsoft.com/en-us/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a)cmdlet 现在显示自动生成的帮助。 自动生成帮助包括命令语法并使用[更新帮助](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)cmdlet 下载帮助文件的说明进行操作。

任何模块作者可以支持可更新帮助其模块。 您可以在模块中包含帮助文件，并使用可更新帮助更新它们或省略帮助文件和使用可更新帮助安装它们。 有关支持可更新的帮助，请参阅 MSDN[支持可更新的帮助](http://go.microsoft.com/FWLink/?LinkID=242129)。

### <a name="BKMK_Online"></a>增强的联机帮助
Windows PowerShell 的联机帮助是重要的资源的所有用户，但不包含或无法安装更新的帮助文件的用户非常重要。

若要用于任何 Windows PowerShell cmdlet 获取联机帮助，请键入︰

```
Get-Help <cmdlet-name> -Online
```

Windows PowerShell 默认 Internet 浏览器中打开帮助主题的联机版本。

**获取帮助-联机**中的 Windows PowerShell 3.0 功能现在更加强大，因为其工作方式，即使当 cmdlet 的帮助文件未安装在计算机上。 **获取帮助-联机**功能获取联机帮助主题的 URI 从 HelpUri 属性的 cmdlet 和高级的功能。

```
PS C:\>(Get-Command Get-ScheduledJob).HelpUri
http://go.microsoft.com/fwlink/?LinkID=223923
```

从 Windows PowerShell 3.0 开始，C# cmdlet 的作者可以通过 cmdlet 类上创建**HelpUri**属性填充**HelpUri**属性。 作者的高级功能可以定义**CmdletBinding**属性**HelpUri**属性。 **HelpUri**属性的值必须以"http"或"https"开头。

您也可以在一个基于 XML 的 cmdlet 的帮助文件的第一个相关链接中包括**HelpUri**值或。链接指令的函数中基于注释的帮助。

支持联机帮助的详细信息，请参阅 MSDN[支持联机帮助](http://go.microsoft.com/fwlink/?LinkId=242132)。

### <a name="BKMK_CIM"></a>CIM 集成
Windows PowerShell 3.0 包括支持为公用信息模型 (CIM)，它提供管理信息的一般定义系统、 网络、 应用程序和服务，从而使他们的管理信息不同系统之间交换。 支持 CIM 中包括的能力作者基于新的或现有 CIM 类，命令的 Windows PowerShell cmdlet 的 Windows PowerShell 3.0 将 XML 文件，支持 CIM.NET Framework 基于 cmdlet 定义。 API、 CIM 管理 cmdlet 和 WMI 2.0 提供商。

### <a name="BKMK_ConfigFile"></a>会话配置文件
从 Windows PowerShell 3.0 开始，您可以通过使用文件设计自定义会话配置。 新的会话配置文件允许您确定使用的会话配置，包括哪些模块、 脚本和格式文件是加载到会话，可以使用哪些 cmdlet 和语言元素用户，哪些模块和脚本他们可以运行，并且可以看到哪些变量会话的环境。

您可以设计在其中用户可以仅运行 cmdlet 从一个特定的模块，会话或完整的语言、 所有模块，访问和访问执行高级的任务的脚本有用户的会话。

在早期版本的 Windows PowerShell，控制此级别是仅适用于那些可以编写 C# 程序或复杂的启动脚本。 现在，任何计算机上的管理员组的成员可以使用自定义会话配置配置文件。

若要创建会话配置文件，请使用[新建 PSSessionConfigurationFile](https://technet.microsoft.com/en-us/library/5f3e3633-6e90-479c-aea9-ba45a1954866) cmdlet。 若要应用于会话配置会话配置文件，使用[Register PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea)或[设置 PSSessionConfiguration](https://technet.microsoft.com/en-us/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) cmdlet。

有关详细信息，请参阅[about_Session_Configuration_Files](https://technet.microsoft.com/en-us/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8)和[新建 PSSessionConfigurationFile](https://technet.microsoft.com/en-us/library/5f3e3633-6e90-479c-aea9-ba45a1954866)。

### <a name="BKMK_ScheduledJob"></a>计划的作业和任务计划程序集成
现在可以计划 Windows PowerShell 背景作业，并对其进行管理，Windows PowerShell 和任务计划程序中。

Windows PowerShell 计划作业是 Windows PowerShell 后台作业和任务计划程序任务的有用混合。

Windows PowerShell 后台作业，如安排的作业异步在后台运行。 可以通过使用作业 cmdlet，如[启动作业](https://technet.microsoft.com/en-us/library/2bc04935-0deb-4ec0-b856-d7290cca6442)和[获取作业](https://technet.microsoft.com/en-us/library/1352c534-7193-46ca-9ab1-0c5219a661ad)管理计划已完成的作业的实例。

任务计划程序任务，您可以运行安排的作业的一次性或重复性时间表，或在响应操作或事件。 您可以查看和管理中任务计划程序安排的作业、 启用和禁用它们，根据需要运行它们或将其用作模板，并设置在其下启动作业的条件。

此外，计划的作业附带 cmdlet 来管理这些自定义设置。 Cmdlet 允许您创建、 编辑、 管理、 禁用和重新启用计划的作业、 创建计划的作业触发器和设置计划的作业选项。

有关计划作业的详细信息，请参阅[about_Scheduled_Jobs](https://technet.microsoft.com/en-us/library/3b546629-703c-4939-b44f-52dd567bce92)。

### <a name="BKMK_Lang"></a>Windows PowerShell 语言增强功能
Windows PowerShell 3.0 包含许多功能，旨在使其语言更简单、 更轻松地使用，并避免常见错误。 改进包括属性枚举、 计数和长度属性标量对象、 新的重定向运算符、 $Using 范围内修改、 PSItem 自动变量、 灵活脚本格式，变量、 简化的属性参数，数值命令名称、 停止分析运算符、 改进的数组展开、 新位运算符、 有序的词典、 PSCustomObject 转换和改进基于注释的帮助的属性。

### <a name="BKMK_Core"></a>新的核心 Cmdlet
新 cmdlet 已添加到 Windows PowerShell 核心安装，包括 cmdlet 来管理计划的作业，断开连接的会话、 CIM 集成和可更新的帮助系统。

|||
|-|-|
|添加 JobTrigger|新 JobTrigger|
|连接 PSSession|新 PSSessionConfigurationFile|
|ConvertFrom Json|新 PSTransportOption|
|ConvertTo Json|新 PSWorkflowExecutionOption|
|禁用 JobTrigger|新 PSWorkflowSession|
|禁用 ScheduledJob|新 ScheduledJobOption|
|断开 PSSession|新 WinEvent|
|启用 JobTrigger|接收 PSSession|
|启用 ScheduledJob|注册 CimIndicationEvent|
|获取 CimAssociatedInstance|注册 ScheduledJob|
|获取 CimClass|删除 CimInstance|
|获取 CimInstance|删除 CimSession|
|获取 CimSession|删除 TypeData|
|获取 ControlPanelItem|重命名计算机|
|获取 IseSnippet|简历作业|
|获取 JobTrigger|保存帮助|
|获取 ScheduledJob|设置 CimInstance|
|获取 ScheduledJobOption|设置 JobTrigger|
|获取 TypeData|设置 ScheduledJob|
|导入 IseSnippet|设置 ScheduledJobOption|
|调用 AsWorkflow|显示命令|
|调用 CimMethod|显示 ControlPanelItem|
|调用 RestMethod|暂停作业|
|调用 WebRequest|测试 PSSessionConfigurationFile|
|新 CimInstance|取消阻止文件|
|新 CimSession|注销 ScheduledJob|
|新 CimSessionOption|更新帮助|
|新 IseSnippet||

### <a name="BKMK_Prov"></a>对现有核心 Cmdlet 和提供商的改进
Windows PowerShell 3.0 新功能包括︰ 现有 cmdlet 包括的简化的语法和新参数以下 cmdlet︰ 计算机 cmdlet、 CSV cmdlet，获取-ChildItem 获取命令获取内容，获取的历史记录，度量值对象，安全 cmdlet 选择对象、 选择字符串、 拆分路径、 开始-流程 t 型对象，测试连接添加成员和 WMI cmdlet。

Windows PowerShell 提供商已也明显改进，包括证书管理安全套接字层 (SSL) 证书 web 托管提供商支持、 支持的凭据、 持久网络驱动器和文件系统驱动器中的备用数据流。

### <a name="BKMK_REM"></a>远程模块导入和发现
Windows PowerShell 3.0 扩展模块发现、 导入和远程计算机上的隐式远程处理功能。 模块 cmdlet 远程计算机上获取模块，并通过使用 Windows PowerShell 远程导入远程或本地计算机的模块。 新 CIM 会话支持允许您使用 CIM 和 WMI 管理非 Windows 的计算机可以通过导入隐式远程计算机运行的本地计算机的命令。

有关详细信息，请参阅[获取模块](https://technet.microsoft.com/en-us/library/2cccd4c4-9a21-4c77-b691-984ee57242e1)和[导入模块](https://technet.microsoft.com/en-us/library/af616c24-e122-4098-930e-1e3ea2080ade)cmdlet 帮助主题。

### <a name="BKMK_TAB"></a>增强的选项卡上完成
选项卡上的完成 Windows PowerShell 控制台中现在完成 cmdlet、 参数、 参数值、 枚举、.NET 框架类型、 COM 对象、 隐藏的目录和详细信息的名称。 选项卡上的自动完成功能完全重写基于新分析器和抽象语法树，以支持更多方案，包括内存内分析树和中线选项卡上完成。

### <a name="BKMK_AutoLoad"></a>模块自动加载
[获取命令](https://technet.microsoft.com/en-us/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad)cmdlet 立即获取所有 cmdlet 和功能的计算机安装的所有模块从即使模块不导入当前会话。

当您获得需要 cmdlet 时，可以不导入任何模块立即使用。 Windows PowerShell 模块现在是在您使用任何 cmdlet 模块中时自动导入。 您不再需要搜索模块并导入其使用其 cmdlet。

自动导入的模块触发命令中使用 cmdlet，运行适用于不带通配符，cmdlet**获取命令**或为不带通配符 cmdlet 运行[获取帮助](https://technet.microsoft.com/en-us/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a)。

您可以启用、 禁用和配置自动通过导入的模块**$PSModuleAutoLoadingPreference**首选项变量。

有关详细信息，请参阅[about_Modules [v4]](https://technet.microsoft.com/en-us/library/94f57429-a539-4aee-bb0d-205cd7e801f9)、 [[v4] about_Preference_Variables](https://technet.microsoft.com/en-us/library/31344314-be29-4286-b039-afa5460cbe8b)和[获取命令](https://technet.microsoft.com/en-us/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad)和[导入模块](https://technet.microsoft.com/en-us/library/af616c24-e122-4098-930e-1e3ea2080ade)cmdlet 帮助主题。

### <a name="BKMK_MOD"></a>模块体验的改进
Windows PowerShell 3.0 将模块，包括以下新功能支持的高级的功能。

1.  单个模块 (LogPipelineExecutionDetails) 模块日志记录和新的"启用在模块的日志记录"组策略设置

2.  扩展的公开模块清单中的值的模块对象

3.  新**ExportedCommands**属性的模块，包括嵌套模块，将所有类型的命令组合在一起

4.  改进的可用 （取消导入） 模块，包括在相同的命令允许的**路径**和**ListAvailable**参数发现

5.  新**DefaultCommandPrefix**密钥模块的清单，而不更改模块的代码避免名称冲突。

6.  改进的模块需求，包括带版本和 GUID 自动导入所需的模块的完全限定的必需的模块

7.  [新建 ModuleManifest](https://technet.microsoft.com/en-us/library/512adced-f42f-4e88-ba7c-834fc9e5d047) cmdlet 的更安静、 简化操作。

8.  新的**模块**参数 #Requires

9. 改进的[导入模块](https://technet.microsoft.com/en-us/library/af616c24-e122-4098-930e-1e3ea2080ade)cmdlet 与**MinimumVersion**和**RequiredVersion**参数。

### <a name="BKMK_SIMPLE"></a>简化的命令发现
您不再需要导入所有模块，了解您的会话可用的命令。 在 Windows PowerShell 3.0，[获取命令](https://technet.microsoft.com/en-us/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad)cmdlet 获取所有命令，从所有已安装的模块。 并且，如果您使用的命令，将导出命令的模块自动导入到您的会话。

特别为初学者设计新的[显示命令](https://technet.microsoft.com/en-us/library/65bba50b-91a8-49d5-80a2-a30fc684ba41)cmdlet。 您可以搜索窗口中的命令。 可以查看所有命令或筛选按模块，通过单击按钮导入模块，使用文本框和下拉列表构造有效的命令，然后复制或不离开窗口中运行命令。

### <a name="BKMK_LOG"></a>改进的日志记录、 诊断和组策略支持
Windows PowerShell 3.0 改进的日志记录和跟踪支持的命令和事件跟踪 Windows (ETW) 日志中支持的模块、 模块，可编辑**LogPipelineExecutionDetails**属性和"打开在模块的日志记录"组策略设置。 您现在可以通过显示日志属性从日志详细信息获取参数值。

### <a name="BKMK_OUT"></a>格式和输出改进
新的格式和输出改进提高效率的 Windows PowerShell 的所有用户。 改进包括所有流输出重定向，添加动态不 Format.ps1xml 文件，word 类型增强的更新类型 cmdlet 环绕在输出中，默认格式属性的自定义对象， **PSCustomObject**文字，改进的格式设置为 WMI 对象和不同的对象，并发现方法重载支持。

### <a name="BKMK_HOST"></a>增强的控制台主机体验
Windows PowerShell 控制台主机程序 Windows PowerShell 3.0 包括默认情况下按线索组织的单个单元中有新功能。 在文件资源管理器中新的"使用 PowerShell 运行"选项允许您只需通过右键单击不受限制的会话中运行脚本。 新控制台主机启动逻辑更快地启动 Windows PowerShell 和新字体允许您进行个性化设置的熟悉控制台窗口体验。

有关详细信息，请参阅[about_Run_With_PowerShell](https://technet.microsoft.com/en-us/library/c9d9ca5f-eff9-4409-be9d-e43b5b4087eb)。

### <a name="BKMK_API"></a>新的 Cmdlet 和托管 Api
新的 Cmdlet API 和托管 API 中包含公共高级的语法树 (AST) Api 和 Api 渠道分页、 嵌套的管道、 运行空间池选项卡上完成、 Windows RT，已过时的 cmdlet 属性和动词和名词 FunctionInfo 对象属性。

### <a name="BKMK_PERF"></a>改进了性能
Windows PowerShell 中的重大性能改进来自新语言分析器，它构建的动态运行时语言 （金额） 在.NET Framework 4。，以及运行时脚本编译，引擎可靠性改进和改进其性能，尤其是在搜索的网络共享时[获取 ChildItem](https://technet.microsoft.com/en-us/library/75cf79bb-4db6-4a67-8c36-3d20754e2190)算法的更改。

### <a name="BKMK_RUNAS"></a>RunAs 和共享的主机支持
Windows PowerShell 3.0 包括 RunAs 和共享主机功能的支持。

*RunAs*功能，用于 Windows PowerShell 工作流，允许用户配置创建的共享的用户帐户权限运行的会话的会话。 这使较低特权的用户具有管理员权限运行特定命令和脚本并减少了将不太高级用户添加到管理员组中。

**SharedHost**功能允许多个用户在多台计算机连接到工作流会话同时和监控工作流的进度。 用户可以在一台计算机上启动工作流，然后连接到另一台计算机上的工作流会话不从原始计算机断开连接会话。 用户必须具有相同的权限，并使用相同的会话配置。 有关详细信息，请参阅"运行 Windows PowerShell 中的工作流"开始使用 Windows PowerShell 工作流。

### <a name="BKMK_CHAR"></a>特殊字符处理改进
改进的功能的 Windows PowerShell 3.0 解释和正确处理特殊字符， **LiteralPath**参数，处理路径中的特殊字符，在才有效有**Path**参数，包括新的[更新帮助](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)和[保存帮助](https://technet.microsoft.com/en-us/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa)cmdlet 的几乎所有 cmdlet。 分析器还包括特殊的逻辑，以提高处理引号字符 (\`) 和方括号中文件名和路径。

## 另请参阅
[about_Windows_PowerShell_4.0](http://technet.microsoft.com/en-us/library/hh847833(v=wps.630).aspx)
[about_Windows_PowerShell_5.0](https://technet.microsoft.com/en-us/library/6d56fa88-371e-40c9-b2de-64a2a0cd49da)
[Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116)

