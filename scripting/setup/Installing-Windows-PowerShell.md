---
title: "安装 Windows PowerShell"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6fbb0409-5a54-48ec-95e6-7f8b7d8c4969
ms.openlocfilehash: 7d9877e415238d96342f1986d55a5cf169b6e14e
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 安装 Windows PowerShell
Windows® 8 和 Windows Server® 2012年包括 Windows PowerShell 3.0 和所有其先决条件。 系统还包括与主机程序不能使用 Windows PowerShell 3.0 向后兼容的 Windows PowerShell 2.0 引擎。

本主题介绍如何安装 Windows PowerShell 3.0 早期系统上安装和启用所需的功能。

本主题包括以下部分︰

-   [在 Windows 8 和 Windows Server 2012 中安装 Windows PowerShell](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows8andWindowsServer2012)

-   [在 Windows 7 和 Windows Server 2008 R2 上安装 Windows PowerShell](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows7andWindowsServer2008R2)

-   [在 Windows Server 2008 上安装 Windows PowerShell](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindowsServer2008LH)

-   [核心服务器上安装 Windows PowerShell](Installing-Windows-PowerShell.md#BKMK_InstallingOnServerCore)

-   [部署 Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/639d0eff-98a3-4124-b52c-26921ebd98b0)

-   [安装 Windows PowerShell 2.0 引擎](Installing-the-Windows-PowerShell-2.0-Engine.md)

## <a name="BKMK_InstallingOnWindows8andWindowsServer2012"></a>在 Windows 8 和 Windows Server 2012 中安装 Windows PowerShell
Windows PowerShell 3.0 到达安装、 配置和准备好使用。 Windows PowerShell 集成脚本环境 (ISE) 已安装并启用。 关于启动 Windows PowerShell 的信息，请参阅[在 Windows 8 上启动 Windows PowerShell](https://technet.microsoft.com/en-us/library/d7be1668-8617-4890-ad90-dd9765fbd2c3)和[Windows Server 2012 年启动 Windows PowerShell](https://technet.microsoft.com/library/hh831491.aspx#BKMK_powershell)。

## <a name="BKMK_InstallingOnWindows7andWindowsServer2008R2"></a>在 Windows 7 和 Windows Server 2008 R2 上安装 Windows PowerShell
这些说明介绍了如何使用 Service Pack 1 和 Windows Server 2008 R2 Service Pack 1 与运行 Windows 7 的计算机上安装 Windows PowerShell 3.0。 有运行 Windows Server 2008 R2 服务器核心安装选项与计算机下方单独安装说明。

#### 准备好安装

-   安装 Windows Management Framework 3.0 之前, 卸载任何早期版本的 Windows Management Framework 3.0。

#### 安装 Windows PowerShell 3.0

1.  从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547)在安装 Microsoft.NET Framework 4 (dotNetFx40_Full_setup.exe) 完全安装。

    或者，从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919)在安装 Microsoft.NET Framework 4.5 (dotNetFx45_Full_setup.exe)。

2.  从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290)在安装 Windows Management Framework 3.0。

关于启动 Windows PowerShell 3.0 的信息，请参阅[在早期版本的 Windows 上启动 Windows PowerShell](Starting-Windows-PowerShell-on-Earlier-Versions-of-Windows.md)。

## <a name="BKMK_InstallingOnServerCore"></a>核心服务器上安装 Windows PowerShell
这些说明解释如何 Service Pack 1 与运行 Windows Server 2008 R2 服务器核心安装选项的计算机上安装 Windows PowerShell 3.0。

过程中的第一个步骤使用部署映像服务和管理 (DISM) 命令服务器核心和 Windows PowerShell 2.0 安装 Microsoft.NET Framework 2.0。 这些程序是 Windows Management Framework 3.0，后续步骤中安装的先决条件。

#### 准备好安装

-   安装 Windows Management Framework 3.0 之前, 卸载任何早期版本的 Windows Management Framework 3.0。

#### 安装 Windows PowerShell 3.0

1.  启动 Cmd.exe

2.  运行以下 DISM 命令。 这些命令安装.NET Framework 2.0 和 Windows PowerShell 2.0。

    ```
    dism /online /enable-feature:NetFx2-ServerCore
    dism /online /enable-feature:MicrosoftWindowsPowerShell
    dism /online /enable-feature:NetFx2-ServerCore-WOW64
    ```

3.  从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=248450](http://go.microsoft.com/fwlink/?LinkID=248450)在安装 Microsoft.NET Framework 4.0 完整服务器核心安装。

4.  从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290)在安装 Windows Management Framework 3.0。

## <a name="BKMK_InstallingOnWindowsServer2008LH"></a>在 Windows Server 2008 上安装 Windows PowerShell
这些说明介绍了如何在运行 Windows Server 2008 Service Pack 2 的计算机上安装 Windows PowerShell 3.0。

在 Windows Server 2008 系统 Windows Management Framework （Windows PowerShell 2.0、 KB 968930） 是 Windows Management Framework 3.0 的先决条件。 "扩展保护的身份验证"功能保护计算机免受转接攻击的身份验证，并允许您创建远程会话时使用的**UseSSL**参数。 若要安装 Windows PowerShell 3.0 和 Windows PowerShell 2.0 引擎，请使用以下过程。

#### 准备好安装

-   安装 Windows Management Framework 3.0 之前, 卸载任何早期版本的 Windows Management Framework 3.0。

#### 安装 Windows PowerShell 3.0

1.  安装 Service Pack 1 从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=242910](http://go.microsoft.com/fwlink/?LinkID=242910)在使用 Microsoft.NET Framework 3.5。

2.  从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkId=243035](http://go.microsoft.com/fwlink/?LinkId=243035)在安装 Windows Management Framework （Windows PowerShell 2.0、 KB 968930）。

3.  从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547)以安装完整安装 Microsoft.NET Framework 4 (dotNetFx40_Full_setup.exe)。

    或者，从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919)在安装 Microsoft.NET Framework 4.5 (dotNetFx45_Full_setup.exe)。

4.  安装"扩展身份验证的保护"(KB 968389) 从[http://go.microsoft.com/fwlink/?LinkID=186398](http://go.microsoft.com/fwlink/?LinkID=186398)。

5.  从 Microsoft 下载中心[http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290)在安装 Windows Management Framework 3.0。

## 另请参阅
[Windows PowerShell 系统要求](Windows-PowerShell-System-Requirements.md)
[启动 Windows PowerShell [ps]](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
