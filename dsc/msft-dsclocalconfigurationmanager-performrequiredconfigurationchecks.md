---
title: "MSFT_DSCLocalConfigurationManager 类 PerformRequiredConfigurationChecks 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: f9eb975845f6ccabcac80e2591fd987f80f81331
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 PerformRequiredConfigurationChecks 方法

使用任务计划程序启动一致性检查。

语法
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

参数
----------

*标志*\[in\]  
指定运行一致性检查的类型的位掩码。 为以下值有效，而且可以组合使用按位**或**运算︰

|值 |说明 |
|:--- |:---|
|**1** | 普通的一致性检查。 |
|**2** | 重新启动后的一致性检查延续。 此值应不能与其他值。 |
|**4** | 配置应来自节点 metaconfiguration 中指定的提取服务器。 此值应始终与结合使用**1**， **5**的值。 |
|**8** | 发送到报表服务器状态。 |

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


 

 



