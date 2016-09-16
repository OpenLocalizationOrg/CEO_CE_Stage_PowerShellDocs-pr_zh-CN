---
title: "DSC 为 Linux nxService 资源的"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 3835495705297616a41329bcfdaad42b464115d8
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# Linux nxService 资源的 DSC

**NxService**资源 PowerShell 需要状态配置 (DSC) 中提供的机制来管理 Linux 节点中的服务。

## 语法

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | system }  ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]

}
```

## 属性
|  属性 |  说明 | 
|---|---|
| 名称| 服务/后台程序配置的名称。| 
| 控制器| 若要配置该服务时使用的服务控制器的类型。| 
| 启用| 指示服务是否启动时启动。| 
| 状态| 指示服务是否正在运行。 设置此属性为"已停止"以确保不运行该服务。 将其设置为"运行"以确保不运行该服务。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 


## 其他信息

如果不存在， **nxService**资源将不会创建一个服务定义或服务的脚本。 您可以使用 PowerShell 需要状态配置**nxFile**资源资源管理服务定义文件或脚本的内容存在。

## 示例

下面的示例显示使用**SystemD**服务控制器注册 （适用于 Apache HTTP 服务器），"httpd"服务配置。

```
Import-DSCResource -Module nx 

Node $node {
#Apache Service
nxService ApacheService 
{
Name = "httpd"
State = "running"
Enabled = $true
Controller = "systemd"
}
}
```

