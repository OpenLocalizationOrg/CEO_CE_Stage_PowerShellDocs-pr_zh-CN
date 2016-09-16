---
title: "功能或方案 writeup 的模板示例"
contributor: KeithB
ms.openlocfilehash: 025565404b60cebefac27e51c70d70edb5e47bc9
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
>注意︰ 提供建议的描述性标题和简短说明

## PowerShellGet 增强功能 ##
WMF 5.1 中已经有很大更新 PowerShellGet 模块中的 cmdlet。 现在支持以下新方案︰

- **代理支持︰**使用内部的代理 PowerShellGet cmdlet 现在支持，代理和 ProxyCredential 参数查找、 安装-、 保存和发布 cmdlet 的所有 PowerShellGet 模块中添加了 (例如︰ 查找模块、 安装-模块保存模块，发布模块)。 
- **强制目录签名︰**现在，所有 PowerShellGet cmdlet 检查并实施更新的签名的模块。 将通过 PowerShellGet cmdlet，以确保模块不已修改传输，并更新到模块可能仅来自原始 publisher 检查使用新的目录 cmdlet 签名的模块。 这会影响安装模块和更新模块 cmdlet。 
- **共享和获取角色功能︰**角色功能是终结点定义用于配置只需足够管理以限制，并将通过 PowerShell 模块中 PowerShell 库共享。 Cmdlet 包括查找-RoleCapability 和新建 PSRoleCapabilityFile。 
- **查找命令︰**查找命令使用户可以在其中包含正在寻找命令 PowerShell 库中找到模块。 
- **身份验证库︰**Visual Studio 包管理源需要身份验证，现在支持通过 PowerShellGet cmdlet 的内容。

用户反馈标识改进附加 5.1，包括未涉及的区域︰

- **安装脚本更改︰**使用安装脚本的位置不加入 5.1 中自动用户路径。 此更改 PowerShellGet，独立版本中进行，并且现在正在 WMF 5.1。
- **将元数据字段添加到现有的脚本︰**更新 ScriptFileInfo 可在现有的脚本添加到 PowerShellGallery 发布所需的默认元数据字段。 以前，用户需要手动将此合并到一个现有的脚本。
- **发布到库的更低版本控制模块︰**现在，可以将发布到库使用发布模块于当前以前最高的版本更低版本数字模块。 Publisher 发布版本 2.0.0 其模块与重大更改 1.x 版本中的，如果他们无法轻松地释放到版本 1.5.0 修复。 现在，他们可以发布 1.5.1，来改善维护库中的 PowerShell 模块的支持。 
- **安装脚本和模块时检查命令覆盖︰**安装模块和安装脚本现在将检查包含已存在系统的命令，将通过默认出的错误如果发生这种情况。 
- **中发布 cmdlet 引导 Nuget:**以前是无法使用发布模块或发布-脚本，做某些自动化任务很难时自动安装 Nuget 提供商。 用户可能现在添加-强制转换为发布命令绕过该提示。 

>注意︰ 更多详细信息，其中涵盖了新的概念、 实施工作结束后，示例等应链接到的规范技术文档

**了解有关使用 PowerShellGet**
- [有关 CatalogSigning]()
- []()
- [获取模块按筛选结果 CompatiblePSEditions]()
- [防止执行脚本，除非在 PowerShell 兼容版本上运行]()



