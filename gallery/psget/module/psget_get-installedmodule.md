# 获取 InstalledModule

获取安装在计算机上的模块。

## 说明

获取 InstalledModule cmdlet 获取安装的 PowerShell 模块的计算机上安装了使用安装模块 cmdlet。

为每个已安装的模块，获取 InstalledModule 返回 PSRepositoryItemInfo 对象可以选择性地输送到卸载模块卸载安装的模块。

- 获取 InstalledModule 可以筛选安装基于名称、 版本参数的模块。
- 获取 InstalledModule 可以使用版本参数筛选︰ MinimumVersion、 MaximumVersion、 RequiredVersion、 AllVersions。
  - 这些参数是互斥的但 MinmimumVersion 和 MaximumVersion 除外。
  - 仅使用不带任何通配符的单个模块名称允许这些版本参数。
  - 如果未指定 RequiredVersion 参数，获取 InstalledModule 返回如果指定没有最低版本，则等于或大于指定的最低版本或模块的最新版本的安装模块最新版本。 
  - 如果指定 RequiredVersion 参数，则获取 InstalledModule 只返回与指定的版本完全匹配的安装模块的版本。

## Cmdlet 语法
```powershell
Get-Command -Name Get-InstalledModule -Module PowerShellGet -Syntax
```

## Cmdlet 联机帮助引用

[获取 InstalledModule](http://go.microsoft.com/fwlink/?LinkId=526863)

## 示例命令

```powershell

# Get all modules installed using PowerShellGet cmdlets
Get-InstalledModule

# Get a specific installed module
Get-InstalledModule DJoin

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        DJoin                               PSGallery            This is a PowerShell frontend to the DJOIN.exe c...

# Get installed module with wildcards
Get-InstalledModule -Name AzureRM*

# Get all versions of an installed module
Get-InstalledModule -Name AzureRM.Automation -AllVersions

# Get installed module with MinimumVersion
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0

# Get installed module with MaximumVersion
Get-InstalledModule -Name AzureRM.Automation -MaximumVersion 1.0.8

# Get installed module with version range
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0 -MaximumVersion 1.0.8

# Get installed module with RequiredVersion
Get-InstalledScript -Name AzureRM.Automation -RequiredVersion 1.0.3

# Properties of Get-InstalledModule returned object
Get-InstalledModule DJoin | Format-List * -Force

Name                       : DJoin
Version                    : 1.0
Type                       : Module
Description                : This is a PowerShell frontend to the DJOIN.exe command which provides better
                             discoverability and usability.
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 7:12:37 PM
InstalledDate              : 4/5/2016 4:13:39 PM
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSModule}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Modules\DJoin\1.0

```



## InstalledDate 和 UpdatedDate PSGetRepositoryItemInfo 对象中的属性

    During the install operation:
        InstalledDate: current DateTime (Get-Date) value
        UpdatedDate: null

    During the Update operation:
        InstalledDate: InstalledDate from the previous installation otherwise current DateTime (Get-Date) value
        UpdatedDate: current DateTime (Get-Date) value

```powershell
Install-Module -Name ContosoServer -RequiredVersion 1.0 -Repository INT
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM


\Update-Module -Name ContosoServer
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM 2/29/2016 12:00:15 PM
```