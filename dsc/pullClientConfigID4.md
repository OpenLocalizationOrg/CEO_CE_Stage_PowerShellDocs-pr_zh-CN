---
title: "使用 PowerShell 4.0 中配置 ID 提取客户端设置"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 730f2f26e2811996e79cf0073a4ef65cad390687
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用 PowerShell 4.0 中配置 ID 提取客户端设置

>适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

每个目标节点具有要判断使用拉入模式和提供 URL，它可以提取与服务器联系以获取配置。 要执行此操作，您必须配置本地配置管理器 (LCM) 与所需的信息。 若要配置 LCM，您可以创建特殊类型的配置称为"metaconfiguration"。 配置 LCM 有关详细信息，请参阅[Windows PowerShell 4.0 需要状态配置本地配置管理器](metaConfig4.md)

以下脚本配置 LCM 提取配置从名为"PullServer"的服务器︰

```powershell
Configuration SimpleMetaConfigurationForPull 
{ 
    LocalConfigurationManager 
    { 
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "WebDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30; 
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "http://PullServer:8080/PSDSCPullServer/PSDSCPullServer.svc"; AllowUnsecureConnection = “TRUE”}
    } 
} 
SimpleMetaConfigurationForPull -Output "."
```

在脚本**DownloadManagerCustomData**传递的 URL 的提取服务器和 （对于此示例中） 允许不安全的连接。 

此脚本运行之后，它会创建称为**SimpleMetaConfigurationForPull**的新输出文件夹，并那里放置 metaconfiguration MOF 文件。

若要应用配置，用于**设置 DscLocalConfigurationManager**参数与**计算机名称**（使用"主机"） 和**路径**（目标节点 localhost.meta.mof 文件的位置的路径）。 例如︰ 
```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path . –Verbose.
```

## 配置 ID
脚本将 LCM **ConfigurationID**属性设置为实现此目的 （您可以通过**新建 Guid** cmdlet 创建 GUID） 以前创建的 GUID。 **ConfigurationID**是 LCM 用来提取服务器上查找适当的配置。 必须命名提取服务器上的配置 mof `ConfigurationID.mof`，其中*ConfigurationID*为的目标节点 LCM **ConfigurationID**属性的值。

## 从 SMB 服务器

如果为 SMB 文件共享，而不是 web 服务的提取服务器的设置，您可以指定**DscFileDownloadManager** ，而不是**WebDownLoadManager**。
**DscFileDownloadManager**非常简单，而不是**ServerUrl****源路径**属性。 以下脚本配置 LCM 提取从名为"CONTOSO-服务器"的服务器上名为"SmbDscShare"SMB 共享配置︰

```powershell
Configuration SimpleMetaConfigurationForPull 
{ 
    LocalConfigurationManager 
    { 
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "DscFileDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30; 
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "\\CONTOSO-SERVER\SmbDscShare"}
    } 
} 
SimpleMetaConfigurationForPull -Output "."
```

## 另请参阅

- [DSC web 提取服务器设置](pullServer.md)
- [DSC SMB 提取服务器的设置](pullServerSMB.md)

