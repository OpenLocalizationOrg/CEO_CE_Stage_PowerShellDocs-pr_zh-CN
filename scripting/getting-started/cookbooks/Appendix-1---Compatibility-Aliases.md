---
title: "附录 1 兼容性别名"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 4474d3f078021cb1799597c866cba481d2e30e04
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 附录 1-兼容性别名
Windows PowerShell 有几个切换别名，允许 UNIX 和 Cmd 用户可在 Windows PowerShell 中使用熟悉的命令名称。 以及别名和标准的 Windows PowerShell 别名，如果存在后面的 Windows PowerShell 命令，在下表中显示的最常见的别名。

您可以找到任何别名指向从 Windows PowerShell 中使用获取别名 cmdlet 的 Windows PowerShell 命令。 例如，键入**获取别名 cls**。

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|CMD 命令|UNIX 命令|PS 命令|PS 别名|
|---------------|----------------|--------------|------------|
|**dir**|**ls**|**获取 ChildItem**|**gci**|
|**cls**|**清除**|**清除主机**（函数）|N/A|
|**del，擦除、 rmdir**|**rm**|**删除项目**|**ri**|
|**复制**|**cp**|**复制项目**|**ci**|
|**移动**|**mv**|**移动项目**|**英里**|
|**重命名**|**mv**|**重命名项目**|**rni**|
|**类型**|**猫**|**获取内容**|**gc**|
|**cd**|**cd**|**设置位置**|**sl**|
|**医师**|**mkdir**|**新项**|**ni**|
|N/A|**pushd**|**推送位置**|N/A|
|N/A|**popd**|**Pop 位置**|N/A|

