# 存档 cmdlet

两个新 cmdlet**压缩存档**和**展开存档**，允许您将压缩并展开 ZIP 文件。

## 压缩存档
**压缩存档**cmdlet 指定文件中创建新的存档文件。 存档文件允许打包和选择性地压缩到一个文件以便于处理和存储多个文件。 可以通过使用**-CompressionLevel**参数中指定的压缩算法压缩存档文件。
```PowerShell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>] 
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## 展开存档
**展开存档**cmdlet 指定的存档文件中提取的文件。 存档文件允许打包和选择性地压缩到一个文件以便于处理和存储多个文件。
```PowerShell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```
