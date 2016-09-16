---
title: "配置本地配置管理器"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 17f86e99a3352303b4e55e42f4d251318ce1db8f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 配置本地配置管理器

> 适用于︰ Windows PowerShell 5.0

本地配置管理器 (LCM) 是引擎的 Windows PowerShell 需要状态配置 (DSC)。 LCM 每个目标节点上, 运行，并且是负责分析和制定发送到节点的配置。 也是负责 DSC，包括以下的其他方面的数目。

* 确定刷新模式 （强制或请求）。
* 指定节点提取并制定配置的频率。
* 将节点与提取服务器相关联。
* 指定部分配置。

使用特殊类型的配置配置 LCM 指定每个这些行为。 下面部分将介绍如何配置 LCM。

> **注意**︰ 本主题适用于 Windows PowerShell 5.0 中引入 LCM。 有关在 Windows PowerShell 4.0 配置 LCM 信息，请参阅[Windows PowerShell 4.0 需要状态配置本地配置管理器](metaconfig4.md)。

## 编写和制定 LCM 配置

若要配置 LCM，创建并运行配置的一种特殊类型。 若要指定 LCM 配置，您可以使用 DscLocalConfigurationManager 属性。 下图显示设置推送模式 LCM 简单配置。

```powershell
[DSCLocalConfigurationManager()]
configuration LCMConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Push'
        }
    }
} 
```

呼叫和运行的配置创建配置 MOF，就像普通配置 （创建配置 MOF 的信息，请参阅[编译配置](configurations.md#compiling-the-configuration)）。 与普通配置，您不通过致电[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet 制定 LCM 配置。 相反，您调用[设置 DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) cmdlet，提供了配置 MOF 作为参数的路径。 制定配置后，您可以通过致电[获取 DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) cmdlet 看到 LCM 的属性。

LCM 配置可以包含一组有限的资源块。 在上一示例中，仅称为资源是**设置**。 可用的其他资源包括︰

* **ConfigurationRepositoryWeb**︰ 指定 HTTP 提取服务器配置。 
* **ConfigurationRepositoryShare**︰ 指定 SMB 提取服务器配置。
* **ResourceRepositoryWeb**︰ 指定 HTTP 拉服务器的模块。
* **ResourceRepositoryShare**︰ 指定 SMB 拉服务器的模块。
* **ReportServerWeb**︰ 指定 HTTP 拉报表发送到服务器。
* **PartialConfiguration**︰ 指定部分配置。

## 基本设置

以外指定拉服务器和部分配置，将所有属性的 LCM 配置**设置**块中。 下列属性**设置**块中不可用。

|  属性  |  类型  |  说明   | 
|----------- |------- |--------------- | 
| ConfigurationModeFrequencyMins| UInt32| 频率，以分钟为单位，当前配置检查和应用。 如果 ConfigurationMode 属性设置为 ApplyOnly，则忽略此属性。 默认值为 15。 <br> __注意__︰ 此属性的值必须是__RefreshFrequencyMins__属性的值的倍数，或者__RefreshFrequencyMins__属性的值必须是此属性的值的倍数。| 
| RebootNodeIfNeeded| 布尔值| 将其设置为__$true__以在需要重新启动应用配置后自动重新启动节点。 否则，必须手动重新启动需要任何配置的节点。 默认值为__$false__。| 
| ConfigurationMode| 字符串 | 指定如何 LCM 实际应用配置到目标节点。 可能的值为__"ApplyOnly"__，__"ApplyandMonitior"(default)__，并且__"ApplyandAutoCorrect"__。 <ul><li>__ApplyOnly__: DSC 应用配置并不执行任何操作进一步除非新配置推送到目标节点或从服务器请求新的配置。 在新的配置的初始应用程序之后, DSC 不检查偏移从以前配置状态。</li><li> __ApplyAndMonitor__︰ 这是默认值。 LCM 应用任何新的配置。 后的新配置初始应用程序，如果所需的状态从移动目标节点 DSC 将报告日志中的差异。</li><li>__ApplyAndAutoCorrect__: DSC 应用任何新的配置。 之后的新配置初始应用程序，如果所需的状态从移动目标节点 DSC 报表日志中的差异，然后重新将应用当前配置。</li></ul>| 
| ActionAfterReboot| 字符串| 指定期间配置的应用程序的操作后重新启动。 可能的值为__"ContinueConfiguration(default)"__和__"StopConfiguration"__。 <ul><li> __ContinueConfiguration__︰ 继续应用当前配置后重新启动计算机。</li><li>__StopConfiguration__︰ 停止当前配置后重新启动计算机。</li></ul>| 
| RefreshMode| 字符串| 指定如何 LCM 获取配置。 可能的值为__"已禁用"__、 __"Push(default)"__，然后__"提取"__。 <ul><li>__禁用__︰ DSC 配置被禁用此节点。</li><li> __推送__︰ 配置启动，请致电[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet。 配置立即应用于节点。 这是默认值。</li><li>__拉出︰__节点配置为定期检查从提取服务器配置。 如果此属性设置为__提取__，您必须__ConfigurationRepositoryWeb__或__ConfigurationRepositoryShare__块中指定提取服务器。 关于提取服务器的详细信息，请参阅[DSC 提取服务器的设置](pullServer.md)。</li></ul>| 
| CertificateID| 字符串| 指定证书用于保护配置的访问权限的凭据 GUID。 有关更多信息，请参阅[希望安全凭据在 Windows PowerShell 需要状态配置](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx)?。| 
| ConfigurationID| 字符串| GUID，用于标识要拉入模式中提取服务器获得的配置文件。 将获取节点请求配置服务器如果 ConfigurationID.mof 名为配置 MOF 的名称。<br> __注意︰__如果您设置此属性，使用__RegistrationKey__注册提取服务器节点不起作用。 有关详细信息，请参阅[配置名称与提取客户端设置](pullClientConfigNames.md)。| 
| RefreshFrequencyMins| Uint32| 时间间隔，以分钟为单位，则 LCM 检查提取服务器以获取更新的配置。 如果 LCM 配置不在拉入模式，则忽略此值。 默认值为 30。<br> __注意︰__ 此属性的值必须是__ConfigurationModeFrequencyMins__属性的值的倍数，或者__ConfigurationModeFrequencyMins__属性的值必须是此属性的值的倍数。| 
| AllowModuleOverwrite| 布尔值| 允许__$TRUE__如果从配置服务器下载新的配置改写旧的目标节点上。 否则为 $FALSE。| 
| DebugMode| 字符串| 可能的值是__None(Default)__、 __ForceModuleImport__，和__所有__。 <ul><li>设置为__无__使用缓存的资源。 这是默认值，应在生产方案中使用。</li><li>将设置为__ForceModuleImport__，导致重新加载任何 DSC 资源模块，即使以前加载并缓存已 LCM。 在使用每个模块重新加载时，这会影响 DSC 操作的性能。 通常会在调试资源时使用此值</li><li>在此版本中，__所有__是相同__ForceModuleImport__</li></ul> |
| ConfigurationDownloadManagers| CimInstance]| 过时。 使用__ConfigurationRepositoryWeb__和__ConfigurationRepositoryShare__块定义配置提取服务器。| 
| ResourceModuleManagers| CimInstance]| 过时。 使用__ResourceRepositoryWeb__和__ResourceRepositoryShare__块定义资源提取服务器。| 
| ReportManagers| CimInstance]| 过时。 使用__ReportServerWeb__块定义报表提取服务器。| 
| PartialConfigurations| CimInstance| 未实现。 不要使用。| 
| StatusRetentionTimeInDays | UInt32| LCM 保留当前配置的状态天数。| 

