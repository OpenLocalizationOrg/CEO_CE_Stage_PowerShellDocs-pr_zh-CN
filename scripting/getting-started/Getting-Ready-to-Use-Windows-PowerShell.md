---
title: "准备好使用 Windows PowerShell"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6dc7052d-cc5a-4220-950f-98f963a2b587
ms.openlocfilehash: 403de939c88d3f76f6bfc3dcc973a50a4fb51e0d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 准备好使用 Windows PowerShell
在安装并启动 Windows PowerShell，请考虑以下设置选项。 您可以随时执行这些任务。

-   **安装帮助文件。** Windows PowerShell 3.0 中包含的 cmdlet 未附带的帮助文件。 但是，您可以使用[更新帮助](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)cmdlet 下载并安装最新的帮助文件，您的计算机上。 安装文件时，您可以使用[获取帮助](https://technet.microsoft.com/en-us/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a)cmdlet 来显示它们右在命令行。 有关详细信息，请参阅[about_Updatable_Help](https://technet.microsoft.com/en-us/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe)。

    如果您决定不安装的帮助文件，您仍然可以阅读的帮助主题。 若要查找任何 cmdlet 帮助主题的联机版本，请键入︰ `Get-Help <CmdletName> -Online`。 若要浏览 TechNet 库中的 Windows PowerShell 帮助主题，请从[http://go.microsoft.com/fwlink/?LinkID=107116](http://go.microsoft.com/fwlink/?LinkID=107116)开始。

-   **运行脚本。** 若要保持 Windows PowerShell 的安全，Windows PowerShell 的默认执行策略是**受限制**。 此策略允许您运行的 cmdlet，但不是脚本。 若要运行脚本，请使用[Set-executionpolicy [PSITPro5_Security]](https://technet.microsoft.com/en-us/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) cmdlet 若要更改**AllSigned**或**RemoteSigned**执行策略。 只有在计算机上的管理员组的成员可以运行该 cmdlet。 有关详细信息，请参阅[about_Execution_Policies [v4]](https://technet.microsoft.com/en-us/library/347708dc-1515-4d74-978b-8334603472e6)。

-   **启用远程处理。** 为您在其他计算机上运行远程命令已配置系统。 在 Windows Server 2012 R2 和 Windows Server 2012，系统也配置用于接收远程命令，即，允许其他计算机的本地计算机上运行远程命令。 若要启用运行其他版本的 Windows 接收远程命令的计算机，请您想要管理远程计算机上运行[启用 PSRemoting](https://technet.microsoft.com/en-us/library/19437c28-33b8-4ac1-9113-8439cc8beffb) cmdlet。 只有在计算机上的管理员组的成员可以运行该 cmdlet。 有关详细信息，请参阅[about_Remote](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)。

    注意︰ 如果在运行 Windows PowerShell 2.0 的计算机上启用远程处理，则启用了远程处理仍安装 Windows Management Framework 3.0 后。 但是，在 Windows Server 2008 (不 Windows Server 2008 R2)，您必须重新启用远程安装 Windows Management Framework 3.0 之后。

## 另请参阅
[安装 Windows PowerShell](../setup/Installing-Windows-PowerShell.md)
[启动 Windows PowerShell [ps]](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)

