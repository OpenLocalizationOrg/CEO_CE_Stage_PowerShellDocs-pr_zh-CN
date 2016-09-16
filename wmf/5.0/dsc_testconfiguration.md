# 测试 DscConfiguration cmdlet 支持引用配置

已更新测试 DscConfiguration cmdlet 以允许通过指定要进行比较的参考配置文档所需的配置状态的一个或多个目标节点测试。

下面的新参数设置仅测试到指定的路径中使用 DSC 配置和永远不会在指定的目标的节点上应用的每个配置。 如同开始 DscConfiguration 和其他 DSC cmdlet，每个 MOF 名称用于确定哪个目标节点上测试配置。 

```PowerShell
Test-DscConfiguration   [-Path] <string> 
                        [[-ComputerName] <string[]>] 
                        [-Credential <pscredential>] 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]

Test-DscConfiguration   [-Path] <string> 
                        -CimSession <CimSession[]> 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]
```

下面的新参数设置使用单个 DSC 配置仅测试和永远不会在指定的目标的节点上应用配置。 

```PowerShell
Test-DscConfiguration   -ReferenceConfiguration <string> 
                        [[-ComputerName] <string[]>]
                        [-Credential <pscredential>] 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]

Test-DscConfiguration   -ReferenceConfiguration <string> 
                        -CimSession <CimSession[]> 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]
```
