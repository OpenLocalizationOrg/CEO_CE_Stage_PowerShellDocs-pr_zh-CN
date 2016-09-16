---
title: "开始 linux 需要状态配置 (DSC)"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: c585dc929e85a404aecfb1e9f06daf2dfaf21832
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 开始 linux 需要状态配置 (DSC)

本主题介绍如何开始使用 Linux PowerShell 需要状态配置 (DSC)。 有关 DSC 常规信息，请参阅[开始使用 Windows PowerShell 需要状态配置](overview.md)。

## 支持的 Linux 操作系统版本

以下 Linux 操作系统版本为 Linux 支持 DSC。
- CentOS 5、 6 和 7 (x86/x64)
- Debian GNU/Linux 6 和 7 (x86/x64)
- Oracle Linux 5、 6 和 7 (x86/x64)
- 红色帽子企业 Linux 服务器 5、 6 和 7 (x86/x64)
- SUSE Linux Enterprise Server 10、 11 和 12 (x86/x64)
- Ubuntu 服务器 12.04 LTS 和 14.04 LTS (x86/x64)

下表用于 Linux DSC 描述所需的程序包依赖项。

|  所需的包 |  说明 |  最低版本 | 
|---|---|---|
| glibc| GNU 库| 2...4-31.30| 
| python| Python| 24-3.4| 
| omiserver| 打开管理基础结构| 1.0.8.1| 
| openssl| OpenSSL 库| 0.9.8 或 1.0| 
| ctypes| Python CTypes 库| 必须匹配 Python 版本| 
| libcurl| 卷曲 http 客户端库| 7.15.1| 

## 安装用于 Linux DSC

