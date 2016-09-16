# PowerShell 模块发现、 安装和使用 PowerShellGet 库存
 
PowerShellGet WMF 此版本中包括︰
-   查找模块可以筛选模块元数据以及-标记参数
-   查找模块可以筛选特定存储库中的搜索语言与-筛选器参数
-   查找模块可以基于模块筛选了-命令，-DscResource，内容，并-包括参数
-   查找 DscResource 允许发现存储库中的单个 DSC 资源
-   从安装和发布到 NuGet 的文件共享的支持

## 示例命令
```powershell
\# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

\# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

\#Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

\# Find all modules with Dsc resources
Find-Module -Includes DscResource

\# Find all modules with cmdlets
Find-Module -Includes Cmdlet

\# Find all modules with functions
Find-Module -Includes Function

\# Find all DSC resources
Find-DscResource

\# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking

\# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

\# Find modules using -Filter parameter
\# Specified filter value is searched in Name and Description properties
Find-Module -Filter Cookbook -Repository PSGallery
Find-Module -Filter RBAC -Repository PSGallery
```

## PowerShellGet 中的新增功能
-   并排比较版本支持 Windows PowerShell 5.0 或更高版本
-   模块相关性安装支持
-   三个新 cmdlet
    -   获取 InstalledModule
    -   卸载模块
    -   保存模块
    