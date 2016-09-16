---
title: "使用 DSC Nano 服务器上"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: a8faf242fcc8c72461d6cb7609a562fbb92dfdb9
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 使用 DSC Nano 服务器上

> 适用于︰ Windows PowerShell 5.0

**DSC Nano 服务器上的**是一个可选包中的`NanoServer\Packages`Windows Server 2016 媒体的文件夹。 当您通过指定**Microsoft NanoServer DSC 程序包**为**新建 NanoServerImage**函数的参数的**包**中的值创建 VHD Nano 服务器的则可以安装程序包。 例如，如果您正在创建虚拟机 VHD，命令将如下如下所示︰

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

有关安装和使用 Nano 服务器，以及如何管理使用远程 PowerShell 处理 Nano 服务器的信息，请参阅[开始使用 Nano 服务器](https://technet.microsoft.com/en-us/library/mt126167.aspx)。


## DSC Nano 服务器上可用的功能

 Nano 服务器支持仅相比完整版本的 Windows Server 的 Api 的有限的集，因为 DSC Nano 服务器上的没有完整功能奇偶与 DSC 目前完整 Sku 上运行。 DSC Nano 服务器上的处于活动状态的开发，尚未完成的功能。
 
 以下 DSC 功能目前 Nano 服务器上︰ 


* 推送和拉入模式

* 所有 DSC cmdlet 存在于完整版本的 Windows Server，包括以下内容︰ 
  * [获取 DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx)
  * [设置 DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx)   
  * [启用 DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx)
  * [禁用 DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx)       
  * [开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx)
  * [停止 DscConfiguration](https://technet.microsoft.com/en-us/library/mt143542.aspx)
  * [获取 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx)
  * [测试 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx)      
  * [发布 DscConfiguraiton](https://technet.microsoft.com/en-us/library/mt517875.aspx) 
  * [更新 DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx)
  * [还原 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407383.aspx)
  * [删除 DscConfigurationDocument](https://technet.microsoft.com/en-us/library/mt143544.aspx)
  * [获取 DscConfigurationStatus](https://technet.microsoft.com/en-us/library/mt517868.aspx)
  * [调用 DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx)
  * [查找 DscResource](https://technet.microsoft.com/en-us/library/mt517874.aspx)
  * [获取 DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)
  * [新 DscChecksum](https://technet.microsoft.com/en-us/library/dn521622.aspx)    

* 编译的配置 （请参阅[DSC 配置](configurations.md)）

  **问题︰**密码加密 （请参阅[保护 MOF 文件](securemof.md)） 配置期间编译不起作用。

* 编译的 metaconfigurations （请参阅[配置本地配置管理器](metaConfig.md)）

* 运行在用户的上下文资源 （请参阅[使用用户凭据 (RunAs) 运行 DSC](runAsUser.md)）

* （请参阅[编写自定义 DSC 资源与 PowerShell 类](authoringResourceClass.md)） 的基于类的资源

* Debugging 的 DSC 资源 （请参阅[调试 DSC 资源](debugresource.md)）
  
  **问题︰**如果使用 PsDscRunAsCredential 资源不起作用 （请参阅[使用用户凭据运行 DSC](runAsUser.md)）

* [指定跨节点相关性](crossNodeDependencies.md) 

* [资源版本控制](sxsResource.md)

* 提取客户端 （配置和资源） （请参阅[使用配置名称提取客户端设置](pullClientConfigNames.md)）

* [部分配置 （提取和推送）](partialConfigs.md)

* [向提取服务器报告](reportServer.md) 

* MOF 加密

* 事件日志记录

* Azure 自动化 DSC 报告

* 齐全的资源
  * [存档](archiveResource.md)
  * [环境](environmentResource.md)
  * [文件](fileResource.md)
  * [日志](logResource.md)
  * ProcessSet
  * [注册表](registryResource.md)
  * [脚本](scriptResource.md)
  * WindowsPackageCab
  * [WindowsProcess](windowsProcessResource.md)
  * WaitForAll （请参阅[指定跨节点相关性](crossNodeDependencies.md)）
  * WaitForAny （请参阅[指定跨节点相关性](crossNodeDependencies.md)）
  * WaitForSome （请参阅[指定跨节点相关性](crossNodeDependencies.md)）

* 资源的部分功能
  * [组](groupResource.md)
  * GroupSet
  
  **问题︰**资源上方失败如果特定实例调用两次 （运行相同的配置两次）
  
  * [服务](serviceResource.md)
  * ServiceSet
  
  **问题︰**仅适用于启动/停止 （状态） 服务。 如果一个尝试更改例如 startuptype、 凭据、 说明等其他服务属性，失败... 引发错误是类似于︰
  
  *找不到类型 [management.managementobject]: 验证是否加载包含此类型的程序集。*
  
* 均无法正常工作的资源
  * [用户](userResource.md)
  

## DSC Nano 服务器上不可用的功能

下面的 DSC 功能当前尚不提供 Nano 服务器上︰

* 使用密码加密的解密 MOF 文档 
* 提取服务器--您不能当前设置 Nano 服务器上提取服务器
* 不在功能的工作方式的列表中的任何内容

## 使用自定义 DSC 资源 Nano 服务器上
 
由于 Windows Api 和 CLR 库 Nano 服务器上可用的有限集，不一定支持 DSC 资源的完整的 CLR 版本的 Windows 上工作在 Nano 服务器。 完成到生产环境中部署 DSC 的任何自定义资源之前的端到端测试。

## 另请参阅
- [入门 Nano 服务器](https://technet.microsoft.com/en-us/library/mt126167.aspx)

