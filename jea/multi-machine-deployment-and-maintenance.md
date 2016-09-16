---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell cmdlet jea
ms.date: 2016-06-22
title: "多计算机部署和维护"
ms.technology: powershell
ms.openlocfilehash: 8117d0d12c062b460cb7117b54c138c8db5a1d0c
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 多计算机部署和维护
此时，您已经部署 JEA 到本地系统几次。
因为生产环境可能包含多台计算机，务必每台计算机上引导您完成必须重复部署过程中的关键步骤。

## 高级步骤︰
1.  将您 （带有角色功能） 的模块复制到每个节点。
2.  将您会话的配置文件复制到每个节点。
3.  运行`Register-PSSessionConfiguration`与会话配置。
4.  保留的安全位置的会话配置和工具包的副本。
当您进行修改，最好有"一个事实源"。

## 示例脚本
下面是一个示例脚本部署。
若要在您的环境中使用它，您将需要使用的实际的文件共享和模块名称/路径。
```PowerShell
# First, copy the session configuration and modules (containing role capability files) onto a file share you have access to.
Copy-Item -Path 'C:\Demo\Demo.pssc' -Destination '\\FileShare\JEA\Demo.pssc'
Copy-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\SomeModule\' -Recurse -Destination '\\FileShare\JEA\SomeModule'

# Next, author a setup script (C:\JEA\Deploy.ps1) to run on each individual node
    # Contents of C:\JEA\Deploy.ps1
    New-Item -ItemType Directory -Path C:\JEADeploy
    Copy-Item -Path '\\FileShare\JEA\Demo.pssc' -Destination 'C:\JEADeploy\'
    Copy-Item -Path '\\FileShare\JEA\SomeModule' -Recurse -Destination 'C:\Program Files\WindowsPowerShell\Modules' # Remember, Role Capability Files are found in modules
    if (Get-PSSessionConfiguration -Name JEADemo -ErrorAction SilentlyContinue)
    {
        Unregister-PSSessionConfiguration -Name JEADemo -ErrorAction Stop
    }

    Register-PSSessionConfiguration -Name JEADemo -Path 'C:\JEADeploy\Demo.pssc'
    Remove-Item -Path 'C:\JEADeploy' # Don't forget to clean up!

# Now, invoke the script on all of the target machines.
# Note: this requires PowerShell Remoting be enabled on each machine. Enabling PowerShell remoting is a requirement to use JEA as well.
# You may need to provide the "-Credential" parameter if your current user account does not have admin permissions on these machines.
Invoke-Command –ComputerName 'Node1', 'Node2', 'Node3', 'NodeN' -FilePath 'C:\JEA\Deploy.ps1'

# Finally, delete the session configuration and role capability files from the file share.
Remove-Item -Path '\\FileShare\JEA\Demo.pssc'
Remove-Item -Path '\\FileShare\JEA\SomeModule' -Recurse
```
## 修改的功能
当处理多个机，很重要一致的方式的推出修改。
一旦 JEA 有 DSC 资源，这有助于确保您的环境同步。
之前，我们强烈建议您保留会话配置的主副本和重新部署每次进行修改。

## 删除功能
若要从您的系统中删除 JEA 配置，请在每台计算机上使用以下命令︰
```PowerShell
Unregister-PSSessionConfiguration -Name JEADemo
```

