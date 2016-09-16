---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "使用 jea"
ms.technology: powershell
ms.openlocfilehash: 55c8f2d6a8e2bb9f33a3e9af5c3ee94fa5259716
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用 JEA
本节重点介绍了解*使用 JEA*最终用户体验。
在先决条件部分中，您可以创建演示 JEA 终结点。
我们将使用此演示操作中显示 JEA。
以下各节，指南将向后-简介操作并且文件所做的最终用户体验。

## 使用 JEA 作为非管理员
若要显示 JEA 中的操作，您将需要使用远程 PowerShell 处理，就好像是非管理员用户。
在新窗口 PowerShell 中运行以下命令︰   

```PowerShell
$NonAdminCred = Get-Credential
```

非管理员帐户出现提示时输入凭据。
如果您执行[设置设置用户和组](creating-a-domain-controller.md#set-up-users-and-groups)部分中，他们将为︰
-   用户名 ="OperatorUser"
-   密码 ="$$ w0rd pa"

接下来，请运行以下命令以连接到使用所提供的凭据的演示终结点︰

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEA_Demo -Credential $NonAdminCred
```

您现在输入本地计算机上的交互式的远程 PowerShell 会话。
通过使用"凭据"参数，您已连接*，就好像*OperatorUser （或使用哪个帐户）。
在到提示符处更改`[localhost]: PS>`指明您正在对远程会话操作。  

在您远程的命令提示符处，向您显示可用的命令运行以下命令︰

```PowerShell
Get-Command
```

您可以辨别，这是非常有限普通 PowerShell 窗口 （其中可以通常包括多个千命令） 中的可用命令的子集。
具体而言，仅显示 8 默认 JEA 命令 (清除主机，退出-PSSession 获取命令，获取-FormatData 获取的帮助，度量值的对象，传出默认、 选择对象) 和维护角色功能文件中显式包含两个命令。

接下来，通过维护角色功能文件中包含自定义的函数调用下运行看一下用户上下文此会话我们︰

```PowerShell
Get-UserInfo
```

此函数的输出显示"ConnectedUser"以及"RunAsUser"。
连接的用户已连接到远程会话 （例如您的帐户） 的帐户。
连接的用户不需要具有管理员权限。
"运行"帐户是实际执行特权的操作的帐户。
通过连接为一个用户，并运行特权用户，我们将允许非特权用户执行特定管理任务，而不授予他们管理权限。

为了说明此操作，请运行以下命令︰

```PowerShell
Restart-Service -Name Spooler -Verbose
```

通常情况下，请重新启动服务需要管理员权限才能运行。
与 JEA 虚拟帐户，但是，我们可以以运行它使用非特权凭据。

因此，JEA 使您可以使用已使用的命令完成工作。
怎样命令您，但*不*允许使用？
请尝试喜欢 JEA 会话，请在运行其他命令`Restart-Computer`，，请注意，JEA 防止此类命令正在执行。

```PowerShell
[localhost]: PS> Restart-Computer
The term 'Restart-Computer' is not recognized as the name of a cmdlet, function, script file, or
operable program. Check the spelling of the name, or if a path was included, verify that the path
is correct and try again.
    + CategoryInfo          : ObjectNotFound: (Restart-Computer:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

最后，留下的约束的 JEA 终结点，请运行以下命令︰

```PowerShell
Exit-PSSession
```

使用它可断开从远程 PowerShell 会话。

