---
title: "MSFT_DSCLocalConfigurationManager 类 ResourceSet 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: cbc499f293aad941d40fcb720ef53e832c3b1ea8
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 ResourceSet 方法

直接呼叫 DSC 资源的**设置**方法。

语法
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
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

*RebootRequired*\[出\]  
返回时，此属性设置为**true**如果目标节点需要重新启动。

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

 

 



