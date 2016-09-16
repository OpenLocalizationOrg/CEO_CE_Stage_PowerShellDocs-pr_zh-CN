---
title: "管理与流程 Cmdlet 流程"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: 1f42ca709a3ffe9ddac69f34ca51f2494e42244e
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 管理与流程 Cmdlet 的流程
您可以使用 Windows PowerShell 中流程 cmdlet 管理 Windows PowerShell 中的本地和远程流程。

## 入门 （获取进程） 的流程
若要获取本地计算机上运行的进程，不带参数运行**获取流程**。

您可以通过指定其进程名称或进程 Id 获取特定流程。 以下命令获取空闲过程︰

```
PS> Get-Process -id 0
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

虽然是正常的 cmdlet，以便不返回数据在某些情况下，指定一个通过其流程 Id 的过程时，**获取流程**生成错误，如果它未找到匹配项，因为通常的目的是要检索已知正在运行的进程。 如果没有与该 Id 的进程，则很可能 Id 不正确或已退出感兴趣的过程︰

```
PS> Get-Process -Id 99
Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

获取流程 cmdlet 的名称参数用于指定流程基于流程名称的子集。 Name 参数可以执行以逗号分隔的列表中的多个名称，它支持使用通配符，以便您可以键入文件名模式。

例如，以下命令获取的流程名称开头"上"。

```
PS> Get-Process -Name ex*
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

.NET System.Diagnostics.Process 类是 Windows PowerShell 流程的基础，因为它遵循一些使用 System.Diagnostics.Process 的约定。 这些约定之一是名称的可执行文件的进程名称永远不会包括".exe"的末尾的可执行文件。

**获取过程**也接受名参数的多个值。

```
PS> Get-Process -Name exp*,power* 
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

获取流程的计算机名称参数可用于在远程计算机上获取流程。 例如，以下命令 （由"本地主机"） 的本地计算机上获取 PowerShell 流程和两个远程计算机上。

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

计算机名称不在这种显示，很明显，但它们存储在获取过程返回的流程对象名属性。 以下命令使用表格格式 cmdlet 来显示进程 ID、 ProcessName 和计算机名 （计算机名称） 的进程对象属性。

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName
  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

此更复杂的命令添加到标准获取流程显示机器名属性。 引号 (\`)(ASCII 96) 是 Windows PowerShell 延续字符。

```
get-process powershell -computername localhost, Server01, Server02 | format-table -property Handles, `
                    @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}}, `
                    @{Label="PM(K)";Expression={[int]($_.PM/1024)}}, `
                    @{Label="WS(K)";Expression={[int]($_.WS/1024)}}, `
                    @{Label="VM(M)";Expression={[int]($_.VM/1MB)}}, `
                    @{Label="CPU(s)";Expression={if ($_.CPU -ne $()` 
                    {$_.CPU.ToString("N")}}}, `                                                                         
                    Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## 停止进程 （停止进程）
Windows PowerShell 为您提供了灵活性列举过程，但怎样停止流程？

**停止流程**cmdlet 所需的姓名或 Id 来指定您要停止的流程。 您要停止流程取决于您的权限。 不能停止一些过程。 例如，如果您尝试停止空闲的过程，您将收到的错误︰

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

您也可以强制使用**确认**参数提示。 此参数是时，如果使用通配符指定过程的名称，因为您可能会意外地匹配不希望停止一些的进程特别有用︰

```
PS> Stop-Process -Name t*,e* -Confirm
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "explorer (408)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "taskmgr (4072)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
```

复杂的过程操作可能是对象的使用一些筛选 cmdlet。 因为处理对象它不再响应时如此响应属性，您可以停止所有无响应的应用程序使用以下命令︰

```
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

您可以在其他情况下使用相同的方法。 例如，假设辅助通知区域应用程序的用户启动另一个应用程序时自动运行。 您可能会发现这不起作用正确终端服务会话中，但您仍要将其保留在物理计算机控制台运行的会话中。 始终连接到物理计算机桌面会话有会话 ID 为 0，以便您可以停止的过程中使用**的位置对象**和流程，**会话 Id**是其他会话中的所有实例︰

```
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

停止流程 cmdlet 没有计算机名称参数。 因此，若要在远程计算机上运行停止进程命令，您需要使用调用命令 cmdlet。 例如，若要停止 PowerShell 流程 Server01 远程计算机上，键入︰

```
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## 停止所有其他 Windows PowerShell 会话
有时可能有用能够停止当前会话以外的所有正在运行 Windows PowerShell 会话。 如果使用过多的资源的会话，或无法访问 （它可能会运行远程或其他桌面会话中），您可能不能直接将其停止。 如果您尝试停止运行的所有会话，但是，可能会改为终止当前会话。

每个 Windows PowerShell 会话具有一个环境变量 PID 包含 Windows PowerShell 进程的 Id。 您可以检查针对每个会话的 Id $PID 和终止仅 Windows PowerShell 会话的具有不同的 id。 下面的管道命令执行此操作，并返回终止会话的列表 （是由于使用**层通过**参数）︰

```
PS> Get-Process -Name powershell | Where-Object -FilterScript {$_.Id -ne $PID} | Stop-Process -
PassThru
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    334       9    23348      29136   143     1.03    388 powershell
    304       9    23152      29040   143     1.03    632 powershell
    302       9    20916      26804   143     1.03   1116 powershell
    335       9    25656      31412   143     1.09   3452 powershell
    303       9    23156      29044   143     1.05   3608 powershell
    287       9    21044      26928   143     1.02   3672 powershell
```

## 启动、 调试和等待流程
Windows PowerShell 还附带 cmdlet，以便开始 （或重新启动），调试过程，并等待过程完成，才能运行的命令。 有关使用这些 cmdlet 的详细说明，请参阅有关每个 cmdlet cmdlet 帮助主题。

## 另请参阅
[获取流程 [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)
[停止流程 [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)
[开始流程](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
[等待过程](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
[调试进程](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
[调用命令](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)

