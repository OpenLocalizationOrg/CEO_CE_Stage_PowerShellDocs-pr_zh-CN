---
title: "MSFT_DSCLocalConfigurationManager 类 SendConfiguration 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 95b141472d9428cee71b6970fc1f496704211c0b
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 SendConfiguration 方法

将配置文档发送到管理节点并将其保存为挂起的更改。

语法
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

参数
----------

*配置数据*\[in\]  
配置的环境数据。

*强制*\[in\]  
**true**强制要停止的配置。

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


 

 



