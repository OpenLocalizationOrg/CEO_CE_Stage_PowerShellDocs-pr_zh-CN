---
title: "获取 WMI 对象获取 WmiObject"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: 517b07a9ebca91029381684beaec95d37934f3ce
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 获取 WMI 对象 (获取 WmiObject)

## 获取 WMI 对象 (获取 WmiObject)
Windows 管理工具 (WMI) 是信息的 Windows 系统管理的核心技术，因为它以统一的方式公开广泛。 由于多少 WMI 使可能的 Windows PowerShell cmdlet 访问 WMI 对象，**获取 WmiObject**，是最有用的之一执行操作的实际工时。 我们将讨论如何使用获取 WmiObject 访问 WMI 对象，然后选择如何使用 WMI 对象执行特定操作。

### 列出 WMI 类
大多数 WMI 用户遇到的第一个问题尝试了解可以使用 WMI 做什么。 WMI 类描述可管理的资源。 有数百个 WMI 类，其中一些包含数十个属性。

**获取 WmiObject**通过使 WMI 发现解决此问题。 您可以通过键入本地计算机上获取可用的 WMI 类的列表︰

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

您可以检索相同信息从远程计算机使用计算机名称参数中，指定计算机名称或 IP 地址︰

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

由于特定的计算机运行的操作系统和安装的应用程序通过添加特定 WMI 扩展，返回的远程计算机的类列表可能会有所不同。

> [!NOTE]
> 当使用获取 WmiObject 连接到远程计算机，必须运行远程计算机 WMI，并且默认配置中，在您正在使用的帐户必须在远程计算机上本地 administrators 组。 远程系统不需要安装 Windows PowerShell。 这允许您管理未运行 Windows PowerShell，但具有 WMI 可用的操作系统。

连接到本地系统时，您甚至可以包括计算机名称。 您可以使用本地计算机的名称、 其 IP 地址 （或回送地址 127.0.0.1），或 WMI 样式。 计算机名称。 如果您正在运行 Windows PowerShell 名 Admin01 为 IP 地址 192.168.1.90 的计算机上，以下命令将所有返回 WMI 类该计算机的列表︰

```
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

默认情况下，获取 WmiObject 使用根/cimv2 命名空间。 如果您想要指定其他 WMI 命名空间，使用**Namespace**参数，并指定相应的命名空间路径︰

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### 显示 WMI 类详细信息
如果您已经知道 WMI 类的名称，可用于立即获取信息。 例如，通常用于检索计算机信息 WMI 类之一是**Win32_OperatingSystem**。

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

尽管我们正在显示的所有参数，该命令可以用来表示更简洁的方式。 连接到本地系统时不需要的**计算机名称**参数。 我们将向演示最常见的情况，提醒您有关参数。 **Namespace**默认为根 cimv2，并可以同时省略。 最后，大多数 cmdlet 允许忽略常见参数的名称。 与获取-WmiObject，如果未指定名称的第一个参数的 Windows PowerShell 将其视为**类**参数。 这意味着的最后一个命令可以通过键入发出︰

```
Get-WmiObject Win32_OperatingSystem
```

**Win32_OperatingSystem**类有比下面显示的多个属性。 您可以使用获取成员看到所有属性。 WMI 类的属性是自动可用等其他对象属性︰

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Get-Member -MemberType Property

   TypeName: System.Management.ManagementObject#root\cimv2\Win32_OperatingSyste
m

Name                                      MemberType Definition
----                                      ---------- ----------
__CLASS                                   Property   System.String __CLASS {...
...
BootDevice                                Property   System.String BootDevic...
BuildNumber                               Property   System.String BuildNumb...
...
```

#### 显示使用格式 Cmdlet 的非默认属性
如果您希望默认不显示**Win32_OperatingSystem**类中包含的信息，可以使用**格式**cmdlet 来显示它。 例如，如果您想要显示可用内存的数据，键入︰

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMem FreePhysicalMem FreeVirtualMemo FreeSpaceInPagi
                              ory              ry         ngFiles
--------------- --------------- --------------- --------------- ---------------
        2097024          785904          305808         2056724         1558232
```

> [!NOTE]
> 通配符处理属性名称中**表格格式**，以便最终渠道元素可以减少到**表格格式-属性 TotalV\&#42; 免费\&#42;**

将内存数据可能为列表格式通过键入更易于阅读︰

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```

