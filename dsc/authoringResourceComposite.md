---
"标题︰ 复合资源︰ 使用 DSC 配置作为资源 ms.date": "2016年-05-16 关键字︰ powershell，DSC 说明︰"
"ms.topic︰ 文章作者︰ eslesar 管理器︰ dongill ms.prod": powershell
ms.openlocfilehash: cbe8a4df6459c93749cbe93489c62f2e8e72702c
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 复合资源︰ 作为资源使用 DSC 配置

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

在现实情况下，配置会变得较长和复杂，调用许多不同的资源并设置大量属性。 若要帮助解决此复杂性，可用于 Windows PowerShell 需要状态配置 (DSC) 配置作为资源其他配置。 我们称之为复合资源。 复合资源是采用参数 DSC 配置。 配置的参数作为该资源的属性。 配置保存为文件**。 schema.psm1**扩展，并会在典型 DSC 资源脚本 MOF 架构和资源的位置 （DSC 资源有关的详细信息，请参阅[Windows PowerShell 需要状态配置资源](resources.md)。

## 创建复合资源

在我们的示例，我们创建配置调用现有资源以配置虚拟机的数目。 而不是指定的值，以将其设置中配置块，配置采用然后配置块中使用参数的数目。

```powershell
Configuration xVirtualMachine
{
    param
    (
        # Name of VMs
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String[]] $VMName,

        # Name of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchName,

        # Type of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchType,

        # Source Path for VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDParentPath,

        # Destination path for diff VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDPath,

        # Startup Memory for VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMStartupMemory,

        # State of the VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMState
    )

    # Import the module that defines custom resources
    Import-DscResource -Module xComputerManagement,xHyper-V

    # Install the Hyper-V role
    WindowsFeature HyperV
    {
        Ensure = "Present"
        Name = "Hyper-V"
    }

    # Create the virtual switch
    xVMSwitch $SwitchName
    {
        Ensure = "Present"
        Name = $SwitchName
        Type = $SwitchType
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check for Parent VHD file
    File ParentVHDFile
    {
        Ensure = "Present"
        DestinationPath = $VHDParentPath
        Type = "File"
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check the destination VHD folder
    File VHDFolder
    {
        Ensure = "Present"
        DestinationPath = $VHDPath
        Type = "Directory"
        DependsOn = "[File]ParentVHDFile"
    }

    # Creae VM specific diff VHD
    foreach ($Name in $VMName)
    {
        xVHD "VHD$Name"
        {
            Ensure = "Present"
            Name = $Name
            Path = $VHDPath
            ParentPath = $VHDParentPath
            DependsOn = @("[WindowsFeature]HyperV",
                          "[File]VHDFolder")
        }
    }

    # Create VM using the above VHD
    foreach($Name in $VMName)
    {
        xVMHyperV "VMachine$Name"
        {
            Ensure = "Present"
            Name = $Name
            VhDPath = (Join-Path -Path $VHDPath -ChildPath $Name)
            SwitchName = $SwitchName
            StartupMemory = $VMStartupMemory
            State = $VMState
            MACAddress = $MACAddress
            WaitForIP = $true
            DependsOn = @("[WindowsFeature]HyperV",
                          "[xVHD]VHD$Name")
        }
    }
}
```

### 配置另存为复合资源

若要使用参数化的配置为 DSC 资源，将其保存在目录结构等的其他任何基于 MOF 的资源，并将其与命名**。 schema.psm1**扩展名。 对于此示例中，我们将命名文件**xVirtualMachine.schema.psm1**。 您还需要创建名为包含以下行的**xVirtualMachine.psd1**的清单。 请注意，这是除了**MyDscResources.psd1**， **MyDscResources**文件夹下的所有资源的模块清单。

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

当您完成文件夹结构应如下所示。

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

资源是现在可发现通过获取 DscResource cmdlet，并且其属性发现任一该 cmdlet 或使用 Windows PowerShell ISE 中的自动完成**Ctrl + 空格键**。

## 使用复合资源

接下来创建呼叫复合资源配置。 此配置呼叫 xVirtualMachine 复合资源创建虚拟机，然后调用**xComputer**资源以将其重命名。

```powershell

configuration RenameVM
{

    Import-DscResource -Module TestCompositeResource
    Node localhost
    {
        xVirtualMachine VM
        {
            VMName = "Test"
            SwitchName = "Internal"
            SwitchType = "Internal"
            VhdParentPath = "C:\Demo\VHD\RTM.vhd"
            VHDPath = "C:\Demo\VHD"
            VMStartupMemory = 1024MB
            VMState = "Running"
        }
    }

    Node "192.168.10.1"
    {
        xComputer Name
        {
            Name = "SQL01"
            DomainName = "fourthcoffee.com"
        }
    }
}
```

## 另请参阅
### 概念
* [编写自定义与 MOF DSC 资源](authoringResourceMOF.md)
* [开始使用 Windows PowerShell 所需的状态配置](overview.md)

