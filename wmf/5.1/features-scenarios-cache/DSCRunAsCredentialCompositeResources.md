---
title: "DSC 复合资源 PsDscRunAsCredential"
author:  jaimeo
contributor: ?
---
# 使用 DSC 复合资源 PsDscRunAsCredential   

我们已添加了用于[*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) DSC[复合](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite)资源。    

使用内部配置复合资源时，用户现在可以为 PsDscRunAsCredential 指定值。 如果指定，我们可以作为 RunAs 用户运行复合资源内的所有资源。 如果复合资源调用另一个复合资源，作为 RunAs 用户以及执行所有资源。  RunAs 凭据传播到任何复合资源层次结构级别。 如果复合资源内的任何资源指定自己的值为 PsDscRunAsCredential 我们配置编译期间提供合并错误。

下面介绍了如何使用它与[WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources) PSDesiredStateConfiguration 模块中包含的复合资源。 



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
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}


InstallWindowsFeature -ConfigurationData $configData 

```