## 如何解决"警告︰ 下载程序包您程序包名称失败"问题？




报告，安装模块或更新模块有时会失败在某些计算机上。
根据我们的调查，它是如何与网络连接。
最近我们更新 NuGet 提供商，以便它可以可靠地下载程序包。
您可以按照下面以安装最新版本的 NuGet 提供商和重新安装或更新您的模块的说明。
下面的示例，我们来使用 Azure 模块。

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```
