# 安装说明

下载您的操作系统和体系结构正确的程序包︰

| 操作系统       | 体系结构 | 程序包名称              | 
|------------------------|--------------|---------------------------| 
| Windows Server 2012 R2 | x64      | [Win8.1AndW2K12R2-KB3134758 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) | 
| Windows 2012 Server    | x64      | [W2K12-KB3134759 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) | 
| Windows Server 2008 R2 | x64      | [Win7AndW2K8R2-KB3134760 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 8.1            | x64          | [Win8.1AndW2K12R2-KB3134758 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
| Windows 8.1            | x86          | [Win8.1-KB3134758 x86.msu](http://go.microsoft.com/fwlink/?LinkID=717963) |
| Windows 7 SP1          | x64          | [Win7AndW2K8R2-KB3134760 x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 7 SP1          | x86          | [Win7-KB3134760 x86.msu](http://go.microsoft.com/fwlink/?LinkID=717962) |


**若要从 Windows 资源管理器 （或 Windows Server 2012 R2 和 Windows 8.1 中的文件资源管理器） 安装 WMF 5.0:**

1. 导航到 MSU 文件下载到其中的文件夹。

2. 双击以运行它 MSU。

**若要从命令提示符安装 WMF 5.0:** 

1. 下载后正确包，您的计算机体系结构，使用提升的用户权限 （以管理员身份运行） 打开命令提示符窗口。 Windows Server 2012 R2 或 Windows Server 2012 或 Windows Server 2008 R2 SP1 的服务器核心安装选项，在命令提示符默认情况下打开提升的用户权限。

2. 更改目录的文件夹，其中有下载或复制 WMF 5.0 安装程序包。

3. 运行以下命令之一︰
    - 在计算机上运行的 Windows Server 2012 R2 或 Windows 8.1 x64，运行**Win8.1AndW2K12R2-KB3134758 x64.msu /quiet**。
    - 在计算机上运行的 Windows Server 2012，运行**W2K12-KB3134759 x64.msu /quiet**。
    - 在计算机上运行的 Windows Server 2008 R2 SP1 或 Windows 7 SP1 x64，运行**Win7AndW2K8R2-KB3134760 x64.msu /quiet**。
    - 在计算机上运行的 Windows 8.1 x86，运行**Win8.1-KB3134758 x86.msu /quiet**。
    - 在计算机上运行的 Windows 7 SP1 x86，运行**Win7-KB3134760 x86.msu /quiet**。

**Windows Server 2008 SP1 和 Windows 7 SP1 的其他安装说明︰**

确保已满足下列先决条件︰
- 安装最新 service pack。
- 安装了[WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855)

*WinRM 相关性︰*Windows PowerShell 需要状态配置 (DSC) 取决于 WinRM。 默认情况下，在 Windows Server 2008 R2 和 Windows 7 中，不会启用 WinRM。 若要启用 WinRM，提升 Windows PowerShell 会话，运行**设置 WSManQuickConfig**。


