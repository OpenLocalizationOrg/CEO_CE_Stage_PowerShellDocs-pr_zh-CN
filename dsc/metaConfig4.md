---
title: "Windows PowerShell 4.0 需要状态配置本地配置管理器 (LCM)"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 64fc906cf0328d7be3aba7d5d6819640b4dcb4fa
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows PowerShell 4.0 需要状态配置本地配置管理器 (LCM)

>适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

本地配置管理器是 Windows PowerShell 需要状态配置 (DSC) 引擎。 在所有目标节点，运行，和其负责调用 DSC 配置脚本中包括的配置资源。 本主题列出了属性的本地配置管理器，并介绍如何，您可以修改目标节点的本地配置管理器设置。

## 本地配置管理器属性
下面列出了您可以设置或检索的本地配置管理器属性。
 
* **AllowModuleOverwrite**︰ 新的配置是否下载从配置服务器是否允许改写旧的目标节点上的控件。 可能的值为 True 和 False。
* **CertificateID**: GUID 证书用于保护配置的访问权限的凭据。 有关详细信息，请参阅[希望保护在 Windows PowerShell 需要状态配置凭据？](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx)。
* **ConfigurationID**︰ 指示 GUID 用于从服务器设置为"提取"服务器获取特定配置文件。 GUID 确保正确的配置文件的访问。
* **ConfigurationMode**︰ 指定如何本地配置管理器实际应用配置到目标节点。 它可以采用以下值︰
    - **ApplyOnly**︰ 使用此选项，DSC 应用配置并不执行任何操作进一步除非检测到新的配置，或者由您直接向目标发送一个新的配置节点 （"推入"），或如果您已配置的"提取"服务器和 DSC 发现新的配置检查与"提取"服务器时。 如果目标节点配置移动，不执行任何操作。
    - **ApplyAndMonitor**︰ 使用此选项 （这是默认值），DSC 应用任何新的配置，无论是由您直接发送到目标节点还是发现"提取"服务器上。 以后，如果目标节点的配置移动从配置文件，DSC 报告日志中的差异。 有关 DSC 日志记录的详细信息，请参阅[向诊断需要状态配置中的错误使用事件日志](http://blogs.msdn.com/b/powershell/archive/2014/01/03/using-event-logs-to-diagnose-errors-in-desired-state-configuration.aspx)。
    - **ApplyAndAutoCorrect**︰ 使用此选项，DSC 应用任何新的配置，无论是由您直接发送到目标节点还是发现"提取"服务器上。 之后，如果目标节点的配置移动从配置文件，DSC 报表日志中的差异，然后再尝试调整目标节点配置，将遵循的配置文件。
* **ConfigurationModeFrequencyMins**︰ 表示背景应用程序的 DSC 尝试在目标节点上实现当前配置的频率 （以分钟为单位）。 默认值为 15。 可以结合 RefreshMode 设置此值。 当 RefreshMode 设置为提取时，目标节点 RefreshFrequencyMins 通过设置的时间间隔联系人配置服务器，并下载当前配置。 无论 RefreshMode 值中，通过 ConfigurationModeFrequencyMins，设置间隔一致性引擎会将应用到目标节点下载最新的配置。 应为整数设置 RefreshFrequencyMins ConfigurationModeFrequencyMins 的倍数。
* **凭据**: （以获取凭据的） 指示凭据访问远程资源，如联系配置服务器所需。
* **DownloadManagerCustomData**︰ 表示数组包含特定于下载管理器的自定义数据。
* **DownloadManagerName**︰ 指示配置和模块下载管理器的名称。
* **RebootNodeIfNeeded**︰ 在目标节点上的某些配置更改可能需要重新启动以应用更改。 包含**True**值，此属性将立即重新启动节点配置已被完全适用，不会进一步警告。 如果**False** （默认值），，将完成的配置，但节点必须手动重新启动以使更改生效。
* **RefreshFrequencyMins**︰ 当您已经设置了"提取"服务器时使用。 表示本地配置管理器的联系人"提取"服务器下载当前配置的频率 （以分钟为单位）。 可以结合 ConfigurationModeFrequencyMins 设置此值。 当 RefreshMode 设置为提取时，目标节点联系人 RefreshFrequencyMins 通过设置的时间间隔"提取"服务器，并下载当前配置。 通过 ConfigurationModeFrequencyMins 设置间隔，一致性引擎然后应用到目标节点下载最新的配置。 如果未设置为整数 RefreshFrequencyMins 基数的 ConfigurationModeFrequencyMins，系统将向上舍入它。 默认值为 30。
* **RefreshMode**︰ 可能的值是**推送**（默认值），然后**拉出**。 在"推入"配置中，您必须将配置文件在每个目标节点，使用任何客户端计算机。 在"提取"模式中，您必须设置"提取"服务器的本地配置管理器联系并访问的配置文件。

### 更新本地配置管理器设置的示例

下面的示例中所示，您可以更新本地配置管理器中配置脚本，阻止通过包括**LocalConfigurationManager**块节点内的目标节点的设置。

```powershell
Configuration ExampleConfig
{
    Node “Server001”
    {
        LocalConfigurationManager
        {
            ConfigurationID = "646e48cb-3082-4a12-9fd9-f71b9a562d4e"
            ConfigurationModeFrequencyMins = 45
            ConfigurationMode = "ApplyAndAutocorrect"
            RefreshMode = "Pull"
            RefreshFrequencyMins = 90
            DownloadManagerName = "WebDownloadManager"
            DownloadManagerCustomData = (@{ServerUrl="https://$PullServer/psdscpullserver.svc"})
            CertificateID = "71AA68562316FE3F73536F1096B85D66289ED60E"
            Credential = $cred
            RebootNodeIfNeeded = $true
            AllowModuleOverwrite = $false
        }
# One or more resource blocks can be added here
    }
}

# The following line invokes the configuration and creates a file called Server001.meta.mof at the specified path
ExampleConfig -OutputPath "c:\users\public\dsc"  
```

在上例中运行脚本生成 MOF 文件，用于指定和存储所需的设置。 若要应用的设置，可以使用**设置 DscLocalConfigurationManager** cmdlet，如下面的示例中所示。

```powershell
Set-DscLocalConfigurationManager -Path "c:\users\public\dsc"
```

> **注意**︰ 您必须**Path**参数中，指定当您激活上例中的配置为**OutputPath**参数指定的相同路径。

若要查看当前的本地配置管理器设置，您可以使用**获取 DscLocalConfigurationManager** cmdlet。 如果您调用不带参数此 cmdlet，默认情况下它会在其运行的节点的本地配置管理器设置。 若要指定其他节点，请使用此 cmdlet **CimSession**参数。

