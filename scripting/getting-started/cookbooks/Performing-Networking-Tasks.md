---
title: "执行网络任务"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: a43cc55f-70c1-45c8-9467-eaad0d57e3b5
ms.openlocfilehash: 5fbe64a5720bf76565452a271dbcb34ffe6563de
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 执行网络任务
由于 TCP/IP 是最常用的网络协议，大多数低级别的网络协议管理任务涉及 TCP/IP。 在此部分中，我们使用 Windows PowerShell 和 WMI 执行这些任务。

### 列出的计算机的 IP 地址
若要在本地计算机上使用获取所有 IP 地址，请使用以下命令︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Format-Table -Property IPAddress
```

此命令的输出与大多数属性的列表，因为值括在括号中︰

<pre>Ip 地址
---------
{192.168.1.80} {192.168.148.1 {192.168.171.1} {0.0.0.0</pre>

若要了解为什么大括号显示，用于获取成员 cmdlet 检查**ip 地址**属性︰

<pre>PS > 获取 WmiObject-类 Win32_NetworkAdapterConfiguration-筛选 IPEnabled = TRUE 计算机名称。 |获取成员的名称 ip 地址 TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapter 配置名称 MemberType 定义...---...ip 地址属性 System.String [] ip 地址 {获取;}</pre>

每个网络适配器的 ip 地址属性是实际数组。 在定义大括号表示**ip 地址**不可**System.String**值，但**System.String**值的数组。

### 列表 IP 配置数据
若要显示的每个网络适配器的详细的 IP 配置数据，请使用以下命令︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName .
```

网络适配器配置对象的默认显示是信息的一组非常缩减的可用。 有关深层次检查和疑难解答，请使用选择对象或格式的 cmdlet，如格式列表中，指定要显示的属性。

如果您不感兴趣 IPX 或 WINS 属性 — 可能现代 TCP/IP 网络中的这种情况，可用于选择对象的 ExcludeProperty 参数隐藏属性与"获胜"开头的名称或"IPX:"

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

此命令返回 DHCP，DNS 路由，有关详细的信息和其他次要 IP 配置属性。

### 执行 ping 命令的计算机
您可以执行简单 ping 针对通过**Win32_PingStatus**计算机使用。 以下命令执行 ping 操作所花，但返回冗长输出︰

```
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

其他有用窗体的地址、 响应时间，和状态代码属性的摘要信息显示生成的以下命令。 表格格式的 Autosize 参数调整表格的列，以便他们在 Windows PowerShell 中正确显示。

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
A status code of 0 indicates a successful ping.
```

您可以使用数组 ping 单个命令的多台计算机。 因为有多个地址，使用**ForEach 对象**单独 ping 每个地址︰

```
"127.0.0.1","localhost","research.microsoft.com" | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

您可以使用相同的命令格式 ping 所有子网，如使用网络号 192.168.1.0 和标准 C 类子网掩码 (255.255.255.0) 专用网络上的计算机。，则只 192.168.1.1 到 192.168.1.254 区域中的地址合法的本地地址 （0 是始终保留网络号和 255 是网广播的地址）。

若要从 1 到 254 Windows PowerShell 中代表数字的数组，使用语句**1..254。** 完成网 ping 可以执行生成数组并，然后在 ping 语句中，添加到部分地址值︰

```
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

注意，可以在其他地方也使用此方法用于生成的地址范围。 您可以生成组完整的地址，这种方式︰

`$ips = 1..254 | ForEach-Object -Process {"192.168.1." + $_}`

### 检索网络适配器属性
在此用户指南前面我们提到，您可以通过使用**Win32_NetworkAdapterConfiguration**检索常规配置属性。 虽然不是严格 TCP/IP 信息，例如 MAC 网络适配器信息地址和适配器类型可以用于了解进展的计算机。 若要获取此信息的摘要，请使用以下命令︰

```
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### 网络适配器分配域
要分配自动名称解析的 DNS 域，请使用**Win32_NetworkAdapterConfiguration SetDNSDomain**方法。 因为独立分配的每个网络适配器配置 DNS 域，您需要使用**ForEach 对象**语句将域分配给每个适配器︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain("fabrikam.com") }
```

筛选语句"IPEnabled = true"是必需的因为使用仅 TCP/IP 的网络，甚至在多个网络适配器配置的计算机上没有 true TCP/IP 适配器;它们是支持 RAS、 PPTP、 QoS，以及所有适配器其他服务的常规软件元素，因此不具有其自己的地址。

