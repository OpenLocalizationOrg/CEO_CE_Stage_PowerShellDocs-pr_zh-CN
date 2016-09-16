---
title: "DSC SMB 提取服务器的设置"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 35ac9b38086b12fb48844c56a488854f63529e21
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC SMB 提取服务器的设置

>适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

DSC [SMB](https://technet.microsoft.com/en-us/library/hh831795.aspx)拉服务器是使 DSC 配置文件和/或 DSC 资源适用于目标节点时这些节点寻求它们 SMB 文件共享。

要使用 DSC SMB 提取服务器，您必须︰
- 设置服务器运行 PowerShell 4.0 或更高版本上 SMB 文件共享
- 配置运行 PowerShell 4.0 或更高版本的客户端从该 SMB 共享获取

## 使用 xSmbShare 资源创建 SMB 文件共享

有多种方法来设置 SMB 文件共享，但我们来看一下如何您可以执行此操作通过使用 DSC。

### 安装 xSmbShare 资源

致电[安装模块](https://technet.microsoft.com/en-us/library/dn807162.aspx)cmdlet 来安装**xSmbShare**模块。
>**注意**︰**安装模块**包括在**PowerShellGet**模块中，包括在 PowerShell 5.0。 您可以下载**PowerShellGet**模块 PowerShell 3.0 和 4.0 [PackageManagement PowerShell 模块](https://www.microsoft.com/en-us/download/details.aspx?id=49186)的预览。 **XSmbShare**包含 DSC 资源**xSmbShare**，它可用于创建 SMB 文件共享。

### 创建目录和文件共享

以下配置使用[文件](fileResource.md)资源创建目录中的共享，以及设置 SMB 共享**xSmbShare**资源︰

```powershell
Configuration SmbShare {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare
 
    Node localhost {
 
        File CreateFolder {
 
            DestinationPath = 'C:\DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
 
        }
 
        xSMBShare CreateShare {
 
            Name = 'DscSmbShare'
            Path = 'C:\DscSmbShare'
            FullAccess = 'admininstrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
 
        }
        
    }
 
}
```

配置创建目录`C:\DscSmbShare`如果它已不存在，并且然后，该目录将用作 SMB 文件共享。 **FullAccess**应授予对任何需要写入或从文件共享，删除的帐户和**ReadAccess**必须提供给任何客户端节点，将收到配置和/或 DSC 资源从共享 （这是因为 DSC 以系统帐户默认运行，因此本身的计算机必须有权访问该共享）。


### 让提取客户端的文件系统访问

供客户端节点**ReadAccess**允许访问 SMB 共享，但不能为中的文件或文件夹共享该节点。 您必须显式授予客户端节点访问 SMB 共享文件夹和子文件夹。 我们可以这样做 DSC 与通过添加使用**cNtfsPermissionEntry**资源，其中包含[CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0)模块中。 以下配置添加**cNtfsPermissionEntry**块为提取客户端授予 ReadAndExecute 访问权限︰

```powershell
Configuration DSCSMB {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare
Import-DscResource -ModuleName cNtfsAccessControl
 
    Node localhost {
 
        File CreateFolder {
 
            DestinationPath = 'DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
 
        }
 
        xSMBShare CreateShare {
 
            Name = 'DscSmbShare'
            Path = 'DscSmbShare'
            FullAccess = 'administrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
 
        }

        cNtfsPermissionEntry PermissionSet1 {
            
        Ensure = 'Present'
        Path = 'C:\DSCSMB'
        Principal = 'myDomain\Contoso-Server$'
        AccessControlInformation = @(
            cNtfsAccessControlInformation
            {
                AccessControlType = 'Allow'
                FileSystemRights = 'ReadAndExecute'
                Inheritance = 'ThisFolderSubfoldersAndFiles'
                NoPropagateInherit = $false
            }
        )
        DependsOn = '[File]CreateFolder'
        
        }
 
        
    }
 
}
```

## 放置配置和资源

保存任何配置 MOF 文件和/或所需客户端节点 SMB 共享文件夹中提取 DSC 资源。

任何配置 MOF 文件必须命名_ConfigurationID_.mof，其中_ConfigurationID_是目标节点 LCM 的**ConfigurationID**属性的值。 有关请求客户端设置的详细信息，请参阅[使用配置 ID 提取客户端设置](pullClientConfigID.md)。

>**注意︰**如果您使用的 SMB 提取服务器，您必须使用配置 Id。 不支持 SMB 配置名称。

客户端所需的任何资源必须放置 SMB 共享文件夹中归档`.zip`文件。  

## 创建 MOF 校验和
配置 MOF 文件需要成对使用校验和文件，以便在目标节点 LCM 可以验证配置。 若要创建一个校验和，请致电[新建 DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet。 该 cmdlet 所需的指定配置 MOF 所在的文件夹的**路径**参数。 该 cmdlet 创建校验和名为`ConfigurationMOFName.mof.checksum`，其中`ConfigurationMOFName`是配置 mof 文件的名称。 如果有多个配置 MOF 文件中指定的文件夹，为每个文件夹中配置创建校验和。

校验和文件必须配置 MOF 文件所在的目录中存在 (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration`默认情况下)，并且具有相同的名称`.checksum`扩展名附加。

>**注意**︰ 如果您更改任何方式配置 MOF 文件，必须也重新创建校验和文件。

## 确认

特殊致谢下列操作︰

- Mike f。 Robbins 上用于 DSC SMB 其帖子帮助通知本主题中的内容。 他的博客位于[Mike F Robbins](http://mikefrobbins.com/)。
- 作者**cNtfsAccessControl**模块 serge Nikalaichyk。 此模块的源位于 https://github.com/SNikalaichyk/cNtfsAccessControl。

## 另请参阅
- [Windows PowerShell 需要状态配置概述](overview.md)
- [制定配置](enactingConfigurations.md)
- [设置推送客户端使用配置 ID](pullClientConfigID.md)

 
