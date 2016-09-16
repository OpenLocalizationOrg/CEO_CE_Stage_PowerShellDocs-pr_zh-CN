---
title: "改进的 OneGet 中 WMF 5.1 （预览）"
ms.date: 2016-07-13
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 8bc4abd8d62bd328a3a47449cd790cf73a5a0eec
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# OneGet 改进
WMF 5.1 包括修复的数目和改进地址的某些用户体验间隙 WMF 5.0 版本中。 

##别名删除版本

**方案**︰ 如果有 1.0 和 2.0 程序包中，P1，您系统上安装的版本，并且您想要卸载 1.0 版，将运行"卸载包-名称 P1-1.0 版"并且预计运行该 cmdlet 之后要卸载的 1.0 版。 但是结果是该版本 2.0 获取卸载。 
    
这是因为"-版本"参数是的别名"-minimumversion"参数。 当 OneGet 正在寻找 1.0 的最低版本与限定程序包时，它返回的最新版本。 此行为预计一般情况下，因为查找最新版本通常所需的结果。 但是，它应不适用于卸载程序包大小写。
    
**解决方案**︰ 在 WMF 5.1-版本 OneGet 和 PowerShellGet 中完全删除别名。 

##引导 NuGet 提供商的多个提示

**方案**︰ OneGet 运行时查找模块或安装模块或其他 OneGet cmdlet 您的计算机上的第一次，尝试引导 NuGet 提供商。 这是因为 PowerShellGet 提供程序也使用 NuGet 提供商下载 PowerShell 模块。 然后，OneGet 提示用户安装 NuGet 提供程序的权限。 在用户选择"是"引导之后，将安装最新版本的 NuGet 提供商。 
    
但是，在某些情况下，当您有较旧版本的 NuGet 提供商在您的计算机上安装较旧版本 NuGet 有时获取载入首先 PowerShell 会话 （即中 OneGet 的竞争条件）。 但是 PowerShellGet 需要 NuGet 提供程序工作，更高版本，以便 PowerShellGet 要求 OneGet 再次引导 NuGet 提供商。 这会导致引导 NuGet 提供商的多个提示。

**解决方案**︰ 在 WMF 5.1、 OneGet 现在加载 NuGet 提供商处，来避免引导 NuGet 提供商的多个提示最新版本。

您可能还解决此问题，通过手动删除旧版本的 NuGet 提供商 (NuGet Anycpu.exe)，如果存在从 $env: ProgramFiles\PackageManagement\ProviderAssemblies $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies


##支持 OneGet intranet 访问权限的计算机上

**方案**︰ 在 WMF 5.0、 OneGet 不支持仅限 intranet （而不是 internet） 的计算机访问。

**解决方案**︰ 在 WMF 5.1，您可以按照以下步骤，允许使用 OneGet intranet 计算机︰

1. 下载使用通过安装 PackageProvider NuGet 具有 internet 连接的另一台计算机的 NuGet 提供程序。

2. 查找下任一 $env NuGet 提供商︰ ProgramFiles\PackageManagement\ProviderAssemblies\nuget 或 $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget。 

3. 将二进制文件复制到的文件夹或网络共享位置的 intranet 计算机可以访问，然后重新安装 NuGet 提供商"安装 PackageProvider NuGet-源<Path to folder>"。


##事件日志记录的改进

在安装包时，您要更改计算机的状态。 在 WMF 5.1 OneGet 现在到安装 Windows 事件日志记录事件、 卸载，然后保存程序包活动。 事件通道是 PowerShell，即-Windows-PowerShell 的 Microsoft，操作一样。

##支持基本身份验证

在 WMF 5.1 OneGet 支持查找并从需要基本身份验证库中安装程序包。 您可以提供查找程序包和安装程序包 cmdlet 到您的凭据。 例如︰

``` PowerShell
Find-Package -Source <SourceWithCredential> -Credential (Get-Credential)
```
##在代理后面使用 OneGet 支持

WMF 5.1 OneGet 现在采用新代理参数:-ProxyCredential 和代理服务器。 使用这些参数，您可以指定的代理 URL 和 OneGet cmdlet 的凭据。 默认情况下，使用系统代理设置。 例如︰

``` PowerShell
Find-Package -Source http://www.nuget.org/api/v2/ -Proxy http://www.myproxyserver.com -ProxyCredential (Get-Credential)
```
