---
title: "DSC 配置"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: c9a2563a8474b5a8f5c9e3b06c76aceabd9df05b
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 配置

>适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

DSC 配置是定义函数的一种特殊类型的 PowerShell 脚本。 若要定义配置，您可以使用 PowerShell 关键字__配置__。

```powershell
Configuration MyDscConfiguration {

    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
```

将脚本保存为.ps1 文件。

## 配置语法

配置脚本由以下部分组成︰

- **配置**块中。 这是最外层的脚本块。 定义通过使用**配置**关键字并提供一个名称。 在此例中，配置的名称是"MyDscConfiguration"。
- 一个或多个**节点**块。 这些定义要配置的节点 （计算机或虚拟机）。 在上述配置，没有面向名为"测试电脑 1"的计算机的一个**节点**块。
- 一个或多个资源块。 这是在其中配置设置它已配置的资源的属性。 在此例中，有两个资源块，其中每个呼叫"WindowsFeature"资源。

在**配置**块中，您可以执行通常无法 PowerShell 函数中的任何内容。 例如，在上一示例中，如果您不想在配置中，在目标计算机名称进行硬编码可以添加节点名称的参数︰

```powershell
Configuration MyDscConfiguration {

    param(
        [string[]]$ComputerName="localhost"
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
```

通过将其作为 $ComputerName 参数传递的节点的名称指定在此示例中，当您[编译配置](# Compiling the configuration)。 该名称默认为"本地主机"。

## 编译配置
您可以制定配置之前，必须将其编译到 MOF 文档。 通过致电配置一样 PowerShell 函数执行此操作。
>__注意︰__要呼叫的配置，该函数必须是全局范围 （与任何其他 PowerShell 函数）。 您可以做到这一点或者通过"点-采购"脚本，或通过使用 F5 或单击__运行脚本__运行配置脚本按钮 ISE 中。 与点源脚本，运行命令`. .\myConfig.ps1`位置`myConfig.ps1`是包含您的配置的脚本文件的名称。

当您调用配置，它︰

- 解析所有变量 
- 配置同名的当前目录中创建一个文件夹。
- 创建一个名为新的目录中的_节点名称_.mof_节点名称_哪里配置的目标节点的名称的文件。 如果有多个节点，则将为每个节点创建 MOF 文件。

>__注意__︰ MOF 文件包含所有目标节点的配置信息。 由于此操作，请务必确保安全。 有关详细信息，请参阅[保护 MOF 文件](secureMOF.md)。

编译以下文件夹结构中的结果上方的第一个配置︰

```powershell
PS C:\users\default\Documents\DSC Configurations> . .\MyDscConfiguration.ps1
PS C:\users\default\Documents\DSC Configurations> MyDscConfiguration
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name                                                                                              
----                -------------         ------ ----                                                                                         
-a----       10/23/2015   4:32 PM           2842 TEST-PC1.mof
```  

如果配置采用参数，如下所示的第二个示例，必须在编译时提供。 下面介绍了如何这将如下︰

```powershell
PS C:\users\default\Documents\DSC Configurations> . .\MyDscConfiguration.ps1
PS C:\users\default\Documents\DSC Configurations> MyDscConfiguration -ComputerName 'MyTestNode'
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name                                                                                              
----                -------------         ------ ----                                                                                         
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```      

## 使用取决于
有用的 DSC 关键字是__取决于__。 通常 （但不一定始终），DSC 适用配置中显示的顺序中的资源。 但是，__取决于__指定哪些资源依赖于其他资源，并且 LCM 确保按正确的顺序，而不考虑哪个资源中定义实例的顺序应用。 例如，配置可能指定__用户__资源的实例，取决于存在的一个__组__实例︰

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = "Present"
            GroupName = "TestGroup"
        }

        User UserExample {
            Ensure = "Present"
            UserName = "TestUser"
            FullName = "TestUser"
            DependsOn = "[Group]GroupExample"
        }
    }
}
```

## 在您的配置中使用新资源
如果您运行的上一个示例，您可能已注意到了警告您已使用不显式导入的资源。
现在，DSC 附带有 12 资源为 PSDesiredStateConfiguration 模块的一部分。 外部模块中的其他资源必须置于`$env:PSModulePath`才能 LCM 识别。 新 cmdlet，[获取 DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)，可以用于确定哪些资源通过 LCM 是系统上安装并可供使用。 一旦这些模块已放在`$env:PSModulePath`和正确识别[获取 DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)，他们仍然需要加载中您的配置。 __导入 DscResource__是仅在__配置__块 （即不 cmdlet） 被识别动态关键字。 __导入 DscResource__支持两个参数︰
* __ModuleName__是使用__导入 DscResource__的推荐的方式。 它接受模块包含要导入 （以及模块名称的字符串数组） 的资源的名称。 
* __名称__是要导入的资源的名称。 这不是通过[获取 DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)，返回为"名称"的友好名称，但定义资源架构 （作为__资源类型__[获取 DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)返回） 时使用的课程名称。 

## 另请参阅
* [Windows PowerShell 需要状态配置概述](overview.md)
* [DSC 资源](resources.md)
* [配置本地配置管理器](metaConfig.md)

