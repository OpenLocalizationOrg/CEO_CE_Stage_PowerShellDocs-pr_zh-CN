---
title: "安装 Windows PowerShell 2.0 引擎"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 82928f2b-f96a-4ae6-a0d0-6e7b181da308
ms.openlocfilehash: 2791deaa8e32715831ca42f1c6230e9b1a08d559
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 安装 Windows PowerShell 2.0 引擎
本主题介绍如何安装 Windows PowerShell 2.0 引擎。

Windows PowerShell 3.0 旨在与 Windows PowerShell 2.0 向后兼容。 Cmdlet、 提供商、 单元、 模块和 for Windows PowerShell 2.0 编写的脚本运行在 Windows PowerShell 3.0 和 Windows PowerShell 4.0 不变。 但是，在运行时激活策略 Microsoft.NET framework 4 的更改，由于 Windows PowerShell 主机已 for Windows PowerShell 2.0 编写和编译与公共语言运行时 (CLR) 2.0 无法运行程序而无需修改更高版本的 Windows PowerShell，与 CLR 4.0 编译。

若要保持与命令和受这些更改的主机程序向后兼容，Windows PowerShell 2.0、 Windows PowerShell 3.0 和 Windows PowerShell 4.0 引擎旨在运行并排比较。 此外，在 Windows Server 2012 R2、 Windows 8.1、 Windows 8、 Windows Server 2012 和 Windows Management Framework 3.0 包括 Windows PowerShell 2.0 引擎。 Windows PowerShell 2.0 引擎旨在只能在一个现有的脚本或主机程序无法运行，因为它与 Windows PowerShell 3.0、 Windows PowerShell 4.0 或 Microsoft.NET Framework 4 不兼容。 这种情况下会很少出现。

Windows PowerShell 2.0 引擎是可选的 Windows Server 2012 R2、 Windows 8.1、 WindowsÂ® 8 和 Windows ServerÂ® 2012年功能。 在早期版本的 Windows，当安装 Windows Management Framework 3.0，Windows PowerShell 3.0 安装完全会替换 Windows PowerShell 2.0 安装 Windows PowerShell 安装目录中。 但是，Windows PowerShell 2.0 引擎会保留。

有关启动 Windows PowerShell 2.0 引擎的信息，请参阅[启动 Windows PowerShell 2.0 引擎](Starting-the-Windows-PowerShell-2.0-Engine.md)。

## 在 Windows 8.1 和 Windows 8
在 Windows 8.1 和 Windows 8，默认情况下打开 Windows PowerShell 2.0 引擎功能。 但是，若要使用它，您需要打开 Microsoft.NET Framework 3.5，它需要的选项。 本节还介绍了如何打开和关闭 Windows PowerShell 2.0 引擎功能。

#### 若要开启.NET Framework 3.5

1.  在**开始**屏幕中，键入**Windows 功能**。

2.  在**应用程序**栏上，单击**设置**，然后单击**打开或关闭 Windows 功能**。

3.  在**Windows 功能**框中，单击**.NET Framework 3.5 (包括.NET 2.0 和 3.0**以将其选中。

    当您选择**.NET Framework 3.5 (包括.NET 2.0 和 3.0**，框中填充，以指示选定仅功能的一部分。 但是，这是足够的 Windows PowerShell 2.0 引擎。

#### 若要打开或关闭 Windows PowerShell 2.0 引擎

1.  在**开始**屏幕中，键入**Windows 功能**。

2.  在**应用程序**栏上，单击**设置**，然后单击**打开或关闭 Windows 功能**。

3.  在**Windows 功能**框中，展开**Windows PowerShell 2.0**节点，然后单击**Windows PowerShell 2.0 引擎**框中，选择或清除此复选框。

## 在 Windows Server 2012 R2 和 Windows Server 2012
使用以下过程添加的 Windows PowerShell 2.0 引擎和 Microsoft.NET Framework 3.5 功能。 Windows PowerShell 2.0 引擎需要使用 Microsoft.NET Framework 2.0.50727 至少。 通过 Microsoft.NET Framework 3.5 满足该要求。

#### 若要添加的.NET Framework 3.5 功能

1.  在**服务器管理器**，从**管理**菜单上，选择**添加角色和功能**。

    或在**服务器管理器**中，单击**所有服务器**、 服务器名称，用鼠标右键单击，然后选择**添加角色和功能**。

2.  在**安装类型**页中，选择**基于角色的或基于功能的安装**。

3.  在**功能**页面中，展开**.NET 3.5 框架功能**节点，然后选择**.NET Framework 3.5 （包括.NET 2.0 和 3.0）**。

    并非必需的 Windows PowerShell 2.0 引擎下该节点的其他选项。

#### 若要添加的 Windows PowerShell 2.0 引擎功能

-   在**服务器管理器**，从**管理**菜单上，选择**添加角色和功能**。

    或**服务器管理器**中，单击**所有服务器**、 服务器名称，用鼠标右键单击，然后选择**添加角色和功能**。

-   在**安装类型**页中，选择**基于角色的或基于功能的安装**。

-   在**功能**页面中，展开**Windows PowerShell （已安装）**节点，然后选择**Windows PowerShell 2.0 引擎**。

有关启动 Windows PowerShell 2.0 引擎的信息，请参阅[启动 Windows PowerShell 2.0 引擎](Starting-the-Windows-PowerShell-2.0-Engine.md)。

## 在早期系统
在 Windows 7、 Windows Server 2008 R2 和 Windows Server 2012，安装 Windows PowerShell 4.0 [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881)程序包中包含 Windows PowerShell 2.0 引擎。 Windows PowerShell 2.0 引擎启用了视频并且准备好使用，如有必要，无需其他安装、 安装或配置。

在 Windows 7、 Windows Server 2008 R2 和 Windows Server 2008 安装 Windows PowerShell 3.0 Windows Management Framework 3.0 程序包中包含 Windows PowerShell 2.0 引擎。 Windows PowerShell 2.0 引擎启用了视频并且准备好使用，如有必要，无需其他安装、 安装或配置。

## 另请参阅
[Windows PowerShell 系统要求](Windows-PowerShell-System-Requirements.md)
[安装 Windows PowerShell](Installing-Windows-PowerShell.md)
[启动 Windows PowerShell [ps]](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
[启动 Windows PowerShell 2.0 引擎](Starting-the-Windows-PowerShell-2.0-Engine.md)

