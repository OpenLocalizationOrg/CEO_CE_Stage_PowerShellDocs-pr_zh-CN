# 保存脚本

保存脚本 cmdlet 使您可以通过将其保存到指定位置查看脚本文件。

## 说明

保存脚本 cmdlet 保存指定的脚本。

## Cmdlet 语法

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## Cmdlet 联机帮助引用

[保存脚本](http://go.microsoft.com/fwlink/?LinkId=619786)

## 示例命令

### 示例 1︰ 保存从库中的脚本
此命令将保存的最新版本的脚本仕-ClientScript GalleryINT 存储库从本地文件夹 C:\ScriptSharingDemo

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### 示例 2︰ 通过从查找脚本 cmdlet 的管道保存的版本的脚本

第一个命令查找版本 1.5 的 GalleryINT 资源库中的仕 ClientScript 并将其保存到文件夹 C:\ScriptSharingDemo

第二个命令验证已保存的脚本元数据。

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```
