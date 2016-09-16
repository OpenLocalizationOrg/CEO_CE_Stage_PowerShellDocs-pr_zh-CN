---
title: "安装和使用 windows powershell web access"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 37763fd59b8d8dc3bd5ae96a0a03d4b9cef3b438
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
#  安装和使用 Windows PowerShell Web Access

更新时间︰ 2013 2013年 11 月 5日日

适用于︰ Windows Server 2012 R2，Windows Server 2012

Windows PowerShell® Web Access，第一次引入 Windows Server® 2012，作为 Windows PowerShell 网关，提供基于 web 的 Windows PowerShell 控制台针对远程计算机。 允许 IT 专业人士，若要从 web 浏览器，没有 Windows PowerShell、 远程管理软件或有必要，在客户端设备上的浏览器插件安装 Windows PowerShell 控制台运行 Windows PowerShell 命令和脚本。 所有的是正确配置 Windows PowerShell Web Access 网关，并且客户端设备浏览器支持 JavaScript® 并接受 cookie 运行基于 web 的 Windows PowerShell 控制台是所必需的。

客户端设备包括便携式计算机、 非工作个人计算机、 租借的计算机、 平板电脑的计算机、 web 展台、 计算机运行的不是基于 Windows 的操作系统和浏览器中，移动电话。 IT 专业人士可以从有权访问 Internet 连接和 web 浏览器的设备的远程基于 Windows 的服务器上执行关键的管理任务。

后成功网关设置和配置，用户可以使用 web 浏览器访问 Windows PowerShell 控制台。 当用户打开受保护的 Windows PowerShell Web 访问网站时，他们可以身份验证成功后运行基于 web 的 Windows PowerShell 控制台。

Windows PowerShell Web Access 安装和配置了三步流程︰

1.  安装 Windows PowerShell Web Access

2.  配置网关

3.  配置授权规则，允许用户访问基于 web 的 Windows PowerShell 控制台

安装和配置 Windows PowerShell Web Access 之前，我们建议您阅读本整个指南，包含有关如何安装说明，请确保安全，并卸载 Windows PowerShell Web Access。 [使用基于 Web 的 Windows PowerShell 控制台](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)主题介绍如何用户登录到基于 web 的控制台中，并介绍限制以及基于 web 的 Windows PowerShell 控制台和**powershell.exe**控制台之间的差异。 最终用户的基于 web 的控制台应阅读[使用基于 Web 的 Windows PowerShell 控制台](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)，但不是需要阅读本指南的其余部分。

本主题未提供详细的 Web 服务器 (IIS) 操作指南;本主题中介绍了 Windows PowerShell Web Access 网关配置所需的这些步骤。 有关配置和保护 IIS 中的网站的详细信息，请参阅另请参阅部分中的 IIS 文档资源。

下图显示了 Windows PowerShell Web Access 的工作原理。

<span><img src="https://i-technet.sec.s-msft.com/dynimg/IC564303.jpeg" title="Windows PowerShell Web Access diagram" alt="Windows PowerShell Web Access diagram" id="ee15fa8f-ce13-49e5-933d-514f6d60a2b1" /></span>

本主题内容︰

