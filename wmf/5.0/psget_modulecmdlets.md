# 模块管理 PowerShellGet Cmdlet

- [查找 DscResource](https://technet.microsoft.com/en-us/library/mt654006.aspx)
- [查找模块](https://technet.microsoft.com/en-us/library/dn807167.aspx)
- [查找脚本](https://technet.microsoft.com/en-us/library/mt654001.aspx)
- [获取 InstalledModule](https://technet.microsoft.com/en-us/library/mt653990.aspx)
- [获取 InstalledScript](https://technet.microsoft.com/en-us/library/mt653994.aspx)
- [获取 PSRepository](https://technet.microsoft.com/en-us/library/dn807170.aspx)
- [安装模块](https://technet.microsoft.com/en-us/library/dn807162.aspx)
- [安装脚本](https://technet.microsoft.com/en-us/library/mt653998.aspx)
- [新 ScriptFileInfo](https://technet.microsoft.com/en-us/library/mt653995.aspx)
- [发布模块](https://technet.microsoft.com/en-us/library/dn807163.aspx)
- [发布脚本](https://technet.microsoft.com/en-us/library/mt654003.aspx)
- [注册 PSRepository](https://technet.microsoft.com/en-us/library/dn807168.aspx)
- [保存模块](https://technet.microsoft.com/en-us/library/mt653992.aspx)
- [保存脚本](https://technet.microsoft.com/en-us/library/mt654004.aspx)
- [设置 PSRepository](https://technet.microsoft.com/en-us/library/dn807165.aspx)
- [测试 ScriptFileInfo](https://technet.microsoft.com/en-us/library/mt654005.aspx)
- [卸载模块](https://technet.microsoft.com/en-us/library/mt653996.aspx)
- [卸载脚本](https://technet.microsoft.com/en-us/library/mt653989.aspx)
- [更新模块](https://technet.microsoft.com/en-us/library/dn807166.aspx)
- [更新 ModuleManifest](https://technet.microsoft.com/en-us/library/mt654002.aspx)
- [更新脚本](https://technet.microsoft.com/en-us/library/mt653997.aspx)
- [更新 ScriptFileInfo](https://technet.microsoft.com/en-us/library/mt653991.aspx)
- [注销 PSRepository](https://technet.microsoft.com/en-us/library/dn807161.aspx)

## 获取 InstalledModule 和卸载模块 cmdlet 模块相关性安装支持
- 添加模块相关性总体中发布模块 cmdlet。 在准备模块的依赖项列表中使用的 PSModuleInfo RequiredModules 和 NestedModules 列表用于发布。
- 若要增加的相关性安装模块和更新模块 cmdlet 安装支持。 安装和更新默认模块依赖关系。
- 添加要包括在结果中的模块依赖关系的查找模块 cmdlet-IncludeDependencies 参数。
- 查找模块上添加-MaximumVersion 支持安装模块和更新模块 cmdlet。
- 添加新的获取 InstalledModule 和卸载模块 cmdlet。

## 与模块相关性 PowerShellGet cmdlet 演示支持︰

### 确保模块相关性上存储库中可用︰
```powershell
Find-Module -Repository LocalRepo -Name RequiredModule1,RequiredModule2,RequiredModule3,NestedRequiredModule1,NestedRequiredModule2,NestedRequiredModule3 | Sort-Object -Property Name

Version    Name                     Repository    Description                  
-------    ----                     ----------    -----------                  
2.5        NestedRequiredModule1    LocalRepo     NestedRequiredModule1 module 
2.5        NestedRequiredModule2    LocalRepo     NestedRequiredModule2 module 
2.0        NestedRequiredModule3    LocalRepo     NestedRequiredModule3 module 
2.5        RequiredModule1          LocalRepo     RequiredModule1 module  
2.5        RequiredModule2          LocalRepo     RequiredModule2 module  
2.0        RequiredModule3          LocalRepo     RequiredModule3 module
```

### 创建包含其模块清单 RequiredModules 和 NestedModules 属性中指定的依赖关系的模块。
```powershell
$RequiredModules = @('RequiredModule1',
                     @{ModuleName = 'RequiredModule2'; ModuleVersion = '1.5'; },
                     @{ModuleName = 'RequiredModule3'; RequiredVersion = '2.0'; })

$NestedRequiredModules = @('TestDepWithNestedRequiredModules1.psm1', 'NestedRequiredModule1',
                            @{ModuleName = 'NestedRequiredModule2'; ModuleVersion = '1.5'; },
                            @{ModuleName = 'NestedRequiredModule3'; RequiredVersion = '2.0'; })

New-ModuleManifest -Path 'C:\Program Files\WindowsPowerShell\Modules\TestDepWithNestedRequiredModules1\TestDepWithNestedRequiredModules1.psd1' `
-NestedModules $NestedRequiredModules -RequiredModules $RequiredModules -ModuleVersion "1.0" -Description "TestDepWithNestedRequiredModules1 module"
```

###  发布 TestDepWithNestedRequiredModules1 模块与存储库的依赖关系的两个版本 （**"1.0"**和**"2.0"**）。
```powershell
Publish-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -NuGetApiKey "MyNuGet-ApiKey-For-LocalRepo"
```

###  通过指定-IncludeDependencies 查找与其依赖项的 TestDepWithNestedRequiredModules1 模块。
```powershell
Find-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo –IncludeDependencies -MaximumVersion "1.0"

Version    Name                                Repository  Description 
-------    ----                                ----------  -----------  
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module  
2.5        RequiredModule1                     LocalRepo   RequiredModule1 module      
2.5        RequiredModule2                     LocalRepo   RequiredModule2 module      
2.0        RequiredModule3                     LocalRepo   RequiredModule3 module      
2.5        NestedRequiredModule1               LocalRepo   NestedRequiredModule1 module
2.5        NestedRequiredModule2               LocalRepo   NestedRequiredModule2 module
2.0        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
``` 

### 查找模块元数据用于查找模块依赖关系。
```powershell
$psgetModuleInfo = Find-Module -Repository MSPSGallery -Name ModuleWithDependencies2
$psgetModuleInfo.Dependencies.ModuleName

RequiredModule1
RequiredModule2
RequiredModule3
NestedRequiredModule1
NestedRequiredModule2
NestedRequiredModule3

$psgetModuleInfo.Dependencies

Name Value
---- -----
ModuleName RequiredModule1
CanonicalId PowerShellGet:RequiredModule1/#http://psget/psGallery/api/v2/

ModuleName RequiredModule2
ModuleVersion 2.0
CanonicalId PowerShellGet:RequiredModule2/2.0#http://psget/psGallery/api/v2/

ModuleName RequiredModule3
RequiredVersion 2.5
CanonicalId PowerShellGet:RequiredModule3/2.5#http://psget/psGallery/api/v2/

ModuleName NestedRequiredModule1
CanonicalId PowerShellGet:NestedRequiredModule1/#http://psget/psGallery/api/v2/

ModuleName NestedRequiredModule2
ModuleVersion 2.0
CanonicalId PowerShellGet:NestedRequiredModule2/2.0#http://psget/psGallery/api/v2/

ModuleName NestedRequiredModule3
RequiredVersion 2.5
CanonicalId PowerShellGet:NestedRequiredModule3/2.5#http://psget/psGallery/api/v2/
```

###  与相关性安装 TestDepWithNestedRequiredModules1 模块。
```powershell
Install-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -RequiredVersion "1.0"
Get-InstalledModule

Version    Name                    Repository   Description                 
-------    ----                    ----------   -----------                 
1.0        NestedRequiredModule1   LocalRepo    NestedRequiredModule1 module
2.5        NestedRequiredModule2   LocalRepo    NestedRequiredModule2 module
2.0        NestedRequiredModule3   LocalRepo    NestedRequiredModule3 module
1.0        RequiredModule1         LocalRepo    RequiredModule1 module      
2.5        RequiredModule2                    LocalRepo    RequiredModule2 module 
2.0        RequiredModule3                    LocalRepo    RequiredModule3 module 
1.0        TestDepWithNestedRequiredModules1  LocalRepo    TestDepWithNestedRequiredModules1 module
```

###  更新与相关性 TestDepWithNestedRequiredModules1 模块。
```powershell
Find-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -AllVersions

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module

Update-Module -Name TestDepWithNestedRequiredModules1 -RequiredVersion 2.0
Get-InstalledModule

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        NestedRequiredModule1               LocalRepo   NestedRequiredModule1 module
2.5        NestedRequiredModule2               LocalRepo   NestedRequiredModule2 module
2.0        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
2.5        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
1.0        RequiredModule1                     LocalRepo   RequiredModule1 module
2.5        RequiredModule2                     LocalRepo   RequiredModule2 module
2.0        RequiredModule3                     LocalRepo   RequiredModule3 module
2.5        RequiredModule3                     LocalRepo   RequiredModule3 module
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
```

###  运行卸载模块 cmdlet 卸载您使用 PowerShellGet 安装的模块。
如果任何其他模块取决于您确实要删除的模块，PowerShellGet 会引发错误。
```powershell
Get-InstalledModule -Name RequiredModule1 | Uninstall-Module

PackageManagement\Uninstall-Package : The module 'RequiredModule1' of version '2.5' in module base folder 'C:\Program Files\WindowsPowerShell\Modules\RequiredModule1\2.5' cannot be uninstalled, because one or more other modules 'ModuleWithDependencies2' are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'RequiredModule1'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\PSGet.psm1:1303 char:25
+ ... $null = PackageManagement\\Uninstall-Package @PSBoundParameters
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Package], Exception
+ FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.UninstallPackage
```

## 保存模块 cmdlet
```powershell
Save-Module -Repository MSPSGallery -Name ModuleWithDependencies2 -Path C:\MySavedModuleLocation
dir C:\MySavedModuleLocation

Directory: C:\MySavedModuleLocation

Mode LastWriteTime Length Name
---- ------------- ------ ----
d----- 4/21/2015 5:40 PM ModuleWithDependencies2
d----- 4/21/2015 5:40 PM NestedRequiredModule1
d----- 4/21/2015 5:40 PM NestedRequiredModule2
d----- 4/21/2015 5:40 PM NestedRequiredModule3
d----- 4/21/2015 5:40 PM RequiredModule1
d----- 4/21/2015 5:40 PM RequiredModule2
d----- 4/21/2015 5:40 PM RequiredModule3
```

## 更新 ModuleManifest cmdlet
此新 cmdlet 用于帮助清单面额输入的属性的文件的更新。 需要测试 ModuleManifest 的所有参数。

我们注意到了大量模块作者想要指定"\*"中导出的值，如 FunctionsToExport，CmdletsToExport，等等。期间模块发布到 PowerShell 库，未指定的功能和命令不会填充正确拖到库。 因此，我们建议模块作者更新各自的清单具有正确的值。

如果您有已导出属性的模块，更新 ModuleManifest 将填充指定的清单文件中导出的函数、 cmdlet、 变量等的信息︰
```powershell
Get-Content -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
@{
# Script module or binary module file associated with this manifest.
# RootModule = ''
# Version number of this module.
ModuleVersion = '2.5'
# ID used to uniquely identify this module
GUID = '610e5c5b-dc42-4eaa-8511-ebfb44066d5e'

#(Other properties removed here for Simplicity…)

# Functions to export from this module
FunctionsToExport = '*'
# Cmdlets to export from this module
CmdletsToExport = '*'
# Variables to export from this module
VariablesToExport = '*'
# Aliases to export from this module
AliasesToExport = '*'
}
```

后更新-ModuleManifest:
```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
Get-Content -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
#
# Module manifest for module 'NewManifest'
#
# Generated by: author name
#
# Generated on: 11/13/2015
#
@{
# Script module or binary module file associated with this manifest.
# RootModule = ''
# Version number of this module.
ModuleVersion = '2.5'
# ID used to uniquely identify this module
GUID = '610e5c5b-dc42-4eaa-8511-ebfb44066d5e'
# Functions to export from this module
FunctionsToExport = 'Get-FooFn Get-FooWF'
# Cmdlets to export from this module
CmdletsToExport = 'Test-PSGetTestCmdlet'
}
```

对于每个模块，也有一些与其关联的元数据字段。 为了在 PowrShell 库中正确显示元数据，可以使用更新 ModuleManifest 来填充这些字段在专用数据下。
```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1" -Tags "Tag1" -LicenseUri "http://license.com" -ProjectUri "http://project.com" -IconUri "http://icon.com" -ReleaseNotes "Test module"
```
从清单的文件模板的专用数据哈希表具有以下属性︰
```powershell
# Private data to pass to the module specified in RootModule/ModuleToProcess. This may also contain a PSData hashtable with additional module metadata used by PowerShell.
PrivateData = @{
    PSData = @{
        # Tags applied to this module. These help with module discovery in online galleries.
        # Tags = @()

        # A URL to the license for this module.
        # LicenseUri = ''
    
        # A URL to the main website for this project.
        # ProjectUri = ''
        
        # A URL to an icon representing this module.
        # IconUri = ''
        
        # ReleaseNotes of this module
        # ReleaseNotes = ''
        
        # External dependent modules of this module
        # ExternalModuleDependencies = ''
    } # End of PSData hashtable
} # End of PrivateData hashtable
```
***注意︰***在最新的 PowerShell 5.0 仅支持 DscResourcesToExport。 我们无法更新域，如果您运行的早期 PowerShell 版本。
