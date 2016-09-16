---
title: "提取部分配置命名约定"
author: jaimeo
contributor: berheabrha
ms.openlocfilehash: 4e4c742ea8c2b6b2f94b0ad08da4202e6045bda1
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
##提取部分配置命名约定
在早期版本中，为一个完整的配置的命名约定时 mof 文件名中提取服务器 /service 应该匹配的本地配置管理器设置中指定的部分配置名称又具有匹配 MOF 文件中嵌入的配置名称。 请参阅下面的快照:-定义允许节点收到一个完整的配置 • 本地配置设置。

![示例 metaconfiguration](../../images/MetaConfigPartialOne.png)

• 示例部分配置定义 

```Powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test 
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

• 生成 MOF 文件中的配置名嵌入。

![示例生成的 mof 文件](../../images/PartialGeneratedMof.png)

• 提取配置存储库中的文件名 

![配置存储库中的文件名](../../images/PartialInConfigRepository.png)

Azure 自动化服务生成名称 mof 文件作为``<ConfigurationName>.<NodeName>.mof``。 因此下面的配置将编译到 PartialOne.Localhost.mof。  
这使得无法提取配置与 Azure 自动化服务的部分。

```Powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test 
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

在 WMF 5.1 提取服务中的部分配置可以命名为``<ConfigurationName>.<NodeName>.mof``。 此外，如果计算机提取提取从一种配置服务配置文档然后在提取服务器配置库可以具有任何名称。 此命名灵活性使管理部分配置使用 onprem 和 Azure 自动化提取服务节点。 例如，您可以获取本地推送的基本部分配置和另一个完整的配置，获取从 Azure 自动化服务请求。

下面 metaconfiguration 将设置要管理的节点本地既 Azure 自动化服务。

```Powershell
  [DscLocalConfigurationManager()]
   Configuration RegistrationMetaConfig
   {
        Settings
        {
            RefreshFrequencyMins = 30;
            RefreshMode = "PULL";            
        }

        ConfigurationRepositoryWeb web
        {
            ServerURL =  $endPoint
            RegistrationKey = $registrationKey
            ConfigurationNames = $configurationName
        }

        # Partial configuration managed by Azure Automation Service.
        PartialConfiguration PartialCOnfigurationManagedByAzureAutomation
        {
            ConfigurationSource = "[ConfigurationRepositoryWeb]Web"   
        }
    
        # This partial configuration is managed locally.
        PartialConfiguration OnPremConfig
        {
            RefreshMode = "PUSH"
            ExclusiveResources = @("Script")
        }

   }

   RegistrationMetaConfig
   slcm -Path .\RegistrationMetaConfig -Verbose
 ```