-   [运行 Windows PowerShell Web Access 要求](#BKMK_reqs)

-   [在浏览器和客户端设备支持](#BKMK_browser)

-   [建议的 （快速） 部署](#BKMK_recm)

-   [自定义部署](#BKMK_custom)

-   [配置真品证书](#BKMK_configcert)

<a href="" id="BKMK_reqs"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">运行 Windows PowerShell Web Access 要求</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_0" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

需要 Windows PowerShell Web Access 的 Web 服务器 (IIS)、.NET Framework 4.5，和 Windows PowerShell 3.0 或要在其中运行网关服务器上运行的 Windows PowerShell 4.0。 通过添加角色和功能向导在服务器管理器或部署的 Windows PowerShell cmdlet 的服务器管理器，您可以在运行 Windows Server 2012 R2 服务器或 Windows Server 2012 中安装 Windows PowerShell Web Access。 使用服务器管理器或其部署 cmdlet 安装 Windows PowerShell Web Access 时，所需的角色和功能自动添加为安装过程的一部分。

Windows PowerShell Web Access 允许远程用户通过在 web 浏览器中使用 Windows PowerShell 中访问您的组织中的计算机。 虽然 Windows PowerShell Web Access 是一个方便且功能强大的管理工具，基于 web 的访问安全风险，并应尽可能安全地配置。 建议管理员配置 Windows PowerShell Web Access 网关使用可用的安全层，基于 cmdlet 的授权规则包含 Windows PowerShell Web 访问和安全的 Web 服务器 (IIS) 和第三方应用程序中可用的图层。 此文档中包含这两个不安全的示例为测试环境中，仅推荐的和推荐安全部署使用的示例。

<a href="" id="BKMK_browser"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">在浏览器和客户端设备支持</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

Windows PowerShell Web Access 支持以下 Internet 浏览器。 移动浏览器不正式支持，虽然许多可能无法运行基于 web 的 Windows PowerShell 控制台。 接受 cookie、 运行的 JavaScript，并运行的 HTTPS 网站被期待工作，但不是提供正式其他浏览器测试。

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">支持的桌面计算机浏览器</span></a>

------------------------------------------------------------------------

-   对于 Microsoft Windows® 8.0、 9.0、 10.0 和 11.0 Windows® Internet Explorer®

-   10.0.2 Mozilla Firefox®

-   Google Chrome™ 17.0.963.56m for Windows

-   适用于 Windows 的 Apple Safari® 5.1.2

-   Apple Safari 5.1.2 for Mac OS®

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">最小测试移动设备或浏览器</span></a>

------------------------------------------------------------------------

-   Windows Phone 7 和 7.5

-   Google Android WebKit 3.1 浏览器 Android 2.2.1 （内核 2.6）

-   适用于 iPhone 操作系统 5.0.1 Apple Safari

-   适用于 iPad 2 操作系统 5.0.1 Apple Safari

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">浏览器要求</span></a>

------------------------------------------------------------------------

若要使用 Windows PowerShell Web Access 基于 web 的控制台，浏览器中，必须执行下列操作。

-   允许来自 Windows PowerShell Web Access 网关网站 cookie。

-   无法打开并阅读 HTTPS 页面。

-   打开并运行使用 JavaScript 的网站。

<a href="" id="BKMK_recm"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">建议的 （快速） 部署</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

通过使用任一 Windows PowerShell cmdlet，或通过使用添加角色和从服务器管理器中打开的功能向导，您可以在运行 Windows Server 2012 R2 服务器或 Windows Server 2012 中安装 Windows PowerShell Web Access 网关。 快速安装和配置，此部分中所述使用 Windows PowerShell cmdlet。

-   [步骤 1︰ 安装 Windows PowerShell Web Access](#BKMK_step1)

-   [步骤 2︰ 配置网关](#BKMK_step2)

-   [步骤 3︰ 配置严格授权规则](#BKMK_step3)

<a href="" id="BKMK_step1"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 1︰ 安装 Windows PowerShell Web Access</span></a>

------------------------------------------------------------------------

#### 若要使用 Windows PowerShell cmdlet 安装 Windows PowerShell Web Access

1.  执行下列操作之一以打开 Windows PowerShell 会话与提升的用户权限。

    -   在 Windows 桌面上，右键单击任务栏上的**Windows PowerShell** ，然后单击**以管理员身份运行**。

    -   在 Windows**启动**屏幕上，右键单击**Windows PowerShell**，，然后单击**以管理员身份运行**。

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
    <td><p>在 Windows PowerShell 3.0 和 4.0，则无需导入之前运行属于模块的 cmdlet 的 Windows PowerShell 会话的服务器管理器 cmdlet 模块。 模块是自动导入首次运行属于模块 cmdlet。 此外，Windows PowerShell cmdlet 均不区分大小写。</p></td>
    </tr>
    </tbody>
    </table>

2.  键入以下内容，并按**Enter**，其中*计算机名称*表示远程计算机您要安装 Windows PowerShell Web Access 中，如果适用。 <span class="code">重新启动</span>参数在需要时自动重新启动目标服务器。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_374a9c21-4f6e-471e-b957-bb190a594533')"复制到剪贴板。"）

        Install-WindowsFeature –Name WindowsPowerShellWebAccess -ComputerName <computer_name> -IncludeManagementTools -Restart

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
    <td><p>使用 Windows PowerShell cmdlet 安装 Windows PowerShell Web Access 不默认情况下添加 Web 服务器 (IIS) 管理工具。 如果您想要在 Windows PowerShell Web Access 网关相同的服务器上安装管理工具，添加<span class="code">IncludeManagementTools</span>参数安装提供的命令 （在此步骤中）。 如果您从远程计算机管理 Windows PowerShell Web 访问网站，请安装 IIS 管理器管理单元中通过安装<a href="http://go.microsoft.com/fwlink/?LinkID=304145">远程服务器管理工具的 Windows 8.1</a>或<a href="http://go.microsoft.com/fwlink/p/?LinkID=238560">远程服务器管理工具适用于 Windows 8</a>要管理网关的计算机上。</p></td>
    </tr>
    </tbody>
    </table>

    要安装脱机 VHD 角色和功能，必须将同时添加<span class="code">计算机名称</span>参数和<span class="code">VHD</span>参数。 <span class="code">计算机名称</span>参数包含要装载 VHD 的服务器的名称和<span class="code">VHD</span>参数包含指定服务器上的 VHD 文件的路径。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_d841d509-347e-49d0-bf54-8d1f306bece6')"复制到剪贴板。"）

        Install-WindowsFeature –Name WindowsPowerShellWebAccess –VHD <path> -ComputerName <computer_name> -IncludeManagementTools -Restart

3.  安装完成后，请验证在目标服务器上安装 Windows PowerShell Web Access，通过在已打开提升的用户权限使用 Windows PowerShell 控制台中的目标服务器上运行**获取 WindowsFeature** cmdlet。 您还可以验证服务器管理控制台中，在安装 Windows PowerShell Web Access，方法是选择**所有服务器**页面上的目标服务器，然后查看所选的服务器的**角色和功能**的图块。 您还可以查看 Windows PowerShell Web Access 的自述文件。

4.  安装 Windows PowerShell Web Access 后，会提示您要查看的自述文件，其中包含网关的基本、 所需的安装说明进行操作。 在以下部分中，也是这些设置说明[步骤 2︰ 配置网关](#BKMK_step2)。 自述文件的路径是<span class="computerOutputInline">c:\\Windows\\Web\\PowerShellWebAccess\\wwwroot\\README.txt</span>。

<a href="" id="BKMK_step2"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 2︰ 配置网关</span></a>

------------------------------------------------------------------------

**安装 PswaWebApplication** cmdlet 是一种快速方法，以获取配置的 Windows PowerShell Web Access。 尽管您可以添加<span class="code">UseTestCertificate</span>参数<span class="code">安装 PswaWebApplication</span> cmdlet 来安装自签名的 SSL 证书，用于测试目的，这是不安全;对于安全生产环境中，始终使用有效的 SSL 证书已签名的证书颁发机构 (CA)。 使用 IIS 管理控制台，管理员可以使用自己的签名证书替换测试证书。

您可以完成要么地运行的 Windows PowerShell Web Access web 应用程序配置<span class="code">安装 PswaWebApplication</span> cmdlet 或通过执行配置基于图形用户界面的步骤在 IIS 管理器。 默认情况下，该 cmdlet 安装 web 应用程序， **pswa** （和为其**pswa_pool**应用程序池） 中的**默认网站**容器中，如下所示在 IIS 管理器中;如果需要，您可以指示 cmdlet 来更改 web 应用程序的默认网站容器。 IIS 管理器中提供了可用于 web 应用程序，例如更改的端口号或安全套接字层 (SSL) 证书的配置选项。

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
<td><p>我们强烈建议管理员配置网关要用有效 ca 已签名的证书。</p></td>
</tr>
</tbody>
</table>

-   [若要使用测试证书的 Windows PowerShell Web Access 网关配置使用安装 PswaWebApplication](#BKMK_testcert)

-   [若要使用真品证书的 Windows PowerShell Web Access 网关配置使用安装 PswaWebApplication 和 IIS 管理器](#BKMK_gencert)

#### 若要使用测试证书的 Windows PowerShell Web Access 网关配置使用安装 PswaWebApplication

1.  执行下列操作之一来打开 Windows PowerShell 会话。

    -   在 Windows 桌面上，右键单击任务栏上的**Windows PowerShell** 。

    -   在 Windows**开始**屏幕中，单击**Windows PowerShell**。

2.  键入以下内容，并按**Enter**。

    **安装 PswaWebApplication UseTestCertificate**

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
    <td><p><span class="code">UseTestCertificate</span>仅应在私有测试环境中使用参数。 对于安全生产环境中，我们建议使用有效 ca 已签名的证书。</p></td>
    </tr>
    </tbody>
    </table>

    运行该 cmdlet 安装 IIS 默认网站容器中的 Windows PowerShell Web Access web 应用程序。 该 cmdlet 创建所需的默认网站，在运行 Windows PowerShell Web Access 的基础结构 https://&lt;服务器名称&gt;/pswa。 若要安装不同的网站中的 web 应用程序，通过添加提供网站名称<span class="code">网站名称</span>参数。 若要更改 web 应用程序的名称 (默认值是<span class="code">pswa</span>)，添加<span class="code">WebApplicationName</span>参数。

    通过运行该 cmdlet 配置下列设置。 如果需要，您可以更改这些手动在 IIS 管理控制台中。

    -   路径︰ /pswa

    -   ApplicationPool: pswa_pool

    -   EnabledProtocols: http

    -   PhysicalPath: %windir**%/Web/PowerShellWebAccess/wwwroot

    <span class="label">示例︰</span> <span class="code">安装 PswaWebApplication-webApplicationName myWebApp-useTestCertificate</span>

    在本示例中生成用于 Windows PowerShell Web 访问网站是 https://&lt; *服务器名称*&gt;/myWebApp。

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
    <td><p>您不能登录，直到用户已被授予网站访问，通过添加授权规则。 有关详细信息，请参阅<a href="#BKMK_step3">步骤 3︰ 配置严格授权规则</a>和<a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">授权规则和安全功能的 Windows PowerShell Web Access</a>。</p></td>
    </tr>
    </tbody>
    </table>

#### 若要使用的真品证书的 Windows PowerShell Web Access 网关配置使用安装 PswaWebApplication 和 IIS 管理器

1.  执行下列操作之一来打开 Windows PowerShell 会话。

    -   在 Windows 桌面上，右键单击任务栏上的**Windows PowerShell** 。

    -   在 Windows**开始**屏幕中，单击**Windows PowerShell**。

2.  键入以下内容，并按**Enter**。

    **安装 PswaWebApplication**

    通过运行该 cmdlet 配置以下的网关设置。 如果需要，您可以更改这些手动在 IIS 管理控制台中。 您还可以指定的值<span class="code">网站名称</span>和<span class="code">WebApplicationName</span>的参数<span class="code">安装 PswaWebApplication</span> cmdlet。

    -   路径︰ /pswa

    -   ApplicationPool: pswa_pool

    -   EnabledProtocols: http

    -   PhysicalPath: %windir**%/Web/PowerShellWebAccess/wwwroot

3.  通过执行下列操作之一打开 IIS 管理控制台。

    -   在 Windows 桌面上，通过单击 Windows 任务栏中的**服务器管理器**中启动服务器管理器。 在服务器管理器中**工具**菜单中，单击**Internet 信息服务 (IIS) 管理器**。

    -   在 Windows**开始**屏幕中，单击**服务器管理器**。

4.  IIS 管理器树窗格中，展开**网站**文件夹直至看到在其安装 Windows PowerShell Web Access 的服务器节点。 展开**网站**文件夹。

5.  选择您在其中安装 Windows PowerShell Web Access web 应用程序的网站。 在**操作**窗格中，单击**绑定**。

6.  在**网站绑定**对话框中，单击**添加**。

7.  在**添加网站绑定**对话框中，在**类型**字段中，选择**https**。

8.  在**SSL 证书**字段中，从下拉菜单中选择签名的证书。 单击**确定**。 请参阅[配置 SSL 证书在 IIS 管理器](#BKMK_cert)在本主题中有关如何获取证书的详细信息。

    Windows PowerShell Web Access web 应用程序现在配置为使用您的签名的 SSL 证书。 您可以通过打开 https:// 访问 Windows PowerShell Web Access&lt;服务器名称&gt;/pswa 浏览器窗口中的。

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
    <td><p>您不能登录，直到用户已被授予网站访问，通过添加授权规则。 有关详细信息，请参阅<a href="#BKMK_step3">步骤 3︰ 配置严格授权规则</a>和<a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">授权规则和安全功能的 Windows PowerShell Web Access</a>。</p></td>
    </tr>
    </tbody>
    </table>

<a href="" id="BKMK_step3"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 3︰ 配置严格授权规则</span></a>

------------------------------------------------------------------------

Windows PowerShell Web Access 的安装和配置网关后，用户可以在浏览器中，打开登录页面，但他们无法登录，直到 Windows PowerShell Web Access 管理员授予用户访问显式。 Windows PowerShell Web Access 访问控制，通过使用下表中描述的 Windows PowerShell cmdlet 的组。 添加或管理授权规则没有任何类似 GUI。 有关 Windows PowerShell Web Access 的 cmdlet 的详细信息，请参阅[Windows PowerShell Web Access Cmdlet](https://technet.microsoft.com/library/hh918342.aspx)的 cmdlet 参考主题。

有关 Windows PowerShell Web Access 授权规则和安全的详细信息，请参阅[授权规则和安全功能的 Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)。

#### 若要添加严格授权规则

1.  执行下列操作之一以打开 Windows PowerShell 会话与提升的用户权限。

    -   在 Windows 桌面上，右键单击任务栏上的**Windows PowerShell** ，然后单击**以管理员身份运行**。

    -   在 Windows**启动**屏幕上，右键单击**Windows PowerShell**，，然后单击**以管理员身份运行**。

2.  <span class="label">可选步骤，以使用会话配置限制用户访问权限︰</span>验证会话配置要使用的规则中已经存在。 如果尚未创建，使用以创建会话配置[about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) MSDN 上的说明。

3.  键入以下内容，并按**Enter**。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_f9e7959b-75d0-4d63-8f8e-02334a8dd09d')"复制到剪贴板。"）

        Add-PswaAuthorizationRule –UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    此授权规则允许对其他们通常具有访问权限，有权访问特定会话配置的适用于用户的典型脚本和 cmdlet 需要的网络上的特定用户访问到一台计算机。 在下面的示例中，用户名为<span class="code">JSmith</span>中<span class="code">Contoso</span>域授予访问权限来管理计算机<span class="code">Contoso_214</span>，并使用一个名为会话配置<span class="code">NewAdminsOnly</span>。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_ebd5bc5e-ec5d-4955-a86a-63843e480e37')"复制到剪贴板。"）

        Add-PswaAuthorizationRule –UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4.  验证规则已通过运行**获取 PswaAuthorizationRule** cmdlet 或**测试 PswaAuthorizationRule 用户名&lt;域\\用户 | 计算机\\用户&gt;-计算机名称**&lt;计算机名称&gt;。 例如，**测试 PswaAuthorizationRule-用户名 Contoso\\JSmith-计算机名称 Contoso_214**。

配置授权规则之后，您准备授权用户登录到基于 web 的控制台并开始使用 Windows PowerShell Web Access。

<a href="" id="BKMK_custom"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">自定义部署</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

通过使用添加角色和功能向导服务器管理器中，您可以在运行 Windows Server 2012 R2 服务器或 Windows Server 2012 中安装 Windows PowerShell Web Access 网关。 安装 Windows PowerShell Web Access 后，您可以自定义 IIS 管理器中的网关配置。

<a href="" id="BKMK_custom1"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 1︰ 安装 Windows PowerShell Web Access</span></a>

------------------------------------------------------------------------

#### 若要通过使用添加角色和功能向导中安装 Windows PowerShell Web Access

1.  如果服务器管理器已打开，请转到下一步。 如果服务器管理器尚未打开，请执行下列操作之一以打开它。

    -   在 Windows 桌面上，通过单击 Windows 任务栏中的**服务器管理器**中启动服务器管理器。

    -   在 Windows**开始**屏幕中，单击**服务器管理器**。

2.  在**管理**菜单上，单击**添加角色和功能**。

3.  在**选择安装类型**页上，选择**基于角色的或基于功能的安装**。 单击**下一步**。

4.  在**选择目标服务器**页面服务器从服务器池，或选择一个脱机 VHD。 若要选择作为目标服务器的脱机 VHD，首先选择要装载 VHD 的服务器，然后选择 VHD 文件。 有关如何添加到您的服务器池的服务器的信息，请参阅服务器管理器帮助。 选择目标服务器后，单击**下一步**。

5.  在向导的**选择功能**页中，展开**Windows PowerShell**，，然后选择**Windows PowerShell Web Access**。

6.  请注意，系统会提示您添加所需的功能，如.NET Framework 4.5 和角色服务的 Web 服务器 (IIS)。 添加所需的功能，并继续。

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
    <td><p>通过使用添加角色和功能向导中安装 Windows PowerShell Web Access 也会安装 Web 服务器 (IIS)，包括 IIS 管理器管理单元中。 如果您使用添加角色和功能向导，将默认安装中对齐和其他 IIS 管理工具。 如果您使用 Windows PowerShell cmdlet，如下面的过程中所述安装 Windows PowerShell Web Access，不会默认情况下添加管理工具。</p></td>
    </tr>
    </tbody>
    </table>

7.  在**确认安装选择**页面上，如果 Windows PowerShell Web Access 的功能文件不您在步骤 4 中选择目标服务器上存储的单击**指定备用源路径**，并提供功能文件的路径。 否则，单击**安装**。

8.  单击**安装**后，**安装进度**页显示安装进度、 结果和消息，如警告、 失败次数或安装后配置步骤所需的 Windows PowerShell Web Access。 安装 Windows PowerShell Web Access 后，会提示您要查看的自述文件，其中包含网关的基本、 所需的安装说明进行操作。 本主题中还包括以下说明操作。 自述文件的路径是<span class="computerOutputInline">c:\\Windows\\Web\\PowerShellWebAccess\\wwwroot\\README.txt</span>。

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 2︰ 配置网关</span></a>

------------------------------------------------------------------------

本部分中的说明进行操作是子目录中安装 Windows PowerShell Web Access web 应用程序 — 而不能在根目录-您的网站。 此过程是由执行的操作的基于图形用户界面的等效<span class="code">安装 PswaWebApplication</span> cmdlet。 本节还包括有关如何使用 IIS 管理器配置为根网站的 Windows PowerShell Web Access 网关的说明进行操作。

-   [若要使用 IIS 管理器在现有网站中配置网关](#BKMK_configman)

-   [若要使用 IIS 管理器将网关配置为使用测试证书的根网站](#BKMK_configroot)

-   

#### 若要使用 IIS 管理器在现有网站中配置网关

1.  通过执行下列操作之一打开 IIS 管理控制台。

    -   在 Windows 桌面上，通过单击 Windows 任务栏中的**服务器管理器**中启动服务器管理器。 在服务器管理器中**工具**菜单中，单击**Internet 信息服务 (IIS) 管理器**。

    -   在 Windows**开始**屏幕中，键入任何名称的一部分的**Internet 信息服务 (IIS) 管理器**。 显示在结果中**的应用程序**时，请单击快捷方式。

2.  为 Windows PowerShell Web Access 中创建新的应用程序池。 展开 IIS 管理器树窗格中的网关服务器节点，选择**应用程序池**，然后单击**操作**窗格中的**添加应用程序池**。

3.  添加新的应用程序池与**pswa_pool**名称，或提供另一个名称。 单击**确定**。

4.  IIS 管理器树窗格中，展开**网站**文件夹直至看到在其安装 Windows PowerShell Web Access 的服务器节点。 选择**网站**文件夹。

5.  右键单击对其您想要添加的 Windows PowerShell Web 访问网站，，然后单击**添加应用程序**的网站 （例如，**默认网站**）。

6.  在**别名**字段中，键入 pswa，或提供另一个别名。 别名会成为虚拟目录名称。 例如，以下 url **pswa**表示在此步骤中指定的别名︰ https://&lt;服务器名称&gt;/pswa。

7.  在**应用程序池**字段中，选择您在步骤 3 中创建的应用程序池。

8.  在**物理路径**字段中，浏览应用程序的位置。 您可以使用默认位置、 %windir%/web/powershellwebaccess/wwwroot。 单击**确定**。

9.  按照本主题中的过程[以配置 SSL 证书在 IIS 管理器](#BKMK_cert)中的步骤。

10. <span class="label">可选的安全步骤︰</span>使用树窗格中选定的网站，在内容窗格中双击**SSL 设置**。 选择**要求 SSL**，，然后在**操作**窗格中，单击**应用**。 （可选） 在**SSL 设置**窗格中，可以要求用户连接到 Windows PowerShell Web Access 网站具有客户端证书。 客户端证书帮助客户端设备用户的身份验证。 有关如何需要客户端证书提高安全性的 Windows PowerShell Web Access 的详细信息，请参阅本指南中的[授权规则和安全功能的 Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx) 。

11. 打开在客户端设备上的浏览器会话。 有关支持的浏览器和设备的详细信息，请参阅本主题中的[浏览器和客户端支持的设备](#BKMK_browser)。

12. 打开新的 Windows PowerShell Web 访问网站，https://&lt; *gateway_server_name*&gt;/pswa。

    在浏览器应显示的 Windows PowerShell Web Access 控制台登录页面。

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
    <td><p>您不能登录，直到用户已被授予网站访问，通过添加授权规则。</p></td>
    </tr>
    </tbody>
    </table>

13. 在 Windows PowerShell 会话中的已打开具有提升的用户权限 （以管理员身份运行），运行以下脚本，其中*application_pool_name*表示您在步骤 3 到授权文件的访问权限授予应用程序池中创建的应用程序池的名称。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_c1a80a93-8fcf-4beb-a025-5f81bfb8bdae')"复制到剪贴板。"）

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    若要授权文件中查看现有的访问权限，请运行以下命令︰

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_ac2179c2-9548-4a17-8663-267fdd105380')"复制到剪贴板。"）

        c:\windows\system32\icacls.exe $authorizationFile

#### 若要使用 IIS 管理器将网关配置为使用测试证书的根网站

1.  通过执行下列操作之一打开 IIS 管理控制台。

    -   在 Windows 桌面上，通过单击 Windows 任务栏中的**服务器管理器**中启动服务器管理器。 在服务器管理器中**工具**菜单中，单击**Internet 信息服务 (IIS) 管理器**。

    -   在 Windows**开始**屏幕中，键入任何名称的一部分的**Internet 信息服务 (IIS) 管理器**。 显示在结果中**的应用程序**时，请单击快捷方式。

2.  IIS 管理器树窗格中，展开**网站**文件夹直至看到在其安装 Windows PowerShell Web Access 的服务器节点。 选择**网站**文件夹。

3.  在**操作**窗格中，单击**添加网站**。

4.  为网站键入名称，如**Windows PowerShell Web Access**。

5.  应用程序池会自动创建新网站。 使用不同的应用程序池，请单击**选择**以选择要使用新的网站相关联的应用程序池。 在**选择应用程序池**对话框中，选择备用应用程序池，然后单击**确定**。

6.  在**物理路径**文本框中，导航到*%windir%*/ Web/PowerShellWebAccess/wwwroot。

7.  在**装订**区域**类型**字段中，选择**https**。

8.  分配到不是由另一个网站或应用程序的网站的端口号。 若要查找打开的端口，可以在命令提示符窗口中运行**netstat**命令。 默认端口号是 443。

    如果已使用另一个网站 443，或如果您有更改的端口号的其他安全原因，更改默认端口。 如果网关服务器运行的另一个网站使用您所选的端口，将显示一条警告，当您单击**添加网站**对话框中的**确定**。 您必须使用未使用的端口运行 Windows PowerShell Web Access。

9.  或者，如果需要为您的组织，指定对您的组织和用户，例如**www.contoso.com**有意义的主机名。 单击**确定**。

10. 为更安全生产环境中，我们强烈建议提供有效的证书由 CA 已签名。 您必须提供 SSL 证书，因为用户只能通过 HTTPS 网站连接到 Windows PowerShell Web Access。 请参阅[配置 SSL 证书在 IIS 管理器](#BKMK_cert)在本主题中有关如何获取证书的详细信息。

11. 单击**确定**关闭**添加网站**对话框。

12. 在 Windows PowerShell 会话中的已打开具有提升的用户权限 （以管理员身份运行），运行以下脚本，其中*application_pool_name*表示您在步骤 4 中的授权文件的访问权限授予应用程序池中创建的应用程序池的名称。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_35ae9944-ca44-4af7-9c96-616083b3e3db')"复制到剪贴板。"）

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    若要授权文件中查看现有的访问权限，请运行以下命令︰

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_0eb6d70a-2807-498b-b088-fa5233ed68d5')"复制到剪贴板。"）

        c:\windows\system32\icacls.exe $authorizationFile

13. 使用 IIS 管理器树窗格中选择新的网站，在**操作**窗格中，若要开始网站中单击**开始**。

14. 打开在客户端设备上的浏览器会话。 有关支持的浏览器和设备的详细信息，请参阅本文档中的[浏览器和客户端支持的设备](#BKMK_browser)。

15. 打开新的 Windows PowerShell Web 访问网站。

    当您打开 https:// 根网站指向 Windows PowerShell Web Access 的文件夹，因为在浏览器应显示 Windows PowerShell Web Access 登录页面&lt; *gateway_server_name*&gt;。 不需要添加**/pswa**到 URL。

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
    <td><p>您不能登录，直到用户已被授予网站访问，通过添加授权规则。</p></td>
    </tr>
    </tbody>
    </table>

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 3︰ 配置严格授权规则</span></a>

------------------------------------------------------------------------

Windows PowerShell Web Access 的安装和配置网关后，用户可以在浏览器中，打开登录页面，但他们无法登录，直到 Windows PowerShell Web Access 管理员授予用户访问显式。 Windows PowerShell Web Access 访问控制，通过使用下表中描述的 Windows PowerShell cmdlet 的组。 添加或管理授权规则没有任何类似 GUI。 有关 Windows PowerShell Web Access 的 cmdlet 的详细信息，请参阅[Windows PowerShell Web Access Cmdlet](https://technet.microsoft.com/library/hh918342.aspx)的 cmdlet 参考主题。

有关 Windows PowerShell Web Access 授权规则和安全的详细信息，请参阅[授权规则和安全功能的 Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)。

#### 若要添加严格授权规则

1.  执行下列操作之一以打开 Windows PowerShell 会话与提升的用户权限。

    -   在 Windows 桌面上，右键单击任务栏上的**Windows PowerShell** ，然后单击**以管理员身份运行**。

    -   在 Windows**启动**屏幕上，右键单击**Windows PowerShell**，，然后单击**以管理员身份运行**。

2.  <span class="label">可选步骤，以使用会话配置限制用户访问权限︰</span>验证会话配置要使用的规则中已经存在。 如果尚未创建，使用以创建会话配置[about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) MSDN 上的说明。

3.  键入以下内容，并按**Enter**。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_4df22c91-f56f-4bb5-91e7-99f9b365ed5d')"复制到剪贴板。"）

        Add-PswaAuthorizationRule –UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    此授权规则允许对其他们通常具有访问权限，有权访问特定会话配置的适用于用户的典型脚本和 cmdlet 需要的网络上的特定用户访问到一台计算机。 在下面的示例中，用户名为<span class="code">JSmith</span>中<span class="code">Contoso</span>域授予访问权限来管理计算机<span class="code">Contoso_214</span>，并使用一个名为会话配置<span class="code">NewAdminsOnly</span>。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_efc3999a-2905-453f-86cd-014b41658ffc')"复制到剪贴板。"）

        Add-PswaAuthorizationRule –UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4.  验证规则已通过运行**获取 PswaAuthorizationRule** cmdlet 或**测试 PswaAuthorizationRule 用户名&lt;域\\用户 | 计算机\\用户&gt;-计算机名称**&lt;计算机名称&gt;。 例如，**测试 PswaAuthorizationRule-用户名 Contoso\\JSmith-计算机名称 Contoso_214**。

配置授权规则之后，您准备授权用户登录到基于 web 的控制台并开始使用 Windows PowerShell Web Access。

<a href="" id="BKMK_configcert"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">配置真品证书</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_4" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

对于安全生产环境中，始终使用有效的 SSL 证书已签名的证书颁发机构 (CA)。 本部分中的过程介绍如何获取和从 CA 应用有效的 SSL 证书。

### 若要在 IIS 管理器中配置 SSL 证书

1.  IIS 管理器树窗格中，选择在其安装 Windows PowerShell Web Access 的服务器。

2.  在内容窗格中，双击**服务器证书**。

3.  在**操作**窗格中，请执行下列操作之一。 有关 IIS 中配置服务器的证书的详细信息，请参阅[在 IIS 7 配置服务器的证书](https://technet.microsoft.com/library/cc732230.aspx)。

    -   单击**导入**从您的网络上的某个位置导入现有的有效的证书。

    -   单击**创建证书请求**从如 VeriSign™、 Thawte 或 GeoTrust® CA 申请证书。 证书的常用名称必须匹配主机标头中请求。 例如，如果客户端浏览器请求 http://www.contoso.com/，常用名称也必须为 http://www.contoso.com/。 这是提供的证书的 Windows PowerShell Web Access 网关的最安全的和推荐的选项。

    -   单击**创建自签名证书**创建您可以立即使用，并具有更高版本由签名 CA 如果所需的证书。 指定自签名证书，如**Windows PowerShell Web Access**的友好名称。 此选项不被视为安全，并仅为私有测试环境建议。

4.  创建或获取证书之后, IIS 管理器树窗格中，选择 （例如，**默认网站**） 证书应用于网站，然后单击**操作**窗格中的**绑定**。

5.  如果尚未显示，请在**添加网站绑定**对话框中，添加网站中，为**https**绑定。 如果您没有使用自签名的证书，指定此过程的步骤 3 中的主机名。 如果您使用的自签名的证书，此步骤不是必需的。

6.  选择您获得或者在此过程的步骤 3 中创建的证书，然后单击**确定**。

<a href="" id="BKMK_using"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">使用基于 web 的 Windows PowerShell 控制台</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_5" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

安装 Windows PowerShell Web Access 和网关配置本主题中所述完毕后，基于 web 的 Windows PowerShell 控制台已准备好使用。 对于基于 web 的控制台中启动获取有关的详细信息，请参阅[使用基于 Web 的 Windows PowerShell 控制台](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)。

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">另请参阅</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_6" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[Internet 信息服务 (IIS) 7.0 文档](https://technet.microsoft.com/library/cc753433.aspx)
[IIS 管理器 7.0 帮助](https://technet.microsoft.com/library/cc732664.aspx)
[配置 Web 服务器的安全性 (IIS 7)](https://technet.microsoft.com/library/cc731278.aspx)
[IPsec 部署资源](https://technet.microsoft.com/network/bb531150)

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

