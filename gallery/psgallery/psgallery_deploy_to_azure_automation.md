
部署到 Azure 自动化
===========================

部署到项目详细信息页面上的 Azure 自动化按钮将部署到 Azure 自动化 PowerShell 库中的项目。

![部署到 Azure 自动化按钮](Images/DeployToAzureAutomationButton.png)

单击时，它将您重定向到 Azure 管理门户中，您在使用 Azure 帐户凭据登录的位置。
如果项目包括相关性，所有相关项将部署到 Azure 自动化也。

警告︰ 如果自动化帐户中已有的相同的项目和版本，从 PowerShell 库再次部署将覆盖您的自动化帐户中的项。

如果您部署模块，它将显示在模块部分中的 Azure 自动化。  如果您部署脚本，它将显示在运行手册部分中的 Azure 自动化。

可以通过添加到项目元数据 AzureAutomationNotSupported 标记禁用部署到 Azure 自动化按钮。

若要了解有关 Azure 自动化的详细信息，请参阅 Azure 自动化网站[Azure 自动化网站](http://azure.microsoft.com/en-us/services/automation/)。

