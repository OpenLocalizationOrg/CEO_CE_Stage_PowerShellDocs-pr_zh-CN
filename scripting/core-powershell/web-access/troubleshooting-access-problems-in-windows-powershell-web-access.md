---
title: "在 windows powershell web access 中的 access 问题故障排除"
ms.date: 2016-05-11
keywords: powershell cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 70699be88438bd51dc23d0cf73f81ed8b4f4c01f
ms.sourcegitcommit: 2fa86409b9183dfc80f4e9d4ff1015496e04fffd
translationtype: MT
---
#  在 Windows PowerShell Web Access 中的 Access 问题故障排除

更新时间︰ 2013 2013年 6 月 24日日

适用于︰ Windows Server 2012 R2，Windows Server 2012

<a href="" id="BKMK_trouble"></a>

------------------------------------------------------------------------

下表列出了一些常见的问题，用户在他们试图使用 Windows PowerShell Web Access，连接到远程计算机时可能遇到和包括用于解决问题的建议。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>问题</p></th>
<th><p>可能的原因和解决方案</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>登录失败</p></td>
<td><p>由于以下任何可能会出现故障。</p>
<ul>
<li><p>在远程计算机上，允许用户访问到计算机或特定会话配置授权规则不存在。 Windows PowerShell Web Access 安全会限制;通过使用授权规则，用户必须授予显式访问远程计算机。 有关创建授权规则的详细信息，请参阅<a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">授权规则和安全功能的 Windows PowerShell Web Access</a>本指南中。</p></li>
<li><p>用户没有授权的访问目标计算机。 这取决于访问控制列表 (Acl)。 有关详细信息，请参阅登录中向 Windows PowerShell Web 访问"<a href="https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx">使用基于 Web 的 Windows PowerShell 控制台</a>，或<a href="https://msdn.microsoft.com/library/windows/desktop/ee706585.aspx">Windows PowerShell 团队博客</a>。</p>
<ul>
<li><p>不可能在目标计算机启用远程管理的 Windows PowerShell。 验证已启用用户尝试连接到其计算机上。 详细信息，请参阅"如何为配置您的计算机为远程处理"中<a href="https://technet.microsoft.com/library/dd315349.aspx">about_Remote_Requirements</a>在 Windows PowerShell 有关帮助主题。</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><p>当用户尝试登录到在 Internet Explorer 窗口中的 Windows PowerShell Web Access 时，它们显示<strong>内部服务器错误</strong>页面上或 Internet Explorer 停止响应。 此问题是特定于 Internet Explorer。</p></td>
<td><p>这可能会导致出现用户有登录域名包含中文字符，或者如果一个或多个中文字符是网关服务器名称的一部分。 若要解决此问题，用户应<a href="http://ie.microsoft.com/testdrive/info/downloads/Default.html">安装和运行 Internet Explorer 10</a>，然后执行下列步骤。</p>
<ol>
<li><p>更改 Internet Explorer<strong>文档模式</strong>设置为<strong>IE10 标准</strong>。</p>
<ol>
<li><p>按<strong>F12</strong>以打开开发人员工具控制台。</p></li>
<li><p>在 Internet Explorer 10 中，单击<strong>浏览器模式</strong>，然后选择<strong>Internet Explorer 10</strong>。</p></li>
<li><p>单击<strong>文档模式</strong>，然后单击<strong>IE10 标准</strong>。</p></li>
<li><p>按<strong>F12</strong>来关闭开发人员工具控制台。</p></li>
</ol></li>
<li><p>禁用自动代理配置。</p>
<ol>
<li><p>在 Internet Explorer 10 中，单击<strong>工具</strong>，然后单击<strong>Internet 选项</strong>。</p></li>
<li><p>在<strong>Internet 选项</strong>对话框中，在<strong>连接</strong>选项卡上，单击<strong>局域网设置</strong>。</p></li>
<li><p>清除<strong>自动检测设置</strong>复选框。 单击<strong>确定</strong>，然后单击<strong>确定</strong>来关闭<strong>Internet 选项</strong>对话框。</p></li>
</ol></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>无法连接到远程工作组计算机</p></td>
<td><p>如果目标计算机的工作组成员，请使用以下语法提供您的用户名和登录到计算机︰&lt;<em>工作组名称</em>&gt;\&lt;<em>用户名</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>找不到 Web 服务器 (IIS) 管理工具，即使已安装的角色</p></td>
<td><p>如果您使用安装 Windows PowerShell Web Access<span class="code">安装 WindowsFeature</span> cmdlet，除非没有安装工具管理<span class="code">IncludeManagementTools</span>参数添加到该 cmdlet。 例如，请参阅使用 Windows PowerShell cmdlet 安装 Windows PowerShell Web Access"中<a href="https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx">安装和使用 Windows PowerShell Web Access</a>。 您可以添加 IIS 管理控制台和其他 IIS 管理工具，您需要通过添加角色和目标网关服务器上的功能向导会话中选择工具。 添加角色和功能向导将在服务器管理器中打开从。</p></td>
</tr>
<tr class="odd">
<td><p>Windows PowerShell Web Access 网站不可访问</p></td>
<td><p>如果在 Internet Explorer (IE ESC) 启用增强安全配置，则可以将 Windows PowerShell Web Access 网站添加到受信任的站点列表或禁用 IE ESC。 您可以禁用 IE ESC 中<strong>属性</strong>图块<strong>本地服务器</strong>服务器管理器页面。</p></td>
</tr>
<tr class="even">
<td><p>试图连接的网关服务器目标计算机，并且也是工作组中时显示以下错误消息︰<strong>授权失败。 验证您有权连接到的目标计算机。</strong></p></td>
<td><p>当网关服务器也是目标服务器上，并且其工作组中时，指定用户名、 计算机名称和用户组名称下表中所示。 不要使用句点 （.） 本身来表示的计算机名称。</p>
<div>
<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th><p>方案</p></th>
<th><p>用户名参数</p></th>
<th><p>用户组参数</p></th>
<th><p>参数名</p></th>
<th><p>ComputerGroup 参数</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>网关服务器是在域中</p></td>
<td><p><em>服务器名称</em>\<em>用户名</em>，Localhost\<em>用户名</em>，或。 \<em>用户名</em></p></td>
<td><p><em>服务器名称</em>\<em>user_group</em>，Localhost\<em>user_group</em>，或。 \<em>user_group</em></p></td>
<td><p>完全限定网关服务器或本地主机名称</p></td>
<td><p><em>服务器名称</em>\<em>computer_group</em>，Localhost\<em>computer_group</em>，或。 \<em>computer_group</em></p></td>
</tr>
<tr class="even">
<td><p>网关服务器处于工作组中</p></td>
<td><p><em>服务器名称</em>\<em>用户名</em>，Localhost\<em>用户名</em>，或。 \<em>用户名</em></p></td>
<td><p><em>服务器名称</em>\<em>user_group</em>，Localhost\<em>user_group</em>或。 \<em>user_group</em></p></td>
<td><p>服务器名称</p></td>
<td><p><em>服务器名称</em>\<em>computer_group</em>，Localhost\<em>computer_group</em>或。 \<em>computer_group</em></p></td>
</tr>
</tbody>
</table>
</div>
<p>登录到网关服务器作为目标计算机使用的凭据格式设置为以下选项之一。</p>
<ul>
<li><p><em>服务器名称</em>\<em>用户名</em></p></li>
<li><p>Localhost\<em>用户名</em></p></li>
<li><p>。 \<em>用户名</em></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>安全标识符） 显示在授权规则，而不是语法<em>用户名</em>/<em>计算机名称</em> </p></td>
<td><p>规则不再有效，或者 Active Directory 域服务查询失败。 授权规则无效通常方案此时网关服务器已在工作组中，一次，但以后加入域中。</p></td>
</tr>
<tr class="even">
<td><p>无法登录到域与 IPv6 地址为指定授权规则中的目标计算机。</p></td>
<td><p>授权规则在域名的窗体中不支持 IPv6 地址。 若要指定目标计算机使用 IPv6 地址，请授权规则中使用原始 IPv6 地址 （包含冒号）。 支持将域和数字 （用冒号） IPv6 地址作为目标计算机名称在 Windows PowerShell Web Access 登录页上，而不是授权规则。 有关 IPv6 地址的详细信息，请参阅<a href="https://technet.microsoft.com/library/cc781672.aspx">IPv6 的工作方式</a>。</p></td>
</tr>
</tbody>
</table>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">另请参阅</span></a>
<a href="/en-us/library/dn282395(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[授权规则和安全功能的 Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)
[使用基于 Web 的 Windows PowerShell 控制台](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)
[about_Remote_Requirements](https://technet.microsoft.com/library/dd315349.aspx)

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

