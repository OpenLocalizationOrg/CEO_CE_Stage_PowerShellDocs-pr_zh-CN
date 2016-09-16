---
title: "使用安装软件"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
ms.openlocfilehash: 437c1242b798ce9892ec29b62bfa3d4ae8b66d48
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用安装软件
设计用于 Windows Installer 应用程序可以访问通过 WMI 的**Win32_Product**类，但并非所有应用程序中使用今天使用 Windows Installer。 由于 Windows Installer 提供用于处理可安装的应用程序的最大范围的标准技术，我们将重点介绍主要这些应用程序。 使用备用安装例程的应用程序通常不会管理 Windows 安装程序。 用于处理这些应用程序的特定技术取决于安装软件和作出的应用程序开发人员。

> [!NOTE]
> 无法使用此处讨论技术管理通过通常将应用程序文件复制到计算机安装的应用程序。 您可以通过使用"使用与文件和文件夹"部分中讨论的技术管理这些应用程序文件和文件夹。

### 列出 Windows Installer 应用程序
若要列出与本地或远程系统上 Windows Installer 安装的应用程序，请使用下面的简单 WMI 查询︰

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

要显示所有 Win32_Product 对象的属性的显示，请使用格式 cmdlet，如格式列表 cmdlet，属性参数值\*（全部）。

```
PS> Get-WmiObject -Class Win32_Product -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Microsoft .NET Framework 2.0"} | Format-List -Property *
Name              : Microsoft .NET Framework 2.0
Version           : 2.0.50727
InstallState      : 5
Caption           : Microsoft .NET Framework 2.0
Description       : Microsoft .NET Framework 2.0
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
InstallDate       : 20060506
InstallDate2      : 20060506000000.000000-000
InstallLocation   :
PackageCache      : C:\WINDOWS\Installer\619ab2.msi
SKUNumber         :
Vendor            : Microsoft Corporation
```

或者，您可以使用**获取 WmiObject 筛选器**参数来选择仅 Microsoft.NET Framework 2.0。 使用此命令中的筛选器 WMI 筛选器，因为它使用 WMI 查询语言 (WQL) 语法，Windows PowerShell 的语法。 相反:

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

