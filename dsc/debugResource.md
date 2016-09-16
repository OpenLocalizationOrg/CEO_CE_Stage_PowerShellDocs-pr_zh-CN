---
title: "调试 DSC 资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: e1922008a92f00c9ddab28598735839c25219d24
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 调试 DSC 资源

> 适用于︰ Windows PowerShell 5.0

PowerShell 5.0 中的新增功能引入了中所需状态配置 (DSC)，您可以根据应用配置调试 DSC 资源。

## 启用 DSC 调试
调试资源之前，必须启用调试通过致电[启用 DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx) cmdlet。 此 cmdlet 采用必需参数， **BreakAll**。 

您可以验证已启用调试看呼叫转接至[获取 DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx)的结果。 下面的 PowerShell 输出显示启用调试的结果︰


```powershell
PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
NONE

PS C:\DebugTest> Enable-DscDebug -BreakAll

PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
ForceModuleImport
ResourceScriptBreakAll

PS C:\DebugTest>
```


## 配置开头启用调试
若要调试 DSC 资源，您可以开始呼叫该资源的配置。 对于此示例中，我们来看呼叫[WindowsFeature](windowsfeatureResource.md)资源以确保"WindowsPowerShellWebAccess"功能的安装配置简单︰

```powershell
Configuration PSWebAccess
    {
    Import-DscResource -ModuleName 'PsDesiredStateConfiguration'
    Node localhost
        {
        WindowsFeature PSWA
            {
            Name = 'WindowsPowerShellWebAccess'
            Ensure = 'Present'
            }
        }
    }
PSWebAccess
```
编译后配置，通过致电[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx)中启动它。 本地配置管理器 (LCM) 呼叫进入配置中的第一个资源时，将停止配置。 如果您使用`-Verbose`和`-Wait`参数，输出显示您需要输入开始调试的行。

```powershell
PS C:\DebugTest> Start-DscConfiguration .\PSWebAccess -Wait -Verbose
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfiguration
Manager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Set      ]
WARNING: [TEST-SRV]:                            [DSCEngine] Warning LCM is in Debug 'ResourceScriptBreakAll' mode.  Resource script processing will 
be stopped to wait for PowerShell script debugger to attach.
VERBOSE: [TEST-SRV]:                            [DSCEngine] Importing the module C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateCo
nfiguration\DscResources\MSFT_RoleResource\MSFT_RoleResource.psm1 in force mode.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Resource ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]: LCM:  [ Start  Test     ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]:                            [[WindowsFeature]PSWA] Importing the module MSFT_RoleResource in force mode.
WARNING: [TEST-SRV]:                            [[WindowsFeature]PSWA] Resource is waiting for PowerShell script debugger to attach.  Use the follow
ing commands to begin debugging this resource script:
Enter-PSSession -ComputerName TEST-SRV -Credential <credentials>
Enter-PSHostProcess -Id 9000 -AppDomainName DscPsPluginWkr_AppDomain
Debug-Runspace -Id 9
```
此时，LCM 称为资源，并且到第一个符点。 最后三行输出中的显示了如何连接到该过程并启动调试资源脚本。

## 调试资源脚本

启动 PowerShell ISE 的新实例。 在控制台窗格中，输入输出的最后三行`Start-DscConfiguration`命令，将替换为输出`<credentials>`有效用户凭据。 您现在应该可以看到类似的提示︰

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

在脚本窗格中，将会打开该资源脚本和调试程序已停止 （课堂基于资源的**Test()**方法） 的**测试 TargetResource**函数的第一行处。
现在您可以使用 ISE 中调试命令来逐步执行资源脚本，看变量值、 查看调用堆栈，依此类推。 有关 PowerShell ISE 中调试信息，请参阅[如何在 Windows PowerShell ISE 调试脚本](https://technet.microsoft.com/en-us/library/dd819480.aspx)。 请记住，每个资源脚本 （或类） 中的行设置为符点。

## 禁用 DSC 调试

调用后[启用 DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx)，所有呼叫转接到[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx)将导致分成调试程序的配置。 若要允许配置正常运行，必须禁用调试通过致电[禁用 DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx) cmdlet。

>**注意︰**重新启动不会更改 LCM 的调试状态。 如果已启用调试，启动配置仍将分为调试程序后重新启动。


## 另请参阅
- [编写自定义与 MOF DSC 资源](authoringResourceMOF.md) 
- [编写自定义使用 PowerShell 类 DSC 资源](authoringResourceClass.md)

