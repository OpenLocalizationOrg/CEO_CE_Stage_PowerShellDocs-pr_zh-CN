---
title: "配置数据中的凭据选项"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 58ba849bbf0789a66bc752385c7954edf95c9d03
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 配置数据中的凭据选项
>适用于︰ Windows PowerShell 5.0

## 纯文本密码和域的用户

包含未加密凭据 DSC 配置将生成有关纯文本密码错误消息。
此外，DSC 将生成一个警告时使用域凭据。
若要取消这些错误和警告消息，请使用 DSC 配置数据关键字︰
* **PsDscAllowPlainTextPassword**
* **PsDscAllowDomainUser**

## 处理 DSC 中的凭据

DSC 配置资源以运行`Local System`默认情况下。
但是，一些资源需要凭据，例如当`Package`资源需要安装软件的特定用户帐户。

使用早期的资源的硬编码`Credential`用于处理此属性名称。
WMF 5.0 添加自动`PsDscRunAsCredential`属性的所有资源。 有关使用信息`PsDscRunAsCredential`，请参阅[使用用户凭据运行 DSC](runAsUser.md)。
较新的资源和自定义资源可以使用此自动属性，而不是创建其自己的属性对于凭据。

*请注意，设计的一些资源是多个凭据用于特定的原因，他们将具有其自己的凭据属性。*

若要查找可用的凭据对资源的属性使用`Get-DscResource -Name ResourceName -Syntax`或使用 ise Intellisense (`CTRL+SPACE`)。

```PowerShell
PS C:\> Get-DscResource -Name Group -Syntax
Group [String] #ResourceName
{
    GroupName = [string]
    [Credential = [PSCredential]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Members = [string[]]]
    [MembersToExclude = [string[]]]
    [MembersToInclude = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

此示例使用[组](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource)资源从`PSDesiredStateConfiguration`内置 DSC 资源模块。
它可以创建本地组和添加或删除成员。
它接受两者`Credential`属性和自动`PsDscRunAsCredential`属性。
但是，资源仅使用`Credential`属性。
阅读有关`PsDscRunAsCredential` [WMF 发行说明](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_runas)中。

## 示例︰ 组资源凭据属性

在下运行 DSC `Local System`，所以它已具有更改本地用户和组的权限。
如果添加的成员，本地帐户无凭据是必需的。
如果`Group`资源将域帐户添加到本地组中，则需要凭据。

不允许匿名到 Active Directory 的查询。
`Credential`属性`Group`资源是用于为查询 Active Directory 域帐户。
大多数情况下这可能是通用的用户帐户，因为默认情况下用户可以*读取*大部分 Active Directory 中的对象。

## 配置示例

下面的代码示例使用 DSC 填充本地组与特定域的用户︰

```PowerShell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred
```

此代码生成错误和警告消息︰

```
ConvertTo-MOFInstance : System.InvalidOperationException error processing
property 'Credential' OF TYPE 'Group': Converting and storing encrypted
passwords as plain text is not recommended. For more information on securing
credentials in MOF file, please refer to MSDN blog:
http://go.microsoft.com/fwlink/?LinkId=393729

At line:11 char:9
+   Group
At line:297 char:16
+     $aliasId = ConvertTo-MOFInstance $keywordName $canonicalizedValue
+                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessProperty,ConvertTo-MOFInstance

WARNING: It is not recommended to use domain credential for node 'localhost'.
In order to suppress the warning, you can add a property named
'PSDscAllowDomainUser' with a value of $true to your DSC configuration data
for node 'localhost'.
```

此示例包含两个问题︰
1.  错误说明不建议使用纯文本密码
2.  警告，建议不要使用域凭据

## PsDscAllowPlainTextPassword

第一条错误消息具有与文档的 URL。
此链接解释如何对使用[配置数据](https://msdn.microsoft.com/en-us/powershell/dsc/configdata)结构和证书的密码进行加密。
有关证书和 DSC[阅读此文章](http://aka.ms/certs4dsc)的详细信息。

若要强制纯文本密码，资源需要`PsDscAllowPlainTextPassword`配置数据中的关键字部分，如下所示︰

```PowerShell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowPlainTextPassword = $true
        }
    )
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred -ConfigurationData $cd
```

*请注意，`NodeName`不能等于星号、 特定节点名称为必填项。*

**Microsoft 建议以避免由于重大安全风险的纯文本密码。**

## 域凭据

运行示例配置脚本再次 （具有或不加密） 仍然生成的警告中使用域帐户凭据不建议。
使用本地帐户可以省去域凭据可用于其他服务器上的潜在风险。

**当使用 DSC 资源的凭据，对域帐户时可能希望本地帐户。**

如果存在\'或 @ 中`Username`的凭据，然后 DSC 属性会将其视为域帐户。
没有异常"主机"，"127.0.0.1"和":: 1 英寸的用户名称域部分中。

## PSDscAllowDomainUser

在 DSC`Group`资源示例上方，查询 Active Directory 域*需要*一个域的帐户。
在此例中添加`PSDscAllowDomainUser`属性`ConfigurationData`阻止，如下所示︰

```PowerShell
$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowDomainUser = $true
            # PSDscAllowPlainTextPassword = $true
            CertificateFile = "C:\PublicKeys\server1.cer"
        }
    )
}
```

现在配置脚本将生成 MOF 文件没有错误或警告。

