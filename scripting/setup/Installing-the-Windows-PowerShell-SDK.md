---
title: "安装 Windows PowerShell SDK"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: 8df8b9bb74eba5921263ad9d802dcece41261f9a
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 安装 Windows PowerShell SDK

以下主题介绍如何在不同版本的 Windows 上安装 PowerShell SDK。

## 安装 Windows PowerShell 3.0 SDK 的 Windows 8 和 Windows Server 2012

使用 Windows 8 和 Windows Server 2012，将自动安装 Windows PowerShell 3.0。
此外，您可以下载并安装 Windows PowerShell 3.0 引用程序集作为 Windows 8 SDK 的一部分。
这些程序集，可以为 Windows PowerShell 3.0 编写 cmdlet、 提供商和主机程序。
安装 Windows SDK 适用于 Windows 8 时，Windows PowerShell 集将自动安装在 \Program 文件 (x86) \Reference Assemblies\Microsoft\WindowsPowerShell\3.0 中的引用集文件夹中。
有关详细信息，请参阅[Windows 8 SDK 下载网站](http://msdn.microsoft.com/windows/hardware/hh852363.aspx)。
Windows PowerShell 代码示例在开发中心，还提供。
有关详细信息，请参阅[适用于开发人员中心网站](http://code.msdn.microsoft.com/windowsdesktop/)上的桌面的代码示例页。

此外，Windows PowerShell 3.0 是向后兼容使用 Windows PowerShell 2.0 SDK，其中包括代码示例的数字。
有关如何下载 Windows PowerShell 2.0 SDK 的详细信息，请参阅下面。
（请注意，与 Windows 8 和 Windows PowerShell 3.0 兼容 2.0 的代码示例时，您无法在 Windows 8 平台上安装 Windows PowerShell 2.0）。

##安装 Windows PowerShell 3.0 SDK for Windows 7 和 Windows Server 2008 R2

Windows 7 和 Windows Server 2008 R2 自动具有 PowerShell 2.0 安装。
此外，您可以在这些系统上安装 PowerShell 3.0。
（有关详细信息，请参阅[安装 Windows PowerShell](Installing-Windows-PowerShell.md)。）。
根据上述内容，您也可以在 Windows 7 和 Windows Server 2008 R2 上安装 Windows 8 SDK。

## 安装 Windows PowerShell 2.0 SDK 对于 Windows 7、 Vista、 XP、 Server 2003 和 Server 2008

Windows PowerShell 2.0 SDK 提供引用程序集需要通过编写 cmdlet、 提供商和托管的应用程序，并提供 C# 代码示例编写代码开始时可用作起始点。

若要安装此 SDK，请参阅[Windows PowerShell 2.0 SDK](http://go.microsoft.com/fwlink/?LinkId=184611)。

## 引用程序集

默认情况下在以下位置安装了引用程序集︰ `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`。

> **注意**︰ 针对 Windows PowerShell 2.0 程序集编译代码无法加载到 Windows PowerShell 1.0 安装。
>但是，针对 Windows PowerShell 1.0 集编译代码可以加载到 Windows PowerShell 2.0 安装。

## 示例

默认情况下在以下位置安装代码示例︰ `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`。

以下各节提供了每个示例用途的简要说明。

## Cmdlet 示例
**GetProcessSample01**

显示如何编写获取本地计算机的所有进程简单 cmdlet。

**GetProcessSample02**

介绍如何将参数添加到该 cmdlet。
该 cmdlet 所需的一个或多个进程名称，并返回匹配的过程。

**GetProcessSample03**

演示如何添加参数从管道接受输入。

**GetProcessSample04**

显示如何处理 nonterminating 错误。

**GetProcessSample05**

介绍如何显示指定进程的列表。

**SelectObject**

显示如何编写筛选器以选择特定的对象。

**SelectString**

显示如何搜索指定模式的文件。

**StopProcessSample01**

显示如何实现*层通过*参数，以及如何通过呼叫转接到的[ShouldProcess](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldprocess.aspx)和[ShouldContinue](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldcontinue.aspx)方法申请用户反馈。
用户时他们想要强制 cmdlet 返回一个对象，指定*层通过*参数

**StopProcessSample02**

介绍如何停止特定的过程。

**StopProcessSample03**

显示如何声明参数的别名，以及如何支持通配符。

**StopProcessSample04**

演示如何声明参数设置为输入，以及如何指定默认参数设置为使用采用 cmdlet 的对象。

## 远程处理示例

**RemoteRunspace01**

显示如何创建用于建立远程连接远程运行空间。

**RemoteRunspacePool01**

显示如何构建远程运行空间池以及如何使用此池同时运行多个命令。

**Serialization01**

介绍如何查看现有.NET 类并确保从所选公共属性，此类信息保留跨序列化/反序列化。

**Serialization02**

介绍如何查看现有.NET 类并确保此类实例中的信息将保留跨序列化/反序列化的类公共属性中没有信息时。

**Serialization03**

介绍如何查看现有.NET 类并确保此类和派生类的实例反序列 （解除冻结） 到实时.NET 对象。

## 事件示例

**Event01**

显示如何通过从 ObjectEventRegistrationBase 派生创建的事件注册 cmdlet。

**Event02**

显示如何向演示如何接收通知的 Windows PowerShell 在远程计算机生成的事件。
它使用通过[运行空间](https://technet.microsoft.com/library/system.management.automation.runspaces.runspace.aspx)类公开 PSEventReceived 事件。

## 托管的应用程序示例

**Runspace01**

显示如何使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)类同步运行[获取流程](http://go.microsoft.com/fwlink/?LinkId=113324)cmdlet。
[获取流程](http://go.microsoft.com/fwlink/?LinkId=113324)cmdlet 返回每个进程本地计算机上运行的[进程](https://technet.microsoft.com/library/system.diagnostics.process.aspx)对象。

**Runspace02**

显示如何使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)类同步运行[获取流程](http://go.microsoft.com/fwlink/?LinkId=113324)和[排序对象](http://go.microsoft.com/fwlink/?LinkID=113403)cmdlet。
[获取流程](http://go.microsoft.com/fwlink/?LinkId=113324)cmdlet 返回每个进程的本地计算机上运行的[进程](https://technet.microsoft.com/library/system.diagnostics.process.aspx)对象并排序对象进行排序的基于其[Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx)属性的对象。
使用[DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx)控件显示这些命令的结果。

**Runspace03**

显示如何使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)类运行脚本同步，以及如何处理非终止错误。
脚本接收进程名称列表，然后检索这些流程。
在控制台窗口中显示脚本，包括任何非终止错误时运行的脚本，生成的结果。

**Runspace04**

显示如何使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)类运行命令，以及如何捕捉终止运行命令时引发错误。
运行两个命令，并不是有效参数传递的最后一个命令。
因此，返回没有对象，并引发终止错误。

**Runspace05**

显示如何以便管理单元的 cmdlet 可打开运行空间时管理单元添加到[InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx)对象。
管理单元中提供了使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)对象在同步运行获取进程 cmdlet （由[GetProcessSample01 示例](https://technet.microsoft.com/library/ff602028.aspx)定义）。

**Runspace06**

介绍如何向[InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx)对象添加模块，以便在模块加载时打开运行空间。
模块提供了使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)对象在同步运行获取进程 cmdlet （由[GetProcessSample02 示例](https://technet.microsoft.com/library/ff602027.aspx)定义）。

**Runspace07**

演示如何创建运行空间，然后使用该运行空间使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)对象同步运行两个 cmdlet。

**Runspace08**

显示如何将命令和参数添加到一个[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)对象的管道和同步运行命令。

**Runspace09**

显示如何将脚本添加到一个[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)对象的管道和异步运行该脚本。
事件用于处理脚本的输出。

**Runspace10**

显示如何创建默认初始会话状态、 如何向[InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx)添加 cmdlet、 如何创建使用初始会话状态，运行空间和如何使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)对象运行命令。

**Runspace11**

显示如何使用[ProxyCommand](https://technet.microsoft.com/library/system.management.automation.proxycommand.aspx)类创建代理命令呼叫现有 cmdlet，但限制可用参数的设置。
代理命令然后添加到用于创建约束运行空间初始会话状态。
这意味着，用户可以访问只能通过代理命令的 cmdlet 的功能。

**PowerShell01**

显示如何创建使用[InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx)对象约束运行空间。

**PowerShell02**

显示如何使用运行空间池同时运行多个命令。

## 主机示例

**Host01**

介绍如何使用自定义主机主机应用程序实现。
运行空间创建此示例中使用的自定义主机，然后使用[PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) API 运行脚本的呼叫"退出"。
然后，宿主应用程序查看该脚本的输出，并打印出的结果。

**Host02**

介绍如何编写使用 Windows PowerShell 运行时，以及自定义主机实施主机应用程序。
宿主应用程序将主机区域性设置为德语、 运行[获取流程](http://go.microsoft.com/fwlink/?LinkId=113324)cmdlet 和使用 pwrsh.exe，看到显示结果以及然后打印出的当前数据和德语中的时间。

**Host03**

显示如何构建交互式的基于控制台主机读取并应用程序命令从命令行、 执行命令，然后将结果显示在控制台。

**Host04**

显示如何构建交互式基于控制台主机读取并应用程序命令从命令行、 执行命令，然后将结果显示在控制台。
此宿主应用程序还支持显示允许用户指定多个选项的提示。

**Host05**

显示如何构建交互式的基于控制台主机读取并应用程序命令从命令行、 执行命令，然后将结果显示在控制台。
通过使用[Enter PsSession](http://go.microsoft.com/fwlink/?LinkId=135210)和[退出 PsSession](http://go.microsoft.com/fwlink/?LinkId=135212) cmdlet，此宿主应用程序也支持呼叫转接到远程计算机。

**Host06**

显示如何构建交互式基于控制台主机读取并应用程序命令从命令行、 执行命令，然后将结果显示在控制台。
此外，此示例使用标记器 Api 指定用户输入的文本的颜色。

## 提供商示例

**AccessDBProviderSample01**

显示如何声明派生直接从[CmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.cmdletprovider.aspx)类的提供商类。
它提供了仅针对完整性。

**AccessDBProviderSample02**

显示如何覆盖[须先](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.newdrive.aspx)和[RemoveDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.removedrive.aspx)方法，以支持呼叫转接到新建 PSDrive 和删除 PSDrive cmdlet。
在此示例中的提供程序类派生自[DriveCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.aspx)课堂。

**AccessDBProviderSample03**

显示如何覆盖[GetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.getitem.aspx)和[SetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.setitem.aspx)方法，以支持呼叫转接到获取项目和设置项目 cmdlet。
在此示例中的提供程序类派生自[ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx)类。

**AccessDBProviderSample04**

显示如何覆盖容器方法，以支持呼叫转接到复制项目，获取-ChildItem 新建项目和删除项目 cmdlet。
数据存储区包含容器的项目时，应实现这些方法。
容器是一组通用的父项下的子项目。
在此示例中的提供程序类派生自[ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx)课堂。

**AccessDBProviderSample05**

显示如何覆盖容器方法，以支持呼叫转接到移动项目和加入路径 cmdlet。
当用户需要移动容器中的项目时，如果数据存储区包含嵌套的容器，则应实现这些方法。
在此示例中的提供程序类派生自[NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx)类。

**AccessDBProviderSample06**

显示如何覆盖内容的方法，以支持呼叫转接到清除内容获取内容和设置内容 cmdlet。
当用户需要管理中数据存储的项目的内容，则应实现这些方法。
在此示例中的提供程序类派生自[NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx)类，并实现[IContentCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.icontentcmdletprovider.aspx)界面。
