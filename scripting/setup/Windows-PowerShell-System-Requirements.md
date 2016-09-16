---
title: "Windows PowerShell 系统要求"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6d1d3c75-3be4-4fc9-8805-ca9b2c454d42
ms.openlocfilehash: 91713114c3190e521bcbb55a62337b0755150996
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Windows PowerShell 系统要求
本主题列出了用于 Windows PowerShell 3.0 和 Windows PowerShell 4.0，以及特殊功能，如 Windows PowerShell 集成脚本环境 (ISE)、 CIM 命令和工作流的系统要求。

Windows® 8.1 和 Windows Server® 2012 R2 包括所有必需的程序。 本主题适用于 Windows 的早期版本的用户。

## 操作系统要求
在以下版本的 Windows 上运行的 Windows PowerShell 4.0。

-   Windows 8.1 中，默认情况下安装

-   Windows Server 2012 R2，默认情况下安装

-   Windows® 7 Service Pack 1，安装[Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkId=293881)运行 Windows PowerShell 4.0

-   Windows Server® 2008 R2 Service Pack 1，安装[Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkId=293881)运行 Windows PowerShell 4.0

在以下版本的 Windows 上运行的 Windows PowerShell 3.0。

-   Windows 8 中，默认情况下安装

-   Windows Server 2012，默认情况下安装

-   Windows® 7 Service Pack 1，安装[Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595)运行 Windows PowerShell 3.0

-   Windows Server® 2008 R2 Service Pack 1，安装[Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595)运行 Windows PowerShell 3.0

-   Windows Server 2008 Service Pack 2，安装[Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595)运行 Windows PowerShell 3.0

## Microsoft.NET Framework 要求
Windows PowerShell 4.0 需要使用 Microsoft.NET Framework 4.5 完全安装。 Windows 8.1 和 Windows Server 2012 R2 中包含默认 Microsoft.NET Framework 4.5。

Windows PowerShell 3.0 需要完全安装 Microsoft.NET framework 4。 Windows 8 和 Windows Server 2012 中包含 Microsoft.NET Framework 4.5 默认情况下，可以满足此要求。

若要安装 Microsoft.NET Framework 4.5 (dotNetFx45_Full_setup.exe)，请参阅 Microsoft 下载中心[Microsoft.NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkID=242919) 。

若要安装 Microsoft.NET Framework 4 (dotNetFx40_Full_setup.exe) 完全安装，请参阅 Microsoft 下载中心[Microsoft.NET Framework 4 （Web 安装程序）](http://go.microsoft.com/fwlink/?LinkID=212931) 。

## Ws-management 3.0
Windows PowerShell 3.0 和 Windows PowerShell 4.0 需要使用 Ws-management 3.0，支持 WinRM 服务和 WSMan 协议。 在 Windows 8.1、 Windows Server 2012 R2、 Windows 8、 Windows Server 2012、 Windows Management Framework 4.0 和 Windows Management Framework 3.0 包含此程序。

## Windows 管理规范 3.0
Windows PowerShell 3.0 和 Windows PowerShell 4.0 需要使用 Windows 管理工具 3.0 (WMI)。 在 Windows 8.1、 Windows Server 2012 R2、 Windows 8、 Windows Server 2012、 Windows Management Framework 4.0 和 Windows Management Framework 3.0 包含此程序。 如果未在计算机上安装该程序，需要 WMI，如 CIM 命令功能未运行。

## 公共语言运行时 4.0
Windows PowerShell 3.0 和 Windows PowerShell 4.0 编译针对公共语言运行时 (CLR) 4.0。

## 图形用户界面要求
Windows PowerShell 是一个基于控制台的应用程序不需要图形用户界面。 因此，它也适用于不具有屏幕或监视器或用户界面，如的 Windows Server 2012 R2 或 Windows Server 2012 服务器核心安装选项的计算机。

但是，某些项目，如以下，需要图形用户界面。 有关详细信息，请参阅帮助主题的每个项目。

-   Windows PowerShell 集成脚本环境 (ISE)

-   Cmdlet

    1.  [出 GridView](https://technet.microsoft.com/en-us/library/70915a86-d753-464e-8349-cba02316154c)

    2.  [显示命令](https://technet.microsoft.com/en-us/library/65bba50b-91a8-49d5-80a2-a30fc684ba41)

    3.  [显示 ControlPanelItem](https://technet.microsoft.com/en-us/library/0685d42c-37cc-498f-acf6-0ecfeb0cb162)

    4.  [显示事件日志](https://technet.microsoft.com/en-us/library/a3b0f5ad-0438-42c7-915b-d1b4793a431c)

-   参数

    1.  [获取帮助](https://technet.microsoft.com/en-us/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a)cmdlet **ShowWindow**参数。

    2.  **ShowSecurityDescriptorUI**的[Register PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea)和[设置 PSSessionConfiguration](https://technet.microsoft.com/en-us/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) cmdlet 的参数。

## Windows PowerShell 引擎要求
Windows PowerShell 4.0 旨在与 Windows PowerShell 3.0 和 Windows PowerShell 2.0 向后兼容。 Cmdlet、 提供商、 单元、 模块和 Windows PowerShell 2.0 和 Windows PowerShell 3.0 编写的脚本运行在 Windows PowerShell 4.0 不变。

但是，由于 Microsoft.NET framework 4 运行时激活策略中的更改，Windows PowerShell 主机已 for Windows PowerShell 2.0 编写和编译与公共语言运行时 (CLR) 2.0 无法运行程序而无需使用 CLR 4.0 编译的 Windows PowerShell 3.0 中修改。

Windows PowerShell 2.0 引擎需要使用 Microsoft.NET Framework 2.0.50727 至少。 通过 Microsoft.NET Framework 3.5 Service Pack 1 满足此要求。 不能通过 Microsoft.NET Framework 4 和更高版本的 Microsoft.NET Framework 满足这一要求。

有关添加安装 Windows PowerShell 2.0 引擎，以及添加或安装 Microsoft.NET Framework 所需的版本的信息，请参阅[安装 Windows PowerShell 2.0 引擎](Installing-the-Windows-PowerShell-2.0-Engine.md)。 有关启动 Windows PowerShell 2.0 引擎的信息，请参阅[启动 Windows PowerShell 2.0 引擎](Starting-the-Windows-PowerShell-2.0-Engine.md)。

## Windows 预安装环境
Windows PowerShell 2.0、 Windows PowerShell 3.0 和 Windows PowerShell 4.0 运行在 Windows 预安装环境 (Windows PE)。 但是，不支持以下 cmdlet。

-   [后台智能传输服务 （位） Cmdlet](http://go.microsoft.com/fwlink/?LinkId=257514)

-   [获取事件日志](https://technet.microsoft.com/en-us/library/b4985b11-82bf-487d-928d-becd96fc0419)

-   [获取 WinEvent](https://technet.microsoft.com/en-us/library/5fe94870-ed6b-4ce2-9500-93846cc65c95)

-   [保存帮助](https://technet.microsoft.com/en-us/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa)

-   [更新帮助](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)

此外， **WinRM**服务不存在的 Windows PE。

## 另请参阅
[使用 Windows PowerShell 入门](../getting-started/Getting-Started-with-Windows-PowerShell.md)

[安装 Windows PowerShell](Installing-Windows-PowerShell.md)

[启动 Windows PowerShell](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)

