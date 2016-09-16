---
title: "对刚好足够管理改进"
contributor: ryanpu
ms.openlocfilehash: 1efe9df882a2b40450ff85dd9dafc2c112c43556
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
## 限制的文件复制到从 JEA 终结点

现在，您可以远程复制到从 JEA 终结点和保证连接的用户不能复制只是您的系统上的*任何*文件的其余部分的文件。
这是通过配置 PSSC 文件装载用户连接用户驱动器。
用户驱动器是新的 PSDrive 是唯一的每个连接的用户，并在会话之间仍然存在。
使用复制项目时将文件复制到或从 JEA 会话，它被约束仅允许用户驱动器的访问。
尝试将文件复制到其他任何 PSDrive 将失败。

若要 JEA 会话配置文件中设置用户驱动器，请使用以下新字段︰
```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

将在创建备份用户驱动器的文件夹 `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`

利用用户驱动器，并将文件复制到/从 JEA 终结点配置为公开用户驱动器，请使用`-ToSession`和`-FromSession`参数复制项目。
```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine. You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

然后，您可以编写自定义的函数处理存储在用户驱动器中的数据，并让这些用户角色功能文件中。

## 支持组托管服务帐户

在某些情况下，用户需要在 JEA 会话中执行的任务可能需要访问到本地计算机之外的资源。
当 JEA 会话配置为使用虚拟帐户时，将显示任何尝试达到此类资源来自本地计算机的标识，而不是虚拟帐户或已连接的用户。
在 TP5，我们已启用支持运行 JEA 的上下文 [组托管服务帐户] (https://technet.microsoft.com/en-us/library/jj128431(v=ws.11\).aspx)，使其更易于使用的域标识访问网络资源。

要配置的 JEA 会话 gMSA 帐户运行，请使用 PSSC 文件中的下面的新项︰
```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> **注意︰**组托管服务帐户不能隔离或限制的范围的虚拟帐户。
> 每个连接的用户将共享相同的 gMSA 标识整个企业可能具有的权限。
> 要选择使用 gMSA，并总是虚拟帐户限定为本地计算机时可能更喜欢使用时非常小心。

## 条件访问策略

在限制在已连接到一个系统来管理，用户可以执行非常 JEA，但如果还希望*时*限制其他人可以使用 JEA？
我们已添加到会话配置文件 (.pssc) 的配置选项以使您可以指定用户必须属于才能建立 JEA 会话的安全组。
如果您有实时 (JIT) 系统在您的环境，并且想要使您访问高权限 JEA 终结点之前提升其权限的用户，则可以十分有用。

PSSC 文件中的新*RequiredGroups*字段允许您指定的逻辑以确定是否用户可以连接到 JEA。
它包含的值，指定的哈希表 （或者嵌套） 使用和和或者键，以构造的规则。
下面是如何利用此字段的一些示例︰
```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## 固定︰ 虚拟帐户现在支持在 Windows Server 2008 R2 上
在 WMF 5.1 中，您就可以在 Windows Server 2008 R2，启用一致配置和功能相似性跨 Windows Server 2008 R2-2016年上使用虚拟帐户。
在 Windows 7 上使用 JEA 时，虚拟帐户将保持不受支持。