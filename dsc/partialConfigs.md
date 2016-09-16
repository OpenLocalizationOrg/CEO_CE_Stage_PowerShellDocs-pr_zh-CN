---
title: "PowerShell 需要状态配置部分配置"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 5f3d40fe431d026d8d83dfc720d919048c6bf336
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# PowerShell 需要状态配置部分配置

>适用于︰ Windows PowerShell 5.0

在 PowerShell 5.0 需要状态配置 (DSC) 允许配置中断句和多个来源传送。 在目标节点本地配置管理器 (LCM) 集中片段应用作为单个配置之前。 此功能允许共享控制权的团队或个人之间的配置。 例如，如果两个或多个团队的开发人员正在处理一项服务，它们可能每个想要创建配置管理其服务的一部分。 这些配置的每个可能来自不同提取服务器和他们无法添加开发的不同阶段。 部分配置也允许在不同的人员或团队来控制配置节点，而无需协调编辑单个配置文档的不同方面。 例如，一个工作组可能是负责部署虚拟机和操作系统，而其他应用程序和服务的虚拟机上可能部署另一个团队。 具有部分配置，每个团队可以创建自己的配置不被不必要地复杂其中任一。

您可以使用推送模式、 拉入模式或两者的组合中的部分配置。

## 推送模式中的部分配置
推送模式下使用部分配置，您可以在目标节点接收部分配置中配置 LCM。 使用发布 DSCConfiguration cmdlet，每个部分配置必须推送到目标。 目标节点进行组合到单个配置，部分配置，您可以通过致电[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet 应用配置。

### 配置推送模式部分配置 LCM
若要配置部分配置 LCM 推送模式下，请使用一个**PartialConfiguration**块为每个部分配置创建**DSCLocalConfigurationManager**配置。 有关配置 LCM 的详细信息，请参阅[Windows 配置本地配置管理器](https://technet.microsoft.com/en-us/library/mt421188.aspx)。 下面的示例演示需要两个部分配置 LCM 配置 — 一个部署操作系统、，另一个部署和配置 SharePoint。

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {
        
           PartialConfiguration ServiceAccountConfig
        {
            Description = 'Configuration to add the SharePoint service account to the Administrators group.'
            RefreshMode = 'Push'
        }
           PartialConfiguration SharePointConfig
        {
            Description = 'Configuration for the SharePoint server'
            RefreshMode = 'Push'
        }
    }
}
PartialConfigDemo 
```

为每个部分配置**RefreshMode**设置为"推入"。 **PartialConfiguration**块 （本示例中，"ServiceAccountConfig"和"SharePointConfig"） 的名称必须匹配完全会将发送到目标节点的配置的名称。

### 发布和启动推送模式部分配置
![PartialConfig 文件夹结构](./images/PartialConfig1.jpg)

然后调用**发布 DSCConfiguration**为每个配置，传递包含作为路径参数的配置文档的文件夹。 在发布后这两种配置，您可以呼叫`Start-DSCConfiguration –UseExisting`目标节点上。

## 拉入模式中的部分配置

可以从一个或多个提取服务器提取部分配置 （有关提取服务器的详细信息，请参阅[Windows PowerShell 需要状态配置提取服务器](pullServer.md)。 要执行此操作，您必须配置 LCM 目标节点提取的部分配置和命名并正确提取服务器上找到的配置文档上。

### 配置提取节点配置 LCM

若要配置 LCM 提取部分提取服务器配置，您定义**ConfigurationRepositoryWeb** （适用于 HTTP 提取服务器） 或 （适用于 SMB 提取服务器） **ConfigurationRepositoryShare**块中提取服务器。 然后，您可以创建通过使用**ConfigurationSource**属性引用提取服务器的**PartialConfiguration**块。 您还需要创建**设置**基块以指定 LCM 使用拉入模式，并指定用于标识配置提取服务器和目标节点的**ConfigurationNames**或**ConfigurationID** 。 以下元配置定义名为 CONTOSO PullSrv HTTP 提取服务器，并使用它的两个部分配置提取服务器。

有关配置使用**ConfigurationNames**LCM 的详细信息，请参阅[使用配置名称提取客户端设置](pullClientConfigNames.md)。 有关配置使用**ConfigurationID**LCM 的信息，请参阅[使用配置 ID 提取客户端设置](pullClientConfigID.md)。

#### 配置为使用配置名称提取模式配置 LCM

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               ="ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'    
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38     
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }     
        
        PartialConfiguration ServiceAccountConfig 
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv") 
        }
 
        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
        }
   
}
``` 

#### 配置为使用 ConfigurationID 提取模式配置 LCM

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemoConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode                     = 'Pull'
            ConfigurationID                 = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins            = 30 
            RebootNodeIfNeeded              = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }
        
           PartialConfiguration ServiceAccountConfig
        {
            Description                     = 'Configuration for the Base OS'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode                     = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description                     = 'Configuration for the Sharepoint Server'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Pull'
        }
    }
}
PartialConfigDemo 
```

您可以提取来自多个拉服务器部分配置-只需定义每个拉服务器，并让每个**PartialConfiguration**块中的适当拉服务器于。

在创建之后元配置，您必须运行它以创建配置文档 （MOF 文件），然后调用[设置 DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621(v=wps.630).aspx)配置 LCM。

### 命名和放置在提取服务器 (ConfigurationNames) 上的配置文档

必须为**ConfigurationPath**中指定的文件夹中放置的部分配置文档`web.config`提取服务器的文件 (通常`C:\Program Files\WindowsPowerShell\DscService\Configuration`)。 配置文档必须命名，如下所示︰ `ConfigurationName.mof`，其中_配置名_为部分配置的名称。 在本例中，配置文档应命名为，如下所示︰

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### 命名和放置在拉服务器 (ConfigurationID) 上的配置文档

必须为**ConfigurationPath**中指定的文件夹中放置部分配置文档`web.config`提取服务器的文件 (通常`C:\Program Files\WindowsPowerShell\DscService\Configuration`)。 配置文档必须命名，如下所示︰_配置名_。 _ConfigurationID_`.mof`，其中_配置名_是部分配置的名称，而_ConfigurationID_是在目标节点 LCM 中定义的配置 ID。 在本例中，配置文档应命名为，如下所示︰

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```


