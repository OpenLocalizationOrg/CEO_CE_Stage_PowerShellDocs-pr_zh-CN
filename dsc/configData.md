---
title: "分离配置和环境的数据"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: e1cf91111288edf4bce5cbf1d9ad953a7442b93d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 分离配置和环境数据

>适用于︰ Windows PowerShell 4.0，Windows PowerShell 5.0

在 Windows PowerShell 需要状态配置 (DSC)，则可以从您的配置的逻辑分隔配置数据。 另一种方法可以看到这是要考虑的结构配置 （例如，配置可能需要安装 IIS） 从环境配置为单独 (即，这种情况是否与生产其中一个测试环境 — 节点名称将有所不同，但为其应用配置都是相同的)。 这具有以下优点︰

* 它可以重复使用不同的资源、 节点和配置您配置数据。
* 配置逻辑是更可重用如果它不包含硬编码的数据。 这是类似于好脚本准则的函数。
* 如果某些数据需要更改，您可以在一个位置，进行更改，从而节省时间并减少错误。

## 基本概念和示例

若要指定环境配置的一部分，DSC 使用**配置数据**参数，这是哈希表 （或可能需要一些.psd1 文件，其中包含哈希表）。 此哈希表必须至少一个键**所有节点均**，即为结构化的值。 例如︰

```powershell
$MyData = 
@{
    AllNodes = @()
    NonNodeData = ""   
}
```

请注意其值为数组的所有节点均键。 此数组中的每个元素也是哈希表，这需要键节点名称︰

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName = "VM-1"
        },

 
        @{
            NodeName = "VM-2"
        },

 
        @{
            NodeName = "VM-3"
        }
    );

    NonNodeData = ""   
}
```

所有节点均在每个哈希表项对应于配置数据中配置的节点。 除了所需的节点名称密钥，您可以添加其他键到哈希表，例如︰

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName = "VM-1"
            Role     = "WebServer"
        },

 
        @{
            NodeName = "VM-2"
            Role     = "SQLServer"
        },

 
        @{
            NodeName = "VM-3"
            Role     = "WebServer"
        }
    );

    NonNodeData = ""   
}
```

DSC 提供了特殊的三个变量中配置脚本用于︰

* **$AllNodes**︰ 引用的所有节点。 您可以使用与**筛选。Where()**和**。ForEach()**，因此，而不是硬编码节点名称来选择特定节点的操作，可以编写此选项来选择虚拟机 1 和虚拟机 3 在上面的示例类似︰

```powershell
configuration MyConfiguration
{
    node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
    }
}
```

* **$Node**︰ 后的节点集进行筛选，您可以使用 $Node 引用特定项。 例如︰

```powershell
configuration MyConfiguration
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite
    node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = "Present"
        }
    }
}
```

若要应用于所有节点的属性，您可以设置节点名称 ="*"。 例如，要为每个节点 LogPath 属性，可以执行此操作︰

```
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName           = "*"
            LogPath            = "C:\Logs"
        },

 
        @{
            NodeName = "VM-1"
            Role     = "WebServer"
            SiteContents = "C:\Site1"
            SiteName = "Website1"
        },

 
        @{
            NodeName = "VM-2"
            Role     = "SQLServer"
        },

 
        @{
            NodeName = "VM-3"
            Role     = "WebServer"
            SiteContents = "C:\Site2"
            SiteName = "Website3"
        }
    );
}
```

* **$ConfigurationData**︰ 您可以使用此配置内的变量访问配置数据哈希表作为参数传递。 例如︰

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName           = "*"
            LogPath            = "C:\Logs"
        },

 
        @{
            NodeName = "VM-1"
            Role     = "WebServer"
            SiteContents = "C:\Site1"
            SiteName = "Website1"
        },

 
        @{
            NodeName = "VM-2"
            Role     = "SQLServer"
        },
 

        @{
            NodeName = "VM-3"
            Role     = "WebServer"
            SiteContents = "C:\Site2"
            SiteName = "Website3"
        }
    );

    NonNodeData = 
    @{
        ConfigFileContents = (Get-Content C:\Template\Config.xml)
     }   
} 

configuration MyConfiguration
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = "Present"
        }

        File ConfigFile
        {
            DestinationPath = $Node.SiteContents + "\\config.xml"
            Contents = $ConfigurationData.NonNodeData.ConfigFileContents
        }
    }
}
```

您可以找到[xWebAdministration 模块](https://powershellgallery.com/packages/xWebAdministration)中包括一个完整的示例。

