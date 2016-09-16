# 提取和分析出字符串的结构化对象
这还引入了一些附加功能用于 ConvertFrom 字符串 cmdlet:

-   默认情况下删除程度文本属性。 您可以将其包含与-IncludeExtent 参数。

-   许多学习从 MVP 和社区反馈算法错误修复。

-   若要将学习算法的结果另存为模板文件中的注释新-UpdateTemplate 参数。 这使得流程 （慢阶段） 一次性成本的学习。 现在几乎是瞬时包含已编码的学习算法的模板与运行转换的字符串。


提取和分析出的字符串内容的结构化的对象
----------------------------------------------------------

在与[Microsoft 研究](http://research.microsoft.com/)进行协作，添加新的**ConvertFrom 字符串**cmdlet。

此 cmdlet 支持两种模式︰ 基本分隔分析，并自动生成示例驱动的分析。

带分隔符的分析，默认情况下，将在空白区域中，输入拆分，并将属性名称分配到得到的组。 您可以自定义分隔符︰

> 1 \[c:\\temp\]
> &gt;&gt; "Hello World"|ConvertFrom 字符串 |设置表格格式-自动

P1 P2
--    --

该 cmdlet 还支持自动生成基于[Microsoft 研究](http://research.microsoft.com) [FlashExtract](http://research.microsoft.com/en-us/um/people/sumitg/flashextract.html)研究工时示例驱动分析。

若要开始，请考虑基于文本的通讯簿︰

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

    Thomas Hardy

    Seattle, WA

    Christina Berglund

    Redmond, WA

    Hanna Moos

    Puyallup, WA

复制到一个文件，您将使用与您的模板的一些示例︰

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

   

将数据要从中提取，周围的大括号将其命名为您执行此操作。 因为**Name**属性 (及其关联的其他属性) 可以出现多次，请使用星号 (\*) 来指示这导致多条记录 （而不是到一个记录提取大量属性）︰

    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}

设置此示例，从**ConvertFrom 字符串**可以立即自动提取从输入文件具有类似的结构基于对象的输出。

> 2 \[c:\\temp\]
>
> &gt;&gt;获取的内容。\\addresses.output.txt |ConvertFrom 字符串-TemplateFile。\\addresses.template.txt |&gt;&gt;&gt;表格格式-自动
>
> ExtentText 名称城市状态
> ----------                     ----               ----     -----
> 一个 Trujillo...               一个 Trujillo Redmond WA 安东尼奥莫雷诺...             安东尼奥莫雷诺 Renton WA Thomas Hardy...               Thomas Hardy 华盛顿西雅图炫 Berglund...         炫 Berglund Redmond WA Hanna Moos...                 Hanna Moos Puyallup WA

为提取的文本上的其他数据操作， **ExtentText**属性捕获从中提取记录的原始文本。 若要提供反馈，此功能，或共享的内容遇到困难编写示例，请通过<psdmfb@microsoft.com>电子邮件。

