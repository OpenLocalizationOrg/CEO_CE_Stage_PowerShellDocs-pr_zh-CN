---
title: "MSFT_DSCLocalConfigurationManager 类 ResourceGet 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 1666b85402f17230090f7290c8cb400dd9fbf0a6
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 ResourceGet 方法

直接呼叫 DSC 资源的**获取**方法。

语法
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

参数
----------

*资源类型*\[in\]  
要呼叫的资源的名称。

*ModuleName*\[in\]  
包含要呼叫的资源的模块的名称。

*resourceProperty*\[in\]  
指定资源属性名称及其值哈希表中为键和值，分别。 [获取 DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet 用于发现资源属性和它们的类型。

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


 

 



