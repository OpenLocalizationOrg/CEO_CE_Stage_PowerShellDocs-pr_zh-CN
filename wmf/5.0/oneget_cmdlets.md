# PackageManagement Cmdlet
这是 PackageManagement 支持软件发现、 安装和库存 (SDII) 的核心。 请尝试这些操作的 cmdlet:
-   查找包
-   查找 PackageProvider
-   获取包
-   获取 PackageProvider
-   获取 PackageSource
-   导入 PackageProvider
-   安装程序包
-   安装 PackageProvider
-   注册 PackageSource
-   保存程序包
-   设置 PackageSource
-   卸载程序包
-   注销 PackageSource

PackageManagement 是 PowerShell 模块，您可以执行下列操作以更新 PackageManagement 本身︰
```powershell
PS C:\> Install-Module PackageManagement –Force
```
在此例中，您必须向重新输入 PowerShell 会话，切换到 PackageManagement 最新版本。

## [查找程序包 Cmdlet](https://technet.microsoft.com/en-us/library/dn890709.aspx)
此 cmdlet 允许发现软件包使用可用程序包源中的加载包提供商。
```powershell
# Find all available Windows PowerShell module packages from galleries registered
# with PowerShellGet provider
Find-Package -Provider PowerShellGet -Source PSGallery

# Find a package from a provider that is not yet installed
# This will bootstrap NuGet provider and then search for jquery package using NuGet
# with <http://www.nuget.org/api/v2/> as source
Find-Package -Name jquery –Provider NuGet -Source http://www.nuget.org/api/v2/

# Find package with name and version
# Here we are assuming that the user already registered nuget.org using
# Register-PackageSource. You can specify either the provider or the source, or
# neither. For the latter, performance may be less optimal as it searches through all
# the providers and registered sources.
Find-Package -Name jquery –Provider NuGet –RequiredVersion 2.1.4 -Source nuget.org
```

## [查找 PackageProvider Cmdlet](https://technet.microsoft.com/en-us/library/mt676544.aspx)
查找 PackageProvider cmdlet 查找匹配 PackageManagement 提供程序在注册 PowerShellGet 程序包源中都可用。 以下是可用于安装 PackageProvider cmdlet 安装包提供程序。 默认情况下，这在 PowerShell 库中的 PackageManagement 和提供商标签包括可用的模块。 

查找 PackageProvider 还会找到匹配 PackageManagement 提供商，我们使用查找和安装它们 PackageManagement boostrapper 提供商的 PackageManagement azure blob 存储中的可用。
```powershell
#Find all available package providers in PackageManagement azure blob store as well as in PowerShellGallery.com
Find-PackageProvider

#Find all versions of a provider
Find-PackageProvider -Name "Nuget" -AllVersions

#Find a provider from a specified source
Find-PackageProvider -Name "Gistprovider" -Source "PSGallery"
```

## [获取程序包 Cmdlet](https://technet.microsoft.com/en-us/library/dn890704.aspx)
此 cmdlet 返回的所有软件包使用 PackageManagement 已安装的列表。
```powershell
# Get all the packages installed by Programs provider
Get-Package –Provider Programs

# Get all the packages installed by NuGet provider at c:\test using the dynamic
# parameter destination
Get-Package –Provider NuGet -Destination c:\test
```

## [获取 PackageProvider Cmdlet](https://technet.microsoft.com/en-us/library/dn890703.aspx)
可以使用 cmdlet 盘点包提供程序加载并准备好在本地计算机上使用。
```powershell
# Get all currently loaded package providers
Get-PackageProvider

# The following cmdlet will show all the package providers available on the machine (including those that are not loaded):
Get-PackageProvider -ListAvailable
```

## [获取 PackageSource Cmdlet](https://technet.microsoft.com/en-us/library/dn890705.aspx)
此 cmdlet 包提供商获取的已注册的包源的列表。
```powershelll
# Get all package sources
Get-PackageSource

# Get all package sources for a specific provider
Get-PackageSource –ProviderName PowerShellGet
```

