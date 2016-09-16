---
title: "示例模板中的已知问题或限制 writeup"
contributor: 
ms.openlocfilehash: e3b98044902cb6665e06582c8259bd5defd6f2ca
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
>注意︰ 提供建议的描述性标题和简短说明

## 示例︰ 错误 ExecutionPolicy 错误 ##
在 Windows 7 中，使用 PowerShell 模块和 DSC 资源可能会导致报告 ExecutionPolicy 有关的错误。

### 解决方法

若要解决，请通过在提升的 PowerShell 会话 （以管理员身份运行） 中运行以下命令设置**RemoteSigned** **ExecutionPolicy** :

```powershell
Set-ExecutionPolicy RemoteSigned
```
