---
title: "DSC web 提取服务器设置"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 0c65fbe97ac33b75872e1a2954b215107a2bf093
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC web 提取服务器设置

> 适用于︰ Windows PowerShell 5.0

DSC web 拉服务器是使用 OData 界面这些节点提出问题时进行 DSC 配置文件适用于目标节点的 IIS 中的 web 服务。

使用提取服务器要求︰

* 运行的服务器︰
  - WMF/PowerShell 5.0 或更高版本
  - IIS 服务器角色
  - DSC 服务
* 理想情况下，一些意味着生成的证书，来保护凭据目标节点传送到本地配置管理器 (LCM)

您可以使用添加角色和功能向导中服务器管理器中，或使用 PowerShell 添加 IIS 服务器角色和 DSC 服务。 本主题中包含的示例脚本将两个步骤为您处理也。

## 使用 xWebService 资源
设置推送 web 服务器的最简单方法是使用 xWebService 资源，包括在 xPSDesiredStateConfiguration 模块。 以下步骤介绍如何配置设置 web 服务中使用的资源。

1. 致电[安装模块](https://technet.microsoft.com/en-us/library/dn807162.aspx)cmdlet 来安装**xPSDesiredStateConfiguration**模块。 **注意**︰**安装模块**包括在**PowerShellGet**模块中，包括在 PowerShell 5.0。 您可以下载**PowerShellGet**模块 PowerShell 3.0 和 4.0 [PackageManagement PowerShell 模块](https://www.microsoft.com/en-us/download/details.aspx?id=49186)的预览。 
1. 从受信任证书颁发机构，或者您 orgnaization 或公共机构内获取 DSC 提取服务器 SSL 证书。 证书颁发机构收到通常是 PFX 格式。 将成为默认位置应证书︰ \LocalMachine\My DSC 提取服务器的节点上安装该证书。 记下证书指纹。
1. 选择要用作注册密钥 GUID。 若要生成一个使用 PowerShell 输入以下信息 PS 提示，并按 enter:``` [guid]::newGuid()```。 此键将用作由客户端节点共享密钥进行身份验证在注册过程。 有关详细信息，请参阅下面的[注册密钥](#RegKey)部分。
1. 使用 PowerShell ise，启动 (F5) 以下配置脚本 （包含作为 Sample_xDscWebService.ps1 **xPSDesiredStateConfiguration**模块的示例文件夹中）。 此脚本设置提取服务器。
  
```powershell
configuration Sample_xDscPullServer
{ 
    param  
    ( 
            [string[]]$NodeName = 'localhost', 
            
            [ValidateNotNullOrEmpty()] 
            [string] $certificateThumbPrint,
            
            [Parameter(Mandatory)]
            [ValidateNotNullOrEmpty()]
            [string] $RegistrationKey 
     ) 
 
 
     Import-DSCResource -ModuleName xPSDesiredStateConfiguration 

     Node $NodeName 
     { 
         WindowsFeature DSCServiceFeature 
         { 
             Ensure = 'Present'
             Name   = 'DSC-Service'             
         } 
 
         xDscWebService PSDSCPullServer 
         { 
             Ensure                  = 'Present' 
             EndpointName            = 'PSDSCPullServer' 
             Port                    = 8080 
             PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer" 
             CertificateThumbPrint   = $certificateThumbPrint          
             ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules" 
             ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration" 
             State                   = 'Started'
             DependsOn               = '[WindowsFeature]DSCServiceFeature'                         
         } 

        File RegistrationKeyFile
        {
            Ensure          = 'Present'
            Type            = 'File'
            DestinationPath = "$env:ProgramFiles\WindowsPowerShell\DscService\RegistrationKeys.txt"
            Contents        = $RegistrationKey
        }
    }
}

```

1. 运行配置，将 SSL 证书的指纹传递**certificateThumbPrint**参数以及作为**RegistrationKey**参数 GUID 注册表项︰

```powershell
# To find the Thumbprint for an installed SSL certificate for use with the pull server list all certifcates in your local store 
# and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
dir Cert:\LocalMachine\my

# Then include this thumbprint when running the configuration
Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

# Run the compiled configuration to make the target node a DSC Pull Server
Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
```

## 注册密钥
若要允许客户端节点注册服务器，以便他们可以使用配置名称，而不是配置 ID，上述配置创建一个注册密钥保存在一个名为文件`RegistrationKeys.txt`中`C:\Program Files\WindowsPowerShell\DscService`。 为共享机密与提取服务器客户端初始注册过程中使用函数的注册密钥。 客户端将生成自签名的证书用于唯一身份验证到提取服务器后成功完成注册。 此指纹本地存储证书并将其与提取服务器的 URL。
> **注意**︰ PowerShell 4.0 中不支持注册键。 

为了配置节点服务器进行身份验证提取注册键需处于将与此提取服务器注册任何目标节点 metaconfiguration。 请注意后目标计算机已成功注册，在下面 metaconfiguration **RegistrationKey**将被删除，并且值 140a952b-b9d6-406b-b416-e0f759c9c0e4' 必须匹配在 RegistrationKeys.txt 文件中提取服务器上存储的值。 始终将注册关键值安全，因为知道它允许任何目标计算机注册提取服务器。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode          = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded   = $true
        }
        
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey    = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }   
        
        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
        }
    }
}

