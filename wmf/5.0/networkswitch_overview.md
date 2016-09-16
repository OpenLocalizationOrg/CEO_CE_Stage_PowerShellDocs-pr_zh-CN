# 使用 PowerShell 网络切换管理

此时将**获取 NetworkSwitchEthernetPort** cmdlet 返回实例与以下附加信息︰
-   Ip 地址 – 与端口相关联的 IP 地址
-   PortMode-端口模式︰ access、 路由或 trunk
-   AccessVLAN – 与此端口中访问模式关联的 VLAN ID
-   TrunkedVLANList – 与 trunk 模式中此端口关联的 Id 的 Vlan 列表

## 使用 Windows PowerShell 的基本网络切换管理
在第一个 WMF 5.0 预览中，引入网络切换 cmdlet 使您能够适用于 Windows Server 2012 R2 徽标认证的网络开关的虚拟 LAN (VLAN) 与基本 2 层网络切换端口配置切换。 Microsoft 仍为支持[数据中心抽象](http://technet.microsoft.com/en-us/cloud/dal.aspx)层 (DAL) 视力，并显示值的客户和合作伙伴此空间中的已提交。 使用这些 cmdlet 可执行︰

-   全局切换配置，如︰
    -   设置主机名
    -   设置切换横幅
    -   持久配置
    -   启用或禁用功能

-   VLAN 配置︰
    -   创建或删除 VLAN
    -   启用或禁用 VLAN
    -   枚举 VLAN
    -   设置为 VLAN 的友好名称

-   图层 2 端口配置︰
    -   枚举端口
    -   启用或禁用端口
    -   设置端口模式和属性
    -   添加或关联到 Trunk 或访问端口 VLAN

开始通过查找所有 NetworkSwitch cmdlet 来浏览 ！

```powershell
PS> Get-Command *-NetworkSwitch*

| CommandType | Name                                      | Source        |
|-------------|-------------------------------------------|---------------|
|             |                                           |               |
| Function    | Disable-NetworkSwitchEthernetPort         | NetworkSwitch |
| Function    | Disable-NetworkSwitchFeature              | NetworkSwitch |
| Function    | Disable-NetworkSwitchVlan                 | NetworkSwitch |
| Function    | Enable-NetworkSwitchEthernetPort          | NetworkSwitch |
| Function    | Enable-NetworkSwitchFeature               | NetworkSwitch |
| Function    | Enable-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Get-NetworkSwitchEthernetPort             | NetworkSwitch |
| Function    | Get-NetworkSwitchFeature                  | NetworkSwitch |
| Function    | Get-NetworkSwitchGlobalData               | NetworkSwitch |
| Function    | Get-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | New-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | Remove-NetworkSwitchEthernetPortIPAddress | NetworkSwitch |
| Function    | Remove-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Restore-NetworkSwitchConfiguration        | NetworkSwitch |
| Function    | Save-NetworkSwitchConfiguration           | NetworkSwitch |
| Function    | Set-NetworkSwitchEthernetPortIPAddress    | NetworkSwitch |
| Function    | Set-NetworkSwitchPortMode                 | NetworkSwitch |
| Function    | Set-NetworkSwitchPortProperty             | NetworkSwitch |
| Function    | Set-NetworkSwitchVlanProperty             | NetworkSwitch |
```

获得 Jeffrey Snover WMF 5.0 预览发布博客文章中的详细信息︰ <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx>
