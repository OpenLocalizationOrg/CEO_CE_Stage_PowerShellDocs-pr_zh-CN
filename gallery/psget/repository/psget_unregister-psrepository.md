# 注销 PSRepository

注销存储库。

## 说明

注销 PSRepository cmdlet 注销为当前用户存储库。
- 注销然后重新注册 PSGallery 存储库的允许的企业版和断开连接方案。
- 用户可以通过只需运行重新注册 PSGallery `Register-PSRepository -Default`
- 由于 PSGallery 是默认中发布模块和发布脚本 cmdlet 发布存储库中，如果 PSGallery 不可用已注册的知识库列表中，将引发错误。

## Cmdlet 语法

```powershell
Get-Command -Name Unregister-PSRepository -Module PowerShellGet -Syntax
```
## Cmdlet 联机帮助引用

[注销 PSRepository](http://go.microsoft.com/fwlink/?LinkID=517130)

## 示例命令

```powershell
Unregister-PSRepository -Name "MyPrivateGallery"

Get-PSRepository exp | Unregister-PSRepository
```

### 注销然后重新注册 PSGallery 存储库的允许的企业版和断开连接的方案。
```powershell

# Unregister PSGallery repository
Unregister-PSRepository PSGallery

# Publish-Module throws an error when PSGallery is not a registered repository
Publish-Module -Name MyModule
publish-module : Unable to find repository 'PSGallery'. Use Get-PSRepository to see all available repositories. Try again after specifying a valid repository name. You can use 'Register-PSRepository -Default' to register the PSGallery repository.
At line:1 char:1
+ publish-module -name mymodule
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (PSGallery:String) [Publish-Module], ArgumentException
    + FullyQualifiedErrorId : PSGalleryNotFound,Publish-Module

# Re-register PSGallery repository
Register-PSRepository -Default
```