请注意 WQL 查询经常使用字符，如空格或等号，Windows PowerShell 中具有特殊的含义。 因此，是明智的筛选器参数的值始终用引号引起来。 您还可以使用 Windows PowerShell 转义字符，引号 (\`)，但它不可能会提高可读性。 以下命令等同于上一个命令和返回相同的结果，但使用引号转义特殊字符，而不是整个筛选器字符串引起来。

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

要列出您感兴趣的属性，请使用格式 cmdlet 的属性参数列出所需的属性。

```
Get-WmiObject -Class Win32_Product -ComputerName . | Format-List -Property Name,InstallDate,InstallLocation,PackageCache,Vendor,Version,IdentifyingNumber
...
Name              : HighMAT Extension to Microsoft Windows XP CD Writing Wizard
InstallDate       : 20051022
InstallLocation   : C:\Program Files\HighMAT CD Writing Wizard\
PackageCache      : C:\WINDOWS\Installer\113b54.msi
Vendor            : Microsoft Corporation
Version           : 1.1.1905.1
IdentifyingNumber : {FCE65C4E-B0E8-4FBD-AD16-EDCBE6CD591F}
...
```

最后，若要查找已安装的应用程序，简单的**格式范围**的名称语句简化了输出:

```
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

尽管我们现在有几种方式查看 Windows Installer 用于安装的应用程序，但我们不考虑其他应用程序。 最常用的应用程序与 Windows 中注册其卸载，因为我们可以处理这些本地通过 Windows 注册表中对它们进行查找。

### 列出所有卸载应用程序
虽然无法保证的系统上查找所有应用程序，就可以用列表显示在添加或删除程序对话框中找到所有程序。 添加或删除程序在以下注册表项中查找这些应用程序︰

**HKEY_LOCAL_MACHINE\\软件\\Microsoft\\Windows\\CurrentVersion\\卸载**。

我们也可以检查此键以查找应用程序。 若要使其更易于查看卸载密钥，我们可以 Windows PowerShell 驱动器映射到此注册表位置︰

```
PS>    

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> **HKLM:**驱动器映射到的根中**HKEY_LOCAL_MACHINE**，这样我们在卸载项的路径中使用的驱动器。 而不是**HKLM:**我们无法使用**HKLM**或**HKEY_LOCAL_MACHINE**指定了注册表路径。 使用现有注册表驱动器的优点是，我们可以使用选项卡上完成填写键名称，因此我们不需要键入它们。

现在，我们有一个名为"卸载"，可用于快速方便地查找应用程序安装驱动器。 我们可以通过注册表项中卸载的数目来查找安装的应用程序的数目︰ Windows PowerShell 驱动器︰

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

我们可以使用多种技术，搜索此列表中的更多应用程序以**获取 ChildItem**开头。 获取应用程序的列表，并将它们保存在**$UninstallableApplications**变量，请使用以下命令︰

```
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> 我们正在使用的漫长变量名称下面清晰度。 在实际使用，没有理由使用长名称。 尽管您可以使用选项卡上完成变量名，您还可以使用速度 1-2 字符名称。 开发供重复使用代码时，较长的描述性名称是最有用。

若要显示在注册表项中，在卸载下的注册表项的值，使用注册表项 GetValue 方法。 方法的值是注册表项的名称。

例如，若要卸载项中查找应用程序的显示名称，请使用以下命令︰

```
PS> Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("DisplayName") }
```

存在不保证这些值是唯一。 在下面的示例中，两个已安装的项目显示为"Windows Media 编码器 9 系列":

```
PS> Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion\Uninstall

SKC  VC Name                           Property
---  -- ----                           --------
  0   3 Windows Media Encoder 9        {DisplayName, DisplayIcon, UninstallS...
  0  24 {E38C00D0-A68B-4318-A8A6-F7... {AuthorizedCDFPrefix, Comments, Conta...
```

### 安装应用程序
您可以使用**Win32_Product**类远程或本地安装 Windows Installer 程序包。

> [!NOTE]
> 在 Windows Vista、 Windows Server 2008 和更高版本的 Windows，才能安装应用程序，您必须启动 Windows PowerShell"以管理员身份运行"选项。

远程安装，请使用通用命名约定 (UNC) 网络路径以指定的路径的.msi 包，因为 WMI 子系统不理解 Windows PowerShell 路径。 例如，若要安装 NewPackage.msi 包位于网络共享\\\\AppServ\\PC01，远程计算机上的 dsp Windows PowerShell 提示符处键入以下命令︰

```
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq "Win32_Product"}).Install(\\AppSrv\dsp\NewPackage.msi)
```

不使用 Windows 安装程序技术的应用程序可能有特定于应用程序可用于方法自动部署。 若要确定是否部署自动化的方法，请检查应用程序的文档，或查阅应用程序供应商支持系统。 在某些情况下，即使应用程序供应商不专门设计的应用程序的安装自动化 installer 软件制造商可能具有自动化的一些技巧。

### 删除应用程序
使用 Windows PowerShell 删除 Windows Installer 程序包的工作方式与安装包大约相同。 下面是一个示例，选择要卸载的包基于其名称。在某些情况下可能能够更轻松地筛选器与**IdentifyingNumber**:

```
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

删除其他应用程序不非常简单，即使是本地完成。 我们可以通过提取**UninstallString**属性来找到这些应用程序命令行卸载字符串。 此方法适用于 Windows Installer 应用程序和卸载项下显示的较旧程序︰

```
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

您可以通过显示名称中，如果您愿意筛选输出︰

```
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -like "Win*"} | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

但是，这些字符串可能无法直接使用 Windows PowerShell 提示符下不使用一些修改。

### 升级 Windows Installer 应用程序
升级应用程序，您需要知道到应用程序升级包的应用程序和路径的名称。 使用该信息，您可以升级应用程序使用单个 Windows PowerShell 命令︰

```
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```

