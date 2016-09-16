---
title: "如何使用 Windows PowerShell ISE 配置文件"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
ms.openlocfilehash: ec13d0abdfad413ebcc1212d6053954108f62438
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 如何使用 Windows PowerShell ISE 配置文件
本主题介绍如何使用在 Windows PowerShellÂ® 集成脚本环境 (ISE) 的配置文件。 我们建议之前执行本节中的任务，您查看[about_Profiles [v4]](https://technet.microsoft.com/en-us/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054)，或在控制台窗格中，键入，"获取帮助 about_profiles"并按**ENTER**。

配置文件是启动一个新的会话时自动运行的 Windows PowerShell ISE 脚本。  您可以为 Windows PowerShell ISE 创建一个或多个 Windows PowerShell 配置文件并使用它们来添加配置 Windows PowerShell 或 Windows PowerShell ISE 的环境中，准备您使用与变量、 别名，函数和所需的颜色和字体首选项。 配置文件会影响您启动的每个 Windows PowerShell ISE 会话。

> [!NOTE]
> Windows PowerShell 执行策略确定是否可以运行脚本并加载的配置文件。 默认执行策略，"受限"阻止所有脚本运行，包括配置文件。 如果您使用"受限"策略，不能加载配置文件。 有关执行策略的详细信息，请参阅[about_Execution_Policies [v4]](https://technet.microsoft.com/en-us/library/347708dc-1515-4d74-978b-8334603472e6)。

## 选择要使用 Windows PowerShell ISE 中的配置文件
Windows PowerShell ISE 支持对当前用户和所有用户配置文件。 它还支持应用于所有主机的 Windows PowerShell 配置文件。

如何使用 Windows PowerShell 和 Windows PowerShell ISE 取决于您使用的配置文件。

-   如果您使用仅 Windows PowerShell ISE 运行 Windows PowerShell，然后保存您的所有项目中选择一种 ISE 特定的配置文件，如 Windows PowerShell ISE 的 CurrentUserCurrentHost 配置文件或 Windows PowerShell ISE 的 AllUsersCurrentHost 配置文件。

-   如果您使用多个主机程序运行 Windows PowerShell，将影响所有主机程序，如 CurrentUserAllHosts 或 AllUsersAllHosts 配置文件的配置文件以保存您的函数、 别名、 变量和命令，并保存 ISE 的特定功能，如颜色和字体自定义的 Windows PowerShell ISE 配置文件或 AllUsersCurrentHost 配置文件的 CurrentUserCurrentHost 配置文件的 Windows PowerShell ISE。

下面是可以创建和使用 Windows PowerShell ISE 在配置文件。 每个配置文件将保存到自己特定的路径。

|配置文件类型|配置文件路径|
|----------------|----------------|
|"当前用户 PowerShell ISE"|$profile。CurrentUserCurrentHost 或 $profile|
|"所有用户，PowerShell ISE"|$profile。AllUsersCurrentHost|
|"当前用户的所有主机"|$profile。CurrentUserAllHosts|
|"所有用户，所有主机"|$profile。AllUsersAllHosts|

## 若要创建新的配置文件
若要创建一个新"当前用户，Windows PowerShell ISE"配置文件，运行以下命令︰

```
if (!(test-path $profile )) 
{new-item -type file -path $profile -force}
```

若要创建新的"所有用户，Windows PowerShell ISE"配置文件，运行以下命令︰

```
if (!(test-path $profile.AllUsersCurrentHost)) 
{new-item -type file -path $profile.AllUsersCurrentHost -force}
```

若要创建新的"当前用户，所有托管"配置文件，请运行以下命令︰

```
if (!(test-path $profile.CurrentUserAllHosts)) 
{new-item -type file -path $profile.CurrentUserAllHosts -force}
```

若要创建新的"所有用户，所有都托管"配置文件，请键入︰

```
if (!(test-path $profile.AllUsersAllHosts)) 
{new-item -type file -path $profile.AllUsersAllHosts-force}
```

## 若要编辑配置文件

1.  若要打开的配置文件，请指定您要编辑的配置文件的变量运行命令 psedit。 例如，若要打开"当前用户，Windows PowerShell ISE"配置文件中，键入︰ `psEdit $profile`

2.  将某些项目添加到您的配置文件。 以下是可帮助您入门的一些示例︰

    -   若要更改控制台窗格中，为蓝色，在文件类型配置文件的默认背景色︰ `$psISE.Options.OutputPaneBackground = 'blue'` 。 有关 $psISE 变量的详细信息，请参阅[Windows PowerShell ISE 对象模型参考](https://technet.microsoft.com/en-us/library/e1a9e7d1-0fd5-47de-8d9b-f1be1ed13b0c)。

    -   若要更改字体大小为 20，在配置文件的文件类型︰ `$psISE.Options.FontSize =20`

3.  要保存您的配置文件的文件，在**文件**菜单上，单击**保存**。 打开 Windows PowerShell ISE 下, 一次应用自定义设置。

## 另请参阅
[about_Profiles [v4]](https://technet.microsoft.com/en-us/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054)
[使用 Windows PowerShell ISE](Using-the-Windows-PowerShell-ISE.md)

