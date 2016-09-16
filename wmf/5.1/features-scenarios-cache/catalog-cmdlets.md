
---
标题︰ 目录 Cmdlet 作者︰ jaimeo 参与者:？
---
# 目录 Cmdlet  

我们有[Microsoft.Powershell.Secuity](https://technet.microsoft.com/en-us/library/hh847877.aspx)模块生成并验证 windows 目录文件中添加两个新 cmdlet。  

新 FileCatalog 
--------------------------------

新的文件目录 windows 目录为创建文件的文件夹和文件。 目录文件包含指定的路径中的所有文件哈希。 用户可以分发以及表示这些文件夹的相应目录文件的文件夹的设置。 它可通过接收器的内容来验证如果目录创建时间后的文件夹进行任何更改。    

```PowerShell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
我们支持创建目录版本 1 和 2。 版本 1 使用 SHA1 哈希算法来创建文件哈希和 2 使用 SHA256 的版本。 在*Windows Server 2008 R2*和*Windows 7*中不支持目录版本 2。 建议使用目录版本 2，如果使用的平台*Windows 8*、 *Windows Server 2012*和上方。  

若要在现有模块中使用此命令，指定 CatalogFilePath 和路径变量，以匹配模块清单的位置。 在下面的示例中，该模块清单位于 C:\Program Files\Windows PowerShell\Modules\Pester。 

![](../../images/NewFileCatalog.jpg)

这将创建目录文件。 

![](../../images/CatalogFile1.jpg)  

![](../../images/CatalogFile2.jpg) 

若要验证的目录文件 (在上述示例 Pester.cat) 完整性它应签名使用[设置 AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet。   


测试 FileCatalog 
--------------------------------

测试文件目录验证目录表示一组文件夹。 

```PowerShell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../../images/TestFileCatalog.jpg)

此 cmdlet 比较所有文件哈希和它们是*磁盘*上的*目录*中找到的相对路径。 如果检测到任何文件哈希和路径，并且提供状态作为*ValidationFailed*之间的不匹配。 用户可以检索所有此信息使用*-详细*标志。 它还表示这是与目录文件中的呼叫[获取 AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) cmdlet 相同的*签名*中显示签名状态的目录。 用户可以跳过任何文件验证期间通过使用*-FilesToSkip*参数。 

