# 注册 PowerShell 资源库
您可以配置 PowerShellGet 操作对内部存储库。 这是通过使用添加了以下内容︰
- 注册-PSRepository︰ 注册当前用户存储库。
- 注销 PSRepository︰ 删除当前用户的已注册的知识库。
- 设置-PSRepository︰ 设置值已注册的知识库。
- 获取-PSRepository︰ 获取当前用户的所有已注册存储库。

注册存储库后，您可以使用查找模块和安装模块对其进行处理。

```powershell
\#Register a default repository
Register-PSRepository –Name DemoRepo –SourceLocation “https://www.myget.org/F/powershellgetdemo/api/v2” –PublishLocation “<https://www.myget.org/F/powershellgetdemo/api/v2>/package” –InstallationPolicy –Trusted

\#Get all of the registered repositories
Get-PSRepository
Name SourceLocation
---- --------------
PSGallery https://msconfiggallery.cloudapp...
DemoRepo https://www.myget.org/F/powershe...

\#Search only the new repository for modules
Find-Module -Repository DemoRepo
Repository Version Name
---------- ------- ----
DemoRepo 1.0.1 xActiveDirectory
DemoRepo 1.1.1 SomeModule

\#By default, PowerShellGet operates against all registered repositories when none is specified. In this example, the “SomeModule” module is installed from the DemoRepo.
Install-Module SomeModule

\#Removing a repository
Unregister-PSRepository DemoRepo
```