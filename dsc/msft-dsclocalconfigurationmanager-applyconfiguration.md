---
title: "MSFT_DSCLocalConfigurationManager 类 ApplyConfiguration 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 6f9c6a8851732574ac72bc4f3a3db1a73fbbecf2
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 ApplyConfiguration 方法

使用配置代理应用挂起的配置。 

如果没有配置挂起，此方法重新应用当前配置。


## 语法
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## 参数
----------

*强制*\[in\]  
如果是**这样**，则将重新应用当前配置，即使没有正在等待配置。

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

 

 