## 提取服务器

提取服务器是 OData web 服务或用作 DSC 文件的中心位置 SMB 共享。 LCM 配置支持定义以下类型的提取服务器︰

* **配置服务器**︰ 对于 DSC 配置存储库。 定义配置服务器使用**ConfigurationRepositoryWeb** （用于基于 web 的服务器） 和 （用于基于 SMB 的服务器） **ConfigurationRepositoryShare**块。
* 资源服务器 — DSC 资源，打包为 PowerShell 模块的存储库。 定义使用**ResourceRepositoryWeb** （用于基于 web 的服务器） 和 （用于基于 SMB 服务器） 的**ResourceRepositoryShare**块服务器资源。
* 报表服务器 — DSC 报表将数据发送给服务。 通过使用**ReportServerWeb**块定义报表服务器。 在报表服务器必须是 web 服务。

有关设置和使用推送服务器的信息，请参阅[DSC 提取服务器的设置](pullServer.md)。

## 配置服务器块

若要定义基于 web 的配置服务器，创建**ConfigurationRepositoryWeb**块。 **ConfigurationRepositoryWeb**定义以下属性。

|属性|类型|说明|
|---|---|---| 
|AllowUnsecureConnection|布尔值|设置为**$TRUE**以允许从节点到无需身份验证服务器的连接。 设置为**$FALSE**以要求身份验证。|
|CertificateID|字符串|GUID 表示用于验证到服务器的证书。|
|ConfigurationNames|String]|配置要通过目标节点中抽取名称的数组。 只有当使用**RegistrationKey**提取服务器注册节点使用这些。 有关详细信息，请参阅[配置名称与提取客户端设置](pullClientConfigNames.md)。|
|RegistrationKey|字符串|提取服务器中注册节点 GUID。 有关详细信息，请参阅[配置名称与提取客户端设置](pullClientConfigNames.md)。|
|ServerURL|字符串|配置服务器的 URL。|

