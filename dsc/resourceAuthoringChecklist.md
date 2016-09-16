---
title: "资源创作核对清单"
ms.date: 2016-07-11
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 59a0e45e3d0ded6cde31418984c3a0cc04c39478
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 资源创作核对清单
创作新 DSC 资源时，此清单是最佳做法的列表。
## 资源模块包含.psd1 文件和每个资源 schema.mof 
检查您的资源具有正确的结构和包含所有所需的文件。 每个资源模块应包含.psd1 文件，并且每个非复合资源应该有 schema.mof 文件。 **获取 DscResource**将不会列出不包含架构的资源，用户将不能在 ISE 中编写针对这些模块的代码时，请使用 intellisense。 目录结构 xRemoteFile 资源，这是[xPSDesiredStateConfiguration 资源模块](https://github.com/PowerShell/xPSDesiredStateConfiguration)的一部分，如下所示︰


```
xPSDesiredStateConfiguration
    DSCResources
        MSFT_xRemoteFile
            MSFT_xRemoteFile.psm1
            MSFT_xRemoteFile.schema.mof
    Examples
        xRemoteFile_DownloadFile.ps1
    ResourceDesignerScripts
        GenerateXRemoteFileSchema.ps1
    Tests
        ResourceDesignerTests.ps1
    xPSDesiredStateConfiguration.psd1
```

## 资源和架构正确无误##
验证资源架构 (*。 schema.mof) 文件。 您可以使用[DSC 资源设计器](https://www.powershellgallery.com/packages/xDSCResourceDesigner/)帮助开发和测试您的架构。 请确保︰
- 属性类型正确无误 （例如不使用属性接受数值的字符串，应改为使用 UInt32 或其他数值类型）
- 属性特性正确指定为: ([键]，[必需]、 [编写]，[阅读])
- 在架构中的至少一个参数必须标记为 [键]
- 属性不会与任何共存 [阅读]: [必需]、 [键]，[编写]
- 如果多个限定符指定除 [read]，[密钥] 将优先
- 如果 [编写] 和 [需要] 有指定，则 [必需] 优先
- 返回指定合适的位置

示例︰
```
[Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
```

- 友好名称指定并确认 DSC 命名约定

示例︰
```[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]```

- 每个字段有意义的说明。 PowerShell GitHub 存储库中具有很好的示例，如[。 xRemoteFile 的 schema.mof](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)

此外，您应该使用从[DSC 资源设计器](https://www.powershellgallery.com/packages/xDSCResourceDesigner/)的**测试 xDscResource**和**测试 xDscSchema** cmdlet 自动验证资源和架构︰
```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```
例如︰
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## 没有错误的资源负载 ##
检查是否可以成功加载资源模块。
这可以通过手动运行`Import-Module <resource_module> -force `并确认没有发生错误，或通过编写测试自动化。 在后者的情况下，您可以按照此结构测试用例中︰
```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```
## 资源是幂等正字母大写 
DSC 资源的基本特征之一是幂等性。 这意味着应用包含该资源多次 DSC 配置将始终获得相同的结果。 例如，我们创建一个配置，其中包含以下文件资源︰
```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
} 
```
第一次将其应用后, 文件 test.txt 应显示在 C:\test 文件夹中。 但是，后续运行相同的配置不应更改 （例如没有 test.txt 文件的副本创建） 的计算机的状态。
以确保资源是您可以重复呼叫**设置 TargetResource**直接测试资源或执行端到端测试时多次调用**开始 DscConfiguration**时的幂。 结果应为相同每次运行之后。 


## 测试用户修改方案 ##
通过更改计算机的状态，然后重新运行 DSC，您可以正确验证该**设置 TargetResource**和**测试 TargetResource**函数。 下面是应采取的步骤︰
1.  启动与该资源不在所需的状态。
2.  与您的资源的运行的配置
3.  验证**测试 DscConfiguration** ，则返回 True
4.  修改配置的项是出所需的状态
5.  验证**测试 DscConfiguration**返回 false 更具体的示例使用注册表资源的操作如下︰
1.  启动与注册表项不在所需的状态
2.  用来将其放入所需的状态，并验证传递的配置运行**开始 DscConfiguration** 。
3.  运行**测试 DscConfiguration**并验证返回 true
4.  修改项的值，以便它不是所需的状态
5.  运行**测试 DscConfiguration**并验证返回 false
6.  获取 TargetResource 功能已验证使用获取 DscConfiguration

获取 TargetResource 应返回的资源的当前状态的详细信息。 请确保对其进行测试之后应用配置调用获取 DscConfiguration，并验证输出正确反映计算机的当前状态。 请务必单独，测试，因为调用开始 DscConfiguration 时，不会显示此区域中的任何问题。

## 直接呼叫**获取/设置/测试 TargetResource**函数 ##

请确保您测试**获取/设置/测试 TargetResource**函数在您的资源中实现直接调用它们，并验证他们按预期方式工作。

## 验证端到端使用**开始 DscConfiguration** ##

通过直接调用它们测试**获取/设置/测试 TargetResource**函数非常重要，但并非所有问题将都发现这种方式。 应注意上使用**开始 DscConfiguration**或提取服务器测试重要的部分。 实际上，这是用户将如何使用该资源，以便不低估测试此类型的倍数。 可能的问题的类型︰
- 因为作为一项服务运行 DSC 代理凭据/会话可能具有不同行为。  请务必测试端到端的以下任何功能。
- 通过**开始 DscConfiguration**错误输出可能不同于直接调用**设置 TargetResource**函数时显示。

## 在所有 DSC 测试兼容性支持的平台 ##
资源应处理所有 DSC 支持的平台 (Windows Server 2008 R2 和更高版本)。 在您的操作系统以获取最新版本的 DSC 上安装最新 WMF (Windows Management Framework)。 如果您的资源不起作用在一些这些平台设计使然，应返回特定错误消息。 此外，确保您的资源检查是否存在特定的计算机上正在呼叫的 cmdlet。 Windows Server 2012 添加大量的甚至与安装的 WMF 不可用在 Windows Server 2008R2 上的新 cmdlet。 

## 验证 Windows 客户端上 （如果适用） ##
一个常见的测试间隙验证仅在服务器版本的 Windows 上的资源。 许多资源也旨在处理客户端 Sku，因此如果是这样在您的情况下，不要忘记经常在这些平台以及对其进行测试。 
## 获取 DSCResource 列表资源 ##
在部署模块之后, 调用获取 DscResource 应列表以及其他资源结果。 如果列表中找不到您的资源，请确保该 schema.mof 文件的存在该资源。 
## 资源模块包含示例 ##
这有助于其他人创建质量示例了解如何使用它。 这是关键，，特别是因为许多用户将示例代码视为文档。 
- 首先，您应该确定将与模块-至少包括下面的示例，您应该涵盖最重要的使用情况下，您的资源︰
- 如果您的模块包含几个需要的端到端方案协同工作的资源，理想情况下将第一个基本的端到端示例。
- 初始示例应非常简单，如何开始使用您的小型易于管理的块 （例如，创建新的 VHD） 的资源
- 后面的示例应构建上 （例如创建虚拟机从 VHD，删除虚拟机，修改虚拟机），这些示例，并显示高级的功能 （例如使用动态内存中创建一个虚拟机）
- 示例配置应参数化 （所有值应作为参数都传递到配置和应无硬编码值）︰
```powershell
configuration Sample_xRemoteFile_DownloadFile
{
    param
    (
        [string[]] $nodeName = 'localhost',

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $destinationPath,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $uri,

        [String] $userAgent,

        [Hashtable] $headers
    )

    Import-DscResource -Name MSFT_xRemoteFile -ModuleName xPSDesiredStateConfiguration

    Node $nodeName
    {
        xRemoteFile DownloadFile
        {
            DestinationPath = $destinationPath
            Uri = $uri
            UserAgent = $userAgent
            Headers = $headers
        }
    }
} 
```
- 它是一个好的做法，包括如何调用实际值末尾的示例脚本配置示例 （已被注释掉）。 例如，在上面的配置不一定明显指定用户代理的最佳方法是︰

`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer`  
在这种情况下批注可以阐明配置的预期的执行︰
```
<# 
Sample use (parameter values need to be changed according to your scenario):

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
-userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
#>  
```
- 对于每个示例中，编写的简短说明，其中介绍了哪些操作，以及参数的含义。 
- 确保示例封面重要资源的大多数情况下，如果没有任何缺少，验证他们执行所有和计算机放到所需的状态。  

## 错误消息是易于理解，帮助用户解决问题 ##
应很好的错误消息︰
- ︰ 错误消息的最大问题存在他们通常不存在，因此请确保它们所在的位置。 
- 易于理解︰ 人为可读、 不遮住错误代码
- 什么是完全问题精确︰ 描述
- 建设性︰ 建议如何修复问题
- 正常︰ 不抱怨用户或使其确定感觉坏使您可以验证 （使用**开始 DscConfiguration**） 的端到端方案中的错误，因为它们可能有所不同时运行的资源直接函数返回。 

## 日志消息是易于理解和信息 (包括-详细信息，-调试和 ETW 日志) ##
确保日志输出资源易于理解，向用户提供的值。 资源应输出可能会对用户来说，很有帮助的所有信息，但详细日志不始终是更好。 您应该避免冗余和输出数据不提供其他值-不将某人贯穿数百个日志条目以查找他们正在查找的内容。 当然，没有日志也不是可接受的解决方案，此问题。 

测试时，您还应该分析详细和调试日志 （通过运行与-详细**开始 DscConfiguration**和-调试开关正确），以及 ETW 日志。 若要查看 DSC ETW 日志，请转到事件查看器中，并打开以下文件夹︰ 应用程序和服务的 Microsoft Windows-所需的状态配置。  默认情况下还将运营通道，但请确保启用分析和运行配置之前调试通道。 若要启用分析/调试通道，您可以执行下面的脚本︰
```powershell
$statusEnabled = $true
# Use "Analytic" to enable Analytic channel
$eventLogFullName = "Microsoft-Windows-Dsc/Debug" 
$commandToExecute = "wevtutil set-log $eventLogFullName /e:$statusEnabled /q:$statusEnabled   "
$log = New-Object System.Diagnostics.Eventing.Reader.EventLogConfiguration $eventLogFullName
if($statusEnabled -eq $log.IsEnabled)
{
    Write-Host -Verbose "The channel event log is already enabled"
    return
}     
Invoke-Expression $commandToExecute 
```
## 资源实现不包含硬编码路径 ##
确保没有硬编码路径中的资源实现，特别是当他们假定语言 (en-我们)，或者当有可用的系统变量。
如果您的资源需要访问特定路径，请使用环境变量，而不是硬路径，因为它在其他计算机上可能不同。

示例︰

而不是：
```
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
 ```
您可以编写︰
```
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)} 
```
## 资源实现不包含用户信息 ##
请确保没有电子邮件姓名、 帐户信息或在代码中的人员的姓名。
## 资源测试/无效有效的凭据 ##
如果您的资源将作为参数的凭据︰
- 本地系统 （或远程资源的计算机帐户） 不能访问时，请验证资源的工作方式。
- 验证资源的工作方式与指定的凭据，请设置和测试 
- 如果您的资源访问共享，请测试支持，如所需的所有变体︰
  - 标准 windows 共享。
  - DFS 共享。
  - SAMBA 共享 （如果您想要支持 Linux。）

## 资源不需要交互式输入 ##
**获取/设置/测试 TargetResource**函数应自动执行和不必须等待的用户的输入执行任何阶段 （如不应使用**获取凭据**这些函数内）。 如果您需要提供用户的输入，您应其配置将作为参数传递在编译阶段。 
## 资源功能全面的测试 ##
此清单包含重要要测试和/或经常错过的项目。 将大量测试，将特定于要测试和未在此处提及的资源的主要功能的文件。 不要忘记有关负测试事例。 
## 最佳做法︰ 资源模块包含 ResourceDesignerTests.ps1 脚本测试文件夹 ##
很好的做法资源模块内创建文件夹"测试"，创建 ResourceDesignerTests.ps1 文件和添加的所有资源使用**测试 xDscResource**和**测试 xDscSchema**测试中提供的模块。 这种方式可以快速验证架构的性能检查之前发布的给定的模块和执行中的所有资源。
为 xRemoteFile，ResourceTests.ps1 看上去像一样简单︰
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof 
```
##最佳做法︰ 资源文件夹包含用于生成架构资源设计器脚本##
每个资源应包含生成的资源的 mof 架构的资源设计器脚本。 此文件应放在<ResourceName>\ResourceDesignerScripts 和命名生成<ResourceName>Schema.ps1 的 xRemoteFile 资源被称作 GenerateXRemoteFileSchema.ps1 和包含此文件︰
```powershell 
$DestinationPath = New-xDscResourceProperty -Name DestinationPath -Type String -Attribute Key -Description 'Path under which downloaded or copied file should be accessible after operation.'
$Uri = New-xDscResourceProperty -Name Uri -Type String -Attribute Required -Description 'Uri of a file which should be copied or downloaded. This parameter supports HTTP and HTTPS values.'
$Headers = New-xDscResourceProperty -Name Headers -Type Hashtable[] -Attribute Write -Description 'Headers of the web request.'
$UserAgent = New-xDscResourceProperty -Name UserAgent -Type String -Attribute Write -Description 'User agent for the web request.' 
$Ensure = New-xDscResourceProperty -Name Ensure -Type String -Attribute Read -ValidateSet "Present", "Absent" -Description 'Says whether DestinationPath exists on the machine'
$Credential = New-xDscResourceProperty -Name Credential -Type PSCredential -Attribute Write -Description 'Specifies a user account that has permission to send the request.'
$CertificateThumbprint = New-xDscResourceProperty -Name CertificateThumbprint -Type String -Attribute Write -Description 'Digital public key certificate that is used to send the request.'

New-xDscResource -Name MSFT_xRemoteFile -Property @($DestinationPath, $Uri, $Headers, $UserAgent, $Ensure, $Credential, $CertificateThumbprint) -ModuleName xPSDesiredStateConfiguration2 -FriendlyName xRemoteFile 
```
## 最佳做法︰ 资源支持-whatif ##
如果您的资源执行"危险的"操作时，最好实现-whatif 功能。 完成后，请确保 whatif 输出正确介绍没有 whatif 开关执行命令时将发生的操作。
此外，验证操作不会执行 （没有为节点的状态进行更改） whatif 切换时。 例如，假设我们要测试文件资源。 下面是将创建文件"test.txt"内容"测试"配置简单︰
```powershell
configuration config
{
    node localhost 
    {
        File file
        {
            Contents="test"
            DestinationPath="C:\test\test.txt"
        }
    }
}
config 
```
如果我们编译，然后执行与 whatif 切换配置输出告诉我们完全会发生什么情况时我们运行配置。 但是未执行配置本身 （未创建 test.txt 文件）。
```powershell 
Start-DscConfiguration -path .\config -ComputerName localhost -wait -verbose -whatif
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer CHARLESX1 with user sid
S-1-5-21-397955417-626881126-188441444-5179871.
What if: [X]: LCM:  [ Start  Set      ]
What if: [X]: LCM:  [ Start  Resource ]  [[File]file]
What if: [X]: LCM:  [ Start  Test     ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]: LCM:  [ End    Test     ]  [[File]file]  in 0.0270 seconds.
What if: [X]: LCM:  [ Start  Set      ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]:                            [C:\test\test.txt] Creating and writing contents and setting attributes.
What if: [X]: LCM:  [ End    Set      ]  [[File]file]  in 0.0180 seconds.
What if: [X]: LCM:  [ End    Resource ]  [[File]file]
What if: [X]: LCM:  [ End    Set      ]
VERBOSE: [X]: LCM:  [ End    Set      ]    in  0.1050 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
```

此列表并不全面，但它涵盖可以设计、 开发和测试 DSC 资源时遇到的许多重要问题。
