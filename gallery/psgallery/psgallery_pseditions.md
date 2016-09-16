# 兼容的 PowerShell 版本的项目
从开始版本 5.1，PowerShell 是这表示不同的功能集和平台兼容性的不同版本中可用。

- **桌面版︰**在.NET Framework 内置并提供与脚本和模块设定 PowerShell 的 Windows Server 核心如和 Windows 台式机的完整资源消耗版本上运行的版本兼容性。
- **核心版︰**基于.NET 核心，并提供与脚本和定位版本的 Windows，如 Nano Server 和 Windows IoT 缩减资源消耗版本上运行的 PowerShell 模块的兼容性。

## PowerShell 库提取支持的 PSEditions 元数据，并允许您筛选器项目兼容的特定 PowerShell 版本

如果项目具有兼容 PSEditions 指定，将被列为 PowerShell 版本的一部分的项目显示页面，也在结果中的项目。
![与 PSEditions 项显示页面](Images/ItemDisplayPageWithPSEditions.PNG)

## 在库 UI 其工作方式在 PowerShellCore 中搜索项目
使用标记:"PSEdition_Desktop"和标记:"PSEdition_Core"筛选器 PowerShell 库中的项目。

### 使用标记:"PSEdition_Core"以搜索与 PowerShell 核心版本兼容的项目。
![项目与核心 PSEdition 兼容的搜索结果](Images/SearchResultsWithPSEditions.PNG)

### 使用标记:"PSEdition_Desktop"以搜索与 PowerShell 桌面版兼容的项目。
![项目与桌面 PSEdition 兼容的搜索结果](Images/SearchResultsWithPSEdition_Desktop.PNG)

## 创作和查找兼容 PowerShell 版本与项目的详细信息
### [带有 PSEditions 模块](../psget/module/modulewithpseditionsupport.md)
### [与 PSEditions 脚本](../psget/script/scriptwithpseditionsupport.md)