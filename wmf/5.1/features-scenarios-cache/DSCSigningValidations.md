---
title: "DSC 模块和配置签名验证"
author: jaimeo
contributor: berheabra
ms.openlocfilehash: 86a2e71e41c844d9aca605e4f79a3d911de5edc0
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
##DSC 模块和配置签名验证
DSC，在配置文档和模块分发给管理机从提取服务器或提取服务器 （对于 Azure 自动化提取服务）。 如果提取服务被泄露，攻击可以潜在修改配置和提取服务器上的模块并分发给所有托管计算机，因此会影响客户的更多的计算机。 

 在 WMF 5.1 针对此威胁。 DSC 支持验证数字签名在模块和配置 (。MOF) 文件。 此功能将会阻止节点执行配置或模块文件的受信任的签名人通过未登录，或者，已被篡改签名由受信任的签名人之后。 



###如何登录配置和模块 
***
1. 配置文件 (。MOF):-现有的 PowerShell cmdlet[设置 AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx)经过了扩展，支持 MOF 文件的签名。  
2. 模块:-签名的模块通过签名相应模块目录使用以下步骤:- 
    * 创建目录文件︰ 目录文件包含加密哈希或指纹的集合。 每个指纹对应模块中包括的文件。  已添加新的 cmdlet[新建 FileCatalog](https://technet.microsoft.com/library/cc732148.aspx)，以启用用户创建目录文件以其模块。 请参阅目录 cmdlet[相对链接](catalog-cmdlets.md)以创建目录文件。 
    * 登录目录文件︰ 使用[设置 AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx)登录目录文件。
    * 将目录文件放在模块文件夹。
按照惯例，应具有相同名称的模块文件夹下放置模块目录文件。

###LocalConfigurationManager 设置以启用签名验证。

####提取
节点的 LocalConfigurationManager 执行签名验证模块和配置基于其当前设置。 默认情况下，禁用签名验证。 签名验证可以启用加上 SignatureValidation 阻止的节点元配置定义如下所示:-

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
        # By default,LCM will use default Windows trusted publisher store to validate the certificate chain. If TrustedStorePath property is specified, LCM will use this custom store for retrieving the trusted publishers to validate the content.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'            
        SignedItemType =  'Configuration','Module'         # Those are list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.       
    }
 
}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose 
 ```

上一个节点设置上述 metaconfiguration 启用下载的配置和模块的签名验证。 Localconfigurationmanager 将执行以下步骤来验证数字签名。
* 验证在配置文件的签名 (。MOF) 才有效。 使用 powershell cmdlet[获取 AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx)，哪些 5.1 支持 MOF sigature 有效性中扩展。
* 验证授权签名的证书颁发机构是受信任。
* 下载到临时位置配置的模块/资源相关性。
* 验证目录模块内包含的签名。
    * 查找<moduleName>.cat 文件并验证使用 cmdlet[获取 AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx)其签名。
    * 验证签名人身份验证的证书颁发机构是受信任。
    * 验证不已使用新的 cmdlet[测试 FileCatalog](https://technet.microsoft.com/library/cc732148.aspx)损坏的模块的内容。
* 安装模块 $env: ProgramFiles\WindowsPowerShell\Modules\
* 流程配置。

注意:-对于第一次，或者在下载并安装该模块配置应用到系统时，才会执行签名验证模块目录和配置。 运行一致性不验证签名的 Current.mof 或其模块依赖项。
如果为实例如果配置来自 pullserver 符号，然后将如下所示的错误终止配置的处理并将删除所有临时文件验证失败任何阶段。

![配置示例错误输出](../../images/PullUnsignedConfigFail.PNG)

同样，提取其目录未签名的模块将导致以下错误:-

![示例错误输出模块](../../images/PullUnisgnedCatalog.PNG)

####推送
交付到节点之前，可能在其源篡改送达通过推送配置。 本地配置管理器将为下压或发布配置执行类似签名验证步骤。
下面是签名验证的推送完成示例。

* 启用签名验证节点上。

```Powershell
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

```Powershell
# Sample configuration
Configuration Test{

    File foo
    {
        DestinationPath =  "$env:TEMP\signingTest.txt"
        Contents = "ABC"
    }
}
Test
```

* 请尝试将无符号的配置文件推送到节点。 

```Powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
``` 
![ErrorUnsignedMofPushed](../../images/PushUnsignedMof.PNG)

* 使用代码签名证书 configurtion 文件签名。

![SignMofFile](../../images/SignMofFile.PNG)

* 请尝试延迟签名的 mof 文件。

![SignMofFile](../../images/PushSignedMof.PNG)