## [导入 PackageProvider Cmdlet](https://technet.microsoft.com/en-us/library/mt676545.aspx)
此 cmdlet 添加到当前会话包管理包提供商。
```powershell
# Import a package provider from the local machine
Import-PackageProvider –Name MyProvider

#The -Name parameter can be either the name of the provider or the full path to the provider. Currently, we support .dll, .exe and.psm1 for the full path case. If the name of the provider is used for the -Name parameter, then additional version parameters such as -RequiredVersion, -MinimumVersion and -MaximumVersion may be specified. Otherwise, the latest version of the provider will be imported.

#If a package provider is not yet loaded to your system, we can discover and install on-demand. You can use explicit discovery and install cmdlets to do so:
 Find-PackageProvider
 Install-PackageProvider –Name MyProvider

#After installed, follow the Import-PackageProvider to load it to your system.

# Import a specific version of a package provider. PackageManagement supports installations of multiple versions of a package provider using PackageProvider cmdlets (not by bootstrapper provider). You can install another version of a package provider given that you already have one up running by:
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force
Get-PackageProvider –ListAvailable
Import-PackageProvider –Name "Nuget" -RequiredVersion "2.8.5.201" -Verbose
Import-PackageProvider –Name MyProvider –RequiredVersion xxxx -force
```

##[ 安装程序包 Cmdlet](https://technet.microsoft.com/en-us/library/dn890711.aspx)

此 cmdlet 允许使用可用的程序包源中的软件包安装加载包提供商。
```powershell
# Install a package by name.
# NuGet provider requires us to provide the dynamic parameter destination path
# when we use this provider to install. Not all providers will require you to supply
# dynamic parameters for PackageManagement cmdlets.
Install-Package -Name jquery -Source nuget.org -Destination c:\test

# Install a package by piping.
Find-Package -Name jquery –Provider NuGet | Install-Package -Destination c:\test
```

## [安装 PackageProvider Cmdlet](https://technet.microsoft.com/en-us/library/mt676543.aspx)
此 cmdlet 安装一个或多个数据包管理包提供商。
```powershell
# Install a package provider from the PowerShell Gallery
Install-PackageProvider –Name "Gistprovider" -Verbose

# Install a specified version of a package provider
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force

# Find a provider and install it
Find-PackageProvider –Name "Gistprovider" | Install-PackageProvider -Verbose

# Install a provider to the current user’s module folder
Install-PackageProvider –Name Gistprovider –Verbose –Scope CurrentUser
```

## [注册 PackageSource Cmdlet](https://technet.microsoft.com/en-us/library/dn890701.aspx)
此 cmdlet 添加程序包源指定的包提供商。
每个 PackageManagement 提供商可能有一个或多个软件源或存储库。 PackageManagement 提供 PowerShell cmdlet 到添加/删除/查询源。 例如，您可以注册 NuGet 提供商程序包源︰
```powershell
Register-PackageSource -Name "NugetSource" -Location "http://www.nuget.org/api/v2" –ProviderName nuget
```

## [保存程序包 Cmdlet](https://technet.microsoft.com/en-us/library/dn890708.aspx)
此 cmdlet 将程序包保存到本地计算机，而不安装它们。
```powershell
# Saves jquery package to c:\test using NuGetProvider
# Notes that the -Path parameter must point to an existing location
Save-Package -Name jquery –Provider NuGet -Path c:\test

# Save a package by piping.
Find-Package -Name jquery -Source http://www.nuget.org/api/v2/ | Save-Package -Path c:\test
Find-Package -source c:\test
```

## [设置 PackageSource Cmdlet](https://technet.microsoft.com/en-us/library/dn890710.aspx)
此 cmdlet 更改现有程序包源的信息。 
```powershell
#Set-PackageSource changes the values for a source that has already been registered by running the Register-PackageSource cmdlet. By #running Set-PackageSource, you can change the source name and location.
Set-PackageSource  -Name nuget.org -Location  http://www.nuget.org/api/v2 -NewName nuget2 -NewLocation https://www.nuget.org/api/v2 
```

## [卸载程序包 Cmdlet](https://technet.microsoft.com/en-us/library/dn890702.aspx)
此 cmdlet 卸载本地计算机上安装程序包。
```powershell
# Uninstall jquery using nuget
Uninstall-Package -Name jquery –Provider NuGet -Destination c:\test

# Uninstall a package with by piping with Get-Package
Get-Package -Name jquery –Provider NuGet -Destination c:\test | Uninstall-Package
```

## [注销 PackageSource Cmdlet](https://technet.microsoft.com/en-us/library/dn890707.aspx)
```powershell
# Unregister a package source for the NuGet provider. You can use command Unregister-PackageSource, to disconnect with a repository, and Get-PackageSource, to discover what the repositories are associated with that provider.
Unregister-PackageSource  -Name "NugetSource"
```