您可以使用**位置对象**cmdlet，而不是使用**获取 WmiObject**筛选器筛选命令。

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain("fabrikam.com")}
```

### 执行 DHCP 配置任务
修改 DHCP 详细信息涉及到使用一组的网络适配器，就像 DNS 配置一样。 有几种不同的操作，您可以通过使用 WMI 中，执行，我们将通过的常见的几个步骤。

#### 确定 DHCP 启用适配器
若要查找的计算机上启用 DHCP 的适配器，请使用以下命令︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=true" -ComputerName .
```

若要排除适配器 IP 配置问题，可以检索仅启用 IP 的适配器︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName .
```

#### 检索 DHCP 属性
因为 DHCP 相关适配器属性通常开头"DHCP"，您可以使用表格格式属性参数显示仅这些属性︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=true" -ComputerName . | Format-Table -Property DHCP*
```

#### 每个适配器上启用 DHCP
若要在所有适配器上启用 DHCP，请使用以下命令︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

您可以使用**筛选**语句"IPEnabled = true 和 DHCPEnabled = false"以避免启用的 DHCP 其中已经启用了，但忽略此步骤不会导致错误。

#### 释放和续订 DHCP 租赁特定适配器上
**Win32_NetworkAdapterConfiguration**类具有**ReleaseDHCPLease**和**RenewDHCPLease**方法。 同时使用相同的方式。 一般情况下，使用这些方法，如果您只需要释放或更新特定子网适配器的地址。 在子网的筛选器适配器最简单方法是选择用于该子网关的适配器配置。 例如，以下命令释放在本地计算机上从 192.168.1.254 获取 DHCP 租赁的适配器上的所有 DHCP 租赁︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains "192.168.1.254"} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

更改续订 DHCP 租赁只是使用**RenewDHCPLease**方法，而不是**ReleaseDHCPLease**方法︰

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains "192.168.1.254"} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> 在远程计算机上使用以下方法，请注意，您将无法访问远程系统如果您通过使用已发布或续订租赁适配器连接到该。

#### 释放和续订所有适配器 DHCP 租赁
您可以执行全局 DHCP 地址版本或续订所有适配器使用**ReleaseDHCPLeaseAll**和**RenewDHCPLeaseAll** **Win32_NetworkAdapterConfiguration**方法。 但是，该命令必须应用到 WMI 类，而不是特定适配器，因为释放，并且全局续订租赁类，不是在特定适配器上执行。

您可以通过列出所有 WMI 类，然后按名称中选择所需的类获取 WMI 类，而不是类实例的引用。 例如，以下命令返回 Win32_NetworkAdapterConfiguration 类︰

```
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"}
```

可以将整个命令视为类，然后调用**ReleaseDHCPAdapterLease**方法。 在以下命令，括号括起**获取 WmiObject**和**位置对象**渠道元素直接 Windows PowerShell 首先计算它们︰

```
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"} ).ReleaseDHCPLeaseAll()
```

您可以使用相同的命令格式调用**RenewDHCPLeaseAll**方法︰

```
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"} ).RenewDHCPLeaseAll()
```

### 创建网络共享
若要创建的网络共享，请使用**Win32_Share 创建**方法︰

```
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Win32_Share"}).Create("C:\temp","TempShare",0,25,"test share of the temp folder")
```

您可以通过使用 Windows PowerShell 中的**网络共享**来创建共享:

```
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### 删除的网络共享
您可以删除网络共享与**Win32_Share**，但过程略有不同创建共享，因为您需要检索被删除，而不是**Win32_Share**类的特定共享。 以下语句删除共享"TempShare":

```
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

**净共享**也适用︰

```
PS> net share tempshare /delete
tempshare was deleted successfully.
```

### 连接 Windows 访问网络驱动器
**新建 PSDrive** cmdlet 创建一个 Windows PowerShell 驱动器，但这种方式创建的驱动器仅适用于 Windows PowerShell。 若要创建新的网络的驱动器，您可以使用**WScript.Network** COM 对象。 以下命令地图共享\\\\FPS01\\用户添加到本地驱动器 b:

```
(New-Object -ComObject WScript.Network).MapNetworkDrive("B:", "\\FPS01\users")
```

**净使用**命令也适用︰

```
net use B: \\FPS01\users
```

使用**WScript.Network**或净使用映射驱动器可以立即使用 Windows PowerShell。

