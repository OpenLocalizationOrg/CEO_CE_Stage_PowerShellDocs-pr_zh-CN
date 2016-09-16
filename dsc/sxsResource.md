---
title: "使用多个版本的资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: a3f2cf37eb185124d73443bbe42b5fcc82034f15
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用多个版本的资源

> 适用于︰ Windows PowerShell 5.0

在 PowerShell 5.0 DSC 资源可以有多个版本，，然后可以在计算机的并行安装版本。 通过让相同的模块文件夹中包含的多个版本的资源模块来实现。

## 安装多个资源版本并排通过

您可以使用**MinimumVersion**、 **MaximumVersion**和**RequiredVersion** [安装模块](https://technet.microsoft.com/en-us/library/dn807162.aspx)cmdlet 的参数指定哪个版本的安装的模块。 未指定版本调用**安装模块**安装最新版本。

例如，有多个版本的**xFailOverCluster**模块，其中每个包含**xCluster**资源。 未指定的版本号调用**安装模块**的结果如下所示︰

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

现在，如果呼叫**安装模块**再次，但指定 1.1.0.0 **RequiredVersion** ，它将导致以下结果︰

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster -RequiredVersion 1.1
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## 配置中指定资源版本

如果您有多个资源的计算机上安装，您必须使用配置中时指定该资源的版本。 通过指定**导入 DscResource**关键字的**ModuleVersion**参数来执行此操作。 如果您未指定资源模块都必须安装的多个版本的资源的版本，配置生成错误。

以下配置演示如何指定要呼叫的资源的版本︰

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName xFailOverCluster -ModuleVersion 1.1

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}     
```

>注意︰ 在 PowerShell 4.0 不导入 DscResource 的 ModuleVersion 参数。 在 PowerShell 4.0 中，您可以通过将模块规范对象传递给导入 DscResource 的 ModuleName 参数指定模块版本。 模块规范对象是包含 ModuleName 和 RequiredVersion 密钥哈希表。 例如︰

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName (@{ModuleName='xFailOverCluster'; RequiredVersion='1.1'} )

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}     
```

这还可用于 PowerShell 5.0，但建议使用**ModuleVersion**参数。

## 另请参阅
* [DSC 配置](configurations.md)
* [DSC 资源](resources.md)

