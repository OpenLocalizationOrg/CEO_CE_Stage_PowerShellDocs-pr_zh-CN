---
title: "MSFT_DSCLocalConfigurationManager 类"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: b9cb89bb120151df69e3cb26b50c3a0d15c23711
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 课堂

本地配置管理器 (LCM) 来控制的配置文件的状态，并且使用配置代理应用配置。

下面的语法简化从托管对象格式 (MOF) 代码，包括所有继承属性。

## 语法
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## 成员
-------

**MSFT_DSCLocalConfigurationManager**课堂具有以下成员︰

-   [方法][]

### 方法

**MSFT_DSCLocalConfigurationManager**类具有这些方法。

|方法 |说明 |
|:--- |:---|
| [ApplyConfiguration](msft-dsclocalconfigurationmanager-applyconfiguration.md)| 使用配置代理应用挂起的配置。| 
| [DisableDebugConfiguration](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| 禁用 DSC 资源调试。| 
| [EnableDebugConfiguration](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| 启用 DSC 资源调试。| 
| [GetConfiguration](msft-dsclocalconfigurationmanager-getconfiguration.md)| 配置文档将发送到管理节点并使用配置代理的**获取**方法应用配置。| 
| [GetConfigurationResultOutput](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| 获取配置代理输出将与特定的作业相关联。| 
| [GetConfigurationStatus](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| 获取配置状态历史记录。| 
| [GetMetaConfiguration](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| 获取用于控制配置代理 LCM 设置。| 
| [PerformRequiredConfigurationChecks](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| 启动一致性检查。| 
| [RemoveConfiguration](msft-dsclocalconfigurationmanager-removeconfiguration.md)| 删除的配置文件。| 
| [ResourceGet](msft-dsclocalconfigurationmanager-resourceget.md)| 直接呼叫 DSC 资源的**获取**方法。| 
| [ResourceSet](msft-dsclocalconfigurationmanager-resourceset.md)| 直接呼叫 DSC 资源的**设置**方法。| 
| [ResourceTest](msft-dsclocalconfigurationmanager-resourcetest.md)| 直接呼叫 DSC 资源的**测试**方法。| 
| [回滚](msft-dsclocalconfigurationmanager-rollback.md)| 将返回到以前的配置。| 
| [SendConfiguration](msft-dsclocalconfigurationmanager-sendconfiguration.md)| 配置文档将发送到托管节点并将其保存为挂起的更改。| 
| [SendConfigurationApply](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| 配置文档将发送到托管节点并使用配置代理应用配置。| 
| [SendConfigurationApplyAsync](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| 配置文档发送到管理节点并开始使用配置代理应用配置。 使用 GetConfigurationResultOutput 检索结果输出。| 
| [SendMetaConfigurationApply](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| 设置用于控制配置代理 LCM 设置。| 
| [StopConfiguration](msft-dsclocalconfigurationmanager-stopconfiguration.md)| 停止正在进行配置。| 
| [TestConfiguration](msft-dsclocalconfigurationmanager-testconfiguration.md)| 配置文档将发送到托管节点并验证对文档的当前配置。| 



 

## 要求
------------
>**MOF:**DscCore.mof

>**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration



 

 



