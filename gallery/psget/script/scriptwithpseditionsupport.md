# 使用兼容 PowerShell 版本脚本
从开始版本 5.1，PowerShell 是这表示不同的功能集和平台兼容性的不同版本中可用。

- **桌面版︰**在.NET Framework 内置并提供与脚本和模块设定 PowerShell 的 Windows Server 核心如和 Windows 台式机的完整资源消耗版本上运行的版本兼容性。
- **核心版︰**基于.NET 核心，并提供与脚本和定位版本的 Windows，如 Nano Server 和 Windows IoT 缩减资源消耗版本上运行的 PowerShell 模块的兼容性。

PowerShell 运行 edition 所示的 $PSVersionTable PSEdition 属性。
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

脚本作者可以阻止脚本执行除非 PowerShell 上使用 PSEdition 参数是兼容版本上运行 #requires 语句。
```powershell
Set-Content C:\script.ps1 -Value "#requires -PSEdition Core
Get-Process -Name PowerShell"
Get-Content C:\script.ps1
#requires -PSEdition Core
Get-Process -Name PowerShell

C:\script.ps1
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a "#requires" statement for PowerShell Core edition. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.
At line:1 char:1
+ C:\script.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition
```

PowerShell 库用户可以找到的脚本上特定的 PowerShell 版支持的列表。
脚本而无需 PSEdition_Desktop 和 PSEditon_Core 都被视为正常处理 PowerShell 桌面版本。

```powershell

# Find scripts supported on PowerShell Desktop edition
Find-Script -Tag PSEditon_Desktop

# Find scripts supported on PowerShell Core editions
Find-Script -Tag PSEditon_Core

```

## 更多详细信息
### [带有 PSEditions 模块](../module/modulewithpseditionsupport.md)
### [在 PowerShellGallery PSEditions 支持](../../psgallery/psgallery_pseditions.md)

