# 模块分析缓存 #

PowerShell 从版 5.1 开始，提供以下控制用缓存数据，如命令模块有关的文件，其导出。

默认情况下，在文件中存储此缓存`${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`。
缓存搜索命令时在启动时通常读取并写入后台线程上一段时间后模块导入。

若要更改缓存的默认位置，请先 PowerShell 设置环境变量 PSModuleAnalysisCachePath。 对此环境变量的更改仅会影响子流程。
值应名称 PowerShell 有权创建和写入文件的完整路径 （包括文件名）。
若要禁用文件缓存-此值可以设置为无效的位置例如

```PowerShell
$env:PSModuleAnalysisCachePath = 'nul'
```

此设置无效的设备的路径。 如果 PowerShell 无法写入路径，尽管您可以查看错误报告追踪通过无错误︰

```PowerShell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

编写出缓存时, 将检查 PowerShell 不再存在以避免不必要地大缓存的模块。
有时这些检查都不需要，在这种情况下您可以将其关闭通过设置

```PowerShell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

设置此环境变量将会立即生效当前进程中。