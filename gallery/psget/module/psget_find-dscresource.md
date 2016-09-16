# 查找 DscResource

在模块中查找 DSC 资源。

## 说明

查找 DscResource cmdlet 查找包含已注册的库中指定的条件相匹配的模块中的[所需状态配置 (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview)资源。
为此 cmdlet 可找到每个模块，查找 DscResource 返回到模块安装来安装模块包含此 cmdlet 返回所资源可以管道 PSGetDscResourceInfo 对象。

DSC 是一个新的管理平台，使部署和管理软件服务配置数据管理的环境这些服务在其中运行的 Windows PowerShell 中。

所需状态配置 (DSC) 资源 DSC 配置提供构建基块。 资源公开可以配置 （架构） 和包含本地配置管理器 (LCM) 呼叫以"使其"PowerShell 脚本函数的属性。

资源可以建模为常规为文件或作为 IIS 服务器设置为特定的内容。 类似资源组中合并到 DSC 模块，其组织中为可移植以及包含用于找出资源如何打算使用的元数据结构的所有所需的文件。

- 查找 DscResource 可以使用版本参数筛选︰ MinimumVersion，RequiredVersion，AllVersions。
  - 这些参数是互斥的。
  - 仅使用不带任何通配符的单个模块名称允许这些版本参数。
  - 如果未指定 RequiredVersion 参数，查找 DscResource 返回最新版本的是等于或大于指定的最低版本或模块的最新版本，如果没有最低版本指定的模块。
  - 如果指定 RequiredVersion 参数，则查找 DscResource 只返回与指定的版本完全匹配的模块的版本。
- 查找 DscResource 可以筛选模块元数据以及-标记参数
- 查找 DscResource 可以筛选特定存储库中的搜索语言与-筛选器参数。
- 查找 DscResource 可以筛选所有或少注册存储库中的模块。

## Cmdlet 语法
```powershell
Get-Command -Name Find-DscResource -Module PowerShellGet -Syntax
```

## Cmdlet 联机帮助引用

[查找 DscResource](http://go.microsoft.com/fwlink/?LinkId=517196)

## 示例命令
```powershell

# Find a specific DSC Resource
Find-DscResource -Name xIisFeatureDelegation

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
xIisFeatureDelegation               1.10.0.0   xWebAdministration                  PSGallery

# Find all available DSC Resources from all registered repositories
Find-DscResource

# Find a DSC resource by name
Find-DscResource -Name xWebsite

# Find multiple DSC Resources
Find-DscResource -Name xIisHandler, xFirewall

# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking
Find-DscResource -ModuleName xWebAdministration

# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

# Find available DSC Resources from few registered repositories
Find-DscResource -Repository PSGallery,PrivatePSGallery

# Find all DSC Resources in a specified repository
Find-DscResource -Repository PSGallery

# Find DSC Resources from all versions of a module
Find-DscResource -ModuleName xNetworking -AllVersions

# Find DSC Resources with module name and MinimumVersion.
Find-DscResource -ModuleName xNetworking -MinimumVersion 1.1

# Find DSC Resources with module name and exact version
Find-DscResource -ModuleName xNetworking -RequiredVersion 2.1.1

# Find DSC Resources defined modules with -Filter based search. -Filter searches in description and module names
Find-DscResource -Filter Domain

# Find all DSC Resources with tags Azure or DSC in module metadata
Find-DscResource -Tag Azure, DSC

```
