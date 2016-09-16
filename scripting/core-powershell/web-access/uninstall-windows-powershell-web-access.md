---
title: "卸载 windows powershell web access"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 62d2af274fd765cf36a1988e79f64936155250c0
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
#  卸载 Windows PowerShell Web Access

更新时间︰ 2013 2013年 6 月 24日日

适用于︰ Windows Server 2012 R2，Windows Server 2012

按照本主题，若要删除的网关服务器正在运行的是 Windows Server 2012 R2 或 Windows Server 2012 的 Windows PowerShell Web 访问网站和应用程序中的步骤操作。 在开始之前，告知用户的基于 web 的控制台您要删除的网站。

<a href="" id="BKMK_uninstall"></a>

------------------------------------------------------------------------

卸载 Windows PowerShell Web Access 中的网关服务器之前，或者运行<span class="code">卸载 PswaWebApplication</span> cmdlet 来删除网站和 Windows PowerShell Web Access web 应用程序，或使用 IIS 管理器中[删除](#BKMK_delsite)的过程，使用 IIS 管理器的 Windows PowerShell Web 访问网站和 web 应用程序。

卸载 Windows PowerShell Web Access 不卸载 IIS 或因为 Windows PowerShell Web Access 要求他们运行自动安装的任何其他功能。 卸载过程离开安装 Windows PowerShell Web Access 的依赖; 依据的功能如果需要您可以单独卸载这些功能。

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">推荐 （快速） 卸载</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

本节中的过程帮助您使用 Windows PowerShell cmdlet 卸载 Windows PowerShell Web Access web 应用程序和 Windows PowerShell Web Access 的功能。

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 1︰ 删除 web 应用程序</span></a>

------------------------------------------------------------------------

如果您已经指定您自己，自定义网站的名称，添加<span class="code">网站名称</span>参数与你的命令，并指定网站名称。 如果您已使用自定义 web 应用程序 (不是默认应用程序， **pswa**，添加<span class="code">WebApplicationName</span>参数与你的命令，并指定 web 应用程序的名称。

#### 若要删除的网站和 web 应用程序使用卸载 PswaWebApplication cmdlet

1.  执行下列操作之一来打开 Windows PowerShell 会话。

    -   在 Windows 桌面上，右键单击任务栏上的**Windows PowerShell** 。

    -   在 Windows**开始**屏幕中，单击**Windows PowerShell**。

2.  键入**卸载 PswaWebApplication**，然后再按**Enter**。

3.  如果您使用的一个测试证书，添加<span class="code">DeleteTestCertificate</span>参数 cmdlet，如下面的示例中所示。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_28147344-ab2f-49e7-b1c2-6dbe649d4366')"复制到剪贴板。"）

        Uninstall-PswaWebApplication -DeleteTestCertificate

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 2︰ 卸载 Windows PowerShell Web Access</span></a>

------------------------------------------------------------------------

#### 若要使用 Windows PowerShell cmdlet 卸载 Windows PowerShell Web Access

1.  执行下列操作之一以打开 Windows PowerShell 会话与提升的用户权限。 如果已打开会话，请转到下一步。

    -   在 Windows 桌面上，右键单击任务栏上的**Windows PowerShell** ，然后单击**以管理员身份运行**。

    -   在 Windows**开始**屏幕中，右键单击**Windows PowerShell**，，然后单击**以管理员身份运行**。

2.  键入以下内容，并按**Enter**，*计算机名称*代表您要从中删除 Windows PowerShell Web 访问远程服务器的位置。 <span class="code">-重新启动</span>参数自动重新启动目标服务器所需的删除。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_7b534520-f292-471f-89e3-a1079c03e369')"复制到剪贴板。"）

        Uninstall-WindowsFeature –Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    若要从脱机 VHD 删除角色和功能，必须将同时添加<span class="code">-计算机名称</span>参数和<span class="code">-VHD</span>参数。 <span class="code">-计算机名称</span>参数包含要装载 VHD 的服务器的名称和<span class="code">-VHD</span>参数包含指定服务器上的 VHD 文件的路径。

    [复制](; javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_5d8f91ee-b91a-4653-b7df-e745187fd72d')"复制到剪贴板。"）

        Uninstall-WindowsFeature –Name WindowsPowerShellWebAccess –VHD <path> -ComputerName <computer_name> -Restart

3.  删除完成后，验证您打开服务器管理器中的**所有服务器**页面中删除 Windows PowerShell Web Access，选择您要从中删除功能，服务器和查看的**角色和功能**的图块在选定的服务器的页面上。 您还可以运行<span class="code">获取 WindowsFeature</span> cmdlet 针对所选的服务器 (获取 WindowsFeature 计算机名称&lt;*计算机名称*&gt;) 以查看角色和服务器安装的功能的列表。

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">自定义卸载</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

本部分中的过程帮助您卸载 Windows PowerShell Web Access web 应用程序和 Windows PowerShell Web 访问功能使用删除角色和功能向导服务器管理器和 IIS 管理控制台。

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 1︰ 删除 web 应用程序</span></a>

------------------------------------------------------------------------

#### 若要删除的 Windows PowerShell Web 访问网站和 web 应用程序使用 IIS 管理器

1.  通过执行下列操作之一打开 IIS 管理控制台。 如果已打开，请转到下一步。

    -   在 Windows 桌面上，通过单击 Windows 任务栏中的**服务器管理器**中启动服务器管理器。 在服务器管理器中**工具**菜单中，单击**Internet 信息服务 (IIS) 管理器**。

    -   在 Windows**开始**屏幕中，键入任何名称的一部分的**Internet 信息服务 (IIS) 管理器**。 显示在结果中**的应用程序**时，请单击快捷方式。

2.  IIS 管理器树窗格中，选择正在运行的 Windows PowerShell Web Access web 应用程序的网站。

3.  在**操作**窗格中，在**管理网站**上，下单击**停止**。

4.  在树窗格中，右键单击正在运行 Windows PowerShell Web Access web 应用程序，网站中的 web 应用程序，然后单击**删除**。

5.  树窗格中，选择**应用程序池**，选择 Windows PowerShell Web Access 应用程序池文件夹，在**操作**窗格中，单击**停止**，然后单击内容窗格中的**删除**。

6.  关闭 IIS 管理器。

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
    <td><p>在卸载过程中不会删除证书。 如果您创建自签名的证书或使用测试证书并希望将其删除，删除 IIS 管理器中的证书。</p></td>
    </tr>
    </tbody>
    </table>

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">步骤 2︰ 卸载 Windows PowerShell Web Access</span></a>

------------------------------------------------------------------------

#### 若要通过使用删除角色和功能向导中卸载 Windows PowerShell Web Access

1.  如果服务器管理器已打开，请转到下一步。 如果服务器管理器尚未打开，请执行下列操作之一以打开它。

    -   在 Windows 桌面上，通过单击 Windows 任务栏中的**服务器管理器**中启动服务器管理器。

    -   在 Windows**开始**屏幕中，单击**服务器管理器**。

2.  在**管理**菜单上，单击**删除角色和功能**。

3.  在**选择目标服务器**页面中，选择服务器或脱机 VHD 要从中删除功能。 若要选择脱机 VHD，首先选择要装载 VHD 的服务器，然后选择 VHD 文件。 选择目标服务器后，单击**下一步**。

4.  单击**下一步**再次以跳转到**删除功能**页面。

5.  对于**Windows PowerShell Web Access**中，清除复选框，然后单击**下一步**。

6.  在**确认删除所选内容**页面上，单击**删除**。

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">另请参阅</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[安装和使用 Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx)
[IIS 管理器 7.0 帮助](https://technet.microsoft.com/library/cc732664.aspx)

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

