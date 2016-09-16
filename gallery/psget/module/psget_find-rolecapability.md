# 查找 RoleCapability

在模块中查找角色功能。

## 说明
查找 RoleCapability cmdlet 模块中查找 PowerShell 角色功能。 查找 RoleCapability 搜索在存储库中的已注册的模块。 对于此 cmdlet 可找到每个角色功能，则返回 PSGetRoleCapabilityInfo 对象。 您可以将 PSGetRoleCapabilityInfo 对象传递给安装模块 cmdlet 来安装包含角色功能的模块。
PowerShell 角色功能定义的命令，应用程序，依此类推可供用户只需足够管理 (JEA) 终结点。 由文件扩展名为.psrc 定义角色功能。

- 查找 RoleCapability 可以使用版本参数筛选︰ MinimumVersion，RequiredVersion，AllVersions。
  - 这些参数是互斥的。
  - 仅使用不带任何通配符的单个模块名称允许这些版本参数。
  - 如果未指定 RequiredVersion 参数，查找 RoleCapability 返回最新版本的是等于或大于指定的最低版本或模块的最新版本，如果没有最低版本指定的模块。
  - 如果指定 RequiredVersion 参数，则查找 RoleCapability 只返回与指定的版本完全匹配的模块的版本。
- 查找 RoleCapability 可以筛选模块元数据以及-标记参数
- 查找 RoleCapability 可以筛选搜索存储库特定语言的筛选器参数。
- 查找 RoleCapability 可以筛选所有或少注册存储库中的模块。

## Cmdlet 语法
```powershell
Get-Command -Name Find-RoleCapability -Module PowerShellGet -Syntax
```

## Cmdlet 联机帮助引用

[查找 RoleCapability](http://go.microsoft.com/fwlink/?LinkId=718029)

## 示例命令
```powershell

# Find a specific role capability
Find-RoleCapability -Name Maintenance

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Maintenance                         1.5.0      RoleCapModule                       PrivatePSGallery

# Find multiple role capabilities
Find-RoleCapability -Name MyJeaRole, Maintenance

# Find all available role capabilities from all registered repositories
Find-RoleCapability

# Find available role capabilities from few registered repositories
Find-RoleCapability -Repository PSGallery,PrivatePSGallery

# Find all role capabilities in a specified repository
Find-RoleCapability -Repository PSGallery

# Find a role capability defined in a specific module
Find-RoleCapability -Name Maintenance -ModuleName RoleCapModule

# Find role capabilities from all versions of a module
Find-RoleCapability -ModuleName RoleCapModule -AllVersions

# Find role capabilities with module name and MinimumVersion.
Find-RoleCapability -ModuleName RoleCapModule -MinimumVersion 1.1

# Find role capabilities with module name and exact version
Find-RoleCapability -ModuleName RoleCapModule -RequiredVersion 1.4.0

# Find role capabilities defined modules with -Filter based search. -Filter searches in description and module names
Find-RoleCapability -Filter Cookbook
Find-RoleCapability -Filter RBAC

# Find all role capabilities with tags Azure or DSC in module metadata
Find-RoleCapability -Tag Azure, DSC

```