安装用于 Linux DSC 之前，必须安装[打开管理基础结构 (OMI)](https://collaboration.opengroup.org/omi/) 。

### 安装 OMI

所需的状态配置 linux 需要打开管理基础结构 (OMI) CIM 服务器版本 1.0.8.1。 可以从打开组中下载 OMI︰[打开管理基础结构 (OMI)](https://collaboration.opengroup.org/omi/)。

若要安装 OMI，安装适合您的 Linux 系统 （个.rpm 或.deb） 和 OpenSSL 版本 （ssl_098 或 ssl_100） 和体系结构 (x64/x86) 程序包。 适用于 CentOS、 红色帽子企业 Linux、 SUSE Linux 企业服务器，以及 Oracle Linux 已 RPM 程序包。 DEB 包是适用于 Debian 的 GNU Linux 和 Ubuntu 服务器。 Ssl_098 程序包是适合 OpenSSL 0.9.8 安装虽然 ssl_100 程序包 OpenSSL 1.0 安装适用于计算机的计算机。

> **注意**︰ 要确定安装的 OpenSSL 版本，请运行命令`openssl version`。

运行以下命令以安装 OMI CentOS 7 x64 系统上。

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### 安装 DSC

DSC linux 是可供下载[下面](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/latest)。 

若要安装 DSC，安装适合您的 Linux 系统 （个.rpm 或.deb） 和 OpenSSL 版本 （ssl_098 或 ssl_100） 和体系结构 (x64/x86) 程序包。 适用于 CentOS、 红色帽子企业 Linux、 SUSE Linux 企业服务器，以及 Oracle Linux 已 RPM 程序包。 DEB 包是适用于每个 Linux Debian GNU 和 Ubuntu 服务器。 Ssl_098 程序包是适合 OpenSSL 0.9.8 安装虽然 ssl_100 程序包 OpenSSL 1.0 安装适用于计算机的计算机。

> **注意**︰ 要确定安装的 OpenSSL 版本，请运行命令 openssl 版本。
 
运行以下命令以安装 DSC CentOS 7 x64 系统上。

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`


## 用于 Linux DSC

以下各节介绍了如何创建和运行 DSC 配置 Linux 计算机上。

### 创建配置 MOF 文档

Windows PowerShell 配置关键字用于为创建配置 Linux 计算机，就像 for Windows 的计算机。 以下步骤介绍如何创建的 Linux 计算机使用 Windows PowerShell 配置文档。

1. 导入的 nx 模块。 Nx Windows PowerShell 模块 linux，包含用于 DSC 的内置资源的架构和必须本地计算机上安装和配置中导入。

    到安装 nx 模块，用于选择复制 nx 模块目录`$env:USERPROFILE\Documents\WindowsPowerShell\Modules\`或`$PSHOME\Modules`。 DSC Linux 安装包 (MSI) 中包含 nx 模块。 若要导入您的配置 nx 模块，请使用__导入 DSCResource__命令︰
    
```powershell
Configuration ExampleConfiguration{
   
    Import-DSCResource -Module nx

}
```
2. 定义配置和生成配置文档︰

```powershell
Configuration ExampleConfiguration{
   
    Import-DscResource -Module nx
 
    Node  "linuxhost.contoso.com"{
    nxFile ExampleFile {

        DestinationPath = "/tmp/example"
        Contents = "hello world `n"
        Ensure = "Present"
        Type = "File"
    }

    }
}
ExampleConfiguration -OutputPath:"C:\temp" 
```

### 将配置推送到 Linux 计算机

配置文档 （MOF 文件） 可以推送到 Linux 计算机使用[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet。 为了使用此 cmdlet，以及[获取 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379).aspx 或[测试 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet，远程到 Linux 计算机，您必须使用 CIMSession。 [新建 CimSession](https://technet.microsoft.com/en-us/library/jj590760.aspx) cmdlet 用于创建到 Linux 计算机 CIMSession。

下面的代码演示如何创建用于 Linux DSC CIMSession。

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true 
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90 
```

> **注意**︰
* 对于"推送"模式，用户凭据必须是根用户 Linux 计算机上。
* 对于 Linux、 新建 CimSession 必须使用-UseSSL 参数设置为 $true for DSC 支持仅 SSL/TLS 连接。
* 在文件中指定用于通过 OMI （DSC) 的 SSL 证书︰`/opt/omi/etc/omiserver.conf`属性︰ pemfile 和密钥文件。
如果 Windows 计算机上运行[新建 CimSession](https://technet.microsoft.com/en-us/library/jj590760.aspx) cmdlet 不信任此证书，您可以选择忽略证书验证 CIMSession 选项︰ `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`

运行以下命令以将 DSC 配置推送到 Linux 节点。

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### 分发与提取服务器配置

配置可以分发给 Linux 计算机拉服务器，就像 for Windows 的计算机。 有关使用提取服务器的指导，请参阅[Windows PowerShell 需要状态配置提取服务器](pullServer.md)。 其他信息和相关 Linux 计算机使用拉服务器限制，请参阅发行说明需要状态配置 linux。

### 使用本地配置

DSC linux 包括用于处理来自本地 Linux 计算机配置脚本。 找到中的这些脚本`/opt/microsoft/dsc/Scripts`，并且包含以下内容︰
* GetDscConfiguration.py

 返回当前配置应用于计算机。 类似的 Windows PowerShell cmdlet 获取 DscConfiguration cmdlet。

`# sudo ./GetDscConfiguration.py`

* GetDscLocalConfigurationManager.py

 返回应用于计算机当前元配置。 类似于 cmdlet[获取 DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) cmdlet。

`# sudo ./GetDscLocalConfigurationManager.py`

* InstallModule.py

 安装自定义的 DSC 资源模块。 需要包含模块共享的对象库的.zip 文件和架构 MOF 文件的路径。

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

* RemoveModule.py

 删除自定义 DSC 资源模块。 要求模块后，若要删除的名称。

`# sudo ./RemoveModule.py cnx_Resource`

* StartDscLocalConfigurationManager.py 

 应用于计算机配置 MOF 文件。 类似于[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet。 需要配置 MOF 要应用的路径。

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

* SetDscLocalConfigurationManager.py

 应用于计算机元配置 MOF 文件。 类似于[设置 DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) cmdlet。 需要元配置 MOF 要应用的路径。

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## PowerShell 所需 Linux 日志文件的状态的配置

Linux 邮件为 DSC 生成下列日志文件。

|日志文件|目录|说明|
|---|---|---|
|omiserver.log|/var/opt/omi/log|与 OMI CIM 服务器操作相关的邮件。|
|dsc.log|/var/opt/omi/log|与本地配置管理器 (LCM) 和 DSC 资源操作的操作相关的邮件。|

