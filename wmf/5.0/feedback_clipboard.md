# 剪贴板 cmdlet
**获取剪贴板**和**设置剪贴板**使您更轻松地传输到和 Windows PowerShell 会话的内容。 例如，如果您使用 Windows 资源管理器将三个文件复制到剪贴板 (通过选择它们并按`ctrl-c`，例如)，您就可以轻松地访问剪贴板的内容作为文件的列表︰

```powershell 
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


剪贴板 cmdlet 支持图像、 音频文件，文件列表和文本。
