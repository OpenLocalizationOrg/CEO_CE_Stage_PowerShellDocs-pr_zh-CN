# 库搜索语法

PowerShell 库提供了文本搜索位置使用的单词、 短语和关键字表达式来缩小搜索结果。

## 按关键字搜索

    dsc azure sql

搜索将执行其最大努力，以查找包含所有的 3 个关键字相关的文档，并返回匹配的文档。

## 使用短语和关键字搜索

    "azure sql" deployment

引号之间输入某个短语 ("") 更改搜索以查找特定短语，而不是单独的关键字。
匹配文档应通常包含完全匹配短语"azure sql"，包括的变体大写例如"Azure SQL"，并通常还包含字词部署。

## 筛选的字段

您可以搜索特定项目 ID （或 Id 或 id），或某些其他字段前加上搜索条款与字段名称。

当前的搜索字段是 Id、 版本、 标记、 作者、 所有者、 函数、 Cmdlet'、 'DscResources' 和 'PowerShellVersion。

[什么是 ID 和标题之间的区别？ ID 是控制台中使用的名称。 标题是在搜索结果中的项目页面的顶部显示的内容。

## 示例

    ID:"PSReadline"
    id:"AzureRM.Profile"

分别在其 ID 字段中查找"PSReadline"或"AzureRM.Profile"的项目。

    Id:"AzureRM.Profile"

是另一种方法来查找其 ID 字段"AzureRM.Profile"的项目。

Id 筛选器是子字符串匹配，这样如果搜索以下事项︰

    Id:"azure"
    
您将获得 AzureRM.Profile' 和 'Azure.Storage' 等的结果。

您也可以搜索单个字段中的多个关键字。 或混合并匹配字段。

    id:azure tags:intellisense
    id:azure id:storage

并且，您可以执行短语搜索︰

    id:"azure.storage"


若要搜索 DSC 标记的所有项目。

    Tags:"DSC"

若要搜索与指定的函数的所有项目。

    Functions:"Update-AzureRM"

若要搜索与指定的 cmdlet 的所有项目。
    
    Cmdlets:"Get-AzureRmEnvironment"

若要搜索具有指定 DSC 资源名称的所有项目。

    DscResources:"xArchive"

若要搜索与指定 PowerShellVersion 的所有项目

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


最后，如果您使用的域，我们不支持，如命令，我们只需将忽略它并搜索所有字段。 因此关注查询

    commands:blobs storage
    
已将被解释为此查询完全相同︰

    blobs storage

