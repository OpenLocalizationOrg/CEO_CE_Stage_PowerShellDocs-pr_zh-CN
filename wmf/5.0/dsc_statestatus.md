# 统一且保持一致的状态和状态表示形式

在此版本中的内置 LCM 状态和 DSC 状态的自动化进行了一系列的增强功能。 这些包括统一且保持一致的状态和状态代表、 易于管理的 datetime 属性的状态对象由获取 DscConfigurationStatus cmdlet 返回和增强获取 DscLocalConfigurationManager cmdlet 返回 LCM 状态的详细信息属性。

LCM 状态和 DSC 操作状态的表示形式再次访问和统一根据以下规则︰
1.  LCM 状态和 DSC 状态，不会影响 Notprocessed 资源。
2.  LCM 停止处理其他资源后遇到请求重新启动资源。
3.  请求重新启动资源不在所需的状态，直到重新启动实际的情况。
4.  遇到失败的资源之后, LCM 保留进一步处理资源，只要它们不是依赖于一个失败。
5.  获取 DscConfigurationStatus cmdlet 返回的整体状态是超级组的所有资源状态。
6.  PendingReboot 状态是超集 PendingConfiguration 状态。

下表说明了结果状态相关的一些典型的情况下的属性。

| **方案**                    | **LCMState\***       | **状态** | **重新启动请求**  | **ResourcesInDesiredState**  | **ResourcesNotInDesiredState** |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| S**^**                          | 空闲                 | 成功    | $false        | S                            | $null                          |
| F**^**                          | PendingConfiguration | 失败    | $false        | $null                        | F                              |
| S、 F                             | PendingConfiguration | 失败    | $false        | S                            | F                              |
| F、 S                             | PendingConfiguration | 失败    | $false        | S                            | F                              |
| S<sub>1</sub>, F, S<sub>2</sub> | PendingConfiguration | 失败    | $false        | S<sub>1</sub>, S<sub>2</sub> | F                              |
| F<sub>1</sub>, S, F<sub>2</sub> | PendingConfiguration | 失败    | $false        | S                            | F<sub>1</sub>, F<sub>2</sub>   |
| S、 r                            | PendingReboot        | 成功    | $true         | S                            | r                              |
| F、 r                            | PendingReboot        | 失败    | $true         | $null                        | F、 r                           |
| r、 S                            | PendingReboot        | 成功    | $true         | $null                        | r                              |
| r F                            | PendingReboot        | 成功    | $true         | $null                        | r                              |

^
S<sub>我</sub>︰ 成功应用 F 的资源的一系列<sub>我</sub>︰ 一系列应用未成功需要重新启动的: A 资源的资源
\*

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```
## 在获取 DscConfigurationStatus cmdlet 的增强功能

一些增强功能进行了此版本中获取 DscConfigurationStatus cmdlet。 以前，由 cmdlet 返回的对象的开始日期属性是字符串类型。 现在，它是 Datetime 类型，使复杂选择和筛选变得更容易根据内部的 Datetime 对象属性。
```powershell
(Get-DscConfigurationStatus).StartDate | fl \*
DateTime : Friday, November 13, 2015 1:39:44 PM
Date : 11/13/2015 12:00:00 AM
Day : 13
DayOfWeek : Friday
DayOfYear : 317
Hour : 13
Kind : Local
Millisecond : 886
Minute : 39
Month : 11
Second : 44
Ticks : 635830187848860000
TimeOfDay : 13:39:44.8860000
Year : 2015
```

下面是一个示例返回今天为一周的同一天发生了变化 DSC 操作的所有记录。
```powershell
(Get-DscConfigurationStatus –All) | where { $\_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

消除了对 （即阅读仅操作） 的节点的配置不会进行任何更改的操作的记录。 因此，测试-DscConfiguration 获取 DscConfiguration 操作不再 adulterated 中从获取 DscConfigurationStatus cmdlet 返回对象。
元配置设置操作的记录将添加到获取 DscConfigurationStatus cmdlet 返回。

下面是从获取 DscConfigurationStatus 返回的结果的示例-所有 cmdlet。
```powershell
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## 在获取 DscLocalConfigurationManager cmdlet 的增强功能
LCMStateDetail 的新字段将添加到从获取 DscLocalConfigurationManager cmdlet 返回的对象。 此字段将填充 LCMState 时"忙碌"。 它可通过以下 cmdlet:
```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

下面是连续监视配置远程节点上的两个重启所需的输出实例。
```powershell
Start a configuration that requires two reboots

Monitor LCM State:
LCM State: Busy, LCM is applying a new configuration.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: Idle,
LCM State: Busy, LCM is performing a consistency check.
LCM State: Idle,
```
