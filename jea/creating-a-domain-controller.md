---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "创建域控制器"
ms.technology: powershell
ms.openlocfilehash: 80b957ed666ca626c6083041cf99c263e2e0dc27
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
### 创建域控制器

本文假设您的计算机上加入域。
如果您当前没有安装域才能加入，此部分可以帮助您快速设置域控制器使用 DSC 突出。

#### 先决条件

1.  计算机位于内部网络
2.  计算机未连接到现有的域
3.  计算机正在运行 Windows Server 2016 或 WMF 5.0 安装

#### 安装 xActiveDirectory
如果您的计算机上具有活动的 internet 连接，请在提升 PowerShell 窗口中运行以下命令︰
```PowerShell
Install-Module xActiveDirectory -Force
```
如果您没有连接到 internet，另一台计算机上安装 xActiveDirectory，然后将 xActiveDirectory 文件夹复制到您的计算机上的"C:\Program Files\WindowsPowerShell\Modules"文件夹。

若要确认安装成功，运行以下命令︰
```PowerShell
Get-Module xActiveDirectory -ListAvailable
```

#### 域设置为与 DSC
若要使您的计算机上的新域中的域控制器的 PowerShell 中，复制以下脚本。
**作者的注释︰ 没有提供未使用的凭据的已知的问题。  为安全，请不要忘记您的本地管理员密码。**

```PowerShell
Set-Item WSMan:\localhost\Client\TrustedHosts -Value $env:COMPUTERNAME -Force

# This "MetaConfiguration" sets the DSC Engine to automatically reboot if required
[DscLocalConfigurationManager()]
Configuration MetaConfiguration
{
    Node $env:Computername
    {
        Settings
        {
            RebootNodeIfNeeded = $true
        }
    }

}

MetaConfiguration
# Apply the MetaConfiguration
Set-DscLocalConfigurationManager .\MetaConfiguration

# Configure a domain controller of a new "Contoso" domain
configuration DomainController
{
    param
    (
        $node,
        $cred
    )
    Import-DscResource -ModuleName xActiveDirectory

    Node $node
    {
        WindowsFeature ADDS
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xADDomain Contoso
        {
            DomainName = 'contoso.com'
            DomainAdministratorCredential = $cred
            SafemodeAdministratorPassword = $cred
            DependsOn = '[WindowsFeature]ADDS'
        }

        file temp
        {
            DestinationPath = 'C:\temp.txt'
            Contents = 'Domain has been created'
            DependsOn = '[xADDomain]Contoso'
        }
    }
}

$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = $env:Computername
            PSDscAllowPlainTextPassword = $true
        }
    )
}

# Enter your desired password for the domain administrator (note, this will be stored as plain text)
DomainController -cred (Get-Credential -Message "Enter desired credential for domain administrator") -node $env:Computername -configurationData $ConfigData

# Apply the configuration to create the domain controller
Start-DSCConfiguration -path .\DomainController -ComputerName $env:Computername -Wait -Force -Verbose
```
您的计算机上将重新启动几次。
您将了解完毕后，您将看到一个名为"C:\temp.txt"包含"已创建域。"文件

#### 设置用户和组
在您的域和相应的非管理员用户该组的成员，以下命令将设置运算符和技术支持人员的组。
```PowerShell
# Make Groups
$NonAdminOperatorGroup = New-ADGroup -Name "JEA_NonAdmin_Operator" -GroupScope DomainLocal -PassThru
$NonAdminHelpDeskGroup = New-ADGroup -Name "JEA_NonAdmin_HelpDesk" -GroupScope DomainLocal -PassThru
$TestGroup = New-ADGroup -Name "Test_Group" -GroupScope DomainLocal -PassThru

# Make Users
$OperatorUser = New-ADUser -Name "OperatorUser" -AccountPassword (ConvertTo-SecureString 'pa$$w0rd' -AsPlainText -Force) -PassThru
Enable-ADAccount -Identity $OperatorUser

$HelpDeskUser = New-ADUser -name "HelpDeskUser" -AccountPassword (ConvertTo-SecureString 'pa$$w0rd' -AsPlainText -Force) -PassThru
Enable-ADAccount -Identity $HelpDeskUser

# Add Users to Groups
Add-ADGroupMember -Identity $NonAdminOperatorGroup -Members $OperatorUser
Add-ADGroupMember -Identity $NonAdminHelpDeskGroup -Members $HelpDeskUser
```

