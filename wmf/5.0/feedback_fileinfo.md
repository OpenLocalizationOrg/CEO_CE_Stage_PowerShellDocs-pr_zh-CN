# 对 FileInfo 对象的更新
文件版本信息可能会产生误导，尤其是在该文件已修补位置的情况下。 此版本的 WMF 5.0 将新**FileVersionRaw**和**ProductVersionRaw**脚本属性添加到 FileInfo 的对象。 下面是为 powershell.exe （假设 $pid PowerShell 进程的 ID） 显示属性︰

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117
