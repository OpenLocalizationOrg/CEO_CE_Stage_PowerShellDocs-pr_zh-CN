# 所需的状态配置 (DSC) 已知问题和限制

重大更改︰ 用于加密/解密 DSC 配置中的密码的证书可能不起作用安装 WMF 5.0 RTM 之后
--------------------------------------------------------------------------------------------------------------------------------

在 WMF 4.0 和 5.0 预览 WMF 版本 DSC 将不允许密码中配置的长度超过 121 字符。 强制 DSC 已使用短密码，即使需要较长和强密码。 此重大更改允许密码是 DSC 配置中的任意长度。

**分辨率︰**重新创建带有数据加密或密钥加密密钥用法和文档增强密钥用法 (1.3.6.1.4.1.311.80.1) 的证书。 Technet 文章<https://technet.microsoft.com/en-us/library/dn807171.aspx>包含详细信息。


DSC cmdlet 安装 WMF 5.0 RTM 后可能会失败
------------------------------------------------------------------------------------
开始 DscConfiguration 和其他 DSC cmdlet 可能会失败并出现以下错误安装 WMF 5.0 RTM 之后︰
```powershell
    LCM failed to retrieve the property PendingJobStep from the object of class dscInternalCache .
    + CategoryInfo : ObjectNotFound: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : MI RESULT 6
    + PSComputerName : localhost
```

**解析︰**删除 DSCEngineCache.mof 通过提升的 PowerShell 会话 （以管理员身份运行） 中运行以下命令︰
    
```powershell
Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof
```


如果 WMF 5.0 RTM 顶部 WMF 5.0 生产预览已安装的 DSC cmdlet 可能无法正常工作
------------------------------------------------------
**解析︰**（以管理员身份运行） 提升 PowerShell 会话中运行以下命令︰
```powershell
    mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof
```


LCM 进入不稳定的状态在 DebugMode 使用获取 DscConfiguration 时
-------------------------------------------------------------------------------

如果 LCM DebugMode 中，按 CTRL + C 以停止获取 DscConfiguration 处理可能会导致 LCM 以转到稳定此类不起作用的大部分 DSC cmdlet。

**分辨率︰**不在调试获取 DscConfiguration cmdlet 时按 CTRL + C。


停止 DscConfiguration 可能会在 DebugMode 挂起
------------------------------------------------------------------------------------------------------------------------
如果 LCM 位于 DebugMode，通过获取 DscConfiguration 尝试停止操作开始时可能会挂起停止 DscConfiguration