PullClientConfigID -OutputPath c:\Configs\TargetNodes
```
> **注意**︰ **ReportServerWeb**部分允许报告数据来发送到提取服务器。 

缺少的 metaconfiguration 文件中的**ConfigurationID**属性隐式意味着该提取服务器支持推送服务器协议的 V2 版本以便初始注册是必需的。 相反， **ConfigurationID**状态意味着使用提取服务器协议 V1 版本并不会注册处理。

>**注意**︰ 在推送方案中，可使需要有永远不会与提取服务器注册的节点的 metaconfiguration 文件中定义 ConfigurationID 属性当前 relase 中存在错误。 这将强制 V1 拉出服务器协议，并避免注册失败的消息。

## 放置配置和资源
提取后服务器安装完成之后，由**ConfigurationPath**定义的文件夹， **ModulePath**属性中提取服务器配置，您将在其中放置模块，可用于目标节点中提取的配置。 这些文件需要以特定格式提取服务器正确处理它们的顺序。 

### DSC 资源模块程序包格式
每个资源模块需要压缩和名为按照下面的模式**{模块名称} {模块版本} _.zip**。 例如，一个名为使用模块版本的 3.1.2.0 xWebAdminstration 模块将被命名为 xWebAdministration_3.2.1.0.zip'。 在单个 zip 文件中必须包含每个版本的模块。 因为模块格式与 WMF 5.0 中添加每个 zip 文件中的资源的一个版本不支持对单个目录中的多个模块版本的支持。 这意味着之前用于提取服务器 DSC 资源模块打包您都需要对目录结构进行小更改。 包含在 WMF 5.0 DSC 资源模块的默认格式为 {模块文件夹}\{模块版本} \DscResources\{DSC 资源文件夹}\'。 只需为提取服务器包装删除**{模块版本}**文件夹以便路径将成为之前 ' {模块文件夹} \DscResources\{DSC 资源文件夹}\'。 与此项更改，压缩文件夹，如上面所述，并将这些 zip 文件放在**ModulePath**文件夹中。

### 配置 MOF 格式 
配置 MOF 文件需要成对使用校验和文件，以便在目标节点 LCM 可以验证配置。 若要创建一个校验和，请致电[新建 DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet。 该 cmdlet 所需的指定配置 MOF 所在的文件夹的**路径**参数。 该 cmdlet 创建校验和名为`ConfigurationMOFName.mof.checksum`，其中`ConfigurationMOFName`是配置 mof 文件的名称。 如果有多个配置 MOF 文件中指定的文件夹，为每个文件夹中配置创建校验和。 将 MOF 文件和及其关联的校验和文件**ConfigurationPath**文件夹。

>**注意**︰ 如果您更改任何方式配置 MOF 文件，必须也重新创建校验和文件。

## 工具
构成设置，以便验证和管理拉服务器更轻松，下列工具在作为 xPSDesiredStateConfiguration 模块最新版本中的示例包括︰
1. 将帮助包装 DSC 资源模块和用于提取服务器上的配置文件的模块。 [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1)。 下面的示例︰

```powershell
    # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
     $moduleList = @("xWebAdministration", "xPhp") 
     Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList 
     
     # Example 2 - Package modules and mof documents from c:\LocalDepot
     Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
```

1. 正确配置了验证提取服务器脚本。 [PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/Examples/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1)。


## 拉客户端配置 
以下主题介绍设置提取客户端的详细信息︰

* [使用配置 ID DSC 提取客户端设置](pullClientConfigID.md)
* [使用配置名称 DSC 提取客户端设置](pullClientConfigNames.md)
* [部分配置](partialConfigs.md)


## 另请参阅
* [Windows PowerShell 需要状态配置概述](overview.md)
* [制定配置](enactingConfigurations.md)
* [使用 DSC 报表服务器](reportServer.md)