若要定义 SMB 基于配置服务器，您可以创建**ConfigurationRepositoryShare**块。 **ConfigurationRepositoryShare**定义以下属性。

|属性|类型|说明|
|---|---|---|
|凭据|MSFT_Credential|进行身份验证到 SMB 共享所使用的凭据。|
|源路径|字符串|SMB 共享的路径。|

## 资源服务器块

定义基于 web 的资源服务器，创建**ResourceRepositoryWeb**基块。 **ResourceRepositoryWeb**定义以下属性。

|属性|类型|说明|
|---|---|---|
|AllowUnsecureConnection|布尔值|设置为**$TRUE**以允许从节点的连接到服务器，但不身份验证。 设置为**$FALSE**以要求身份验证。|
|CertificateID|字符串|GUID 表示用于验证到服务器的证书。|
|RegistrationKey|字符串|GUID 标识到提取服务器节点。 有关详细信息，请参阅如何向 DSC 提取服务器注册节点。|
|ServerURL|字符串|配置服务器的 URL。|
 
若要定义基于 SMB 资源服务器，您可以创建**ResourceRepositoryShare**块。 **ResourceRepositoryShare**定义以下属性。

|属性|类型|说明|
|---|---|---|
|凭据|MSFT_Credential|进行身份验证到 SMB 共享所使用的凭据。|
|源路径|字符串|SMB 共享的路径。|

## 报表服务器块

在报表服务器必须 OData web 服务。 若要定义报表服务器，您可以创建**ReportServerWeb**块。 **ReportServerWeb**定义以下属性。

|属性|类型|说明|
|---|---|---| 
|AllowUnsecureConnection|布尔值|设置为**$TRUE**以允许从节点到无需身份验证服务器的连接。 设置为**$FALSE**以要求身份验证。|
|CertificateID|字符串|GUID 表示用于验证到服务器的证书。|
|RegistrationKey|字符串|GUID 标识到提取服务器节点。 有关详细信息，请参阅如何向 DSC 提取服务器注册节点。|
|ServerURL|字符串|配置服务器的 URL。|

## 部分配置

若要定义一个完整的配置，您可以创建**PartialConfiguration**块。 有关部分配置的详细信息，请参阅[DSC 部分配置](partialConfigs.md)。 **PartialConfiguration**定义以下属性。

|属性|类型|说明|
|---|---|---| 
|ConfigurationSource|string]|数组配置服务器，在**ConfiguratoinRepositoryWeb**和**ConfigurationRepositoryShare**块中的部分配置来自以前定义的名称。|
|取决于|字符串 {}|此部分配置应用之前必须完成其他配置名称的列表。|
|说明|字符串|用来描述部分配置的文本。|
|ExclusiveResources|string]|此部分配置独占资源的数组。|
|RefreshMode|字符串|指定 LCM 如何获取此部分配置。 可能的值为__"已禁用"__、 __"Push(default)"__，然后__"提取"__。 <ul><li>__禁用__︰ 此部分配置被禁用。</li><li> __推送__︰ 部分配置通过致电[发布 DscConfiguration](https://technet.microsoft.com/en-us/library/mt517875.aspx) cmdlet 推送到该节点。 配置节点的所有部分配置推送，或者从服务器请求之后，可以通过致电启动`Start-DscConfiguration –UseExisting`。 这是默认值。</li><li>__拉出︰__节点配置为定期检查从拉服务器部分配置。 如果__提取__设置此属性，则必须__ConfigurationSource__属性中指定提取服务器。 关于提取服务器的详细信息，请参阅[DSC 提取服务器的设置](pullServer.md)。</li></ul>|
|ResourceModuleSource|string]|数组的资源从中下载所需的资源，此部分配置的服务器的名称。 这些名称必须引用**ResourceRepositoryWeb**和**ResourceRepositoryShare**块中以前定义的资源服务器。|

## 另请参阅 

### 概念
[Windows PowerShell 需要状态配置概述](overview.md)
 
[DSC 提取服务器的设置](pullServer.md) 

[Windows PowerShell 4.0 需要状态配置本地配置管理器](metaConfig4.md) 

### 其他资源
[设置 DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) 

[设置推送客户端配置名称](pullClientConfigNames.md) 

