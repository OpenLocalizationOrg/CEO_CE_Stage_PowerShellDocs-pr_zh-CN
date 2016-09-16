# 生成基于 OData 终结点的 PowerShell Cmdlet
生成基于 OData 终结点的 Windows PowerShell cmdlet
--------------------------------------------------------------

**导出 ODataEndpointProxy**是生成基于给定的 OData 终结点公开的功能的 Windows PowerShell cmdlet 一组 cmdlet。

下面的示例显示如何使用此新 cmdlet:

\# 导出 ODataEndpointProxy 基本使用大小写

```powershell
Export-ODataEndpointProxy -Uri 'http://services.odata.org/v3/(S(snyobsk1hhutkb2yulwldgf1))/odata/odata.svc' -OutputModule C:\Users\user\Generated.psd1

ipmo 'C:\Users\user\Generated.psd1'
# Cmdlets are created based on the following heuristics
# New-<EntityType> -<Key> [-<Other Attributes>]
#
# Get-<EntityType> [-<Key> -Top –Skip –Filter -OrderBy]
# # If there is a complex key, the keys will actually be -<Key1> -<Key2>…
# # Note this rule applies to any other instances of the key
#
# Set-<EntityType> -<Key> [-<Other Attributes>]
#
# Remove-<EntityType> -<Key>
#
# Invoke-<EntityType><Action> [-<Key> -<Other Parameters>]
#
#
# Cmdlets from associations (Note: Get and Remove get additional parameter sets)
# Get-<EntityType> -<AssociatedEntity>
# New-<EntityType> -<AssociatedEntity> -<Key>
# Remove-<EntityType> -<AssociatedEntity> -<Key>
#
#
# Note: Every cmdlet has the –ConnectionURI parameter for explicitly setting the URI of the endpoint. This normally uses the same address that you gave the Export-ODataEndpointProxy cmdlet, but can be overridden in this fashion for the sake of similar endpoints.
#
```

仍然有关键使用案例中的这一功能，包括但不是限于开发的部分内容︰
-   关联
-   传递流

生成基于起止 OData ODataUtils 的 Windows PowerShell cmdlet
------------------------------------------------------------------------------
ODataUtils 模块允许生成从支持 OData 的其余部分终结点的 Windows PowerShell cmdlet。 以下增量增强功能是 Microsoft.PowerShell.ODataUtils Windows PowerShell 模块中。
-   渠道从服务器端终结点到客户端的其他信息。
-   客户端分页支持
-   使用服务器端筛选-选择参数
-   支持 web 请求标头

导出 ODataEndPointProxy cmdlet 生成的代理 cmdlet 提供附加信息 （不在客户端代理生成 $metadata 中提到） 从服务器端 OData 终结点信息流 （新的 Windows PowerShell 5.0 功能）。 下面介绍了如何获取该信息的示例。
```powershell
Import-Module Microsoft.PowerShell.ODataUtils -Force
$generatedProxyModuleDir = Join-Path -Path $env:SystemDrive -ChildPath 'ODataDemoProxy'
$uri = "http://services.odata.org/V3/(S(fhleiief23wrm5a5nhf542q5))/OData/OData.svc/"
Export-ODataEndpointProxy -Uri $uri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -AllowClobber
Import-Module $generatedProxyModuleDir -Force

# In the below command, we are retrieving top 1 product.
# By specifying -IncludeTotalResponseCount parameter,
# we are getting the total count of all the Product records
# available on the server side. This information
# is surfaced on the client side through the Information stream.
$product = Get-Product -Top 1 -AllowUnsecureConnection -AllowAdditionalData -IncludeTotalResponseCount -InformationVariable infoStream
# The Information stream contains the additional
# information sent from the server side.
$additionalInfo = $infoStream.GetEnumerator() | % MessageData
# 'Odata.Count' indicates the total product records
# available on the server side Odata endpoint.
$additionalInfo['odata.count']
```

使用客户端分页支持，您可以从服务器端分批获取记录。 当您必须从服务器收到大量数据通过网络时，这很有用。
```powershell
$skipCount = 0
$batchSize = 3
# Client-Side Paging Support: The records from the server side
# are retrieved in batches of $batchSize
while($skipCount -le $additionalInfo['odata.count'])
{
Get-Product -AllowUnsecureConnection -AllowAdditionalData -Top $batchSize -Skip $skipCount
$skipCount += $batchSize
}
```

生成的代理 cmdlet 支持-选择参数，您可以将其作为筛选器接收客户端所需的记录属性。 这将减少通过网络，传输的数据的数量，因为服务器端筛选发生。
```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

导出 ODataEndpointProxy cmdlet 和代理 cmdlet 生成的现在支持页眉参数 （供应值为哈希表），它可用于通道预期服务器端 OData 终结点的任何其他信息。 在下面的示例中，您可以通道订阅通过页眉服务需要身份验证的订阅键的键。
```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```
