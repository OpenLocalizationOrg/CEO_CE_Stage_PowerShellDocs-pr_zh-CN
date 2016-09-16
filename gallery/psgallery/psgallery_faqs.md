# 常见问题

## 什么是 PowerShell 模块？

PowerShell 模块是包含某些 PowerShell 功能可重用包。 可以在模块中打包 PowerShell （函数、 变量、 DSC 资源等） 中的所有内容。 通常情况下，模块是包含特定类型的文件存储在一个特定的路径上的文件夹。 有几种不同类型的有 PowerShell 模块。

## 什么是 PowerShell 脚本？

PowerShell 脚本是一系列存储在启用重复使用和共享.ps1 文件中的命令。 PowerShell 工作流也是 PowerShell 脚本，大纲的一组任务并提供这些任务的顺序。 有关详细信息，请访问[开始使用 PowerShell 工作流](https://technet.microsoft.com/en-us/library/jj134242.aspx)。

## 如何将不同于 PowerShell 模块 PowerShell 脚本？

模块通常会更好的共享，但我们已经启用了脚本共享以使其更轻松地社区参与工作流和脚本。 有关详细信息，请参阅下面的博客︰

- [不编写脚本，编写 PowerShell 模块](http://blogs.technet.com/b/heyscriptingguy/archive/2011/06/27/don-t-write-scripts-write-powershell-modules.aspx)
- [了解 PowerShell 模块](http://blogs.technet.com/b/heyscriptingguy/archive/2015/07/10/understanding-powershell-modules.aspx)

## 如何可以发布到 PowerShell 库？

您可以将项目发布到库之前，您必须 PowerShell 库中注册帐户。 这是因为需要发布项目的 NuGetApiKey，在注册时提供。 要注册，请使用您的个人工作或学校帐户登录到 PowerShell 库。 当您首次登录时，一次性注册过程是必需的。 以后，您的个人资料页面上提供了您 NuGetApiKey。

一旦您注册在库中，使用[发布模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)或[发布脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet 到库中发布您的项目。 如何运行这些 cmdlet 的详细信息，请访问发布选项卡，或阅读[发布模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)和[发布脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)文档。

**您不需要注册或登录到安装或保存的项目的库。**

## 我收到"无法处理请求。 指定的 API 密钥无效或不具有指定的包的访问权。。 远程服务器返回了错误: (403)。" 当我尝试将项目发布到 PowerShell 库时的错误。 那是什么意思？

由于下列原因，会出现此错误︰

- **指定的 API 密钥无效。**
     确保您已从您的帐户指定有效的 API 密钥。 若要获取 API 密钥，查看您的个人资料页面。
- **您不属于指定的项名称。**
     如果您已确认的 API 密钥是否正确，然后可能已存在具有相同名称与您尝试使用的一个项目。 该项目可能已经由所有者未列出，这种情况下它不会显示任何搜索结果中。 要确定是否已存在具有相同名称的项目，请打开浏览器并导航到该项目的详细信息页面︰ `https://www.powershellgallery.com/packages/<itemName>`。 例如，直接向导航`https://www.powershellgallery.com/packages/pester`会使你进入 Pester 模块的详细信息页面上，不论是否是未列出。 如果具有冲突名称的项目已存在并且未列出，您可以︰
    - 选择您的项目的另一个名称。
    - 与现有的项目的所有者联系。

## 为什么我无法登录使用我的个人帐户，但无法昨天登录？

请注意库帐户不适用于更改您的主要电子邮件别名。 有关详细信息，请参阅[Microsoft 电子邮件别名](http://windows.microsoft.com/en-us/windows/outlook/add-alias-account)。

## 为什么时看不到所有库项目是否选择了项目选项卡上的所有类别复选框？

通过选择一个类别复选框，即指明"我想要查看此类别中的所有项目。" 将显示所选类别中的项目。 因此同样，通过选择类别的所有复选框，您将表明"我想要查看任何类别中的所有项目。" 但在库中的某些项目不属于任何类别列出，以便它们不会显示在结果中。 若要查看库中的所有项目，请取消选中所有类别，或再次选择项目选项卡。

## 若要将模块发布到 PowerShell 库要求是什么？

可以发布到库的任何类型的 PowerShell 模块 （脚本模块、 二进制模块或清单模块）。 若要发布模块，PowerShellGet 需要了解一些注意事项有关它的版本，说明、 作者和如何获取许可证。 为发布过程从*模块清单*(.psd1) 文件，或[**发布模块**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet **LicenseUri**参数的值的一部分中读取此信息。 发布到库的所有模块都必须模块清单。 任何模块在其清单中包含以下信息可以发布到库中︰

- 版本
- 说明
- 作者
- 模块，或者作为**专用数据**部分中的清单，或[**发布模块**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet 的**LicenseUri**参数中的一部分的许可条款 URI。

## 如何创建正确格式模块清单？

创建模块清单的最简单方法是运行[**新建 ModuleManifest**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。 在 PowerShell 5.0 或更高版本新建 ModuleManifest 将生成正确格式模块清单有用的元数据，如**ProjectUri**、 **LicenseUri**和**标记**的空白字段。 只需在空白处，填写或作为正确格式的示例使用生成的清单。

若要验证所有必需的正确填充元数据字段，请使用[**测试 ModuleManifest**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。

若要更新的模块清单文件字段，请使用[**更新 ModuleManifest**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。

## 若要发布到库的脚本要求是什么？

可以发布到库的任何类型的 PowerShell 脚本 （脚本或工作流）。 若要发布脚本，PowerShellGet 需要了解一些注意事项有关它的版本，说明、 作者和如何获取许可证。 为发布过程从*PSScriptInfo*部分中的脚本文件，或[**发布脚本**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet **LicenseUri**参数的值的一部分中读取此信息。 发布到库的所有脚本必须都具有元数据的信息。 任何脚本 PSScriptInfo 部分中包含以下信息可以发布到库中︰

- 版本
- 说明
- 作者
- 脚本，或者作为**PSScriptInfo**部分中的脚本，或[**发布脚本**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet 的**LicenseUri**参数中的一部分的许可条款 URI。

## 如何搜索？

键入您正在查找的内容在文本框中。 例如，如果您想要查找与 SQL Azure 相关的模块，只需键入"azure sql"。 我们的搜索引擎会查找这些关键字中所有已发布的项目，包括标题、 说明和跨元数据。 然后，根据加权的质量分数，它将显示最接近的匹配项。 您还可以通过使用域的特定字段搜索:"值"中的以下字段搜索查询语法︰

- 标记
- 函数
- Cmdlet
- DscResources
- PowerShellVersion

因此，例如，当您搜索 PowerShellVersion︰ 将显示"2.0"仅结果兼容的 PowerShellVersion 2.0 （基于其模块/脚本清单）。

## 如何创建正确格式的脚本文件？

创建正确格式脚本文件的最简单方法是运行[**新建 ScriptFileInfo**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。 在 PowerShell 5.0 新建 ScriptFileInfo 生成正确设置格式的脚本文件包含空白字段有用的元数据，如**ProjectUri**、 **LicenseUri**和**标记**。 只需在空白处，填写或作为正确格式的示例使用生成的脚本文件。

若要验证所有必需的正确填充元数据字段，请使用[**测试 ScriptFileInfo**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。

若要更新的脚本元数据字段，请使用[**更新 ScriptFileInfo**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。

## 内容存在其他类型的 PowerShell 模块？

术语 PowerShell 模块也是指实现实际功能的文件。 脚本模块文件 (.psm1) 包含 PowerShell 代码。 二进制模块文件 (.dll) 包含不支持经过编译的代码。

下面是一种方法想象一下︰ 封装模块文件夹是模块文件夹。 模块文件夹可以包含一个模块清单 (.psd1)，描述的文件夹的内容。 实际执行工作的文件是脚本模块文件 (.psm1) 和模块二进制文件 (.dll)。 DSC 资源在特定的子文件夹中，位于和实现为脚本模块文件或二进制模块文件。

所有库中的模块包含模块清单，并且其中大多数模块包含脚本模块文件或二进制模块文件。 术语模块可能引起混乱，由于这些不同的含义。 除非明确声明，否则所有使用此页面上的 word 模块都引用包含这些文件的模块文件夹。

## PackageManagement 与 PowerShellGet 关系？ （高级别答案）

PackageManagement 是用于任何程序包管理器处理公共接口。 最终，无论您正在处理 PowerShell 模块、 Msi、 拼音以前、 NuGet 程序包或 Perl 模块，您应该能够使用 PackageManagement 的命令 （查找程序包和安装程序包） 以查找并安装它们。 PackageManagement 执行此操作通过让每个程序包经理插入 PackageManagement 包提供商。 提供商执行所有的实际工时。它们存储库中，从获取内容并安装在本地的内容。 通常情况下，包提供程序只需环绕给定的程序包类型的现有程序包管理器工具。

PowerShellGet 是 PowerShell 项目程序包管理器。 没有 PowerShellGet 通过公开功能 PackageManagement PSModule 包提供商处。 因此，您可以运行[安装模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)或安装包-提供商 PSModule 从 PowerShell 库安装模块。 无法访问某些 PowerShellGet 功能，包括[更新模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)和[发布模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)，通过 PackageManagement 命令。

总之，PowerShellGet 仅致力于遇到 PowerShell 内容 premium 程序包管理体验。 PackageManagement 侧重公开通过常规的一组工具的所有程序包管理体验。 查找此应答 unsatisfying 中, 是否有此文档，底部详尽回答**PackageManagement 实际上与有何 PowerShellGet？**部分。

有关详细信息，请访问[PackageManagement 项目页面](http://oneget.org/)。

## NuGet 与 PowerShellGet 关系？

PowerShell 库是修改的[NuGet 库](http://www.nuget.org/)的版本。 PowerShellGet 使用 NuGet 提供程序使用 PowerShell 库等 NuGet 基于存储库。

您可以对任何有效的 NuGet 存储库或文件共享使用 PowerShellGet。 您只需通过运行[**Register PSRepository**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet 添加存储库。

## 这是否意味着我可以使用 NuGet.exe 使用库？

是的。

## PackageManagement 实际上与有何 PowerShellGet？ （技术详细信息）

在高级选项，下 PowerShellGet 时段利用 PackageManagement 基础结构。

PowerShell cmdlet 图层，在[安装模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)是真正的精简包装安装程序包的提供商 PSModule。

在 PackageManagement 包提供商图层，PSModule 包提供商实际呼叫到其他 PackageManagement 包提供商。 例如，当您使用的基于 NuGet （如 PowerShell 库） 的库，PSModule 包提供商使用 NuGet 程序包提供程序使用的存储库。

![PowerShellGet 体系结构](Images/powershellgetArchitecture.png)

图 1: PowerShellGet 体系结构

## 运行 PowerShellGet 需要是什么？

一般而言，我们建议选取 PowerShellGet 模块 （请注意，它需要.NET 4.5） 的最新版本。

**PowerShellGet**模块需要**PowerShell 3.0 或更高版本**。

因此， **PowerShellGet**需要以下操作系统之一︰

- Windows 10
- Windows 8.1 Pro
- Windows 8.1 企业版
- Windows 7 SP1
- Windows 2016 Server
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1

**PowerShellGet**还需要.NET Framework 4.5 或更高。 您可以安装.NET Framework 4.5 或更高从[此处](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx)。

## 是否可以预订将发布在将来的项目名称？

不能为蹲坐式项目名称。 如果您认为现有项目已采取适合您的更多项的名称，请尝试[联系项目的所有者](psgallery_contacting_item_owners.md)。 如果您没有在几个星期内收到响应，您可以联系支持人员，并为其将查看 PowerShell 库工作组。

## 如何申请所有权的项目？

有关详细信息，请查看[在 PowerShellGallery.com 上管理项目的所有者](Managing-Item-Owners.md)。

## 如何处理项目所有者违反我项目许可证？

我们鼓励 PowerShell 社区协同工作来解决任何争议可能出现之间项目所有者和其他项目的所有者。  我们了精心设计的我们要求您按照之前 PowerShellGallery.com 管理员调解[争议解决过程](psgallery_dispute_resolution.md)。