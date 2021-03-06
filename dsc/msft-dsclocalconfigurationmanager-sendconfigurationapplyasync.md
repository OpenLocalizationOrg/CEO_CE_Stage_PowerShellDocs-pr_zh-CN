---
title: "MSFT_DSCLocalConfigurationManager 类 SendConfigurationApplyAsync 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 41177f2eb2bbcf2dddaf232141fb483efaaeeea5
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 SendConfigurationApplyAsync 方法

将配置文档异步发送到托管节点并使用配置代理应用配置。

语法
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

参数
----------

*配置数据*\[in\]  
配置的环境数据。

*强制*\[in\]  
**true**强制要停止的配置。

*作业 Id*\[in\]  
要为其发送配置作业的 ID。

## 返回值
------------

返回的零成功;否则将返回错误代码。

## 说明

这是静态的方法。

## 要求
------------
>**MOF:**DscCore.mof

>**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration


## 另请参阅


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)


 

 



