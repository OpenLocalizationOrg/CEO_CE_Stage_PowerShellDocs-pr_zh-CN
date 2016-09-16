---
title: "DSC 类资源改进"
author: jaimeo
contributor: amitsara
ms.openlocfilehash: c0d5ee3428ea6a40b18b20ac97de411b12f4f488
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
## DSC 类资源改进

在此版本中，我们已修复以下已知问题从 WMF 5.0:
* 获取 DscConfiguration 可能会返回空值 （空） 或错误如果类 Get() 函数不返回复数/哈希表类型基于 DSC 资源。
* 如果在 DSC 配置使用 RunAs 凭据，则将获取 DscConfiguration 返回错误。
* 复合配置中，不能使用基于类资源。
* 开始 DscConfiguration 挂起如果课堂基于资源具有其自己的类型的属性。
* 基于课堂资源不能用作独占的资源。
