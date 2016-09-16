# 系统要求

- 安装最新的 Windows 更新安装 WMF 5.0 RTM 之前。
- 您可以仅在以下操作系统中安装 WMF 5.0 RTM:

    | 操作系统       | 版本         | 先决条件        |  包链接 |
    |------------------------|--------------|------------------|----------------------| --------------|
    | Windows Server 2012 R2 |  |  | [Win8.1AndW2K12R2-KB3134758 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
    | Windows 2012 Server    |  |  | [W2K12-KB3134759 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) |
    | Windows Server 2008 R2 SP1 | 全部，除了 IA64 | [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855)和[.NET Framework 4.5 或更高](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx)一起安装| [Win7AndW2K8R2-KB3134760 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504)|
    | Windows 8.1 | Pro，企业版 | | **x64:**  [Win8.1AndW2K12R2-KB3134758 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) </br> **x86:**  [Win8.1-KB3134758 x86.msu](http://go.microsoft.com/fwlink/?LinkID=717963)|
    | Windows 7 SP1 | 所有 | [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855)和[.NET Framework 4.5 或更高](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx)一起安装 | **x64:**  [Win7AndW2K8R2-KB3134760 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504)  </br> **x86:**  [Win7-KB3134760 x86.msu](http://go.microsoft.com/fwlink/?LinkID=717962)|

# 安装说明

### 若要从 Windows 资源管理器 （或文件资源管理器） 安装 WMF 5.0:

1. 导航到 MSU 文件下载到其中的文件夹。

2. 双击以运行它 MSU。

### 若要从命令提示符安装 WMF 5.0:

1. 下载后正确包，您的计算机体系结构，使用提升的用户权限 （以管理员身份运行） 打开命令提示符窗口。 Windows Server 2012 R2 或 Windows Server 2012 或 Windows Server 2008 R2 SP1 的服务器核心安装选项，在命令提示符默认情况下打开提升的用户权限。

2. 更改目录的文件夹，其中有下载或复制 WMF 5.0 安装程序包。

3. 运行以下命令之一︰
    - 在计算机上运行的 Windows Server 2012 R2 或 Windows 8.1 x64，运行**Win8.1AndW2K12R2-KB3134758 x64.msu /quiet**。
    - 在计算机上运行的 Windows Server 2012，运行**W2K12-KB3134759 x64.msu /quiet**。
    - 在计算机上运行的 Windows Server 2008 R2 SP1 或 Windows 7 SP1 x64，运行**Win7AndW2K8R2-KB3134760 x64.msu /quiet**。
    - 在计算机上运行的 Windows 8.1 x86，运行**Win8.1-KB3134758 x86.msu /quiet**。
    - 在计算机上运行的 Windows 7 SP1 x86，运行**Win7-KB3134760 x86.msu /quiet**。

### Windows Server 2008 R2 SP1 和 Windows 7 SP1 的其他安装说明︰

确保已满足下列先决条件︰
- 安装最新 service pack。
- [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855)将安装。
- [.NET framework 4.5 或更高](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx)安装。

**WMF 4.0 依赖项**

Windows Server 2008 R2 SP1 和 Windows 7 SP1 系统有内置 PowerShell 2.0、 WinRM 和 WMI。 WMF 3.0 和 WMF 4.0 包，更新这些内置组件以后版本的 Windows Server 2008 R2 SP1 和 Windows 7 SP1, 发布。 安装卸载 WMF 3.0 和 WMF 4.0 程序包发现了以下升级路径中的一些问题︰

- 内置--> WMF 4.0
- 内置--> WMF 3.0--> WMF4.0。 

我们在 WMF 4.0 程序包修复所有这些问题。 因此，在 Windows Server 2008 R2 SP1 和 Windows 7 SP1 上安装 WMF 5.0 是 WMF 4.0 的先决条件。 下面是如果您在升级到 WMF 5.0 之前不安装 WMF 4.0 时，可能会遇到的具体问题︰

- 转发的事件日志不可用，EventCollector 日志后不会显示在事件查看器 WMF 3.0 或 WMF 5.0 （不带 WMF 4.0 安装先决条件） 卸载 Windows 7 SP1 和 Windows Server 2008 R2 SP1 ([KB2809215](https://support.microsoft.com/en-us/kb/2809215)) 中。
- 直接从 WMF 5.0 ([KB2872035](https://support.microsoft.com/en-us/kb/2872035)) 到内置 PowerShell 2.0 或到 WMF 5.0 WMF 3.0 升级时， *PSModulePath*环境变量的自定义获取重置为默认值。 ([KB2872047](https://support.microsoft.com/en-us/kb/2872047)) 在 Windows 7 SP1，然后在 Windows Server 2008 R2 SP1。

**WinRM 依赖项**

Windows PowerShell 需要状态配置 (DSC) 取决于 WinRM。 默认情况下，在 Windows Server 2008 R2 SP1 和 Windows 7 SP1 上未启用 WinRM。 若要启用 WinRM，提升 Windows PowerShell 会话，运行**设置 WSManQuickConfig**。

# 卸载说明进行操作

### 使用命令提示符

1.  打开**命令提示符。**

2.  运行[Windows 更新独立启动器](https://support.microsoft.com/en-us/kb/934307)，如下所示︰

在 Windows Server 2012 R2 和 Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
在 Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
在 Windows Server 2008 R2 SP1 和 Windows 7 SP1:
```powershell
wusa /uninstall /kb:3134760
```

### 使用控制面板

1.  打开**控制面板。**

2.  打开**程序**，然后打开**卸载程序。**

3.  单击**查看已安装的更新。**

4.  从已安装更新的列表中选择**Windows Management Framework 5.0** 。 这对应于*KB3134758*、 *KB3134759*或*KB3134760*。 单击**卸载。**
