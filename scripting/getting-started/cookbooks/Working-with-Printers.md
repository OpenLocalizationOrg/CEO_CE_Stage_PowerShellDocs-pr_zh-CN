---
title: "使用的打印机"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: 2142d7ef1d1cc9b20ecc1ab35b9685817c838347
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用的打印机
您可以使用 Windows PowerShell 管理打印机使用 WMI 和从 WSH WScript.Network COM 对象。 我们将使用这两个工具的混合演示特定的任务。

### 列出打印机连接
列表的计算机上安装的打印机的最简单方法是使用 WMI **Win32_Printer**类︰

```
Get-WmiObject -Class Win32_Printer -ComputerName
```

您也可以通过使用**WSH 脚本通常用于 COM 实例**列出打印机︰

```
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

此命令返回端口名称和不带任何区分标签的打印机设备名称的一个简单字符串集合，因为不容易解释。

### 添加网络打印机
若要添加新的网络打印机，请使用**WScript.Network**:

```
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### 设置默认打印机
若要使用 WMI 设置默认打印机， **Win32_Printer**集合中查找打印机，然后调用**SetDefaultPrinter**方法︰

```
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network**是略更简单易用，，因为它都具有所需的打印机名称将作为参数**SetDefaultPrinter**方法︰

```
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### 删除打印机连接
若要删除的打印机连接，请使用**WScript.Network RemovePrinterConnection**方法︰

```
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```

