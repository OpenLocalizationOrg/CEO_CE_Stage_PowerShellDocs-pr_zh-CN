---
title: "编写自定义与 MOF DSC 资源"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 78407eff4df1c63c35205e235d614538aad231ee
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 编写自定义与 MOF DSC 资源

> 适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

在本主题中，我们将在 MOF 文件中，定义的架构 Windows PowerShell 需要状态配置 (DSC) 自定义资源并实现 Windows PowerShell 脚本文件中的资源。 此自定义资源是用于创建和维护网站。

## 创建 MOF 架构

架构定义您可以通过 DSC 配置脚本来配置的资源的属性。

### 为 MOF 资源文件夹结构

若要实现与 MOF 架构 DSC 自定义资源，创建以下文件夹结构。 Demo_IISWebsite.schema.mof，文件中定义的 MOF 架构和资源脚本定义 Demo_IISWebsite.psm1 中。 （可选） 您可以创建模块清单 (psd1) 文件。

```
$env:PSModulePath (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

请注意，就需要创建一个文件夹下的顶级，名为 DSCResources 文件夹和文件夹的每个资源都必须具有相同资源的名称。

### MOF 文件的内容

以下是可用于自定义网站资源示例 MOF 文件。 要关注此示例中，将此架构保存到一个文件，并调用*Demo_IISWebsite.schema.mof*的文件。

```
[ClassVersion("1.0.0"), FriendlyName("Website")] 
class Demo_IISWebsite : OMI_BaseResource
{
  [Key] string Name;
  [Required] string PhysicalPath;
  [write,ValueMap{"Present", "Absent"},Values{"Present", "Absent"}] string Ensure;
  [write,ValueMap{"Started","Stopped"},Values{"Started", "Stopped"}] string State;
  [write] string Protocol[];
  [write] string BindingInfo[];
  [write] string ApplicationPool;
  [read] string ID;
};
```

请注意以下有关以前的代码︰

* `FriendlyName` 定义您可以使用，请参阅此 DSC 配置脚本中的自定义资源的名称。 在此示例中，`Website`等同于友好名称`Archive`内置存档资源。
* 对于自定义资源必须派生自定义类`OMI_BaseResource`。
* 类型限定符`[Key]`，请在一个属性指示此属性将唯一标识资源实例。 至少一个`[Key]`属性是必需的。
* `[Required]`限定符指示属性是必需 （必须使用此资源的任何配置脚本中指定的值）。
* `[write]`限定符指示此属性是可选的当在配置脚本中使用自定义资源。 `[read]`限定符指示属性不能通过配置，设置和适用于报告目的。
* `Values` 限制可分配给到中定义值列表属性的值`ValueMap`。 有关详细信息，请参阅[返回和值限定符](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx)。
* 包括的属性称为`Ensure`面额`Present`和`Absent`在您的资源建议作为一种方式维护内置 DSC 资源一致的样式。
* 命名自定义资源的架构文件，如下所示︰ `classname.schema.mof`，其中`classname`是后面的标识符`class`架构定义中的关键字。

### 编写资源脚本

资源脚本实现的资源的逻辑。 在此模块中，您必须包括称为**获取 TargetResource**、**设置 TargetResource**和**测试 TargetResource**的三个函数。 这三个函数都必须采取 MOF 架构创建您的资源中定义的属性集相同参数集。 在文档中，这种属性集称为"资源属性"。 存储这些文件中的三个函数调用<ResourceName>.psm1。 在下面的示例中，函数存储在一个名为 Demo_IISWebsite.psm1 文件。

> **注意**︰ 当您资源上运行相同的配置脚本多次、 应接收没有错误和资源都应保持为一次运行该脚本相同的状态。 若要完成此操作，确保**获取 TargetResource**和**测试 TargetResource**函数将保持不变，资源，并且具有相同的参数值的序列中多次调用**设置 TargetResource**函数始终相当于一次调用它。

**获取 TargetResource**函数实施工作结束后，在使用提供的关键资源属性值作为参数来检查指定的资源实例的状态。 此函数必须返回列出作为键，这些属性相应的值的实际值的所有资源属性哈希表。 下面的代码提供的示例。

```powershell
# DSC uses the Get-TargetResource function to fetch the status of the resource instance specified in the parameters for the target machine
function Get-TargetResource 
{
    param 
    (       
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

        $getTargetResourceResult = $null;

        <# Insert logic that uses the mandatory parameter values to get the website and assign it to a variable called $Website #>
        <# Set $ensureResult to "Present" if the requested website exists and to "Absent" otherwise #>

        # Add all Website properties to the hash table
        # This simple example assumes that $Website is not null
        $getTargetResourceResult = @{
                                      Name = $Website.Name; 
                                        Ensure = $ensureResult;
                                        PhysicalPath = $Website.physicalPath;
                                        State = $Website.state;
                                        ID = $Website.id;
                                        ApplicationPool = $Website.applicationPool;
                                        Protocol = $Website.bindings.Collection.protocol;
                                        Binding = $Website.bindings.Collection.bindingInformation;
                                    }
  
        $getTargetResourceResult;
}
```

根据指定的配置脚本中的资源属性的值，**设置 TargetResource**必须执行下列操作之一︰

* 创建新网站
* 更新现有网站
* 删除现有网站

下面的示例阐释了这一点。

```powershell
# The Set-TargetResource function is used to create, delete or configure a website on the target machine. 
function Set-TargetResource 
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param 
    (       
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )
 
    <# If Ensure is set to "Present" and the website specified in the mandatory input parameters does not exist, then create it using the specified parameter values #>
    <# Else, if Ensure is set to "Present" and the website does exist, then update its properties to match the values provided in the non-mandatory parameter values #>
    <# Else, if Ensure is set to "Absent" and the website does not exist, then do nothing #>
    <# Else, if Ensure is set to "Absent" and the website does exist, then delete the website #>
}
```

最后，**测试 TargetResource**函数必须执行相同的参数设置为**获取 TargetResource**和**设置 TargetResource**。 在**测试 TargetResource**实现，选中关键参数中指定的资源实例的状态。 如果资源实例的实际状态与参数设置中指定的值不匹配，则返回**$false**。 否则，返回**$true**。

下面的代码实现**测试 TargetResource**函数。

```powershell
function Test-TargetResource
{
[CmdletBinding()]
[OutputType([System.Boolean])]
param
(
[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[parameter(Mandatory = $true)]
[System.String]
$Name,

[parameter(Mandatory = $true)]
[System.String]
$PhysicalPath,

[ValidateSet("Started","Stopped")]
[System.String]
$State,

[System.String[]]
$Protocol,

[System.String[]]
$BindingData,

[System.String]
$ApplicationPool
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


#Include logic to 
$result = [System.Boolean]
#Add logic to test whether the website is present and its status mathes the supplied parameter values. If it does, return true. If it does not, return false.
$result 
}
```

**注意**︰ 更容易调试，使用以前的三个函数的实现中**编写详细**cmdlet。 此 cmdlet 写入详细邮件流的文本。 默认情况下，不显示详细的邮件流，但可以通过更改**$VerbosePreference**变量的值或使用中 DSC cmdlet 的**详细**参数显示新 =。

### 创建模块清单

最后，使用**新 ModuleManifest** cmdlet 来定义<ResourceName>.psd1 文件以供您自定义资源的模块。 当您调用此 cmdlet 时，参考上一节中所述的脚本模块 (.psm1) 文件。 若要导出的函数的列表中包括**获取 TargetResource**、**设置 TargetResource**和**测试 TargetResource** 。 下面是一个示例清单的文件。

```powershell
# Module manifest for module 'Demo.IIS.Website'
#
# Generated on: 1/10/2013
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '6AB5ED33-E923-41d8-A3A4-5ADDA2B301DE'

# Author of this module
Author = 'Contoso'

# Company or vendor of this module
CompanyName = 'Contoso'

# Copyright statement for this module
Copyright = 'Contoso. All rights reserved.'

# Description of the functionality provided by this module
Description = 'This Module is used to support the creation and configuration of IIS Websites through Get, Set and Test API on the DSC managed nodes.'

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '4.0'

# Minimum version of the common language runtime (CLR) required by this module
CLRVersion = '4.0'

# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @("WebAdministration")

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @("Demo_IISWebsite.psm1")

# Functions to export from this module
FunctionsToExport = @("Get-TargetResource", "Set-TargetResource", "Test-TargetResource")

# Cmdlets to export from this module
#CmdletsToExport = '*'

# HelpInfo URI of this module
# HelpInfoURI = ''
}
```

