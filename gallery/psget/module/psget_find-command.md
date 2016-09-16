# 查找命令

在模块中找到的 PowerShell 命令。

## 说明
查找命令 cmdlet 可找到的 PowerShell 命令，如 cmdlet、 别名、 函数和工作流。 查找命令搜索在存储库中的已注册的模块。
为此 cmdlet 可找到每个命令，则返回 PSGetCommandInfo 对象。 您可以将 PSGetCommandInfo 对象传递给安装模块 cmdlet 来安装该模块，其中包含的命令。

- 查找命令可以使用版本参数筛选︰ MinimumVersion，RequiredVersion，AllVersions。
  - 这些参数是互斥的。
  - 仅使用不带任何通配符的单个模块名称允许这些版本参数。
  - 如果未指定 RequiredVersion 参数，查找命令返回最新版本的是等于或大于指定的最低版本或模块的最新版本，如果没有最低版本指定的模块。
  - 如果指定了 RequiredVersion 参数，查找命令只返回与指定的版本完全匹配的模块的版本。
- 查找命令可以筛选模块元数据以及-标记参数
- 查找命令可以筛选搜索存储库特定语言的筛选器参数。
- 查找命令可以筛选所有或少注册存储库中的模块。

## Cmdlet 语法
```powershell
Get-Command -Name Find-Command -Module PowerShellGet -Syntax
```

## Cmdlet 联机帮助参考

[查找命令](http://go.microsoft.com/fwlink/?LinkId=733636)

## 示例命令
```powershell

# Find a specific command
Find-Command -Name Get-ScriptAnalyzerRule

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Get-ScriptAnalyzerRule              1.5.0      PSScriptAnalyzer                    PSGallery

# Find multiple commands
Find-Command -Name Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

# Find all available commands from all registered repositories
Find-Command

# Find available commands from few registered repositories
Find-Command -Repository PSGallery,PrivatePSGallery

# Find all commands in a specified repository
Find-Command -Repository PSGallery

# Find a command defined in a specific module
Find-Command -Name Get-ScriptAnalyzerRule -Module PSScriptAnalyzer

# Find commands from all versions of a module
Find-Command -ModuleName PSReadline -AllVersions

# Find commands with module name and MinimumVersion.
Find-Command -ModuleName PSReadline -MinimumVersion 1.1

# Find commands with module name and exact version
Find-Command -ModuleName AzureRM -RequiredVersion 1.4.0

# Find commands defined modules with -Filter based search. -Filter searches in description and module names
Find-Command -Filter Cookbook
Find-Command -Filter RBAC

# Find all commands with tags Azure or DSC in module metadata
Find-Command -Tag Azure, DSC

```