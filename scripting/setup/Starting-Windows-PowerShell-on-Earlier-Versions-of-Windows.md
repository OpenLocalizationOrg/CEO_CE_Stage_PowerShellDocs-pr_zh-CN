---
title: "在早期版本的 Windows 上启动 Windows PowerShell"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 57125436-3d1e-4e7f-b5c4-8f0ecb49d642
ms.openlocfilehash: a220696938548d3191034a76d473ec437afabb5d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 在早期版本的 Windows 上启动 Windows PowerShell
本节介绍如何 WindowsÂ® 7、 Windows ServerÂ® 2008 R2 和 Windows Server 2008 上启动 Windows PowerShell 和 Windows PowerShell 集成脚本环境 (ISE)。 此外介绍如何在 Windows ServerÂ® 2008 R2 和 Windows Server 2008 上的 Windows PowerShell 2.0 中的 Windows PowerShell ISE 的启用可选功能。

若要在支持系统上安装 Windows PowerShell 4.0、 下载和安装[Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881)。 有关详细信息，请参阅[安装 Windows PowerShell](Installing-Windows-PowerShell.md)。

若要在支持系统上安装 Windows PowerShell 3.0、 下载和安装[Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290)。 有关详细信息，请参阅[安装 Windows PowerShell](Installing-Windows-PowerShell.md)。

## 如何在早期版本的 Windows 启动 Windows PowerShell
使用下列方法之一以开始安装的 Windows PowerShell 3.0 或 Windows PowerShell 4.0，版本 （如果适用）。

#### 从开始菜单

-   单击**开始**，键入**PowerShell**，，然后单击**Windows PowerShell**。

-   从**开始**菜单上，单击**开始**，单击**所有程序**、**附件**、 **Windows PowerShell**文件夹，然后都单击**Windows PowerShell**。

#### 在命令提示符

-   在 Cmd.exe、 Windows PowerShell 或 Windows PowerShell ISE，启动 Windows PowerShell，请键入︰

    ```
    PowerShell
    ```

    您可以使用 PowerShell.exe 程序的参数以自定义会话。 有关详细信息，请参阅[PowerShell.exe 命令行帮助](../core-powershell/console/PowerShell.exe-Command-Line-Help.md)。

#### 使用管理权限 （"以管理员身份运行"）

1.  单击**开始**，键入**PowerShell**、 **Windows PowerShell**，右键单击，然后单击**以管理员身份运行**。

## 如何在早期版本的 Windows 上启动 Windows PowerShell ISE
使用下列方法之一启动 Windows PowerShell ISE。

#### 从开始菜单

-   单击**开始**，键入**ISE**，，然后单击**Windows PowerShell ISE**。

-   从**开始**菜单上，单击**开始**，单击**所有程序**、**附件**、 **Windows PowerShell**文件夹中，，然后都单击**Windows PowerShell ISE**。

#### 在命令提示符

-   在 Cmd.exe、 Windows PowerShell 或 Windows PowerShell ISE，启动 Windows PowerShell，请键入︰

    ```
    PowerShell_ISE
    ```

    或

    ```
    ISE
    ```

#### 使用管理权限 （"以管理员身份运行"）

1.  单击**开始**，键入**ISE**、 **Windows PowerShell ISE**，右键单击，然后单击**以管理员身份运行**。

## 如何启用在早期版本的 Windows 上的 Windows PowerShell ISE
在 Windows PowerShell 4.0 和 Windows PowerShell 3.0，默认情况下，在所有版本的 Windows 上启用 Windows PowerShell ISE。 如果尚未启用，Windows Management Framework 4.0 或 Windows Management Framework 3.0 启用它。

在 Windows PowerShell 2.0 中，默认情况下，在 Windows 7 上启用 Windows PowerShell ISE。 但是，在 Windows Server 2008 R2 和 Windows Server 2008，它是一项可选功能。

若要启用 Windows Server 2008 R2 或 Windows Server 2008 上的 Windows PowerShell 2.0 中的 Windows PowerShell ISE，请使用以下过程。

#### 若要启用 Windows PowerShell 集成脚本环境 (ISE)

1.  启动服务器管理器。

2.  单击**功能**，然后单击**添加功能**。

3.  在选择的功能，请单击 Windows PowerShell 集成脚本环境 (ISE)。

