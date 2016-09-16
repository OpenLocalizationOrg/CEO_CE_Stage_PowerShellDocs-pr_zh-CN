# 获取 InstalledScript

获取在计算机上安装脚本。

## 说明

获取 InstalledScript cmdlet 获取的计算机上已安装的 PowerShell 脚本。

对于每个已安装的脚本，获取 InstalledScript 返回 PSRepositoryItemInfo 对象可以选择性地输送到卸载脚本卸载已安装的脚本。

- 获取 InstalledScript 可以筛选已安装的脚本基于名称、 版本参数。
- 获取 InstalledScript 可以使用版本参数筛选︰ MinimumVersion、 MaximumVersion、 RequiredVersion、 AllVersions。
  - 这些参数是互斥的但 MinmimumVersion 和 MaximumVersion 除外。
  - 仅使用单个脚本名称不带任何通配符允许这些版本参数。
  - 如果未指定 RequiredVersion 参数，获取 InstalledScript 返回才等于或大于指定的最低版本或最新版本的脚本指定无最小版本的安装脚本最新版本。 
  - 如果指定 RequiredVersion 参数，则获取 InstalledScript 只返回与指定的版本完全匹配的安装脚本的版本。

## Cmdlet 语法

```powershell
Get-Command -Name Get-InstalledScript -Module PowerShellGet -Syntax
```

## Cmdlet 联机帮助引用

[获取 InstalledScript](http://go.microsoft.com/fwlink/?LinkId=619790)

## 示例命令

```powershell

# Get all scripts installed using PowerShellGet cmdlets
Get-InstalledScript

# Get a specific installed script
Get-InstalledScript Show-Tree

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0.0      Show-Tree                           PSGallery            Script to show the layout of PowerShell namespaces (Tr...

# Get installed script with wildcards
Get-InstalledScript -Name *Azure*

# Get all versions of an installed script
Get-InstalledScript -Name Connect-O365 -AllVersions

# Get installed script with MinimumVersion
Get-InstalledScript -Name Connect-O365 -MinimumVersion 1.1

# Get installed script with MaximumVersion
Get-InstalledScript -Name Connect-O365 -MaximumVersion 1.6.3

# Get installed script with version range
Get-InstalledScript -Name Connect-O365 -MinimumVersion 1.1 -MaximumVersion 1.6.3

# Get installed script with RequiredVersion
Get-InstalledScript -Name Connect-O365 -RequiredVersion 1.4

# Properties of Get-InstalledScript returned object
Get-InstalledScript Show-Tree | Format-List * -Force

Name                       : Show-Tree
Version                    : 1.0.0
Type                       : Script
Description                : Script to show the layout of PowerShell namespaces (Trees) using ASCII
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 10:15:35 PM
InstalledDate              : 5/4/2016 11:44:13 PM
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSScript}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Scripts


```