---
title: "使用 web 基于的 windows powershell 控制台"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 279931867f7a7400e61db5079deeb9a2b1312aeb
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
#  使用基于 Web 的 Windows PowerShell 控制台

更新时间︰ 2013 2013年 6 月 24日日

适用于︰ Windows Server 2012 R2，Windows Server 2012

Windows PowerShell® Web Access 允许 Windows PowerShell® 用户登录到安全套接字层 SSL 安全网站以使用 Windows PowerShell 会话、 cmdlet 和脚本管理远程计算机。 在 web 浏览器中运行 Windows PowerShell 控制台，因为它可以从各种客户端设备，包括手机、 平板电脑的计算机、 公共计算展台、 便携式计算机或共享或租借的计算机打开。 基于 web 的 Windows PowerShell 控制台面向作为登录过程的一部分由用户指定的远程计算机。 本主题介绍如何登录并开始使用 Windows PowerShell Web Access 的基于 web 的控制台。

本主题并不介绍如何使用 Windows PowerShell 或运行 cmdlet 或脚本。 有关如何使用 Windows PowerShell 和脚本资源的信息，请参阅本主题结尾的另请参阅部分。

本主题内容︰

-   [支持的浏览器和客户端设备](#BKMK_browser)

-   [登录到 Windows PowerShell Web Access](#BKMK_sign)

-   [注销且超时](#BKMK_timeout)

-   [基于 web 的 Windows PowerShell 控制台中的差异](#BKMK_web)

<a href="" id="BKMK_browser"></a>
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

<a href="" id="BKMK_sign"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">登录到 Windows PowerShell Web Access</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

您的 Windows PowerShell Web Access 管理员应为您提供是您所在组织的 Windows PowerShell Web Access 网关网站的地址的 URL。 默认情况下，此网站地址为 https://&lt;服务器名称&gt;/pswa。 登录到 Windows PowerShell Web Access 之前，请确保您拥有的名称或要管理的远程计算机的 IP 地址。 您必须是授权的用户的远程计算机上，并且必须配置为允许远程管理。 有关配置您的计算机以允许远程管理的详细信息，请参阅[启用和使用 Windows PowerShell 中的远程命令](https://technet.microsoft.com/magazine/ff700227.aspx)。 配置您的计算机以允许远程管理的最简单方法是运行**启用-PSRemoting-强制**cmdlet 的计算机上，在已打开的 Windows PowerShell 会话中提升的 （**以管理员身份运行**） 的用户权限。

### 登录到 Windows PowerShell Web Access

1.  打开 Internet 浏览器窗口或选项卡中的 Windows PowerShell Web 访问网站。

2.  在 Windows PowerShell Web Access 登录页上，提供您的网络的用户名、 密码和要管理的计算机 （和有关您的授权的用户） 的名称。 如果 Windows PowerShell Web Access 管理员指导您使用 URI 到自定义网站或代理服务器，而不是计算机名称，在**连接类型**字段中，选择**连接 URI** ，然后提供 URI。

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
    <td><ul>
    <li><p>如果目标计算机处于工作组中，使用以下语法提供您的用户名，然后登录到计算机︰&lt;<em>工作组名称</em>&gt;\&lt;<em>用户名</em>&gt;。</p></li>
    <li><p>如果目标计算机是网关服务器，您可以指定<strong>本地主机</strong>中<strong>计算机名称</strong>字段。</p></li>
    <li><p>如果目标计算机的网关服务器，而位于工作组中的网关服务器，您可以使用<strong>本地主机</strong>中<strong>计算机名称</strong>字段，但不是使用本地主机\&lt;<em>用户名</em>&gt;中<strong>用户名</strong>字段。 您必须使用&lt;<em>工作组名称</em>&gt;\&lt;<em>用户名</em>&gt;。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>

3.  要管理的远程计算机的授权要求与**可选的连接设置**部分。 有关等同于可选的连接设置的参数的详细信息，请参阅[帮助 Enter PSSession cmdlet](https://technet.microsoft.com/library/dd315384.aspx)。

    通常情况下，使用通过 Windows PowerShell Web Access 网关的凭据都是相同识别的要管理的远程计算机。 但是，如果您想要使用不同的凭据管理您在步骤 2 中指定的远程计算机，展开**可选的连接设置**部分中，并且提供备用凭据。 否则，请跳至步骤 6。

4.  Windows PowerShell Web Access 管理员已创建自定义会话配置为 Windows PowerShell Web Access 的用户，如果在**配置名称**字段中键入的会话配置名称。 有关配置会话的详细信息，请参阅 Microsoft 网站上的[about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx) 。

5.  保留设为**默认值**，除非您有已指示否则 Windows PowerShell Web Access 管理员**的身份验证类型**。

6.  单击**登录**。

<a href="" id="BKMK_timeout"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">注销且超时</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

以下任一将您登录到基于 web 的 Windows PowerShell 会话。

-   在控制台右下角，单击**注销**。 (Windows Server 2012 仅)

-   在控制台 (Windows Server 2012 R2 仅) 右下角，单击**保存**或**退出**。 单击**保存**保存并关闭您的 Windows PowerShell Web Access 会话;您可以重新连接到更高版本的会话。 当您登录到 Windows PowerShell Web Access 再次时，Windows PowerShell Web Access 会显示您已保存的会话; 的列表您可以选择和重新连接到已保存的会话，或开始新会话。 打开已保存和处于活动状态，允许用户的会话最大数量是管理员配置的网关。

    单击**退出**将您登录到 Windows PowerShell Web Access 会话而不保存它。

-   正在尝试登录以管理其他远程计算机中相同的浏览器会话，或在同一浏览器会话的新选项卡。 （这不适用于如果网关服务器运行 Windows Server 2012 R2;在 Windows Server 2012 R2 上运行的 Windows PowerShell Web Access 允许多个用户会话中的新选项卡在同一浏览器会话。）有关如何在同一台计算机上使用多个活动会话的详细信息，请参阅"连接到多个目标计算机同时"在此主题的[基于 web 的控制台的限制](#BKMK_limits)部分。

-   20 分钟的时间处于非活动状态的会话。 网关管理员可以自定义在处于非活动状态超时;有关详细信息，请参阅[会话管理](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx#BKMK_sesmgmt)。

    -   如果从基于 web 的控制台中会话断开由于网络错误或其他意外的关闭或失败，而不是因为您关闭会话自己 Windows PowerShell Web 访问会话继续运行，连接到目标计算机上，直到在客户端方面的失误超时。 默认情况下，此超时是 20 分钟的时间，并由网关管理员配置。 会话已断开连接后或者默认 20 分钟的时间，或在网关管理员指定超时后, 者为准较短。

        如果网关服务器正在运行 Windows Server 2012 R2，Windows PowerShell Web Access 允许用户重新连接以保存会话时更高版本，但不是能查看或保存会话，直到管理员失效指定的网关超时后重新连接。

-   关闭浏览器窗口或选项卡。

-   关闭客户端设备运行，或断开网络浏览器。

-   在 web 控制台运行**退出**命令。 如果已向其连接到的会话配置配置为支持[NoLanguage](https://msdn.microsoft.com/library/windows/desktop/system.management.automation.pslanguagemode.aspx)模式或受限运行空间中，不起作用此命令。

如果您想要重新登录，再次打开 Windows PowerShell Web Access web 页，然后按照本主题中[登录到 Windows PowerShell Web Access](#BKMK_signin)中的步骤登录。

<a href="" id="BKMK_web"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">基于 web 的 Windows PowerShell 控制台中的差异</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

登录到 Windows PowerShell Web Access 之后, 在您的浏览器窗口或选项卡中打开基于 web 的 Windows PowerShell 控制台。 控制台已连接到远程计算机的登录过程中指定，因为这些 Windows PowerShell cmdlet 或在远程计算机可用的脚本可在控制台中。 本节介绍了 Windows PowerShell Web Access 控制台和 Windows PowerShell Web Access 控制台与安装的**PowerShell.exe**控制台之间的差异的其他限制。

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">与 PowerShell.exe 的功能差异</span></a>

------------------------------------------------------------------------

Windows PowerShell 主机功能大部分 Windows PowerShell Web Access 基于 web 的控制台中可用，但某些功能不可用。

-   <span class="label">显示嵌套的进度。</span>  Windows PowerShell Web Access 显示的 cmdlet 进度 GUI 该报告进度，但只有顶级的进度信息显示。

-   <span class="label">输入颜色修改。</span>  输入的颜色 （前景色和背景） 不能更改。 输出、 警告，详细信息，以及错误消息的样式可以所有更改通过运行脚本。

-   <span class="label">PSHostRawUserInterface。</span>  Windows PowerShell Web Access 实现通过 Windows PowerShell 远程管理，并使用远程运行空间。 Windows PowerShell Web Access 不在此界面; 实现一些方法例如，任何命令写入 Windows 控制台。 在 Windows PowerShell Web Access 中不起作用**PowerTab**之类的命令。

-   <span class="label">功能键。</span>  Windows PowerShell Web Access 不支持某些功能键，在许多情况下因为命令保留浏览器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>不受支持的功能键</p></th>
<th><p>操作</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ctrl + C</p></td>
<td><p>在 Windows PowerShell Web Access 中， <strong>Ctrl + C</strong>浏览器用于复制内容。 控制台提供<strong>取消</strong>按钮和用户还可以使用<strong>Ctrl + Q</strong>取消命令。</p></td>
</tr>
<tr class="even">
<td><p>Alt 空格、 e、 l</p></td>
<td><p>滚动浏览屏幕缓冲区</p></td>
</tr>
<tr class="odd">
<td><p>Alt + 空格键、 e、 f</p></td>
<td><p>在屏幕缓冲区中搜索文本</p></td>
</tr>
<tr class="even">
<td><p>Alt + 空格键、 e、 k</p></td>
<td><p>选择要从中复制屏幕缓冲区的文本</p></td>
</tr>
<tr class="odd">
<td><p>Alt + 空格键、 e、 p</p></td>
<td><p>将剪贴板的内容粘贴到 Windows PowerShell 控制台</p></td>
</tr>
<tr class="even">
<td><p>Alt + 空格键 c</p></td>
<td><p>关闭 Windows PowerShell 控制台</p></td>
</tr>
<tr class="odd">
<td><p>Ctrl + 分页符</p></td>
<td><p>强制关闭 Windows PowerShell 窗口</p></td>
</tr>
<tr class="even">
<td><p>按 Ctrl + Home</p></td>
<td><p>删除当前的命令行的开头</p></td>
</tr>
<tr class="odd">
<td><p>Ctrl + End</p></td>
<td><p>删除到命令行的结尾</p></td>
</tr>
<tr class="even">
<td><p>F1</p></td>
<td><p>命令行上，向右移动一个字符的光标</p></td>
</tr>
<tr class="odd">
<td><p>F2</p></td>
<td><p>通过复制你向上您键入的字符的最后一个命令创建一个新的命令</p></td>
</tr>
<tr class="even">
<td><p>F3</p></td>
<td><p>完成命令行的最后一个命令行中的内容</p></td>
</tr>
<tr class="odd">
<td><p>F4</p></td>
<td><p>删除光标所在的位置从字符</p></td>
</tr>
<tr class="even">
<td><p>F5</p></td>
<td><p>向后扫描您命令的历史记录。 若要访问 Windows PowerShell Web Access 中的命令历史记录中的命令，请单击<strong>历史记录</strong>滚动基于 web 的控制台中的按钮。</p></td>
</tr>
<tr class="odd">
<td><p>F7</p></td>
<td><p>交互式命令历史记录中选择一个命令</p></td>
</tr>
<tr class="even">
<td><p>F8</p></td>
<td><p>扫描显示与当前文本匹配的命令的历史记录</p></td>
</tr>
<tr class="odd">
<td><p>F9</p></td>
<td><p>从历史记录运行特定编号的命令</p></td>
</tr>
<tr class="even">
<td><p>Page Up</p></td>
<td><p>运行历史记录中的第一个命令</p></td>
</tr>
<tr class="odd">
<td><p>Page Down</p></td>
<td><p>运行历史记录中的最后一个命令</p></td>
</tr>
<tr class="even">
<td><p>Alt + F7</p></td>
<td><p>清除命令历史记录列表</p></td>
</tr>
</tbody>
</table>

<a href="" id="BKMK_limits"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">基于 web 的控制台的限制</span></a>

------------------------------------------------------------------------

-   <span class="label">双跃点。</span>   您可能会遇到的双跃点 （或连接到另一台计算机从第一个连接） 如果您尝试创建或处理通过使用 Windows PowerShell Web Access 的新会话的限制。 Windows PowerShell Web Access 将使用远程运行空间，并且当前， **PowerShell.exe**不支持从远程运行空间到另一台计算机建立远程连接。 如果您尝试使用连接到另一台远程计算机从现有连接**Enter PSSession** cmdlet，例如，您可以获得各种错误，如"不能获取网络资源"。

    若要避免双跃点错误，您的管理员应在您的组织的网络环境中配置 CredSSP 身份验证。 有关配置 CredSSP 身份验证的详细信息，请参阅 Microsoft 网站上的[第二个跃点远程处理的 CredSSP](http://blogs.msdn.com/b/powershell/archive/2008/06/05/credssp-for-second-hop-remoting-part-i-domain-account.aspx) 。 您还可以提供显式凭据，当您想要管理的第二个远程计算机;隐式凭据不太可能允许的第二个跃点。

-   Windows PowerShell Web Access 使用，并且具有相同的限制为远程的 Windows PowerShell 会话。 直接呼叫 Windows 控制台 Api，如基于控制台编辑器或基于文本的菜单程序的命令不起作用，因为命令执行未读或写到标准输入、 输出和错误的管道。 因此，启动可执行文件的命令文件，如**notepad.exe**，或显示一个 GUI，如<span class="code">OpenGridView</span>或<span class="code">ogv</span>，不起作用。 您的体验受此行为;给您，它将显示 Windows PowerShell Web Access 没有响应你的命令。

-   选项卡上完成不支持在具有受限运行空间或一个处于**NoLanguage**模式的会话配置。 管理员可以配置为支持选项卡上完成的会话，虽然其建议不要是出于安全考虑，因为它可以公开未经授权的用户的以下信息。

    -   内部文件系统路径

    -   内部的计算机上的共享的文件夹

    -   运行空间中的变量

    -   加载的类型储存框架命名空间

    -   环境变量

-   登录到**NoLanguage**会话配置或运行 Windows PowerShell Web Access 中的受限的空间的用户不能运行的**退出**命令结束会话。 若要注销，用户应单击**注销**控制台页面上。

-   <span class="label">同时向多个目标计算机连接。</span>   如果网关服务器正在运行 Windows Server 2012，Windows PowerShell Web Access 仅允许一个远程计算机连接每个浏览器会话。它不允许用户一次，登录并使用单独的浏览器选项卡连接到多个远程计算机。 当您打开新选项卡或新浏览器窗口时，Windows PowerShell Web Access 将提示您断开您当前会话并开始新会话，以便您可以连接到的新 （或相同） 远程计算机。 如果需要不同的远程计算机到两个或多个单独的会话，但是，在 Internet Explorer 中的一个功能允许您创建一个新的会话。 要在 Internet Explorer 中开始新的浏览器会话，请按**ALT**，打开**文件**菜单，然后选择**新会话**。 然后，在新的会话中，打开 Windows PowerShell Web Access 网站中的登录以访问远程的另一台计算机。

    当在 Windows Server 2012 R2 上运行的 Windows PowerShell Web Access 网关时，用户可以打开在其他浏览器选项卡中的多个连接到远程计算机。 如果您想要使用的基于 web 的 Windows PowerShell 控制台打开多个连接到远程计算机，请咨询您的 Windows PowerShell Web Access 网关管理员联系，以查看是否通过网关服务器支持此功能。

-   <span class="label">持久 Windows PowerShell 会话 （重新连接）。</span>   之后您下班时间的 Windows PowerShell Web Access 网关，已关闭网关和目标计算机之间的远程连接。 这将停止任何 cmdlet 或当前正在进行的脚本。 建议使用 Windows PowerShell **-作业**基础结构，以便可以开始作业、 从计算机中断开、 更高版本，重新连接和具有作业保持执行长时间运行任务时。 使用另一个好处**-作业**cmdlet 是您可以首先使用 Windows PowerShell Web Access、 注销，然后再重新运行的 Windows PowerShell Web Access 或其他主机 (如 Windows PowerShell® 集成脚本环境 (ISE)) 通过更高版本，进行连接。

-   <span class="label">调整列宽控制台。</span>   可以通过以下三种方式调整**PowerShell.exe**控制台窗口。

    -   拖动并调整使用鼠标控制台窗口大小

    -   通过使用 GUI 控制台属性更改高度和宽度属性

    -   更改高度和使用 cmdlet 控制台窗口的宽度

        可以使用这些 cmdlet，如下所示配置用于 Windows PowerShell Web Access 的控制台窗口。 在下面的示例中，用户更改 Windows PowerShell Web Access 控制台的宽度为**20**。

        [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_778d5e55-9195-4bd7-b313-d1fbca7876e4')"复制到剪贴板。"）

            $newSize = $Host.UI.RawUI.WindowSize
            $newSize.Width = $newSize.Width - 20

            $oldSize = $Host.UI.RawUI.WindowSize

            $Host.UI.RawUI.WindowSize = $newSize

        类似的方式，您可以更改控制台的高度。

        [Windows PowerShell 团队博客](http://blogs.msdn.com/b/powershell/)提供了用于自定义控制台视图的其他示例。

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">另请参阅</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_4" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[Windows PowerShell Cmdlet 参考](https://technet.microsoft.com/library/ee407531(ws.10).aspx)
[Microsoft TechNet 上的 Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx)
[TechNet 脚本中心存储库](http://gallery.technet.microsoft.com/scriptcenter)
[脚本中心-嗨，脚本专家 ！](https://technet.microsoft.com/scriptcenter)
 [Windows PowerShell 团队博客](http://blogs.msdn.com/b/powershell/)

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