### 从提取服务器运行部分配置

在目标节点 LCM 已配置，并已创建和命名提取服务器上正确配置文档后，目标节点将提取部分配置、 组合它们，并应用定期**RefreshFrequencyMins**属性的 LCM 指定结果的配置。 如果您想要强制刷新，您可以呼叫[更新 DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx) cmdlet，来提取配置，然后`Start-DSCConfiguration –UseExisting`以将其应用。


## 混合推送和请求模式中的部分配置

此外可以混合使用推送和拉入部分配置的模式。 也就是说，您可以拥有推送另一种部分配置时，从提取服务器，请求的一个部分配置。 处理每个部分配置，就像，具体取决于其刷新模式中上一节中所述。 例如，以下元配置介绍相同的示例中，使用服务帐户部分配置在拉入模式和推送模式中的 SharePoint 部分配置。

### 使用 ConfigurationNames 混合的推送和拉入模式

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               = "ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'    
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38     
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }     
        
        PartialConfiguration ServiceAccountConfig 
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            RefreshMode                     = 'Pull' 
        }
 
        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Push'
        }
   
}
``` 

### 使用 ConfigurationID 混合的推送和拉入模式

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {
        Settings
        {
            RefreshMode             = 'Pull'
            ConfigurationID         = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins    = 30 
            RebootNodeIfNeeded      = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL               = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }
        
           PartialConfiguration ServiceAccountConfig
        {
            Description             = 'Configuration for the Base OS'
            ConfigurationSource     = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode             = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description             = 'Configuration for the Sharepoint Server'
            DependsOn               = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode             = 'Push'
        }
    }
}
PartialConfigDemo 
```

请注意， **RefreshMode**设置块中指定"提取"，但 SharePointConfig 部分配置**RefreshMode**是"推送"。

命名并找到配置 MOF 文件，如上面所述对其各自刷新模式。 呼叫**发布 DSCConfiguration**发布`SharePointConfig`部分配置，并等待`ServiceAccountConfig`配置，以便将来自拉服务器，或通过致电[更新 DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541(v=wps.630).aspx)强制刷新。

## 配置示例 ServiceAccountConfig 部分

```powershell
Configuration ServiceAccountConfig
{
    Param (
        [Parameter(Mandatory,
                   HelpMessage="Domain credentials required to add domain\sharepoint_svc to the local Administrators group.")]
        [ValidateNotNullOrEmpty()]
        [pscredential]$Credential
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration


    Node localhost
    {
        Group LocalAdmins
        {
            GroupName           = 'Administrators'
            MembersToInclude    = 'domain\sharepoint_svc',
                                  'admins@example.domain'
            Ensure              = 'Present'
            Credential          = $Credential
            
        }

        WindowsFeature Telnet
        {
            Name                = 'Telnet-Server'
            Ensure              = 'Absent'
        }
    }
}
ServiceAccountConfig

```
## 配置示例 SharePointConfig 部分
```powershell
Configuration SharePointConfig
{
    Param (
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [pscredential]$ProductKey
    )

    Import-DscResource -ModuleName xSharePoint

    Node localhost
    {
        xSPInstall SharePointDefault
        {
            Ensure      = 'Present'
            BinaryDir   = '\\FileServer\Installers\Sharepoint\'
            ProductKey  = $ProductKey
        }
    }
}
SharePointConfig
```
##另请参阅 

**概念**
[Windows PowerShell 需要状态配置拉出服务器](pullServer.md) 

[Windows 配置本地配置管理器](https://technet.microsoft.com/en-us/library/mt421188.aspx) 

