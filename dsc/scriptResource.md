---
title: "DSC 脚本资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: d54c09377ebee94a17858d6ba7ead0f265583927
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 脚本资源

 
> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

在 Windows PowerShell 需要状态配置 (DSC) 的**脚本**资源提供一种机制目标节点上运行 Windows PowerShell 脚本块。 `Script`资源具有`GetScript`， `SetScript`，和`TestScript`属性。 这些属性应设置为每个目标节点运行的脚本块。 

`GetScript`脚本块应返回散列表表示当前节点的状态。 哈希表必须只包含一个键`Result`并且该值必须是类型的`String`。 不需要返回任何内容。 DSC 不执行任何操作使用此脚本块的输出。

`TestScript`脚本块应确定是否需要修改当前节点。 应该返回`$true`如果节点是最新。 应该返回`$false`如果节点的配置已过期，应通过更新`SetScript`脚本块。 `TestScript`脚本块由 DSC。

`SetScript`脚本块应修改节点。 如果由 DSC 调用`TestScript`阻止返回`$false`。

如果您需要使用您的配置脚本中的变量`GetScript`， `TestScript`，或`SetScript`脚本块，请使用`$using:`范围 （请参阅下面的示例）。


## 语法

```
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## 属性

|  属性  |  说明   | 
|---|---| 
| GetScript| 提供当您调用[获取 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) cmdlet 时运行的 Windows PowerShell 脚本块。 此块必须返回哈希表。 哈希表必须只包含一个键**结果**，并且该值必须是**字符串**类型。| 
| SetScript| 提供 Windows PowerShell 脚本的块。 当您调用[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet 时，首先运行**TestScript**块。 如果**TestScript**块返回**$false**，将运行**SetScript**块。 如果**TestScript**块返回**$true**，不会运行**SetScript**块。| 
| TestScript| 提供 Windows PowerShell 脚本的块。 当您调用[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet 时，运行此块。 如果它返回**$false**，将运行 SetScript 块。 如果它返回**$true**，不会运行 SetScript 块。 当您调用[测试 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet，也将运行**TestScript**块。 但是，这种情况下， **SetScript**块将无法运行，无论 TestScript 块哪些值返回。 如果实际配置满足当前的配置所需的状态，并且 False，如果不匹配， **TestScript**块必须返回 True。 （当前所需的状态配置是最后一配置代理使用 DSC 节点）。| 
| 凭据| 指明用于运行此脚本，如果需要凭据的凭据。| 
| 取决于| 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行的资源配置脚本块的 ID 首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。

## 示例 1
```powershell
Script ScriptExample
{
    SetScript = { 
        $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
        $sw.WriteLine("Some sample string")
        $sw.Close()
    }
    TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
    GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }          
}
```

## 示例 2
```powershell
$version = Get-Content 'version.txt'
Script UpdateConfigurationVersion
{
    GetScript = { 
        $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
        return @{ 'Result' = "Version: $currentVersion" }
    }          
    TestScript = { 
        $state = GetScript
        if( $state['Version'] -eq $using:version )
        {
            Write-Verbose -Message ('{0} -eq {1}' -f $state['Version'],$using:version)
            return $true
        }
        Write-Verbose -Message ('Version up-to-date: {0}' -f $using:version)
        return $false
    }
    SetScript = { 
        $using:version | Set-Content -Path (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
    }
}
```

此资源写入文本文件配置的版本。 此版本提供的客户端计算机上，但不在任何节点，使其具有传递给每个`Script`使用 PowerShell 的资源的脚本块`using`范围。 生成的节点 MOF 文件时，值`$version`从客户端计算机上的文本文件中读取变量。 DSC 替换`$using:version`中每个脚本变量的值阻止`$version`变量。

