---
title: "MSFT_DSCLocalConfigurationManager 类 RemoveConfiguration 方法"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 4f3d74949d98e3ab3f5136303e229c23ed903c5d
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# MSFT_DSCLocalConfigurationManager 类 RemoveConfiguration 方法

删除的配置文件。

语法
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

参数
----------

*阶段*\[in\]  
指定要删除的配置文档。 为以下值是有效的︰

|值 |说明 |
|:--- |:---|
|**1** | **当前**配置文档 (current.mof)。 |
|**2** | **等待**配置文档 (pending.mof)。  |
|**4** | **前一节**配置文档 (previous.mof)。 |

*强制*\[in\]  
**true**强制配置的删除。

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


 

 



