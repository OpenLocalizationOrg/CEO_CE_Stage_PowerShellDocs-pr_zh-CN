---
title: "DSC 改进 WMF 5.1 （预览）"
ms.date: 2016-07-13
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 7619daab6ff3023978ed87ae8f507e76c961f2db
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
#WMF 5.1 中的所需状态配置 (DSC) 中的改进

## DSC 类资源改进

在 WMF 5.1，我们已修复以下已知问题︰
* 获取 DscConfiguration 可能返回 (null) 的空值或错误，如果基于类的 DSC 资源的 Get() 函数返回一个复数/哈希表类型。
* 如果在 DSC 配置使用 RunAs 凭据，则将获取 DscConfiguration 返回错误。
* 复合配置中无法使用基于类的资源。
* 开始 DscConfiguration 挂起，如果基于类的资源具有其自己的类型的属性。
* 基于类的资源不能用作异的资源。


## DSC 资源调试改进

在 WMF 5.0 PowerShell 调试程序未停止在基于类的资源方法 （设置/获取/测试） 直接。
WMF 5.1 中调试程序将与 MOF 基于资源的方法相同的方式停止在类基于资源的方法。

## DSC 提取客户端支持 TLS 1.1 和 TLS 1.2 
以前，DSC 提取客户端仅支持 SSL3.0 和 TLS1.0 通过 HTTPS 连接。 当强制使用更安全的协议，提取客户端将停止运行。 在 WMF 5.1 DSC 提取客户端不再支持 SSL 3.0，然后添加更安全的 TLS 1.1 和 TLS 1.2 协议的支持。  

## 改进的拉服务器注册 ##

在早期版本的 WMF，同时登记/报告 DSC 拉服务器使用 ESENT 数据库时请求将导致 LCM 无法注册和/或报告。 在这种情况下，提取服务器上的事件日志将有错误"已在使用实例名称"。
如果这是因为访问 ESENT 数据库中的多线程方案正在使用模式不正确。 在 WMF 5.1 已修复此问题。 并发登记或报告 （涉及 ESENT 数据库） 将 WMF 5.1 中正常工作。 此问题仅适用于 ESENT 数据库并不适用于 OLEDB 数据库。 

##提取部分配置命名约定
在早期版本中，为一个完整的配置的命名约定时 MOF 文件名中提取服务应该匹配反过来必须匹配 MOF 文件中嵌入的配置名称的本地配置管理器设置中指定的部分配置名称。 

下面的快照，请参阅︰

• 本地配置设置定义允许节点收到一个完整的配置。

![示例 metaconfiguration](../images/MetaConfigPartialOne.png)

• 示例部分配置定义 

