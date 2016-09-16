---
title: "PackageManagement （也称为。 OneGet) 改进"
contributor: jianyunt, quoctruong
ms.openlocfilehash: c8470f27af946f24b92ef57f92e68a4c95c81bae
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
>注意︰ 提供建议的描述性标题和简短说明

## PackageManagement （也称为。 OneGet) 改进 ##
以下是地址的某些用户 WMF 5.1 中所做的修复体验间隙 WMF 5.0 版本中。 

1**版本别名**

**方案**︰ 假设您有版本 1.0 和 2.0 的包，P1，安装在您的系统，现在想要卸载 1.0 版，因此您运行"卸载包-命名 P1-1.0 版"。 按照您期望运行该 cmdlet 之后要卸载的 1.0 版。 但是结果是该版本 2.0 获取卸载。 
    
问题的原因是"-版本"参数是的别名"-minimumversion"参数。 当 OneGet 正在寻找 1.0 的最低版本与 qualitied 程序包时，它返回的最新版本。 因为查找最新版本的大多数人的需要，在普通的情况下预期此行为。 但是，它应不适用于卸载程序包大小写。
    
**解决方案**︰ 删除-OneGet 和 PowerShellGet 中完全版本别名。 

2**引导 NuGet 提供商的多个提示**

**方案**︰ 运行时查找模块或安装模块或其他 OneGet cmdlet 在您的计算机上首次，OneGet 尝试引导 NuGet 提供商。 这是因为 PowershellGet 提供程序也使用 NuGet 提供商下载 PowerShell 模块。 然后，OneGet 提示用户安装 NuGet 提供程序的权限。 在用户选择"是"引导之后，将安装最新版本的 NuGet 提供商。 
    
但是有是一种情况，当您有旧版本的较旧版本 NuGet 有时您计算机上安装的 NuGet 提供商获取载入首先 PowerShell 会话 （即中 OneGet 的竞争条件）。 但是 PowerShellGet 需要 Nuget 提供商联系，以使用，更高版本，以便 PowerShellGet 要求 OneGet 再次引导 NuGet 提供商。 这是为什么您看到的引导 NuGet 提供商的多个提示。

**解决方案**︰ OneGet 现在加载 NuGet 提供程序来避免引导 NuGet 提供商的多个提示的最新版本。

解决方法也存在，即手动删除旧版本的 NuGet 提供商 (NuGet Anycpu.exe)，如果存在从 $env: ProgramFiles\PackageManagement\ProviderAssemblies $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies


3**仅限 Intranet 机器**

**方案**︰ 企业方案中，为人员正在同时使用环境下其中有只是没有访问 internet 但 Intranet。 OneGet WMF 5.0 中不支持这种情况。

**解决方案**︰
- 您可以下载 NuGet 提供商在具有 Internet 连接的另一台计算机上使用的命令"安装 PackageProvider-名称 NuGet"。

- 查找你刚才安装在任一 $env 下的 NuGet 提供商︰ ProgramFiles\PackageManagement\ProviderAssemblies\nuget 或 $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget。 

- 复制到包含您的计算机上 （即没有 Internet） 文件夹或网络共享位置上的二进制文件访问过并安装 NuGet 提供商"安装 PackageProvider NuGet-源<Path to folder>"。


4**的事件日志**

在安装包时，您要更改您的计算机上的状态。 用于诊断目的 OneGet 现在到安装 Windows 事件日志记录事件、 卸载和保存程序包。 事件通道是 PowerShell，即-Windows-PowerShell 的 Microsoft，运营相同。

5 的**身份验证支持**OneGet 现在支持查找并从需要基本身份验证库中安装程序包。 您可以提供给查找程序包和安装程序包 cmdlet 您的凭据。 例如︰
``` PowerShell
Find-Package -Source <SourceWithCredential> -Credential (Get-Credential)
```
**使用 OneGet 隐藏代理**6

OneGet 现在采用代理参数:-ProxyCredential 和代理服务器。 使用这些参数，您可以指定代理 url 和 OneGet cmdlet 到代理凭据 （默认情况下，我们使用系统代理服务器设置）。 例如︰
``` PowerShell
Find-Package -Source http://www.nuget.org/api/v2/ -Proxy http://www.myproxyserver.com -ProxyCredential (Get-Credential)
```
