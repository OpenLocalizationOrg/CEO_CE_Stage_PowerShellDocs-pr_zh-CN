---
title: "使用用户凭据运行 DSC"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 8a8af7f4b82b856460427a68ec536e98f7cd981b
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用用户凭据运行 DSC 

> 适用于︰ Windows PowerShell 5.0

您可以通过使用自动**PsDscRunAsCredential**属性配置中运行 DSC 资源，在指定的一组凭据下。 默认情况下，DSC 以系统帐户运行每个资源。 有的次运行时用户是必需的例如特定用户上下文中安装 MSI 包，设置用户的注册表项、 访问特定本地目录中的用户，或访问网络共享。

DSC 的每个资源具有**PsDscRunAsCredential**属性，可以将设置为任何用户凭据 （ [PSCredential](https://msdn.microsoft.com/en-us/library/ms572524(v=VS.85).aspx)对象）。
可以在配置中，属性的值作为硬编码凭据或您可以将该值设置为[获取凭据](https://technet.microsoft.com/en-us/library/hh849815.aspx)，它将提示用户输入凭据编译配置时 （编译配置有关信息，请参阅[配置](configurations.md)。

>**注意︰**不可用在 PowerShell 4.0 **PsDscRunAsCredential**属性。

在下面的示例中，**获取凭据**用于提示用户输入凭据。 [注册表](registryResource.md)资源用于更改注册表项，指定 Windows 命令提示符窗口的背景色。

```powershell
Configuration ChangeCmdBackGroundColor    
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        Registry CmdPath
        {
            Key                  = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'
            ValueName            = 'DefaultColor'
            ValueData            = '1F'
            ValueType            = 'DWORD'
            Ensure               = 'Present'
            Force                = $true
            Hex                  = $true
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

ChangeCmdBackGroundColor -ConfigurationData $configData
```
>**注意︰**假设您有一个有效的证书，在`C:\publicKeys\targetNode.cer`，并且该证书的指纹是所示的值。
>有关加密凭据 DSC 配置 MOF 文件中的信息，请参阅[保护 MOF 文件](secureMOF.md)。

