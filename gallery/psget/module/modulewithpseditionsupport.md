# 使用兼容 PowerShell 版本的模块
从开始版本 5.1，PowerShell 是这表示不同的功能集和平台兼容性的不同版本中可用。

- **桌面版︰**在.NET Framework 内置并提供与脚本和模块设定 PowerShell 的 Windows Server 核心如和 Windows 台式机的完整资源消耗版本上运行的版本兼容性。
- **核心版︰**基于.NET 核心，并提供与脚本和定位版本的 Windows，如 Nano Server 和 Windows IoT 缩减资源消耗版本上运行的 PowerShell 模块的兼容性。

## PowerShell 运行 edition 所示的 $PSVersionTable PSEdition 属性。
```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

## 模块作者可以将其与一个兼容的模块声明或使用 CompatiblePSEditions 模块的详细 PowerShell 版本清单键。 此键仅支持在 PowerShell 5.1 或更高版本。
*注意*一旦 CompatiblePSEditions 密钥指定模块清单，则不在较低版本的 PowerShell 导。

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$moduleInfo = Test-ModuleManifest -Path \TestModuleWithEdition.psd1
$moduleInfo.CompatiblePSEditions
Desktop
Core

$moduleInfo | Get-Member CompatiblePSEditions

   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}

```
当出现可用模块的列表，您可以通过 PowerShell edition 筛选列表。
```powershell
Get-Module -ListAvailable -PSEdition Desktop

    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions

Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
Desktop
Core

```

## 模块作者可以发布到任一或两个 PowerShell 版本 （桌面和核心） 的单个模块设定 

单个模块可以处理桌面和核心版本，该模块中作者在任一 RootModule 或使用 $PSEdition 变量模块清单中添加所需的逻辑。
模块可以具有不支持经过编译的 dll 设定 CoreCLR 和 FullCLR 两组。
下面是几个选项来打包逻辑加载正确 dll 模块。

### 方法 1︰ 包装面向多个版本和多个版本的 PowerShell 模块

#### 模块文件夹内容

 Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll Microsoft.Windows.PowerShell.ScriptAnalyzer.dll PSScriptAnalyzer.psd1 PSScriptAnalyzer.psm1 ScriptAnalyzer.format.ps1xml ScriptAnalyzer.types.ps1xml coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll en-US\about_PSScriptAnalyzer.help.txt en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll Settings\CmdletDesign.psd1 Settings\DSC.psd1 Settings\ScriptFunctions.psd1 Settings\ScriptingStyle.psd1 Settings\ScriptSecurity.psd1

#### PSScriptAnalyzer.psd1 文件的内容

```powershell
@{
 
# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

#### PSScriptAnalyzer.psm1 文件的内容
下面的逻辑加载所需的组件，具体取决于当前版本或版本。

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0') {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }    
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
} 

```

### 要加载的正确 Dll 和所需嵌套/模块的 PSD1 文件中的选项 2︰ 使用 $PSEdition 变量

在 PS 5.1 或更高版本 $PSEdition 全局变量允许模块清单文件中。
使用此变量，模块作者可以模块清单文件中指定条件的值。 受限的语言模式或数据部分中，可以引用 $PSEdition 变量。 

*注意*一旦模块清单指定与 CompatiblePSEditions 键或使用 $PSEdition 变量，不在较低版本的 PowerShell 导。


#### 示例模块清单的文件与 CompatiblePSEditions 键

```powershell
@{ 
# - - -
 
# Script module or binary module file associated with this manifest.
RootModule = if($PSEdition -eq 'Core')
{
'coreclr\MyCoreClrRM.dll'
}
else # Desktop
{
'clr\MyFullClrRM.dll'
}
 
# Supported PSEditions
CompatiblePSEditions = 'Desktop', 'Core'
 
# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = if($PSEdition -eq 'Core')
{
'coreclr\MyCoreClrNM1.dll',
'coreclr\MyCoreClrNM2.dll'
}
else # Desktop
{
'clr\MyFullClrNM1.dll',
'clr\MyFullClrNM2.dll'
}
 
# -- - -
}
```

#### 模块内容

```powershell

PS C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions> dir -Recurse
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
d-----         7/5/2016   1:37 PM                clr                                                                                 
d-----         7/5/2016   1:36 PM                coreclr                                                                             
-a----         7/5/2016   1:34 PM           4906 ModuleWithEditions.psd1                                                             
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
-a----         7/5/2016   1:35 PM              0 MyFullClrNM1.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyFullClrNM2.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyFullClrRM.dl                                                                      
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM1.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM2.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyCoreClrRM.dl                                                                      
```

## PowerShell 库的用户可以找到使用标记 PSEdition_Desktop 和 PSEditon_Core 模块上特定的 PowerShell 版支持的列表。
没有 PSEdition_Desktop 和 PSEditon_Core 标记模块都被视为正常处理 PowerShell 桌面版本。

```powershell

# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEditon_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEditon_Core

```


## 更多详细信息
### [与 PSEditions 脚本](../script/scriptwithpseditionsupport.md)
### [在 PowerShellGallery PSEditions 支持](../../psgallery/psgallery_pseditions.md)
