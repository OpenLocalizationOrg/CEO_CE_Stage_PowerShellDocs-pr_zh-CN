---
title: "DSC 为 Linux nxScript 资源的"
ms.date: 2016-05-16
keywords: powershell DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 4c575bbf0e0553e19e56bcc6edd605e36586cb94
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# DSC 为 Linux nxScript 资源的

**NxScript**资源 PowerShell 需要状态配置 (DSC) 中提供的机制 Linux 节点上运行 Linux 脚本。

## 语法

```
nxScript <string> #ResourceName
{
    GetScript = <string>
    SetScript = <string>
    TestScript = <string>
    [ User = <string> ]
    { Group = <string> ]
    [ DependsOn = <string[]> ]

}
```

## 属性

|  属性 |  说明 | 
|---|---|
| GetScript| 提供了当您调用[获取 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet 运行脚本。 脚本必须开头 shebang，例如 # ！ / 箱/狂欢。| 
| SetScript| 提供了脚本。 当您调用[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet 时，首先**TestScript**运行。 如果**TestScript**块返回退出代码 0 之外，将运行**SetScript**块。 如果**TestScript**返回退出代码为 0，则不会运行**SetScript** 。 脚本必须以 shebang，如`#!/bin/bash`。| 
| TestScript| 提供了脚本。 当您调用[开始 DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet 时，运行此脚本。 如果它返回退出代码 0 之外，将运行 SetScript。 如果它返回的退出代码为 0，则不会运行**SetScript** 。 当您调用[测试 DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet，也将运行**TestScript** 。 但是，这种情况下， **SetScript**将无法运行，无论从**TestScript**返回哪些退出代码。 如果不匹配， **TestScript**必须返回 0; 如果实际配置匹配的当前的所需的状态配置退出代码和退出代码 0 之外。 （当前所需的状态配置为使用 DSC 节点代理的最后一个配置）。 脚本必须开头 shebang，如 1#!/bin/bash.1| 
| 用户| 若要运行该脚本为用户。| 
| 组| 要运行该脚本为的组。| 
| 取决于 | 表示此资源配置之前，必须运行的另一个资源配置。 例如，如果您想要运行该资源配置脚本块**ID**首先是**资源名称**和其类型是**资源类型**，使用此属性的语法是`DependsOn = "[ResourceType]ResourceName"`。| 

## 示例

下面的示例演示如何以执行其他配置管理的**nxScript**资源使用。

```
Import-DSCResource -Module nx 

Node $node {
nxScript KeepDirEmpty{

    GetScript = @"
#!/bin/bash
ls /tmp/mydir/ | wc -l
"@

    SetScript = @"
#!/bin/bash
rm -rf /tmp/mydir/*
"@

    TestScript = @'
#!/bin/bash
filecount=`ls /tmp/mydir | wc -l`
if [ $filecount -gt 0 ]
then
    exit 1
else
    exit 0
fi
'@
} 
}
```

