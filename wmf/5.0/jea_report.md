# 在 JEA 报告
报告 JEA 配置的状态，以便您可以使用︰
1.  **获取 PSSessionConfiguration**返回给定的计算机上的所有已注册的终结点的列表。
2.  **获取 PSSessionCapability**报告功能的任何用户具有特定的终结点。

下面是**获取 PSSessionCapability**示例︰
```powershell
Get-PSSessionCapability -ConfigurationName Maintenance -Username "CONTOSO\JohnDoe"

CommandType     Name                                               Version    Source           
-----------     ----                                               -------    ------           
Alias           clear -> Clear-Host                                                            
Alias           cls -> Clear-Host                                                              
Alias           exsn -> Exit-PSSession                                                         
Alias           gcm -> Get-Command                                                             
Alias           measure -> Measure-Object                                                      
Alias           select -> Select-Object                                                        
Function        Clear-Host                                                                     
Function        Exit-PSSession                                                                 
Function        Get-Command                                                                    
Function        Get-FormatData                                                                 
Function        Get-Help                                                                       
Function        Get-UserInfo                                                                   
Function        Measure-Object                                                                 
Function        Out-Default                                                                    
Function        Select-Object                                                                  
Cmdlet          Restart-Service                                    3.0.0.0 Microsof...


```

要报告的_操作_用户最初 JEA 会话期间，您可以︰
1. 启用该 JEA 终结点"放在即时"脚本和信息，请阅读脚本目录的每个用户操作完整日志
2. 打开 PowerShell 模块日志记录，并检查 PowerShell 事件日志。