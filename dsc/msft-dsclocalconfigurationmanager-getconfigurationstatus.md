---
title: "MSFT_DSCLocalConfigurationManager 类 GetConfigurationStatus 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: b430e98c7ec287c0efcf2c2e2736253797242904
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 GetConfigurationStatus 方法

获取配置状态历史记录。

语法
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

参数
----------

*所有*\[in\]  
在计算机上，包括配置应用程序和一致性检查上运行的是**true**如果此方法应返回所有配置的信息。

*configurationStatus*\[出\]  
返回，包含嵌入的实例的**MSFT_DSCConfigurationStatus**类的定义的设置。

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


 

 



