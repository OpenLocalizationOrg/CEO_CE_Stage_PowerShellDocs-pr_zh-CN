---
title: "管理服务"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: 33cab67b4d6bb301a23125b1ac6713328277aefe
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 管理服务
有八个核心服务 cmdlet，用于广泛的服务任务。 我们将探讨仅在列表，以及更改运行服务的状态，但您可以通过使用获取的列表服务 cmdlet**获取帮助\&#42;-服务**，并且您可以通过使用**获取帮助 < Cmdlet 名称 >**，如**获取帮助新建服务**查找有关每个服务 cmdlet 的信息。

## 获取服务
通过使用**获取服务**cmdlet，您可以在本地或远程计算机上获取本服务。 **获取流程**，与使用不带参数**获取服务**命令返回的所有服务。 您可以筛选按名称，甚至作为通配符使用星号︰

```
PS> Get-Service -Name se*
Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

由于它不是始终明显服务的实际名称，您可能会发现您需要查找服务按显示名称。 使用通配符，或者使用的显示名称的列表，您可以按特定的名称，执行此操作︰

```
PS> Get-Service -DisplayName se*
Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Running  SamSs              Security Accounts Manager
Running  seclogon           Secondary Logon
Stopped  ServiceLayer       ServiceLayer
Running  wscsvc             Security Center
PS> Get-Service -DisplayName ServiceLayer,Server
Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Stopped  ServiceLayer       ServiceLayer
```

获取服务 cmdlet 的参数的计算机名称可用于在远程计算机上获取服务。 计算机名称参数接受多个值和通配符，以便您可以使用单个命令的多台计算机上获取服务。 例如，以下命令获取 Server01 远程计算机上的服务。

```
Get-Service -ComputerName Server01
```

## 获取所需和依赖服务
获取服务 cmdlet 有服务管理中非常有用的两个参数。 DependentServices 参数获取取决于该服务的服务。 RequiredServices 参数都可以依赖的服务。

这些参数只显示 DependentServices 和 ServicesDependedOn 的值 （别名 = RequiredServices） 获取服务返回，但它们简化 System.ServiceProcess.ServiceController 对象的属性命令，并使获取此信息变得更加简单。

以下命令获取 LanmanWorkstation 服务所需的服务。

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices
Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

以下命令获取需要 LanmanWorkstation 服务的服务。

```
PS> Get-Service -Name LanmanWorkstation -DependentServices
Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

您甚至可以获得有相关性的所有服务。 以下命令并只是的然后它使用表格格式 cmdlet 显示计算机上的服务的状态、 名称、 RequiredServices 和 DependentServices 属性。

```
Get-Service -Name * | where {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## 停止、 启动、 挂起，并重新启动服务
所有服务 cmdlet 具有相同的常规格式。 服务可以通过公用名或显示名称来指定，并采取列表和通配符作为值。 若要停止打印后台处理程序，请使用︰

```
Stop-Service -Name spooler
```

若要停止后开始打印后台处理程序，请使用︰

```
Start-Service -Name spooler
```

若要暂停打印后台处理程序，请使用︰

```
Suspend-Service -Name spooler
```

**重新启动服务**cmdlet 合作的其他服务 cmdlet 的方式相同，但我们将为其显示一些更复杂示例。 最简单的用法，在您指定的服务名称︰

```
PS> Restart-Service -Name spooler
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

您将看到您获得有关打印后台处理程序的重复的警告消息启动。 执行需要花费一些时间服务操作时，Windows PowerShell 将通知您，它仍要执行的任务。

如果您想要重新启动多个服务，您可以获得的服务列表，筛选它们，，然后执行重新启动︰

```
PS> Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
Restart-Service : Cannot stop service 'Logical Disk Manager (dmserver)' because
 it has dependent services. It can only be stopped if the Force flag is set.
At line:1 char:57
+ Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service <<<<
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
```

这些服务 cmdlet 不具有计算机名称参数，但是您可以通过使用调用命令 cmdlet 将它们运行远程计算机上。 例如，以下命令将重新启动 Server01 远程计算机上的后台处理程序服务。

```
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## 设置服务属性
设置服务 cmdlet 更改本地或远程计算机上的服务的属性。 因为服务状态是一个属性，您可以使用此 cmdlet 启动、 停止和暂停服务。 设置服务 cmdlet 也具有允许您更改服务启动类型 StartupType 参数。

若要在 Windows Vista 和更高版本的 Windows 上使用设置服务，请使用"以管理员身份运行"选项打开 Windows PowerShell。

有关详细信息，请参阅[设置服务 [m2]](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)

## 另请参阅
[获取服务 [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)
[设置服务 [m2]](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)
[请重新启动服务 [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)
[暂停服务 [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)

