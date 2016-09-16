---
title: "网络切换管理器 cmdlet 失败"
contributor: vaibch
ms.openlocfilehash: e32e31762b665a7e2c6f6938fe494cb6127d4264
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
网络切换管理器 cmdlet 可用于通过 WSMAN 管理网络开关。 此模块的几个 cmdlet 都能接受管线中的值。 在 WMF 5.1 预览中，可以接受来自渠道值 cmdlet 无法执行时不通过管道传递的值。

如果不使用"InputObject"参数，cmdlet 应继续执行但不会失败。

下面是列表的受影响的 cmdlet 即这些 cmdlet 可接受从管线"InputObject"参数的值。 如果此值不从管道传递的 cmdlet 执行将失败。

- 禁用 NetworkSwitchEthernetPort
- 启用 NetworkSwitchEthernetPort
- 删除 NetworkSwitchEthernetPortIPAddress
- 设置 NetworkSwitchEthernetPortIPAddress
- 设置 NetworkSwitchPortMode
- 设置 NetworkSwitchPortProperty
- 禁用 NetworkSwitchFeature
- 启用 NetworkSwitchFeature
- 删除 NetworkSwitchVlan
- 设置 NetworkSwitchVlanProperty

### 解决方法
Cmdlet 工作正常时通过管道传递给它 InputObject 参数的值。 适合上述 cmdlet 的几个示例是︰

- 禁用 NetworkSwitchEthernetPort
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Disable-NetworkSwitchEthernetPort -CimSession $cimSession
```
- 启用 NetworkSwitchEthernetPort
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Enable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- 删除 NetworkSwitchEthernetPortIPAddress
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Remove-NetworkSwitchEthernetPortIPAddress -CimSession $cimSession
```

- 设置 NetworkSwitchEthernetPortIPAddress
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$ipAddress = "192.168.10.1"
$subnetAddress = "255.255.255.0"
$port | Set-NetworkSwitchEthernetPortIPAddress -IpAddress $ipAddress -SubnetAddress $subnetAddress -CimSession $cimSession
```

- 设置 NetworkSwitchPortProperty
```powershell
$portProperties = @{Caption = "New Caption"}
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Set-NetworkSwitchPortProperty -Property $portProperties -CimSession $cimSession
```

- 禁用 NetworkSwitchFeature
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Disable-NetworkSwitchFeature -CimSession $cimSession
```

- 启用 NetworkSwitchFeature
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Enable-NetworkSwitchFeature -CimSession $cimSession
```

- 设置 NetworkSwitchVlanProperty
```powershell
$properties = @{Caption = "New Caption"}
$vlan = Get-CimInstance -ClassName CIM_NetworkVlan -Namespace root/interop -CimSession $cimSession | Select-Object -First 1
$vlan | Set-NetworkSwitchVlanProperty -Property $properties -CimSession $cimSession
```
