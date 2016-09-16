---
title: "MSFT_DSCLocalConfigurationManager 类 GetConfiguration 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 19d4790f22491e0bb11de1e315d1ee3b07929d55
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 GetConfiguration 方法

将配置文档发送到管理节点并使用配置代理的**获取**方法应用配置。

语法
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

参数
----------

*配置数据*\[in\]  
指定要发送的配置数据。

*配置*\[出\]  
返回，包含配置的嵌入式的实例。

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
 

 



