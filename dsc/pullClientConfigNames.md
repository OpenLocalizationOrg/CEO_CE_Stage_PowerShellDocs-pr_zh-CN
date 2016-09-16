---
title: "使用配置名称提取客户端设置"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: ec4ce56d00daa265fb0031f20ded05d3f3c04895
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用配置名称提取客户端设置

> 适用于︰ Windows PowerShell 5.0

每个目标节点具有要判断使用拉入模式和提供 URL，它可以提取与服务器联系以获取配置。 要执行此操作，您必须配置本地配置管理器 (LCM) 与所需的信息。若要配置 LCM，您可以创建特殊类型的配置，使用**DSCLocalConfigurationManager**属性修饰。 有关配置 LCM 的详细信息，请参阅[配置本地配置管理器](metaConfig.md)。

> **注意**︰ 本主题适用于 PowerShell 5.0。 PowerShell 4.0 中提取客户端设置的信息，请参阅[使用 PowerShell 4.0 中的配置 ID 提取客户端设置](PullClientConfigNames4.md)

以下脚本配置 LCM 提取配置从名为"CONTOSO PullSrv"的服务器︰

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
            
        }      
    }
}
PullClientConfigNames
```

在脚本**ConfigurationRepositoryWeb**块定义提取服务器。 **ServerURL**属性指定拉服务器的终结点。

**RegistrationKey**属性是提取服务器的所有客户端节点和该提取服务器之间共享的密钥。 相同的值存储在提取服务器上的文件。 

**ConfigurationNames**属性是数组，指定面向客户端节点的配置的名称。 在拉服务器上，必须对该客户端节点配置 MOF 文件命名*ConfigurationNames*.mof， *ConfigurationNames*与您在此 metaconfiguration 中设置**ConfigurationNames**属性的值相匹配。

>**注意︰**如果您在**ConfigurationNames**中指定多个值，您必须指定**PartialConfiguration**块在您的配置。 有关部分配置信息，请参阅[PowerShell 需要状态配置部分配置](partialConfigs.md)。

运行此脚本之后，它将创建一个新的输出文件夹名为**PullClientConfigNames**并那里放置 metaconfiguration MOF 文件。 在此例中，将命名 metaconfiguration MOF 文件`localhost.meta.mof`。

应用配置，若要**设置 DscLocalConfigurationManager** cmdlet，以及设置为 metaconfiguration MOF 文件的位置的**路径**。 例如︰ `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.`

> **注意**︰ 注册键只使用 web 拉服务器。 您仍然必须**ConfigurationID**使用 SMB 拉服务器。 有关使用**ConfigurationID**配置拉服务器的信息，请参阅[使用配置 ID 提取客户端设置](PullClientConfigNames.md)

## 资源和报表服务器

如果 LCM （如上例） 配置中指定**ConfigurationRepositoryWeb**或**ConfigurationRepositoryShare**块，提取客户端将获取资源从指定的服务器，但它不会向其发送报表。 可用于单个提取服务器配置、 资源和报告，但您需要创建**ReportRepositoryWeb**块设置报告。 下面的示例演示将设置为在客户端推送配置和资源和发送到单个提取服务器报告数据，metaconfiguration。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }
        
        

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigNames
```


您还可以指定不同提取服务器的资源和报告。 若要指定资源服务器，请使用**ResourceRepositoryWeb** （适用于 web 提取服务器） 或**ResourceRepositoryShare**块 （适用于 SMB 提取服务器）。
若要指定在报表服务器，您可以使用**ReportRepositoryWeb**块。 在报表服务器不能为 SMB 服务器。
以下 metaconfiguration 配置拉客户端以获取其配置从**CONTOSO PullSrv**和**CONTOSO ResourceSrv**，从其资源并向**CONTOSO ReportSrv**发送状态报告︰

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }
        
        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-ResourceSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '30ef9bd8-9acf-4e01-8374-4dc35710fc90'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-ReportSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '6b392c6a-818c-4b24-bf38-47124f1e2f14'
        }
    }
}
PullClientConfigNames
```

## 另请参阅

* [设置推送客户端配置 id](PullClientConfigNames.md)
* [DSC web 提取服务器设置](pullServer.md)

