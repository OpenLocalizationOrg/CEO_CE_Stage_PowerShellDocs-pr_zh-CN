---
title: WinRMSecurityRedirect
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
redirect_url: https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity
ms.openlocfilehash: cacf45175dff2b12b332d62d0580469f9eadc747
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# PowerShell 远程安全注意事项

远程 PowerShell 处理是管理 Windows 系统的推荐的方式。 默认情况下，在 Windows Server 2012 R2 中启用了 PowerShell 远程处理。 使用远程 PowerShell 处理时，此文档介绍安全问题、 建议和最佳做法。

## 什么是远程 PowerShell 处理？

PowerShell 远程处理使用[Windows 远程管理 (WinRM)](https://msdn.microsoft.com/en-us/library/windows/desktop/aa384426.aspx)，这是 Microsoft 实施工作结束后的[Web 服务管理 (WS Managment) 的](http://www.dmtf.org/sites/default/files/standards/documents/DSP0226_1.2.0.pdf)协议，若要允许用户在远程计算机上运行的 PowerShell 命令。 您可以找到有关使用远程 PowerShell[运行远程命令](https://technet.microsoft.com/en-us/library/dd819505.aspx)的详细信息。

远程 PowerShell 处理不是使用 cmdlet 的参数的**计算机名称**以运行它在远程计算机上，它作为其基础协议使用远程过程调用 (RPC) 相同。

##  远程 PowerShell 处理默认设置

远程 PowerShell 处理 （和 WinRM） 侦听以下端口︰

- HTTP: 5985
- HTTPS: 5986

默认情况下，远程 PowerShell 处理只允许连接从管理员组的成员。 会话被启动用户的上下文，以便所有操作系统访问控件都应用于单个用户和组继续为其通过 PowerShell 远程连接时应用。

专用网络中，在远程 PowerShell 处理的默认 Windows 防火墙规则接受所有连接。 在公共网络中，默认 Windows 防火墙规则允许仅从相同子网内的远程 PowerShell 连接。 您必须明确地更改该规则，以打开公共网络上的所有连接到远程 PowerShell 处理。

>**警告︰**公共网络的防火墙规则是为了保护计算机免受潜在恶意外部连接。 删除此规则时，请务必小心。

## 进程隔离

PowerShell 远程计算机之间的通信使用[Windows 远程管理 (WinRM)](https://msdn.microsoft.com/en-us/library/windows/desktop/aa384426) 。 WinRM 作为网络服务帐户的服务运行和生成独立的进程到主机 PowerShell 实例运行为用户帐户。 为一个用户运行 PowerShell 的实例，其中不具有访问权限与另一个用户运行的 PowerShell 实例的进程。

## 远程 PowerShell 处理所生成的事件日志

FireEye 提供了良好的事件日志和生成的远程 PowerShell 会话，可在其他安全证据摘要  
[调查 PowerShell 攻击](https://www.fireeye.com/content/dam/fireeye-www/global/en/solutions/pdfs/wp-lazanciyan-investigating-powershell-attacks.pdf)。

## 加密和传输协议

很有帮助的远程 PowerShell 连接从两个方面的安全性，请考虑︰ 初始身份验证和正在进行的通信。 

使用传输协议 （HTTP 或 HTTPS），无论远程 PowerShell 处理始终使用每个会话 AES 256 对称密钥加密初始身份验证之后的所有通信。
    
### 初始身份验证

身份验证确认客户端到服务器-和理想情况下-客户端到服务器的身份。
    
当客户端连接到域服务器使用其计算机名称 (例如︰ server01，或 server01.contoso.com)，默认身份验证协议是[Kerberos](https://msdn.microsoft.com/en-us/library/windows/desktop/aa378747.aspx)。
Kerberos 保证而不发送任何种类的可重用的凭据的用户身份和服务器身份。

当客户端连接到域服务器使用其 IP 地址，或与工作组服务器连接时，不能 Kerberos 身份验证。 在这种情况下，远程 PowerShell 处理依赖于[NTLM 身份验证协议](https://msdn.microsoft.com/en-us/library/windows/desktop/aa378749.aspx)。 NTLM 身份验证协议保证用户标识，而不发送委派凭据任何排序。 以证明用户标识，NTLM 协议要求，客户端和服务器计算会话密钥从用户的密码不以往交换本身的密码。 服务器通常不知道用户的密码，以便它与的知道用户密码和计算服务器的会话密钥的域控制器进行通信。 
      
NTLM 协议不，但是，保证服务器标识。 与使用 NTLM 进行身份验证的所有协议，加入域的计算机的计算机帐户访问攻击可以调用来计算 NTLM 会话密钥，从而模拟服务器的域控制器。

基于 NTLM 的身份验证默认情况下，处于禁用状态，但可能允许使用任一配置 SSL 在目标服务器上，或通过配置 WinRM TrustedHosts 设置。
    
#### 使用 SSL 证书期间基于 NTLM 连接验证服务器标识

由于 NTLM 身份验证协议无法确保的目标服务器 （仅限已知道您的密码） 的标识，您可以配置目标服务器 SSL 用于远程 PowerShell 处理。 将 SSL 证书分配到目标服务器 （如果客户端还信任的证书颁发机构颁发） 允许基于 NTLM 的身份验证确保用户标识和服务器身份。
    
#### 忽略 NTLM 基于服务器的标识错误
      
如果部署到 NTLM 连接的服务器的 SSL 证书是不可行的您可以通过向 WinRM **TrustedHosts**列表中添加服务器禁用生成的标识错误。 请注意，TrustedHosts 列表中添加服务器名称不应该为任何窗体的托管自己的可信度语句的-NTLM 身份验证协议不能保证您实际上连接到主机根据您要连接到。
相反，应考虑的 TrustedHosts 设置为您想要取消正在无法验证服务器的标识生成错误的主机的列表。
    
    
### 正在进行的通信

初始身份验证完成后， [PowerShell 远程处理协议](https://msdn.microsoft.com/en-us/library/dd357801.aspx)对每个会话 AES 256 对称密钥加密所有正在进行的通信。  


## 使第二个跃点

默认情况下，PowerShell 远程处理使用 Kerberos （如果可用） 或 NTLM 身份验证。 这两种协议进行身份验证到远程计算机而不向其发送凭据。
这是最安全的方式进行身份验证，但在远程计算机没有用户凭据，因为它无法访问其他计算机和服务的用户代表。 这称为"双跃点"问题。

有多种方法来避免此问题︰

### Kerberos 约束委派

对于高度受信任的服务器，您可以启用[Kerberos 约束委派](https://technet.microsoft.com/en-us/library/cc995228.aspx)。 这使得远程服务器模拟到指定的计算机和服务列表经过身份验证的用户。

### 信任远程计算机之间

如果您信任用户对*Server2*资源*服务器 1*到远程连接，您可以显式授权*服务器 1*访问这些资源。

### 访问远程资源时使用显式凭据

通过使用 cmdlet 的参数的**凭据**，显式可以将您的凭据传递给远程资源。 例如︰

```powershell
$myCredential = Get-Credential
New-PSDrive -Name Tools \\Server2\Shared\Tools -Credential $myCredential 
```

### CredSSP

您可以使用[凭据安全支持提供程序 (CredSSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb931352.aspx)进行身份验证 (通过指定为值的"CredSSP"`Authentication`呼叫转接至[新建 PSSession](https://technet.microsoft.com/en-us/library/hh849717.aspx) cmdlet 的参数。 CredSSP 传递凭据以纯文本到服务器，以便使用它将打开向上凭据盗用攻击。 如果远程计算机被泄露，攻击者将有权访问该用户的凭据。 默认情况下，客户端和服务器计算机上禁用 CredSSP。 仅在最受信任的环境中，您应启用 CredSSP。 例如，域管理员连接到的域控制器，因为高度受信任的域控制器。

有关使用远程 PowerShell 处理 CredSSP 时的安全问题的详细信息，请参阅[意外破坏︰ 应注意上文中所的 CredSSP](http://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp)。

有关凭据盗用攻击的详细信息，请参阅[Mitigating 传递--哈希 (PtH) 的攻击和其他凭据盗窃](https://www.microsoft.com/en-us/download/details.aspx?id=36036)。








