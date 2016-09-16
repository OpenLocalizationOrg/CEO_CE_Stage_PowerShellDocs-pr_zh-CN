---
title: "授权规则和 windows powershell web access 的安全功能"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 0313704ee6e03277eb7c8acae3b3af2e7e74f33b
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
# 授权规则和 Windows PowerShell Web access 的安全功能

更新时间︰ 2013 2013年 6 月 24日日

适用于︰ Windows Server 2012 R2，Windows Server 2012

在 Windows Server® 2012 R2 和 Windows Server® 2012年中的 Windows PowerShell® Web Access 有严格的安全模型。 必须显式授予用户访问他们可以登录到 Windows PowerShell Web Access 网关并使用基于 web 的 Windows PowerShell 控制台前。

-   [配置授权规则和网站的安全](#BKMK_auth)

-   [会话管理](#BKMK_sesmgmt)


Windows PowerShell Web Access 的安装和配置网关后，用户可以在浏览器中，打开登录页面，但他们不能登录 Windows PowerShell Web Access 管理员授予用户访问显式直到。 Windows PowerShell Web Access 访问控制，通过使用下表中描述的 Windows PowerShell cmdlet 的组。 添加或管理授权规则存在不类似 GUI。 有关 Windows PowerShell Web Access 的 cmdlet 的详细信息，请参阅[Windows PowerShell Web Access Cmdlet](https://technet.microsoft.com/library/hh918342.aspx)的 cmdlet 参考主题。

管理员可以定义 0-*n* Windows PowerShell Web access 的身份验证规则。 默认安全设置限制，而不是许可;零身份验证规则意味着没有用户有权访问的任何内容。

添加 PswaAuthorizationRule 和 Windows Server 2012 R2 中的测试 PswaAuthorizationRule 包括允许您添加并测试 Windows PowerShell Web Access 授权规则的远程计算机或凭据参数活动的 Windows PowerShell Web Access 会话。 为使用其他 Windows PowerShell cmdlet 具有一个凭据参数中，您可以指定 PSCredential 对象作为参数的值。 若要创建包含您要传递到远程计算机的凭据 PSCredential 对象，请运行[获取凭据](https://technet.microsoft.com/library/hh849815.aspx)cmdlet。

Windows PowerShell Web Access 身份验证规则是白名单规则。 每个规则指定的目标计算机上为允许用户、 目标计算机之间 （也称为终结点或运行空间） 的特定的 Windows PowerShell[会话配置](https://technet.microsoft.com/library/dd819508.aspx)连接的定义。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC17938.jpeg" title="System_CAPS_security" alt="System_CAPS_security" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-security" /></span><span class="alertTitle"> 安全注释 </span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>用户需要只有一个要将获取访问的规则。 如果用户授予访问权限与完整语言访问或仅可访问远程管理的 Windows PowerShell cmdlet，基于 web 的控制台中，从一台计算机用户可以 （或跃点） 登录到其他计算机连接到第一个目标计算机。 配置 Windows PowerShell Web Access 的最安全方法是允许用户只访问受限制的会话配置文档 （也称为终结点或运行空间），以便它们以完成他们通常需要执行远程的特定任务。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>名称</p></th>
<th><p>说明</p></th>
<th><p>参数</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/library/jj592890.aspx">添加 PswaAuthorizationRule</a></p></td>
<td><p>向 Windows PowerShell Web Access 授权规则集添加新的授权规则。</p></td>
<td><ul>
<li><p>ComputerGroupName</p></li>
<li><p>计算机名称</p></li>
<li><p>配置名</p></li>
<li><p>RuleName</p></li>
<li><p>UserGroupName</p></li>
<li><p>用户名</p></li>
<li><p>凭据 (Windows Server 2012 R2 及更高版本)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/library/jj592893.aspx">删除 PswaAuthorizationRule</a></p></td>
<td><p>从 Windows PowerShell Web Access 中删除指定的授权规则。</p></td>
<td><ul>
<li><p>Id</p></li>
<li><p>RuleName</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/library/jj592891.aspx">获取 PswaAuthorizationRule</a></p></td>
<td><p>返回一组的 Windows PowerShell Web Access 授权规则。 不带参数使用它时，该 cmdlet 返回所有规则。</p></td>
<td><ul>
<li><p>Id</p></li>
<li><p>RuleName</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/library/jj592892.aspx">测试 PswaAuthorizationRule</a></p></td>
<td><p>计算授权规则来确定特定用户、 计算机或会话配置的访问请求的授权。 默认情况下，如果任何参数不添加，cmdlet 计算所有授权规则。 通过添加参数，管理员可以指定授权规则或规则来测试的子集。</p></td>
<td><ul>
<li><p>计算机名称</p></li>
<li><p>配置名</p></li>
<li><p>RuleName</p></li>
<li><p>用户名</p></li>
<li><p>凭据 (Windows Server 2012 R2 和更高版本)</p></li>
</ul></td>
</tr>
</tbody>
</table>

前一个 cmdlet 创建用于 Windows PowerShell Web Access 网关上的用户授权访问规则的集。 规则不同于访问控制列表 (Acl) 在目标计算机上，并提供额外的安全层 web access。 下一节中介绍了有关安全性的更多详细信息。

如果用户不能通过任何前面的安全层，他们在其浏览器窗口中收到常规"访问被拒绝"消息。 虽然安全的详细信息的网关服务器身份登录，最终用户不会显示登录或身份验证失败的信息有关多少安全层，它们传递，或在哪个图层。

有关配置授权规则的详细信息，请参阅本主题中的[配置授权规则](#BKMK_configrules)。

<a href="" id="BKMK_sec"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">安全</span></a>

------------------------------------------------------------------------

Windows PowerShell Web Access 安全模型具有基于 web 的控制台，end user 和目标计算机之间的四个图层。 Windows PowerShell Web Access 管理员可以在 IIS 管理控制台中添加到其他配置安全层。 有关保护 IIS 管理控制台中的网站的详细信息，请参阅[配置 Web 服务器安全性 (IIS 7)](https://technet.microsoft.com/library/cc731278(v=ws.10).aspx)。 有关 IIS 详细信息的最佳做法和防止拒绝服务攻击，请参阅[为防止 DoS/拒绝服务攻击的最佳做法](https://technet.microsoft.com/library/cc750213.aspx)。 管理员还可以购买并安装其他、 零售身份验证软件。

下表介绍了最终用户和目标计算机之间的安全的四个图层。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>顺序</p></th>
<th><p>图层</p></th>
<th><p>说明</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>Web 服务器 (IIS) 安全功能，如客户端证书身份验证</p></td>
<td><p>用户名和密码进行身份验证的网关上其帐户，必须始终提供 Windows PowerShell Web Access 的用户。 但是，Windows PowerShell Web Access 管理员还可以可选的客户端证书身份验证打开或关闭 (请参阅中的步骤 10 的"以使用 IIS 管理器在现有网站中配置网关"<a href="https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx">安装和使用 Windows PowerShell Web Access</a>)。 可选的客户端证书功能需要最终用户能够拥有有效的客户端证书，除了其用户名和密码，并且是 Web 服务器 (IIS) 配置的一部分。 启用客户端证书图层时，Windows PowerShell Web Access 登录页面会提示用户提供有效的证书，然后计算其登录凭据。 客户端证书自动检查客户端证书身份验证。</p>
<p>如果找不到有效的证书，Windows PowerShell Web Access 会通知用户，以便他们可以提供的证书。 如果找到有效的客户端证书，Windows PowerShell Web Access 会打开以供用户提供他们的用户名和密码登录页面。</p>
<p>这是一个示例的其他安全设置所提供的 Web 服务器 (IIS)。 有关其他 IIS 安全功能的详细信息，请参阅<a href="https://technet.microsoft.com/library/cc731278(ws.10).aspx">配置 Web 服务器安全性 (IIS 7)</a>。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>Windows PowerShell Web Access 的基于表单的网关身份验证</p></td>
<td><p>Windows PowerShell Web Access 登录页面需要一组凭据 （用户名和密码），并提供用户提供不同的凭据目标计算机的选项。 如果用户不提供备用凭据，主要的用户名和密码，以用来连接到网关还用于连接到的目标计算机。</p>
<p>所需的凭据进行身份验证的 Windows PowerShell Web Access 网关上。 这些凭据必须在本地 Windows PowerShell Web Access 网关服务器，或在 Active Directory® 有效的用户帐户。</p>
<p>用户进行身份验证在网关之后，Windows PowerShell Web Access 检查授权规则来验证用户是否具有访问请求的目标计算机。 后成功的授权用户的凭据被传递到目标计算机。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>Windows PowerShell Web Access 授权规则</p></td>
<td><p>用户进行身份验证在网关之后，Windows PowerShell Web Access 检查授权规则来验证用户是否具有访问请求的目标计算机。 后成功的授权用户的凭据被传递到目标计算机。</p>
<p>仅由网关，验证用户后，用户可以在目标计算机上进行身份验证之前计算这些规则。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>目标身份验证和授权规则</p></td>
<td><p>Windows PowerShell Web access 安全性的最终层是目标计算机的安全配置。 用户必须具有相应的访问权限配置的目标计算机上，以及在 Windows PowerShell Web Access 授权规则，以运行通过 Windows PowerShell Web Access 影响目标计算机的 Windows PowerShell 的基于 web 的控制台。</p>
<p>此图层提供的相同的安全机制，如果用户尝试通过运行创建与目标计算机从 Windows PowerShell 中的远程 Windows PowerShell 会话，请将评估连接尝试<strong>Enter PSSession</strong>或<strong>新建 PSSession</strong> cmdlet。</p>
<p>默认情况下，Windows PowerShell Web Access 进行身份验证网关和目标计算机上使用的主要用户名和密码。 基于 web 的登录页面上，在一节中<strong>可选的连接设置</strong>，如果需要向用户提供目标计算机中，为提供不同的凭据的选项。 如果用户不提供备用凭据，主要的用户名和密码，以用来连接到网关还用于连接到的目标计算机。</p>
<p>授权规则可以用于允许用户访问特定会话配置。 您可以创建受限运行空间或会话配置用于 Windows PowerShell Web 访问，并允许特定用户登录到 Windows PowerShell Web Access 时，仅对特定会话配置连接。 您可以使用访问控制列表 (Acl) 来确定哪些用户有权访问特定终结点，并进一步限制访问端点的一组特定的用户使用本部分中介绍的授权规则。 有关受限运行空间的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/desktop/ee706589.aspx">局限运行空间</a>MSDN 上。</p></td>
</tr>
</tbody>
</table>

<a href="" id="BKMK_configrules"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">配置授权规则</span></a>

------------------------------------------------------------------------

管理员可能希望为已定义了用于 Windows PowerShell 远程管理其环境中的 Windows PowerShell Web Access 用户相同的授权规则。 本部分中的第一个过程介绍如何添加授予访问权限，为一位用户，登录管理一台计算机，并在单个会话配置安全授权规则。 第二个过程介绍如何删除不再需要的授权规则。

如果您打算使用自定义会话配置允许特定用户仅在运行 Windows PowerShell Web Access 中的受限空间内工作，创建您的自定义会话配置之前添加引用它们的授权规则。 您无法使用 Windows PowerShell Web Access cmdlet 来创建自定义会话配置。 有关创建自定义会话配置的详细信息，请参阅 MSDN 上的[about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) 。

Windows PowerShell Web Access cmdlet 支持一个通配符，用星号 ( \* )。 不支持在字符串内的通配符;使用单个星号每个属性 （用户、 computers、 或会话配置）。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">注意 </span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>有关更多方式授权规则可用于向用户授予访问权限，并帮助保护 Windows PowerShell Web Access 环境中，请参阅<a href="#BKMK_others">其他授权规则方案示例</a>本主题中。</p></td>
</tr>
</tbody>
</table>

#### 若要添加严格授权规则

1.  执行下列操作之一以打开 Windows PowerShell 会话与提升的用户权限。

    -   在 Windows 桌面上，右键单击任务栏上的**Windows PowerShell** ，然后单击**以管理员身份运行**。

    -   在 Windows**启动**屏幕上，右键单击**Windows PowerShell**，，然后单击**以管理员身份运行**。

2.  <span class="label">可选步骤，以使用会话配置限制用户访问权限︰</span>验证会话配置要使用的规则中已经存在。 如果尚未创建，使用以创建会话配置[about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) MSDN 上的说明。

3.  键入以下内容，并按**Enter**。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_1079478f-cd51-4d35-8022-4b532a9d57a4')"复制到剪贴板。"）

        Add-PswaAuthorizationRule –UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    此授权规则允许对其他们通常具有访问权限，有权访问特定会话配置的适用于用户的典型脚本和 cmdlet 需要的网络上的特定用户访问到一台计算机。 在下面的示例中，用户名为<span class="code">JSmith</span>中<span class="code">Contoso</span>域授予访问权限来管理计算机<span class="code">Contoso_214</span>，并使用一个名为会话配置<span class="code">NewAdminsOnly</span>。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_4e760377-e401-4ef4-988f-7a0aec1b2a90')"复制到剪贴板。"）

        Add-PswaAuthorizationRule –UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4.  验证规则已通过运行**获取 PswaAuthorizationRule** cmdlet 或**测试 PswaAuthorizationRule 用户名&lt;域\\用户 | 计算机\\用户&gt;-计算机名称**&lt;计算机名称&gt;。 例如，**测试 PswaAuthorizationRule-用户名 Contoso\\JSmith-计算机名称 Contoso_214**。

#### 若要删除授权规则

1.  如果 Windows PowerShell 会话尚未打开，请参阅[添加严格授权规则](#BKMK_arar)本部分中的步骤 1。

2.  键入以下内容，并按**Enter**，其中*规则 ID*表示您想要删除的规则的唯一标识号。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_0daef66d-0ecf-47fb-a8a0-d4dbceb8409d')"复制到剪贴板。"）

        Remove-PswaAuthorizationRule -ID <rule ID>

    或者，如果您不知道标识号，但知道您要删除的规则的友好名称，您可以获取名称的规则，并将其输送到<span class="code">删除 PswaAuthorizationRule</span> cmdlet 来删除该规则，如下面的示例中所示︰ 获取 PswaAuthorizationRule RuleName &lt;*规则名称*&gt; |删除-PswaAuthorizationRule。

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">注意 </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>不提示您确认是否要删除指定的授权规则;按时，将删除规则<strong>Enter</strong>。 请确保您确实要删除授权规则之前运行<strong>删除 PswaAuthorizationRule</strong> cmdlet。</p></td>
    </tr>
    </tbody>
    </table>

<a href="" id="BKMK_others"></a>
####

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">其他授权规则方案示例</span></a>

------------------------------------------------------------------------

Windows PowerShell 中的每个会话使用会话配置;如果未指定会话，Windows PowerShell 使用默认、 内置的 Windows PowerShell 会话配置称为 Microsoft.PowerShell。 默认会话配置包括所有可用的计算机的 cmdlet。 管理员可通过定义具有受限运行空间 （有限范围的 cmdlet 和最终用户可以执行的任务） 的会话配置可以限制对所有计算机访问。 已授予对具有完全语言访问或 Windows PowerShell 的远程管理 cmdlet 一台计算机访问权限的用户可以连接到其他计算机连接到第一台计算机。 定义受限运行空间可以阻止用户从其允许的 Windows PowerShell 运行空间，访问其他计算机和提高了安全性的 Windows PowerShell Web Access 环境。 可以到管理员要通过 Windows PowerShell Web Access 进行访问的所有计算机 （通过使用组策略） 分发会话配置。 有关配置会话的详细信息，请参阅[about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx)。 以下是这种情况的一些示例。

-   管理员创建终结点，称为**PswaEndpoint**，受限运行空间。 然后，管理员创建一条规则， ** \*，\*，PswaEndpoint**，并分发到其他计算机的终结点。 规则允许访问与**PswaEndpoint**的终结点的所有计算机上的所有用户。 如果这是仅授权规则中的规则集定义，没有该终结点的计算机将不能访问。

-   管理员使用称为**PswaEndpoint**，受限运行空间创建起止工作表，并且想要限制为特定用户的访问权限。 管理员创建的一组用户名为**Level1Support**，并定义以下规则︰ **Level1Support，\*，PswaEndpoint**。 规则授予组**Level1Support**访问**PswaEndpoint**配置的所有计算机中的任何用户。 同样，可以将访问限制到一组特定的计算机。

-   某些管理员提供特定用户比其他人的访问。 例如，管理员创建两个用户组**管理员**和**BasicSupport**。 管理员还创建名为**PswaEndpoint**，受限运行空间起止工作表并定义以下两个规则︰**管理员\*，\***和**BasicSupport，\*，PswaEndpoint**。 第一条规则提供了所有计算机上，访问的**管理员**组中的所有用户和第二条规则都提供**BasicSupport**组访问仅对具有**PswaEndpoint**这些计算机中的所有用户。

-   管理员已经设置的私有测试环境，并且想要允许他们通常有权访问的访问到其中的所有会话配置它们通常都有权访问网络上的所有授权的网络用户访问所有计算机。 因为这是私有测试环境，管理员会创建不安全的授权规则。 管理员运行该 cmdlet<span class="code">添加 PswaAuthorizationRule \* \* \*</span>，它使用通配符**\***来表示的所有用户、 所有计算机和所有配置。 此规则等同于以下内容︰<span class="code">添加 PswaAuthorizationRule-用户名\*-计算机名称\*-配置名\*</span>。

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC17938.jpeg" title="System_CAPS_security" alt="System_CAPS_security" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-security" /></span><span class="alertTitle"> 安全注释 </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>此规则不建议在安全环境中，并将绕过 Windows PowerShell Web Access 提供的安全的授权规则图层。</p></td>
    </tr>
    </tbody>
    </table>

-   管理员必须允许用户连接到目标环境包含工作组和域，可以在其中工作组计算机有时会用来连接到的域，在目标计算机和域中的计算机有时会用来连接到工作组中的目标计算机中的计算机。 管理员有网关服务器， *PswaServer*，在工作组;而目标计算机*srv1.contoso.com*在域。 用户*Chris*是工作组网关服务器和目标计算机上的本地授权的用户。 他工作组服务器上的用户名是*chrisLocal*;在目标计算机上他用户的姓名和*contoso\\chris*。 要为 Chris 授权访问 srv1.contoso.com，管理员，请添加以下规则。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_8d183d3d-1c19-44b8-9297-530b0efc7c79')"复制到剪贴板。"）

        Add-PswaAuthorizationRule –userName PswaServer\chrisLocal –computerName srv1.contoso.com –configurationName Microsoft.PowerShell

    上面的规则示例在网关服务器上，验证 Chris，然后授予*srv1*其访问权限。 在登录页面中，Chris 必须提供凭据**可选的连接设置**区域中的另一组 (*contoso\\chris*)。 网关服务器使用其他的一组凭据验证他在目标计算机上， *srv1.contoso.com*。

    在前面的方案中，Windows PowerShell Web Access 建立成功连接到目标计算机仅后下列已成功，并允许至少一个授权规则。

    1.  通过在格式*服务器名称*中添加用户名工作组网关服务器上的身份验证\\*用户名*授权规则

    2.  通过使用备用凭据登录在页面上，在**可选的连接设置**区域中提供的目标计算机上的身份验证

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">注意 </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>如果网关和目标计算机不同的工作组或域中，或工作组和域之间的两个工作组计算机的两个域，必须建立信任关系。 这种关系不能通过使用 Windows PowerShell Web Access 授权规则 cmdlet 来配置。 授权规则不定义计算机; 之间的信任关系他们可以仅授权用户连接到特定目标计算机和会话配置。 有关如何配置不同域之间的信任关系的详细信息，请参阅<a href="https://technet.microsoft.com/library/cc794775.aspx">创建域和林信任</a>。 有关如何将工作组计算机添加到受信任的主机列表的详细信息，请参阅<a href="https://technet.microsoft.com/library/dd759202.aspx">远程管理服务器管理器与</a>。</p></td>
    </tr>
    </tbody>
    </table>

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">使用多个网站的一组授权规则</span></a>

------------------------------------------------------------------------

授权规则存储在 XML 文件。 默认情况下，XML 文件的路径名称是 %windir%\\Web\\PowershellWebAccess\\数据\\AuthorizationRules.xml。

授权的路径规则 XML 文件存储在**powwa.config**文件中，找到 %windir%\\Web\\PowershellWebAccess\\数据。 管理员可以灵活地更改默认路径中**powwa.config**以满足首选项或要求的引用。 如果需要此配置允许管理员更改文件的位置允许多个 Windows PowerShell Web Access 网关使用相同的授权规则。

<a href="" id="BKMK_sesmgmt"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">会话管理</span></a>
<a href="/en-us/library/dn282394(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

默认情况下，Windows PowerShell Web 访问限制到三个会话，一次用户。 您可以编辑**web 应用程序的 IIS 管理器中支持的每个用户的会话数目不同**。 **Web.config**文件的路径是 $Env: Windir\\Web\\PowerShellWebAccess\\wwwroot\\Web.config。

默认情况下，配置 Web 服务器 (IIS) 重新启动应用程序池，如果编辑任何设置。 例如，如果对**web.config**文件进行了更改，则重新启动应用程序池。 Windows PowerShell Web Access 将使用内存中会话状态，因为用户登录到 Windows PowerShell Web Access 会话丢失他们重新启动应用程序池时的会话。

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">在登录页面设置默认参数</span></a>

------------------------------------------------------------------------

如果您的 Windows PowerShell Web Access 网关正在运行 Windows Server 2012 R2 上，您可以配置 Windows PowerShell Web Access 登录页面显示的设置为默认值。 您可以在**web.config**文件前面的段落中所述配置值。 登录页面在 web.config 文件; **appSettings**部分中找到设置为默认值下面是**appSettings**部分的示例。 其中许多设置有效值为相应的 Windows PowerShell 中[新建 PSSession](https://technet.microsoft.com/library/hh849717.aspx) cmdlet 的参数相同。 例如， <span class="code">defaultApplicationName</span>键，如下面的代码块中所示的目标计算机上的**$PSSessionApplicationName**首选项变量的值。

[复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_6ccfd0a1-485a-4ac5-9636-89ebab501bef')"复制到剪贴板。"）

    <appSettings>
            <add key="maxSessionsAllowedPerUser" value="3"/>
            <add key="defaultPortNumber" value="5985"/>
            <add key="defaultSSLPortNumber" value="5986"/>
            <add key="defaultApplicationName" value="WSMAN"/>
            <add key="defaultUseSslSelection" value="0"/>
            <add key="defaultAuthenticationType" value="0"/>
            <add key="defaultAllowRedirection" value="0"/>
            <add key="defaultConfigurationName" value="Microsoft.PowerShell"/>
    </appSettings>

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">超时和计划外的断开</span></a>

------------------------------------------------------------------------

Windows PowerShell Web Access 会话超时。 在 Windows Server 2012 上运行 Windows PowerShell Web Access，超时邮件会话处于非活动状态的 15 分钟后显示签名中的用户。 如果用户不会显示超时消息后的 5 分钟内响应，结束会话，然后用户已注销。 您可以更改用于在网站设置 IIS 管理器中的会话超时时间段。

在运行 Windows Server 2012 R2 会话超时，在默认情况下，在处于非活动状态的 20 分钟后 Windows PowerShell Web Access。 如果用户断开会话中基于 web 的控制台由于网络错误或其他意外的关闭或失败次数，而不是因为他们已关闭会话继续运行，Windows PowerShell Web Access 的自己的会话连接到目标计算机上，直到在客户端方面的失误超时。 会话已断开连接后或者默认 20 分钟的时间，或在网关管理员指定超时后, 者为准较短。

网关服务器正在运行 Windows Server 2012 R2，Windows PowerShell Web Access 允许用户重新连接保存会话时更高版本，但网络错误、 意外的关闭或其他故障断开会话，如果用户不能查看或重新连接到指定的网关超时后管理员失效，直到已保存的会话。

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">另请参阅</span></a>
<a href="/en-us/library/dn282394(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[安装和使用 Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx)
[about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx)
[Windows PowerShell Web Access Cmdlet](https://technet.microsoft.com/library/hh918342.aspx)

<span>显示︰</span>继承保护

<span class="stdr-votetitle">是此页有所帮助？</span>
是无

更多的反馈？

<span class="stdr-count"><span class="stdr-charcnt">1500</span>剩余字符</span>提交跳过此

<span class="stdr-thankyou">谢谢！</span> <span class="stdr-appreciate">我们非常感谢您的反馈。</span>

[管理您的配置文件](https://social.technet.microsoft.com/profile)

|

<a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> 网站反馈</a>网站反馈

<a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a>

告诉我们您的体验...

页面加载快速吗？

<span> Yes<span> </span></span> <span> No<span> </span></span>

您喜欢的页面设计？

<span> Yes<span> </span></span> <span> No<span> </span></span>

告诉我们的详细信息

-   [Flash 新闻稿](https://technet.microsoft.com/cc543196.aspx)
-   |
-   [与我们联系](https://technet.microsoft.com/cc512759.aspx)
-   |
-   [隐私声明](https://privacy.microsoft.com/privacystatement)
-   |
-   [使用条款的](https://technet.microsoft.com/cc300389.aspx)
-   |
-   [商标](https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/)
-   |

© 2016 Microsoft

© 2016 Microsoft

第三方脚本和代码链接到或从该网站引用由拥有此类代码方，而不是 Microsoft 授权给您。 请参阅 ASP.NET Ajax CDN 使用条款-http://www.asp.net/ajaxlibrary/CDN.ashx。
<img src="https://m.webtrends.com/dcsjwb9vb00000c932fd0rjc7_5p3t/njs.gif?dcsuri=/nojavascript&amp;WT.js=No" alt="DCSIMG" id="Img1" width="1" height="1" />

