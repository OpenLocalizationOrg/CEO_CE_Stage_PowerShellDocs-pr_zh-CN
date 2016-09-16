# 已知的问题和限制

首次使用时，不保持 PowerShell 快捷方式
------------------------------------------------------------

**分辨率︰**执行下列操作之一︰

1.  右键单击 PowerShell 快捷方式。 选择"Windows PowerShell"以在非提升模式下启动。
2.  右键单击 PowerShell 快捷方式。 右键单击"Windows PowerShell"，然后选择"以管理员身份运行"以在提升模式下启动。

一旦您已执行上述操作之一，将工作 PowerShell 快捷方式。 需要一次只能执行这些操作。


有关在 Windows 7 上 ExecutionPolicy PowerShell 模块和 DSC 资源报表错误
-------------------------------------------------------------------------------------
在 Windows 7 中，使用 PowerShell 模块和 DSC 资源可能会导致报告 ExecutionPolicy 有关的错误。

**分辨率︰**通过在提升的 PowerShell 会话 （以管理员身份运行） 运行以下命令来设置 RemoteSigned ExecutionPolicy:

```powershell
Set-ExecutionPolicy RemoteSigned
```

连接到旧的远程 Exchange 终结点导致了崩溃
------------------------------------------------------------

旧 Exchange 终结点的重定向到新的终结点。 没有 bug 的重定向逻辑该结果崩溃。

**分辨率︰**直接连接到新的终结点。


在 Windows Server 2012 R2 WMF 5.0 安装后错误地停止软件库存日志记录功能
-------------------------------------------------------------------------------------------------------------

安装时 WMF 5.0 已 SIL 在运行 Windows Server 2012 R2 上，在安装后错误地停止软件库存日志记录功能。

**分辨率︰**当在安装过程错误地将停止软件库存日志记录功能，请一次 WMF 安装后，运行开始 SilLogging cmdlet。

如果同时使用-LiteralPath 和递归获取 ChildItem 不起作用
--------------------------------------------------------------------------

如果目录名称包含无效的通配符，然后获取 ChildItem 不会产生预期的结果都-LiteralPath 和-递归一起使用时。

**分辨率︰**不适合，但当前的解决方法是在脚本实施递归，而不是依赖 cmdlet。


Sysprep WMF 5.0 安装后失败
----------------------------------------

有两种解决方法此问题，具体取决于您运行的 Windows Server 的版本。

**解决方法︰**
- 对于运行**Windows Server 2008 R2**系统
  1.    以管理员身份打开 Powershell
  2.    运行以下命令
   ```powershell
    Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
   ```
  3.    运行命令和忽略错误，因为在预期。
   ```powershell
    Publish-SilData
   ```
  4.    删除 \Windows\System32\Logfiles\SIL\ 目录中的文件
  ```powershell
  Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
  ```
  5.    安装所有可用重要 Windows 更新，并开始 Sysyprep 操作正常。
  
- 对于系统运行**Windows Server 2012**
  1.    要在服务器上安装 WMF 5.0 后 Sysprep 获得的以管理员身份登录。
  2.    将 Generize.xml 从目录 \Windows\System32\Sysprep\ActionFiles\ 复制到 Windows 目录，C:\ 以外的位置，例如。
  3.    与记事本中打开 Generalize.xml 副本。
  4.    查找并删除以下文本，每个要删除的需求的一个实例 （他们将文档末尾附近）。
    ```
    <sysprepOrder order="0x3200"></sysprepOrder>
    
    <sysprepOrder order="0x3300"></sysprepOrder>
    ```
  5.    将 Generalize.xml 编辑的副本保存并关闭该文件。
  6.    以管理员身份打开命令提示符
  7.    运行以下命令以所有权 system32 文件夹中的 Generalize.xml 文件︰
    ```
      Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml 
    ```
  8.    运行以下命令以设置文件适当的权限︰
    ```
      Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F 
    ```
      * 确认提示时回答是。 
      * 请注意，`<AdministratorUserName>`应替换为计算机上的管理员的用户名。 例如，"管理员"。
      
  9.    复制的文件编辑和保存在到 Sysprep 目录使用以下命令︰
      ```
      xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml 
      ```
      * 回答是以覆盖 （请注意，如果没有提示符以覆盖，请仔细检查输入的路径）。
      * 假定您已编辑的 Generalize.xml 副本被复制到 C:\。
  10.   解决方法将立即更新 Generalize.xml。 请启用了通用化选项，运行 Sysprep。

