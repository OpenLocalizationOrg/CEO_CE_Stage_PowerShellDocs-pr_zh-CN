---
title: "启动 32 位版本的 Windows PowerShell"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 12b31890-2609-4a76-8c24-0ebe78084f50
ms.openlocfilehash: a911a3b3f7d0dbeebf3ccd7ca64b1512ef61f9ef
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 启动 Windows PowerShell 的 32 位版本
当在 64 位计算机上， **Windows PowerShell (x86)**，安装 Windows PowerShell 除了 64 位版本安装 32 位版本的 Windows PowerShell。 Windows PowerShell 运行时，默认情况下将运行 64 位版本。

但是，您有时可能需要运行**Windows PowerShell (x86)**，例如，当您使用的模块需要 32 位版本或远程连接到 32 位计算机时。

要开始 32 位版本的 Windows PowerShell，请使用下列过程之一。

#### 在 Windows ServerÂ® 2012 R2 中

-   在**开始**屏幕中，键入**Windows PowerShell (x86)**。 单击**Windows PowerShell x86**磁贴。

-   在**服务器管理器**，从**工具**菜单中，选择**Windows PowerShell (x86)**。

-   在桌面上，将光标移到右上角，单击**搜索**，键入**PowerShell x86** ，然后单击**Windows PowerShell (x86)**。

-   通过命令行中，输入︰ `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### 在 Windows Server 2012

-   在**开始**屏幕中，键入**PowerShell** ，然后单击**Windows PowerShell (x86)**。

-   在**服务器管理器**，从**工具**菜单中，选择**Windows PowerShell (x86)**。

-   在桌面上，将光标移到右上角，单击**搜索**，键入**PowerShell** ，然后单击**Windows PowerShell (x86)**。

-   通过命令行中，输入︰ `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### 在 Windows 8.1 中

-   在**开始**屏幕中，键入**Windows PowerShell (x86)**。 单击**Windows PowerShell x86**磁贴。

-   如果您运行 Windows 8.1[远程服务器管理工具](http://go.microsoft.com/fwlink/?LinkID=304145)，您也可以从**服务器 ManagerTools**菜单打开 Windows PowerShell x86。 选择**Windows PowerShell (x86)**。

-   在桌面上，将光标移到右上角，单击**搜索**，键入**PowerShell x86** ，然后单击**Windows PowerShell (x86)**。
   
-   通过命令行中，输入︰ `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### 在 Windows 8 中

-   在**开始**屏幕中，将光标移到右上角，单击**设置**单击**图块**，，然后将**显示管理工具**滑块移动到是。 然后，键入**PowerShell** ，然后单击**Windows PowerShell (x86)**。

-   如果运行的 Windows 8 的[远程服务器管理工具](http://www.microsoft.com/download/details.aspx?id=28972)，您也可以从**服务器 ManagerTools**菜单打开 Windows PowerShell x86。 选择**Windows PowerShell (x86)**。

-   在**开始**屏幕或桌面中，键入**PowerShell (x86)** ，然后单击**Windows PowerShell (x86)**。

-   通过命令行中，输入︰ `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`