**分辨率︰**完成调试[DSC 资源脚本调试](#dsc-resource-script-debugging)部分中所述获取 DscConfiguration 启动操作。


DebugMode 中显示无详细的错误消息
-----------------------------------------------------------------------------------
如果 LCM 位于 DebugMode，从 DSC 资源不显示任何详细的错误消息。

**分辨率︰**禁用*DebugMode*以查看详细的邮件从资源


不能获取 DscConfigurationStatus cmdlet 检索调用 DscResource 操作
--------------------------------------------------------------------------------------
在使用后调用 DscResource cmdlet 直接调用任何资源的方法，这样操作的记录无法检索通过获取 DscConfigurationStatus 以后。

**分辨率︰**无。


获取 DscConfigurationStatus 返回提取循环操作键入*一致性*
---------------------------------------------------------------------------------
获取 DscConfigurationStatus cmdlet 时节点设置为提取刷新模式，每个提取操作执行，而不是*初始**一致性*为报表操作类型

**分辨率︰**无。

调用 DscResource cmdlet 不会返回邮件时所产生的顺序
---------------------------------------------------------------------------------
调用 DscResource cmdlet 不会返回详细信息，警告，和错误消息时所产生 LCM 或 DSC 资源的顺序。

**解析︰**无。


与调用 DscResource 一起使用时不能轻松地调试 DSC 资源
-----------------------------------------------------------------------
LCM 在调试模式下运行时 （请参阅[DSC 资源脚本调试](#dsc-resource-script-debugging)更多详细信息），调用 DscResource cmdlet 不会提供有关运行空间调试连接到的信息。
**分辨率︰**发现并将附加到使用 cmdlet**获取 PSHostProcessInfo**、 **Enter PSHostProcess** 、**获取运行空间**和**调试运行空间**调试 DSC 资源的运行空间。

```powershell
# Find all the processes hosting PowerShell
Get-PSHostProcessInfo

ProcessName ProcessId AppDomainName
----------- --------- -------------
powershell 3932 DefaultAppDomain
powershell_ise 2304 DefaultAppDomain
WmiPrvSE 3396 DscPsPluginWkr_AppDomain

# Enter the process that is hosting DSC engine (WMI process with DscPsPluginWkr_Appdomain)
Enter-PSHostProcess -Id 3396 -AppDomainName DscPsPluginWkr_AppDomain

# Find all the available rusnspaces in that process
Get-Runspace

Id Name ComputerName Type State Availability
-- ---- ------------ ---- ----- ------------
2 Runspace2 localhost Local Opened InBreakpoint
5 RemoteHost localhost Local Opened Busy

# Debug the runspace that is in **InBreakpoint** availability state
Debug-Runspace -Id 2
```


同一节点的各个部分配置文档不能具有相同的资源名称
------------------------------------------------------------------------------------------

对于将部署到单个节点的几个部分配置，相同的名称的资源原因运行时错误。

**解析︰**在不同部分配置中使用不同甚至相同资源的名称。


开始 DscConfiguration-UseExisting 不起作用与-凭据
------------------------------------------------------------------

当使用-UseExisting 参数开始 DscConfiguration – 凭据参数将被忽略。 DSC 使用默认进程标识继续进行操作。 当需要不同的凭据时继续远程节点，这会导致错误。

**分辨率︰**用于远程 DSC 操作 CIM 会话︰
```powershell
$session = New-CimSession -ComputerName $node -Credential $credential
Start-DscConfiguration -UseExisting -CimSession $session
```


为 DSC 配置中节点名称的 IPv6 地址
--------------------------------------------------
在此版本中不支持 IPv6 地址为 DSC 配置脚本中的节点名称。

**分辨率︰**无。


调试类基于 DSC 资源
--------------------------------------
在此版本中不支持调试类基于 DSC 资源。

**解析︰**无。


跨多个呼叫转接到 DSC 资源不保留变量和 DSC 类基于资源中 $script 范围中定义的函数 
-------------------------------------------------------------------------------------------------------------------------------------

如果配置为使用任何基于课堂资源变量或 $script 范围中定义的函数，多个连续的呼叫转接到开始 DSCConfiguration 将失败。

**分辨率︰**DSC 资源类本身中定义所有变量和函数。 No $script 范围变量/函数。


DSC 资源调试资源使用 PSDscRunAsCredential 时
----------------------------------------------------------------------
DSC 资源调试资源配置中使用*PSDscRunAsCredential*属性时不在此版本中的 suported。

**分辨率︰**无。


DSC 复合资源不支持 PsDscRunAsCredential
----------------------------------------------------------------

**分辨率︰**如果可用，请使用凭据属性。 示例 ServiceSet 和 WindowsFeatureSet


*获取 DscResource-语法*不正确反映 PsDscRunAsCredential
-------------------------------------------------------------------------
获取 DscResource-语法并不反映 PsDscRunAsCredential 正确时将其标记为必需的资源，或不支持。

**分辨率︰**无。 但是，创作 ISE 中的配置反映正确的元数据有关 PsDscRunAsCredential 属性时使用智能感知。


WindowsOptionalFeature 不可用在 Windows 7 中
-----------------------------------------------------

WindowsOptionalFeature DSC 资源不可用在 Windows 7 中。 此资源需要 DISM 模块，可在 Windows 8 和更高版本的 Windows 操作系统中启动的 DISM cmdlet。

基于类 DSC 资源导入 DscResource ModuleVersion 可能无法按预期工作   
------------------------------------------------------------------------------------------
如果编译节点有多个版本的基于类 DSC 资源模块，`Import-DscResource -ModuleVersion`不选择指定的版本，导致以下编译错误。

```
ImportClassResourcesFromModule : Exception calling "ImportClassResourcesFromModule" with "3" argument(s): "Keyword 'MyTestResource' already defined in the configuration."
At C:\Windows\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:2035 char:35
+ ... rcesFound = ImportClassResourcesFromModule -Module $mod -Resources $r ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [ImportClassResourcesFromModule], MethodInvocationException
    + FullyQualifiedErrorId : PSInvalidOperationException,ImportClassResourcesFromModule
```

**分辨率︰**通过定义*ModuleSpecification*对象导入所需的版本`-ModuleName`与`RequiredVersion`密钥指定，如下所示︰
``` PowerShell  
Import-DscResource -ModuleName @{ModuleName='MyModuleName';RequiredVersion='1.2'}  
```  

开始等注册表资源一些 DSC 资源可能会花费很长的时间来处理此请求。
--------------------------------------------------------------------------------------------------------------------------------

**Resolution1:**创建以下文件夹定期清理计划任务。
``` PowerShell 
$env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis 
```

**Resolution2:**更改 DSC 配置清理配置末尾处的*CommandAnalysis*文件夹。
``` PowerShell
Configuration $configName
{

   # User Data
    Registry SetRegisteredOwner
    {
        Ensure = 'Present'
        Force = $True
        Key = $Node.RegisteredKey
        ValueName = $Node.RegisteredOwnerValue
        ValueType = 'String'
        ValueData = $Node.RegisteredOwnerData
    }
    #
    # Script to delete the config 
    #
    script DeleteCommandAnalysisCache
    {
        DependsOn="[Registry]SetRegisteredOwner"
        getscript="@{}"
        testscript = 'Remove-Item -Path $env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis -Force -Recurse -ErrorAction SilentlyContinue -ErrorVariable ev | out-null;$true'
        setscript = '$true'
    }
}
```
