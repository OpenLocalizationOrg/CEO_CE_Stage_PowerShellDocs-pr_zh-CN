---
title: "保护 MOF 文件"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 2a7b494050e81450694fba8e8b779c082a904b3f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 保护 MOF 文件

>适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

DSC 告诉目标节点应通过将使用该信息 MOF 文件发送到每个节点，本地配置管理器 (LCM) 位置实现所需的配置哪些配置。 因为此文件包含配置的详细信息，请务必确保安全。 若要执行此操作，您可以设置 LCM 检查用户的凭据。 本主题介绍如何通过使用证书对它们进行加密传输到目标节点安全地这些凭据。

>**注意︰**本主题讨论用于加密证书。 加密，自签名的证书已足够，因为私钥始终保持机密和加密并不意味着信任的文档。 自签名的证书应*不*用于进行身份验证。 进行任何身份验证，应使用证书从受信任证书颁发机构 (CA)。

## 先决条件

要成功加密用于安全 DSC 配置的凭据，请确保您拥有以下︰

* **一些意味着颁发和分发证书**。 本主题和其示例假定您使用的 Active Directory 证书颁发机构。 有关更多 Active Directory 证书服务的背景信息，请参阅[Active Directory 证书服务概述](https://technet.microsoft.com/library/hh831740.aspx)和[Windows Server 2008 中的 Active Directory 证书服务](https://technet.microsoft.com/windowsserver/dd448615.aspx)。
* **管理访问或多个目标节点**。
* **每个目标节点具有保存其个人存储支持加密的证书**。 Windows PowerShell 中存储的路径是证书︰ \LocalMachine\My。 本主题中的示例使用"工作站身份验证"模板，则可以在[默认证书模板](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx)找到 （以及其他证书模板）。
* 如果您将会在目标节点，**导出证书的公钥**，以外的计算机上运行此配置，然后将其导入到将运行来自配置的计算机。 请确保您导出**仅使用公钥;**确保私钥安全。

## 整个过程

 1. 设置证书、 键和指纹，确保每个目标节点具有证书的副本，并配置计算机具有公钥和指纹。
 2. 创建包含的路径和指纹公钥配置数据块。
 3. 创建配置脚本定义您所需的配置目标节点并设置解密目标节点上通过命令本地配置管理器解密配置数据使用的证书和其缩略图。
 4. 运行的配置，这将本地配置管理器设置并开始 DSC 配置。

![图 1](images/CredentialEncryptionDiagram1.png)

## 证书要求

若要制定管理凭据加密，公钥证书必须是**受信任**计算机用于创作 DSC 配置_目标节点_上可用。
此公钥证书有特定要求使用加密 DSC 凭据︰
 1. **密钥用法**︰
   - 必须包含: 'KeyEncipherment' 和 'DataEncipherment。
   - 应_不_包含: 数字签名。
 2. **增强型密钥用法**︰
   - 必须包含︰ 文档加密 (1.3.6.1.4.1.311.80.1)。
   - 应_不_包含︰ 客户端身份验证 (1.3.6.1.5.5.7.3.2) 和服务器身份验证 (1.3.6.1.5.5.7.3.1)。
 3. 私钥的证书位于 * 目标 Node_。
 4. **提供商**的证书必须是"Microsoft RSA 频道加密提供程序"。
 
>**建议的最佳做法︰**虽然您可以使用的证书包含数字签名或其中一个身份验证 EKU 密钥用法，这将使加密密钥以更轻松地将误用和受到攻击。 因此，它是最佳做法使用专门用于保护 DSC 凭据创建的证书，忽略这些密钥用法和 Eku。
  
符合以下条件的_目标节点_上的任何现有证书用于保护 DSC 凭据。

## 创建证书

有两种方法可用于创建和使用所需的加密证书 （公钥私钥对）。

1. 在**目标节点**上创建它并将相同的公钥导出到**创作节点**
2. **创作节点**上创建它并将整个密钥对导出到**目标节点**

方法 1 建议，因为私钥用于解密 MOF 中的凭据始终保持在目标节点。


### 在目标节点上创建的证书

私钥必须保密，因为用于解密 MOF**目标节点**上的执行此操作的最简单方法是**目标节点**，创建私钥证书并复制到计算机创作 DSC 配置到 MOF 文件正在使用的**公钥证书**。
下面的示例︰
 1. 在**目标节点**上创建证书
 2. 导出**目标节点**上的公钥证书。
 3. 导入**我**的证书存储在**创作节点**的公钥证书。

#### 在目标节点上︰ 创建和导出证书
>创作节点︰ Windows Server 2016 和 Windows 10

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
一次导出，```DscPublicKey.cer```需要复制到**创作节点**。

>创作节点︰ Windows Server 2012 R2/Windows 8.1 和更早版本

新建 SelfSignedCertificate cmdlet 在 Windows 操作系统上之前 Windows 10 和 Windows Server 2016 不支持参数的**类型**，因为这些操作系统上需要创建此证书的另一种方法。
在此例中，您可以使用```makecert.exe```或```certutil.exe```以创建证书。

另一种方法是[下载来自 Microsoft 脚本中心的新建 SelfSignedCertificateEx.ps1 脚本](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6)，并使用它来改为创建证书︰
```powershell
# note: These steps need to be performed in an Administrator PowerShell session
# and in the folder that contains New-SelfSignedCertificateEx.ps1
. .\New-SelfSignedCertificateEx.ps1
New-SelfsignedCertificateEx `
    -Subject "CN=${ENV:ComputerName}" `
    -EKU 'Document Encryption' `
    -KeyUsage 'KeyEncipherment, DataEncipherment' `
    -SAN ${ENV:ComputerName} `
    -FriendlyName 'DSC Credential Encryption certificate' `
    -Exportable `
    -StoreLocation 'LocalMachine' `
    -StoreName 'My' `
    -KeyLength 2048 `
    -ProviderName 'Microsoft Enhanced Cryptographic Provider v1.0' `
    -AlgorithmName 'RSA' `
    -SignatureAlgorithm 'SHA256'
# Locate the newly created certificate
$Cert = Get-ChildItem -Path cert:\LocalMachine\My `
    | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') `
        -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
一次导出，```DscPublicKey.cer```需要复制到**创作节点**。

#### 在创作节点︰ 导入证书公钥
```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### 在创作节点上创建的证书
或者，可以**创作节点**上创建、 导出具有**私钥**为 PFX 文件，然后导入到**目标节点**加密证书。
这是当前_Nano 服务器_上实现 DSC 凭据加密方法。
虽然使用密码保护 PFX 它应保持安全在传输过程。
下面的示例︰
 1. **创作节点**上创建一个证书。
 2. 导出包括**创作节点**上的私钥的证书。
 3. 从**创作节点**，删除私钥，但是保留**我**的存储中的公钥证书。
 4. 导入**目标节点**的根证书存储区中的私钥证书。
   - 它必须添加到的根存储，以便将受信任的**目标节点**。

#### 在创作节点︰ 创建和导出证书
>目标节点︰ Windows Server 2016 和 Windows 10

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the private key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```
一次导出，```DscPrivateKey.cer```需要复制到**目标节点**。

>目标节点︰ Windows Server 2012 R2/Windows 8.1 和更早版本

新建 SelfSignedCertificate cmdlet 在 Windows 操作系统上之前 Windows 10 和 Windows Server 2016 不支持参数的**类型**，因为这些操作系统上需要创建此证书的另一种方法。
在此例中，您可以使用```makecert.exe```或```certutil.exe```以创建证书。

另一种方法是[下载来自 Microsoft 脚本中心的新建 SelfSignedCertificateEx.ps1 脚本](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6)，并使用它来改为创建证书︰
```powershell
# note: These steps need to be performed in an Administrator PowerShell session
# and in the folder that contains New-SelfSignedCertificateEx.ps1
. .\New-SelfSignedCertificateEx.ps1
New-SelfsignedCertificateEx `
    -Subject "CN=${ENV:ComputerName}" `
    -EKU 'Document Encryption' `
    -KeyUsage 'KeyEncipherment, DataEncipherment' `
    -SAN ${ENV:ComputerName} `
    -FriendlyName 'DSC Credential Encryption certificate' `
    -Exportable `
    -StoreLocation 'LocalMachine' `
    -StoreName 'My' `
    -KeyLength 2048 `
    -ProviderName 'Microsoft Enhanced Cryptographic Provider v1.0' `
    -AlgorithmName 'RSA' `
    -SignatureAlgorithm 'SHA256'
# Locate the newly created certificate
$Cert = Get-ChildItem -Path cert:\LocalMachine\My `
    | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') `
        -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

#### 在目标节点上︰ 导入为受信任的根证书私钥
```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\Root -Password $mypwd > $null
```

## 配置数据

配置数据块定义的目标节点工作，是否或未加密凭据、 加密的方式和其他信息。 配置数据块的详细信息，请参阅[分隔配置和环境数据](configData.md)。

可以为每个节点配置相关证书加密的元素是︰
* **节点名称**-正在配置为加密凭据目标节点的名称。
* **PsDscAllowPlainTextPassword** -是否将允许未加密的凭据传递给此节点。 这是**不建议这样做**。
* **指纹**-将使用在_目标节点_的 DSC 配置中凭据进行解密证书的指纹。 **此证书必须位于目标节点的本地计算机证书存储区。**
* **CertificateFile** -证书文件 （包含只是公钥） 应使用_目标节点_加密凭据。 它必须是 DER 编码二进制 X.509 或 Base 64 编码 X.509 证书文件格式。

此示例显示指定目标节点行事命名 targetNode，公钥证书文件路径 （名为 targetNode.cer），以及有关公钥指纹配置的数据块。

```powershell
$ConfigData= @{ 
    AllNodes = @(     
            @{  
                # The name of the node we are describing 
                NodeName = "targetNode" 

                # The path to the .cer file containing the 
                # public key of the Encryption Certificate 
                # used to encrypt credentials for this node 
                CertificateFile = "C:\publicKeys\targetNode.cer" 

         
                # The thumbprint of the Encryption Certificate 
                # used to decrypt the credentials on target node 
                Thumbprint = "AC23EA3A9E291A75757A556D0B71CBBF8C4F6FD8" 
            }; 
        );    
    }
```


## 配置脚本

在配置脚本本身，使用`PsCredential`参数，以确保凭据存储的最短的时间。 当您运行提供的示例时，DSC 将提示您输入凭据，然后加密使用与配置的数据块中的目标节点 CertificateFile MOF 文件。 此代码示例为用户的共享保护复制一个文件。

```
configuration CredentialEncryptionExample 
{ 
    param( 
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [PsCredential] $credential 
        ) 
    

    Node $AllNodes.NodeName 
    { 
        File exampleFile 
        { 
            SourcePath = "\\Server\share\path\file.ext" 
            DestinationPath = "C:\destinationPath" 
            Credential = $credential 
        } 
    } 
}
```

## 设置解密

之前[`Start-DscConfiguration`](https://technet.microsoft.com/en-us/library/dn521623.aspx)可以工作，您需要在每个目标节点的证书，用于解密凭据，告诉本地配置管理器用于验证的证书指纹 CertificateID 资源。 此示例函数将找到适当的本地证书 （您可能需要自定义它，以便它将查找您要使用的确切证书）︰

```powershell
# Get the certificate that works for encryption 
function Get-LocalEncryptionCertificateThumbprint 
{ 
    (dir Cert:\LocalMachine\my) | %{
        # Verify the certificate is for Encryption and valid 
        if ($_.PrivateKey.KeyExchangeAlgorithm -and $_.Verify()) 
        { 
            return $_.Thumbprint 
        } 
    } 
}
```

使用由其指纹标识证书，可以更新配置脚本以使用值︰

```powershell
configuration CredentialEncryptionExample 
{ 
    param( 
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [PsCredential] $credential 
        ) 
    

    Node $AllNodes.NodeName 
    { 
        File exampleFile 
        { 
            SourcePath = "\\Server\share\path\file.ext" 
            DestinationPath = "C:\destinationPath" 
            Credential = $credential 
        } 
        
        LocalConfigurationManager 
        { 
             CertificateId = $node.Thumbprint 
        } 
    } 
}
```

## 运行配置

此时，您可以运行的配置，将输出两个文件︰

 * *。 配置本地配置管理器中使用的是存储在本地计算机存储并由其指纹标识的证书凭据进行解密的 meta.mof 文件。[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/en-us/library/dn521621.aspx)适用*。 meta.mof 文件。
 * 实际应用配置 MOF 文件。 开始 DscConfiguration 应用配置。

这些命令将完成这些步骤操作︰

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 
 
Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

此示例中那样将 DSC 配置推送到目标节点。
也可以使用 DSC 拉出服务器，如果有的话应用 DSC 配置。

应用 DSC 配置使用 DSC 提取服务器的详细信息，请参阅[DSC 提取客户端设置](pullClient.md)。

## 凭据加密模块示例

下面是一个完整的示例所涉及的所有这些步骤，以及该导出并复制公钥帮助器 cmdlet:

```powershell
# A simple example of using credentials
configuration CredentialEncryptionExample
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $credential
        )
    

    Node $AllNodes.NodeName
    {
        File exampleFile
        {
            SourcePath = "\\server\share\file.txt"
            DestinationPath = "C:\Users\user"
            Credential = $credential
        }
        
        LocalConfigurationManager
        {
            CertificateId = $node.Thumbprint
        }
    }
}

# A Helper to invoke the configuration, with the correct public key 
# To encrypt the configuration credentials
function Start-CredentialEncryptionExample
{
    [CmdletBinding()]
    param ($computerName)


    [string] $thumbprint = Get-EncryptionCertificate -computerName $computerName -Verbose
    Write-Verbose "using cert: $thumbprint"

    $certificatePath = join-path -Path "$env:SystemDrive\$script:publicKeyFolder" -childPath "$computername.EncryptionCertificate.cer"         

    $ConfigData=    @{
        AllNodes = @(     
                        @{  
                            # The name of the node we are describing
                            NodeName = "$computerName"

                            # The path to the .cer file containing the
                            # public key of the Encryption Certificate
                            CertificateFile = "$certificatePath"

                            # The thumbprint of the Encryption Certificate
                            # used to decrypt the credentials
                            Thumbprint = $thumbprint
                        };
                    );    
    }

    Write-Verbose "Generate DSC Configuration..."
    CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample `
        -credential (Get-Credential -UserName "$env:USERDOMAIN\$env:USERNAME" -Message "Enter credentials for configuration") 

    Write-Verbose "Setting up LCM to decrypt credentials..."
    Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 

    Write-Verbose "Starting Configuration..."
    Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose

}


#region HelperFunctions

# The folder name for the exported public keys
$script:publicKeyFolder = "publicKeys"

# Get the certificate that works for encryptions
function Get-EncryptionCertificate
{
    [CmdletBinding()]
    param ($computerName)
    $returnValue= Invoke-Command -ComputerName $computerName -ScriptBlock {
            $certificates = dir Cert:\LocalMachine\my

            $certificates | %{
                    # Verify the certificate is for Encryption and valid
                    if ($_.PrivateKey.KeyExchangeAlgorithm -and $_.Verify())
                    {
                        # Create the folder to hold the exported public key
                        $folder= Join-Path -Path $env:SystemDrive\ -ChildPath $using:publicKeyFolder
                        if (! (Test-Path $folder))
                        {
                            md $folder | Out-Null
                        }

                        # Export the public key to a well known location
                        $certPath = Export-Certificate -Cert $_ -FilePath (Join-Path -path $folder -childPath "EncryptionCertificate.cer") 

                        # Return the thumbprint, and exported certificate path
                        return @($_.Thumbprint,$certPath);
                    }
                  }
        }
    Write-Verbose "Identified and exported cert..."
    # Copy the exported certificate locally
    $destinationPath = join-path -Path "$env:SystemDrive\$script:publicKeyFolder" -childPath "$computername.EncryptionCertificate.cer"
    Copy-Item -Path (join-path -path \\$computername -childPath $returnValue[1].FullName.Replace(":","$"))  $destinationPath | Out-Null

    # Return the thumbprint
    return $returnValue[0]
}

Start-CredentialEncryptionExample
```

