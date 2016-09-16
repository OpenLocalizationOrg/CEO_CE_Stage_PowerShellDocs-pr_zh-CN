# 分配给 PowerShell 文档

PowerShell 文档中您感兴趣的谢谢 ！ 有关如何参加我们的技术文档的详细信息，请参阅下文。

>有关 Git 和 GitHub 入门的一般信息，请参阅[GitHub 帮助](https://help.github.com/)。 

## 登录 CLA

您可以参与到任何 PowerShell 存储库之前，您必须[注册 Microsoft 贡献许可协议 (CLA)](https://cla.microsoft.com/)。 如果您已已经提供了到 PowerShell 存储库在过去，恭喜 ！ 您已完成此步骤。

## 有关 PowerShell 文档提供反馈

通过[PowerShell 文档存储库问题页面](https://github.com/PowerShell/PowerShell-Docs/issues)上[创建一个问题](https://help.github.com/articles/creating-an-issue/)，您可以指出错误，建议更改或请求新主题。

问题通过 PowerShell 文档团队的成员定期检查和是优先处理、 分配，并且也会相应解决。

## 编写 PowerShell 文档

PowerShell 参与的最简单方法之一是通过帮助编写和编辑文档。 所有我们 GitHub 上托管的文档是使用[GitHub Flavored 减价](https://help.github.com/articles/github-flavored-markdown/)编写的。

## 对现有主题进行次要编辑

[编辑现有文件](https://help.github.com/articles/editing-files-in-another-user-s-repository/)，只需导航到它，然后单击"编辑"按钮。 GitHub 会自动创建您自己分叉的我们存储库，您可以在其中进行更改。 一旦完成后，保存编辑和提交到*暂存* [PowerShell 文档](https://github.com/PowerShell/PowerShell-Docs)存储库的分支[拉请求](https://help.github.com/articles/creating-a-pull-request/)。 创建提取请求之后，PowerShell 文档工作组中的某人将它们合并到*暂存*分支之前查看所做的更改。

## 对现有主题进行主要编辑

如果要对现有项目，进行重大更改，添加或更改图像，或者提供新文章，您将需要手动创建 GitHub 分叉，然后复制到本地计算机分叉。 分叉是基于 GitHub 的主存储库中，在您提供了您可以使用单独的工作副本的 GitHub 帐户下的副本。 您将从您的分叉创建提取请求。 同样，克隆是基于本地副本的存储库，这种情况下，将为您分叉的克隆。 克隆允许您处理 Git 存储库脱机，并使用更强大的本机软件/工具。

下面是对现有文档进行主要编辑工作流︰

1. [PowerShell 文档](https://github.com/PowerShell/PowerShell-Docs)存储库的[创建分叉](https://help.github.com/articles/fork-a-repo/)。
2. 在本地计算机上[创建您的分叉的克隆](https://help.github.com/articles/cloning-a-repository/)。
3. 在您的克隆存储库中创建新的本地分支。
4. 对您想要更新减价编辑器中的文件进行更改。 
   请参阅以下常用减价编辑器。
5. 向您分叉[推入您的本地分支](https://help.github.com/articles/pushing-to-a-remote/)。
6. [PowerShell 文档](https://github.com/PowerShell/PowerShell-Docs)存储库的*暂存*分支到[创建提取请求](https://help.github.com/articles/creating-a-pull-request/)。

## 创建新的主题

如果您想要提供新文档，先检查[问题标记为"进行中"](https://github.com/PowerShell/PowerShell-Docs/labels/in%20progress)以确保您不重复工作。
如果没有人看起来处理您计划的内容︰

* 打开一个新问题并将其标记为"进行中"（如果您是 PowerShell 组织的成员） 中或添加"进度"作为注释告诉他人您正在处理的内容
* 根据上述内容来主要编辑现有主题，请按照相同工作流。
* 编辑`TOC.md`主题 （位于每个文档集的顶级文件夹中） 将您的新主题添加到目录。 
  确定您的新主题的对应目录，并添加适当的级别，与您的主题的链接的标题 (`[My topic title](relative path to my topic)`)。

## 减价编辑器

下面是您可以尝试一些减价编辑器︰

* [Visual Studio 代码](https://code.visualstudio.com)
* [减价拨号盘](http://markdownpad.com/)
* [Atom](https://atom.io/)
* [大文本](http://www.sublimetext.com/)


## GitHub Flavored 的减价 (GFM)

在此知识库文章的所有使用[GitHub Flavored 减价 (GFM)](https://help.github.com/articles/github-flavored-markdown/)。

一些基本 GFM 语法包括︰

* **换行符与段落︰**在减价没有任何 HTML`<br />`或`<p />`元素。 相反，由两个文本块之间空行指定一个新段落。

> **注意**︰ 请在每个句子简化差异和历史记录的命令行输出后添加一个新行。
此当前未采用跨所有 PowerShell-文档，但我们将使用向其一段时间。 随时提供帮助。 

* **斜体︰**HTML`<em>some text</em>`作为写入元素 `*some text*`
* **加粗︰**HTML`<strong>some text</strong>`作为写入元素 `**some text**`
* **标题︰**使用指定 HTML 标题`#`字符开头的行。 
  数`#`字符对应于标题的层次结构级别 (例如，`#` = `<h1>`和`###` = ```<h3>```)。
* **编号列表︰**要开始与行编号 （有序） 列表`1. `。  
  如果您希望在单个列表元素中的多个元素，设置您的列表格式，如下所示︰
```        
1.  For the first element (like this one), insert a tab stop after the 1. 

    To include a second element (like this one), insert a line break after the first and align indentations.
```
若要获取此输出︰

1.  第一个元素 （如此一个），将插入制表位后 1。 

    若要包括的第二个元素 （如此一个），在第一个之后插入换行符的位置和对齐缩进量。

* **项目符号列表︰**项目符号列表几乎是相同的排序列表除了到`1. `已替换为以下一项`* `， `- `，或`+ `。 多个元素列表与排序的列表的工作方式相同。
* **链接︰**超链接的语法如下`[visible link text](link URL)`。
* **链接到同一 docset 内的其他主题︰**Docset 是此资源库中 （例如，"dsc"，"脚本"） 的顶级文件夹。
    指向同一 docset 内的主题的超链接的语法如下`[topic title](relative path to topic)`。 
    有关详细信息，请参阅[自述文件中的相对链接](https://help.github.com/articles/relative-links-in-readmes/)。 
    要链接到另一个顶级文件夹中的主题，请使用发布页面的 URL，根据上述内容。
