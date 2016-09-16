---
title: "设置推送客户端使用配置 ID"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: f6569220fbafdba49bac9ac9dca3e6036a7aad08
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 设置推送客户端使用配置 ID

> 适用于︰ Windows PowerShell 5.0

每个目标节点具有要判断使用拉入模式和提供 URL，它可以提取与服务器联系以获取配置。 要执行此操作，您必须配置本地配置管理器 (LCM) 与所需的信息。 若要配置 LCM，您可以创建特殊类型的配置，下降与**DSCLocalConfigurationManager**属性。 有关配置 LCM 的详细信息，请参阅[配置本地配置管理器](metaConfig.md)。

> **注意**︰ 本主题适用于 PowerShell 5.0。 PowerShell 4.0 中提取客户端设置的信息，请参阅[使用 PowerShell 4.0 中的配置 ID 提取客户端设置](pullClientConfigID4.md)

以下脚本配置 LCM 提取配置从服务器名为"CONTOSO PullSrv"。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }      
    }
}
PullClientConfigID
```

在脚本**ConfigurationRepositoryWeb**块定义提取服务器。 **ServerURL**

此脚本运行之后，它创建名为**PullClientConfigID**的新输出文件夹，并那里放置 metaconfiguration MOF 文件。 在此例中，将命名 metaconfiguration MOF 文件`localhost.meta.mof`。

应用配置，若要**设置 DscLocalConfigurationManager** cmdlet，以及设置为 metaconfiguration MOF 文件的位置的**路径**。 例如︰ `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`

## 配置 ID

脚本将 LCM **ConfigurationID**属性设置为实现此目的 （您可以通过**新建 Guid** cmdlet 创建 GUID） 以前创建的 GUID。 **ConfigurationID**是 LCM 用来提取服务器上查找适当的配置。 提取服务器上的配置 MOF 文件必须命名_ConfigurationID_.mof，其中_ConfigurationID_是目标节点 LCM 的**ConfigurationID**属性的值。

## SMB 提取服务器

若要设置客户端推送配置从 SMB 服务器，请使用**ConfigurationRepositoryShare**块。 在**ConfigurationRepositoryShare**块中，指定**源路径**属性设置到服务器的路径。 以下 metaconfiguration 配置目标节点从名为**SMBPullServer**SMB 提取服务器获取。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb SMBPullServer
        {
            SourcePath = '\\SMBPullServer\PullSource'
            
        }     
    }
}
PullClientConfigID
```

## 资源和报表服务器

如果 LCM （如上例） 配置中指定**ConfigurationRepositoryWeb**或**ConfigurationRepositoryShare**块，提取客户端将获取资源从指定的服务器，但它不会向其发送报表。 可用于单个提取服务器配置、 资源和报告，但您需要创建**ReportRepositoryWeb**块设置报告。 

下面的示例演示将设置为在客户端推送配置和资源和发送到单个提取服务器报告数据，metaconfiguration。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }
        
        
        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

您还可以指定不同提取服务器的资源和报告。 若要指定资源服务器，请使用**ResourceRepositoryWeb** （适用于 web 提取服务器） 或**ResourceRepositoryShare**块 （适用于 SMB 提取服务器）。
若要指定在报表服务器，您可以使用**ReportRepositoryWeb**块。 在报表服务器不能为 SMB 服务器。
以下 metaconfiguration 配置拉客户端以获取其配置从**CONTOSO PullSrv**和**CONTOSO ResourceSrv**，从其资源并向**CONTOSO ReportSrv**发送状态报告︰

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }
        
        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

## 另请参阅

* [设置推送客户端配置名称](pullClientConfigNames.md)

