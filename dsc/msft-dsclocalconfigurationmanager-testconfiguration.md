---
title: "MSFT_DSCLocalConfigurationManager 类 TestConfiguration 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 0777467d37e2f5588f9c0ef368148e3bea963a5b
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 TestConfiguration 方法

将配置文档发送到管理节点并验证对文档的当前配置。

语法
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

参数
----------

*配置数据*\[in\]  
环境 confuguration 的数据。

*InDesiredState*\[出\]  
返回指定托管的节点是否配置文档所指定的状态。

*ResourcesInDesiredState*\[出\]  
返回时，包含指定所需的状态的资源的**MSFT_ResourceInDesiredState**类的嵌入式的实例。

*ResourcesNotInDesiredState*\[出\]  
返回时，包含指定未中所需的状态的资源的**MSFT_ResourceNotInDesiredState**类的嵌入式的实例。

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


 

 



