# DSC 配置的按需拉动

新的更新 DscConfiguration cmdlet 触发提取元配置中定义提取服务器。 行为通常称为立即获取。 


一旦触发，提取完全相同的行为与相同必须何时正常频率期间触发︰

1. 当前配置的校验和与提取服务器上配置的校验和进行比较。 
2. 如果他们是相同的已成功完成而不应用配置。 
3. 如果有不同，配置拉从提取服务器，并应用。

**注意︰**如果元配置 RefreshMode = 推送以便目标节点处于推送模式时，此 cmdlet 将始终不起作用，此 cmdlet 将返回错误。

```PowerShell
Update-DscConfiguration     [[-ComputerName] <string[]>] 
                            [-Wait]
                            [-Force] 
                            [-JobName <string>] 
                            [-Credential<pscredential>] 
                            [-ThrottleLimit <int>] 
                            [-WhatIf] 
                            [-Confirm] 
                            [<CommonParameters>]

Update-DscConfiguration     -CimSession <CimSession[]> 
                            [-Wait] 
                            [-Force] 
                            [-JobName <string>] 
                            [-ThrottleLimit <int>]
                            [-WhatIf] 
                            [-Confirm] 
                            [<CommonParameters>]
```