---
title: "安装和配置 WMF 5.1 （预览）"
ms.date: 2016-05-16
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
contributor: kriscv
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 26a325dc7a18ba167ddc56ca226fce3eded79f52
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 安装和配置 WMF 5.1 （预览） #

## 安装.Net 46
您必须安装.NET Framework 46，使用 WMF 5.1。 这是启用需要新的目录签名功能，这将影响模块和脚本 WMF 5.1 中加载的多个区域。 

[.NET Framework 46 不能作为 KB 3045560](https://support.microsoft.com/en-us/kb/3045560)。 下载位置可用的安装说明。

> **注意︰**这是一个已知的问题的.NET 46 要求未检测到 WMF 5.1 预览安装程序，以便您能够在安装.NET 46 之前安装 WMF 5.1 预览。 我们测试表明您可以在安装 WMF 5.1 预览版之后安装.NET 46。 WMF 5.1 的最终版本将正确地检查之前安装此必备要求。 

## 下载并安装 WMF 5.1 预览

下载 WMF 5.1 包，您希望在电脑上安装的操作系统和体系结构︰

| 操作系统       | 先决条件 | 包链接             |
|------------------------|---------------|---------------------------|
| Windows Server 2012 R2 | [.NET framework 46](https://support.microsoft.com/en-us/kb/3045560) | [Win8.1AndW2K12R2-KB3156422 x64.msu](http://go.microsoft.com/fwlink/?LinkID=823586)|
| Windows 2012 Server    | [.NET framework 46](https://support.microsoft.com/en-us/kb/3045560) | [W2K12-KB3156423 x64.msu](http://go.microsoft.com/fwlink/?LinkID=823587)|
| Windows Server 2008 R2 | [.NET framework 46](https://support.microsoft.com/en-us/kb/3045560) </br> [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) </br> 安全更新[sha-2 代码签名](https://technet.microsoft.com/en-us/library/security/3033929) | [Win7AndW2K8R2-KB3156424 x64.msu](http://go.microsoft.com/fwlink/?LinkID=823588) |
| Windows 8.1            | [.NET framework 46](https://support.microsoft.com/en-us/kb/3045560) | **x64:**[Win8.1AndW2K12R2-KB3156422 x64.msu](http://go.microsoft.com/fwlink/?LinkID=823586) </br> **x86:**[Win8.1-KB3156422 x86.msu](http://go.microsoft.com/fwlink/?LinkID=823589) |
| Windows 7 SP1          | [.NET framework 46](https://support.microsoft.com/en-us/kb/3045560) </br> [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) </br> 安全更新[sha-2 代码签名](https://technet.microsoft.com/en-us/library/security/3033929) | **x64:**[Win7AndW2K8R2-KB3156424 x64.msu](http://go.microsoft.com/fwlink/?LinkID=823588) </br> **x86:**[Win7-KB3156424 x86.msu](http://go.microsoft.com/fwlink/?LinkID=823590) |


## 从 Windows 资源管理器 （或 Windows Server 2012 R2 或 Windows 8.1 中的文件资源管理器） 安装 WMF 5.1

1. 导航到 MSU 文件下载到其中的文件夹。

2. 双击以运行它 MSU。

## 从命令提示符安装 WMF 5.1##

1. 下载后正确包，您的计算机体系结构，使用提升的用户权限 （以管理员身份运行） 打开命令提示符窗口。 Windows Server 2012 R2、 Windows Server 2012，或 Windows Server 2008 R2 SP1 的服务器核心安装选项，在命令提示符默认情况下打开提升的用户权限。

2. 更改目录的文件夹，其中有下载或复制 WMF 5.1 安装程序包。

3. 运行以下命令之一︰
    - 在计算机上运行的 Windows Server 2012 R2 或 Windows 8.1 x64，运行`Win8.1AndW2K12R2-KB3156422-x64.msu /quiet`。
    - 在计算机上运行的 Windows Server 2012，运行`W2K12-KB3156423-x64.msu /quiet`。
    - 在计算机上运行的 Windows Server 2008 R2 SP1 或 Windows 7 SP1 x64，运行`Win7AndW2K8R2-KB3156424-x64.msu /quiet`。
    - 在计算机上运行的 Windows 8.1 x86，运行`Win8.1-KB3156422-x86.msu /quiet`。
    - 在计算机上运行的 Windows 7 SP1 x86，运行`Win7-KB3156424-x86.msu /quiet`。

## Windows Server 2008 SP1 和 Windows 7 SP1 的其他安装说明##
在 Windows Server 2008 SP1 或 Windows 7 SP1，WMF 5.1 安装需要安装︰
- 新的 service pack。
- [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855)
- WMF 5.1 需要使用[Microsoft.NET Framework 46](https://support.microsoft.com/en-us/kb/3045560)。 您可以安装 Microsoft.NET Framework 46 下载位置的说明进行操作。
- [Sha-2 代码签名](https://technet.microsoft.com/en-us/library/security/3033929)的安全更新。 需要新的 PowerShell cmdlet 用于 Windows 目录文件。 

> **WinRM 相关性**的 Windows PowerShell 需要状态配置 (DSC) 取决于 WinRM。 默认情况下，在 Windows Server 2008 R2 和 Windows 7 中，不会启用 WinRM。 运行`Set-WSManQuickConfig`，提升 Windows PowerShell 会话，以启用 WinRM。

