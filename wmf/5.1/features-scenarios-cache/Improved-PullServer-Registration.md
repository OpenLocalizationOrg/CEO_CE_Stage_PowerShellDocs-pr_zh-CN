---
title: "改进的提取服务器登记"
author: jaimeo
contributor: Indhu Sivaramakrishnan
ms.openlocfilehash: 1419bb0d74855d40f214292a817b854cec695309
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
## 改进的提取服务器注册 ##

在早期版本的 WMF，simulataneous 报告登记/请求到 DSC 拉出服务器使用 ESENT 数据库时将导致 LCM 无法注册和/或，具体情况而定的报表。 在这种情况下，提取服务器上的事件日志将有错误"已在使用实例名称"。
这是由于模式不正确用于访问 ESENT 数据库中的多线程方案。 在 WMF 5.1 已修复此问题。 并发登记或报告 （涉及 ESENT 数据库） 将 WMF 5.1 中正常工作。 此问题仅适用于 ESENT 数据库并不适用于 OLEDB 数据库。 