```PowerShell
Configuration PartialOne
{
    Node('localhost')
    {
        File test 
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

• 生成 MOF 文件中的配置名嵌入。

![示例生成的 mof 文件](../images/PartialGeneratedMof.png)

• 提取配置存储库中的文件名 

![配置存储库中的文件名](../images/PartialInConfigRepository.png)

Azure 自动化服务名称生成 MOF 文件保存为`<ConfigurationName>.<NodeName>.mof`。 因此下面的配置将编译到 PartialOne.localhost.mof。

此它不可能对进行提取一个完整的配置从 Azure 自动化服务。

```PowerShell
Configuration PartialOne
{
    Node('localhost')
    {
        File test 
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

WMF 5.1 中提取服务中的部分配置可以指定为`<ConfigurationName>.<NodeName>.mof`。 此外，如果计算机提取提取从一种配置服务然后提取服务器配置库上的配置文件可以具有任何文件的名称。 此命名灵活性允许您通过 Azure 自动化服务，可以在其中您节点一些配置来自 Azure 自动化 DSC 和您有想要在本地管理的部分配置部分管理您的节点。

下面 metaconfiguration 将设置要管理的节点向上本地以及通过 Azure 自动化服务。

```PowerShell
  [DscLocalConfigurationManager()]
   Configuration RegistrationMetaConfig
   {
        Settings
        {
            RefreshFrequencyMins = 30
            RefreshMode = "PULL"            
        }

        ConfigurationRepositoryWeb web
        {
            ServerURL =  $endPoint
            RegistrationKey = $registrationKey
            ConfigurationNames = $configurationName
        }

        # Partial configuration managed by Azure Automation service.
        PartialConfiguration PartialConfigurationManagedByAzureAutomation
        {
            ConfigurationSource = "[ConfigurationRepositoryWeb]Web"   
        }
    
        # This partial configuration is managed locally.
        PartialConfiguration OnPremisesConfig
        {
            RefreshMode = "PUSH"
            ExclusiveResources = @("Script")
        }

   }

   RegistrationMetaConfig
   slcm -Path .\RegistrationMetaConfig -Verbose
 ```

# 使用 DSC 复合资源 PsDscRunAsCredential   

我们已添加[*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser)使用 DSC[复合](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite)资源的支持。    

使用内部配置复合资源时，用户现在可以为 PsDscRunAsCredential 指定一个值。 指定时，所有资源内复合资源 RunAs 以用户身份运行。 复合资源调用另一个复合资源时，如果其所有资源也被执行作为 RunAs 的用户。 RunAs 凭据传播到任何复合资源层次结构级别。 如果任何资源内复合资源 PsDscRunAsCredential 指定自己的值，合并错误将导致配置编译过程。

此示例显示与[WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources)复合资源 PSDesiredStateConfiguration 模块中包含的用法。 



```powershell

Configuration InstallWindowsFeature     
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        WindowsFeatureSet features 
        {  
            Name = @("Telnet-Client","SNMP-Service")  
            Ensure = "Present"  
            IncludeAllSubFeature = $true  
        PsDscRunAsCredential = Get-Credential   
        }  
    }

}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost'
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}


InstallWindowsFeature -ConfigurationData $configData 

```

##DSC 模块和配置签名验证
在 DSC，配置和模块分布到托管计算机从提取服务器。 如果提取服务器被泄露，攻击可潜在修改配置和提取服务器上的模块，并使其分发给所有托管节点，影响所有这些。 

 在 WMF 5.1 DSC 支持验证数字签名在目录和配置 (。MOF) 文件。 此功能将会阻止节点执行配置或其不由受信任的签名人签名或其已被篡改签名由受信任的签名人之后的模块文件。 



###如何登录配置和模块 
***
* 配置文件 (。Mof): 现有的 PowerShell cmdlet[设置 AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx)经过了扩展，支持 MOF 文件的签名。  
* 模块︰ 签名的模块是通过签名相应模块目录使用以下步骤︰ 
    1. 创建目录文件︰ 目录文件包含加密哈希或指纹的集合。 
       每个指纹对应模块中包括的文件。 
       添加了新 cmdlet[新建 FileCatalog](https://technet.microsoft.com/library/cc732148.aspx)，以使用户能够创建其模块目录文件。
    2. 登录目录文件︰ 使用[设置 AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx)目录文件进行签名。
    3. 将目录文件放在模块文件夹。
按照惯例，应具有相同名称的模块文件夹下放置模块目录文件。

###LocalConfigurationManager 设置以启用签名验证

####提取
节点的 LocalConfigurationManager 执行签名验证模块和配置基于其当前设置。 默认情况下，禁用签名验证。 通过添加到下面所示节点的元配置定义 'SignatureValidation' 块可以启用签名验证︰

```PowerShell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PULL'        
    } 
    
    ConfigurationRepositoryWeb pullserver{
      ConfigurationNames = 'sql'
      ServerURL = 'http://localhost:8080/PSDSCPullServer/PSDSCPullServer.svc'
      AllowUnsecureConnection = $true
      RegistrationKey = 'd6750ff1-d8dd-49f7-8caf-7471ea9793fc' # Replace this with correct registration key.
    }
    SignatureValidation validations{
        # By default, LCM will use default Windows trusted publisher store to validate the certificate chain. If TrustedStorePath property is specified, LCM will use this custom store for retrieving the trusted publishers to validate the content.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'            
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.       
    }
 
}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose 
 ```

上一个节点设置上述 metaconfiguration 启用下载的配置和模块的签名验证。 本地配置管理器将执行以下步骤来验证数字签名。

1. 验证在配置文件的签名 (。MOF) 才有效。 
   使用 PowerShell cmdlet[获取 AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx)，哪些扩展 5.1 支持 MOF 验证签名中。
2. 验证授权签名的证书颁发机构是受信任。
3. 下载到临时位置配置的模块/资源相关性。
4. 验证目录模块内包含的签名。
    * 查找`<moduleName>.cat`文件并验证使用 cmdlet[获取 AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx)其签名。
    * 验证签名人身份验证的证书颁发机构是受信任。
    * 验证不已使用新的 cmdlet[测试 FileCatalog](https://technet.microsoft.com/library/cc732148.aspx)损坏的模块的内容。
5. 安装模块 $env: ProgramFiles\WindowsPowerShell\Modules\
6. 流程配置

> 注意︰ 签名模块目录和配置仅时执行验证配置适用于系统的第一次或下载并安装该模块。 一致性运行不会验证 Current.mof 或其模块相关性的签名。
如果验证失败任何阶段，例如，如果配置提取拉从服务器未签名，然后配置的处理将终止，如下所示的错误，将删除所有临时文件。

![配置示例错误输出](../images/PullUnsignedConfigFail.png)

同样，提取其目录未签名的模块将导致以下错误︰

![示例错误输出模块](../images/PullUnisgnedCatalog.png)

####推送
使用推送传递配置可能会篡改在其源之前将其发送到节点。 本地配置管理器将为下压或发布配置执行类似签名验证步骤。
下面是签名验证的推送完成示例。

* 启用签名验证节点上。

```PowerShell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PUSH'        
    } 
    SignatureValidation validations{
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'   
        SignedItemType =  'Configuration','Module'             
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
``` 
* 创建一个示例配置文件。

```PowerShell
# Sample configuration
Configuration Test
{

    File foo
    {
        DestinationPath =  "$env:TEMP\signingTest.txt"
        Contents = "ABC"
    }
}
Test
```

* 请尝试将无符号的配置文件推送到节点。 

```PowerShell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
``` 
![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

* 登录使用代码签名证书的配置文件。

![SignMofFile](../images/SignMofFile.png)

* 请尝试延迟签名的 MOF 文件。

![SignMofFile](../images/PushSignedMof.png)

