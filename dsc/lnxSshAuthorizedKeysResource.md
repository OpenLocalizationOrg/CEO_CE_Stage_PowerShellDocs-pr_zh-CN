---
title: "Linux nxSshAuthorizedKeys 资源的 DSC"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: edc906b4e9c925320c4ed00c5ab295189066ccb9
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 为 Linux nxSshAuthorizedKeys 资源的

**NxAuthorizedKeys**资源 PowerShell 需要状态配置 (DSC) 中提供了一种机制来管理授权 ssh 指定用户的快捷键。

## 语法

```
nxAuthorizedKeys <string> #ResourceName
{
    KeyComment = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Username = <string> ]
    [ Key = <string> ]
    [ DependsOn = <string[]> ]

}
```

## 属性

|  属性 |  说明 | 
|---|---|
| KeyComment| 唯一键批注。 这用于唯一标识键。| 
| 确保| 指定是否定义键。 设置此属性为"无"以确保用户授权的键文件中不存在的键。 将其设置为"演示"，以确保用户授权关键文件中定义键。| 
| 用户名| 若要管理 ssh 用户名授权的快捷键。 如果未定义，默认用户是"根目录"。| 
| 键| 项内容。 如果**确保**设置为"演示"，这是必需的。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 示例

下面的示例定义公共 ssh 授权的用户"monuser"键。

```
Import-DSCResource -Module nx 

Node $node {

nxSshAuthorizedKeys myKey{
   KeyComment = "myKey"
   Ensure = "Present"
   Key = 'ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEA0b+0xSd07QXRifm3FXj7Pn/DblA6QI5VAkDm6OivFzj3U6qGD1VJ6AAxWPCyMl/qhtpRtxZJDu/TxD8AyZNgc8aN2CljN1hOMbBRvH2q5QPf/nCnnJRaGsrxIqZjyZdYo9ZEEzjZUuMDM5HI1LA9B99k/K6PK2Bc1NLivpu7nbtVG2tLOQs+GefsnHuetsRMwo/+c3LtwYm9M0XfkGjYVCLO4CoFuSQpvX6AB3TedUy6NZ0iuxC0kRGg1rIQTwSRcw+McLhslF0drs33fw6tYdzlLBnnzimShMuiDWiT37WqCRovRGYrGCaEFGTG2e0CN8Co8nryXkyWc6NSDNpMzw== rsa-key-20150401'
   UserName = "monuser"
} 
}
```

