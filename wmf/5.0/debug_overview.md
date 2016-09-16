# 改进的 PowerShell 脚本调试

PowerShell 5.0 中进行了改进的数目来增强调试体验︰

## 断开所有

PowerShell 控制台和 Windows PowerShell ISE 现在允许您用于运行脚本中断调试程序。 这在本地和远程会话中工作。

在控制台中，请按**Ctrl + 分页符**。

在 ISE，按**Ctrl + B**，，或使用**调试-> 全部中断**菜单命令。

## 远程调试和远程文件在 Windows PowerShell ISE 中进行编辑

Windows PowerShell ISE 现在可以打开和编辑远程会话中的文件，通过运行 PSEdit 命令。
例如，您可以打开要编辑的文件从命令行远程会话中，如下所示︰

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

此外，您现在可以编辑和保存到断点时自动打开 Windows PowerShell ISE 在远程文件中的更改。
现在，您可以调试远程计算机运行的脚本文件，编辑文件来修复错误，然后重新运行修改后的脚本。

## 高级的脚本调试

有新的高级调试功能，允许您连接到任何已加载 Windows PowerShell 的本地计算机进程和调试该流程中的任意运行空间。

### 运行空间调试

添加新的 cmdlet，让您列表中的过程，当前运行空间，然后将 Windows PowerShell 控制台或 ISE 调试程序附加到该运行空间的脚本调试︰

-   获取运行空间
-   调试运行空间
-   启用 RunspaceDebug
-   禁用 RunspaceDebug
-   获取 RunspaceDebug

### 附加到进程托管 PowerShell

现在可以附加到已加载的 Windows PowerShell 的任何计算机进程。 通过将输入到与该过程，类似于如何输入到交互式远程会话通过运行 Enter PSSession cmdlet 互动会话中执行以下操作︰

-   输入 PSHostProcess
-   退出 PSHostProcess