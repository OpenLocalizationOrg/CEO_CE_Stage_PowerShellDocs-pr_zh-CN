---
title: "PowerShell 引擎改进 WMF 5.1 （预览）"
ms.date: 2016-07-13
keywords: "PowerShell，DSC WMF"
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 118cb91528824b75e28a1eadaa377a696c67f2dd
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
#PowerShell 引擎改进

已在 WMF 5.1 实现核心 PowerShell 引擎的以下改进︰


## 性能 ##

改进了性能，一些重要方面︰

- 启动
- 管道到 ForEach 对象和位置对象之类的 cmdlet 大约是 50%更快 

（您的结果可能会有所不同，具体取决于您的硬件） 一些示例改进︰ 

| 方案 | 5.0 时间 （毫秒） | 5.1 时间 （毫秒） |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | 900 | 250 |
| 首先以往 PowerShell 运行︰ `powershell -command "Unknown-Command"` | 30000 | 13000 |
| 内置命令分析缓存︰ `powershell -command "Unknown-Command"` | 7000 | 520 |
| <code>1..1000000 &#124; % { }</code> | 1400 | 750 |
  
> 注意与启动相关的一次更改可能会影响某些不支持的方案。 
> PowerShell 不再读取文件`$pshome\*.ps1xml`--这些文件已转换为 C# 以避免某些文件和 CPU 开销的处理 XML 文件。 
文件仍然存在到支持 V2 通过并行，因此如果您更改了该文件的内容，它将没有 v5，仅 V2 任何效果。 
请注意，更改这些文件的内容从未受支持的方案。

另一个可见更改是如何 PowerShell 缓存导出命令和系统安装的模块的其他信息。 此缓存存储在目录中以前， `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`。 在 WMF 5.1 缓存是单个文件`$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`。
更多详细信息，请参阅[模块分析缓存](scenarios-features.md#module-analysis-cache)。
