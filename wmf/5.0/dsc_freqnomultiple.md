# RefreshMode 和 ConfigurationMode 频率不需要的彼此的序列图

在早期版本的 DSC，对待 LCM`RefreshFrequencyMins`和`ConfigurationModeFrequencyMins`为彼此的序列图。 在 WMF 5.0 RTM，这些属性被处理相互独立。 

有关详细信息，请参阅[配置本地配置管理器](https://msdn.microsoft.com/powershell/dsc/metaconfig)。