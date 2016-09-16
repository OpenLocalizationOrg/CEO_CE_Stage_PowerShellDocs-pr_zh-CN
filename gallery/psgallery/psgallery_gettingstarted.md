# 开始使用 PowerShell 库

## 什么是 PowerShell 库？

PowerShell 库是 PowerShell 内容的中央存储库。
中，您可以找到包含 PowerShell 命令和所需状态配置 (DSC) 资源的有用 PowerShell 模块。 您也可以查找 PowerShell 脚本，其中某些可能包含 PowerShell 工作流和其分级显示一组任务，并提供了这些任务的顺序。
某些这些项由 Microsoft、 创作和其他人通过 PowerShell 社区创作。

## 要求

将项目从 PowerShell 库下载到您的系统要求[PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)模块。 您可以在以下任一找到 PowerShellGet 模块。 您不需要登录才能从 PowerShell 库下载项目。

-   [Windows 10](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409)
-   [Windows Management 5.0 Framework](http://go.microsoft.com/fwlink/?LinkId=398175)
-   [MSI 安装程序 （适用于 PowerShell 3 和 4)](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

PowerShellGet 还需要使用 PowerShell 库[NuGet 提供商](http://go.microsoft.com/fwlink/?LinkId=722208)。 系统将提示您安装的 PowerShellGet 首次使用时自动 NuGet 提供商，如果 NuGet 提供商不在以下位置之一︰

-   $env: ProgramFiles\\PackageManagement\\ProviderAssemblies
-   $env: LOCALAPPDATA\\PackageManagement\\ProviderAssemblies

或者，您可以运行**安装 PackageProvider-名称 NuGet-强制**自动下载和安装 NuGet 提供程序。

  
如果您有超过 2.8.5.201 NuGet 的版本，您需要呼叫以下 PowerShell cmdlet 安装并切换到 NuGet 最新版本。

1.  安装 PackageProvider NuGet MinimumVersion '2.8.5.201'-强制
2.  导入 PackageProvider NuGet MinimumVersion '2.8.5.201'-强制
3.  从上面的安装位置删除 NuGet 较旧版本。

有关详细信息，请参阅<http://oneget.org/> 。

  
注意︰ 由于包装格式更改，我们建议您更新到最新版本的 PowerShellGet 和 PackageManagement 安装最近已更新的项目。 PowerShellGet 包含在 Windows 10，您可以了解有关[下面](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409)。
PowerShellGet 也是您可以下载的一部分的 Windows Management Framework (WMF) 5.0，[下面介绍](http://go.microsoft.com/fwlink/?LinkId=398175)。

## 发现 PowerShell 库中的项目

使用此网站上，在**搜索**控件，或通过浏览模块和脚本页，您可以在 PowerShell 库中找到项目。 您也可以通过使用运行[**查找模块**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)和[**查找脚本**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet，具体取决于项类型中，查找 PowerShell 库中的项目**-知识库 PSGallery**。

可以使用以下参数[查找模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)和[查找脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)进行筛选库中的结果

- 名称
- AllVersions
- MinimumVersion
- RequiredVersion
- 标记
- 包括
- DscResource
- RoleCapability
- 命令
- 筛选器

如果您只是想发现特定 DSC 资源库中的，您可以运行[**查找 DscResource**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。
[**查找 DscResource**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)返回 DSC 资源包含在库中的数据。 因为 DSC 资源总是传送为模块的一部分，您仍需要运行[安装模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)以安装那些 DSC 资源。

## 学习使用 PowerShell 库中的项目

一旦您确定您感兴趣的项目，您可能想要了解有关详细信息。 您可以通过检查该项目的特定页面上的库来执行此操作。 在该页面上，您将能够查看所有项目使用上载的元数据。 此项目的元数据提供项目的作者和不能由 Microsoft 验证。 项目的所有者强烈仅限于库帐户用于发布该项目，并更可信比 Author 域。

如果您发现您认为项目未发布善意，该项目的页上单击**报表滥用**。

如果您正在运行[查找模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)或[查找脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)，您可以返回 PSGetModuleInfo 对象中查看这些数据。 例如，运行[**查找模块-名称 PSReadLine-知识库 PSGallery |获取成员**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)返回上 PSReadLine 模块库中的数据。

## 从 PowerShell 库下载项目

从 PowerShell 库下载项目时，我们建议以下过程︰

### 检查

若要从用于检查库下载项目，运行任一[**保存模块**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)或[**保存脚本**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet，具体取决于项目类型。 这允许您在本地保存该项目，而不安装它，并检查项内容。 请记住要手动删除已保存的项目。

某些这些项由 Microsoft、 创作和其他人通过 PowerShell 社区创作。 Microsoft 建议您查看的内容和代码在安装之前此库中的项目。

如果您发现您认为项目未发布善意，该项目的页上单击**报表滥用**。

### 安装

若要使用库中安装项目，请运行[**安装模块**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)或[**安装脚本**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet，具体取决于项目类型。

[安装模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)$env 到安装该模块︰ ProgramFiles\\WindowsPowerShell\\默认的模块。 这需要管理员帐户。 如果您添加**-范围 CurrentUser**参数，该模块安装到 $env: USERPROFILE\\文档\\WindowsPowerShell\\模块。

[安装脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)安装到 $env 脚本︰ ProgramFiles\\WindowsPowerShell\\默认脚本。 这需要管理员帐户。 如果您添加**-范围 CurrentUser**参数，该脚本安装到 $env: USERPROFILE\\文档\\WindowsPowerShell\\脚本。

默认情况下，[安装模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)和[安装脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)安装项目的最新版本。 若要安装较早版本的项目，请添加**-RequiredVersion**参数。

### 部署

要部署到 Azure 自动化 PowerShell 库中的项目，请单击项目详细信息页面上的**部署到 Azure 自动化**。 您将重定向到 Azure 管理门户中，在其中您登录通过 Azure 帐户凭据。 请注意，部署的依赖关系的项目将部署的依赖关系到 Azure 自动化。 可以通过将**AzureAutomationNotSupported**标记添加到您的项目元数据中禁用部署到 Azure 自动化按钮。

若要了解有关 Azure 自动化的详细信息，请参阅[Azure 自动化网站](http://azure.microsoft.com/en-us/services/automation/)。

## 更新 PowerShell 库中的项目

要更新从 PowerShell 库安装的项目，请运行的[更新模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)或[更新脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)cmdlet。 运行时不带任何其他参数，[更新模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)尝试更新运行[安装模块](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)已预装每个模块。
若要有选择地更新模块，请添加**-名称**参数。

同样，在运行时不带任何其他参数，[更新脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)也尝试更新通过运行[安装脚本](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)来安装每个脚本。
若要有选择地更新脚本，请添加**-名称**参数。

## 您已经安装 PowerShell 库中的列表项

若要了解您已经安装 PowerShell 库中的模块，请运行[**获取 InstalledModule**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。 此命令列出所有必须在您的系统直接从 PowerShell 库已安装的模块。

同样，若要了解您已经安装 PowerShell 库中的脚本，请运行[**获取 InstalledScript**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) cmdlet。 此命令列出所有直接从 PowerShell 库已安装的脚本必须在您的系统。
