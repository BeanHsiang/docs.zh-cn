# <a name="contributing"></a>参与

感谢你对参与 .NET 文档的关注！

> 我们正在将我们的指导原则转变为网站级参与指南。 
> 若要查看新指南，请访问 [Microsoft Docs 参与者指南概述](https://docs.microsoft.com/contribute/)。

本文档介绍了参与到 [.NET 文档站点](https://docs.microsoft.com/dotnet)上托管的文章和代码示例中的过程。 参与内容可简（更正拼写错误），可繁（编写新文章）。

* [参与流程](#process-for-contributing)
* [C# 交互式体验](#the-c-interactive-experience)
* [注意事项](#dos-and-donts)
* [参与者许可协议](#contributor-license-agreement)

此存储库包含适用于 .NET 的概念文档。 .NET 文档站点建立在多个存储库的基础上，还包括下面这个：

- [代码示例和代码片段](https://github.com/dotnet/samples)
- [API 参考](https://github.com/dotnet/dotnet-api-docs)
- [.NET Compiler Platform SDK 参考](https://github.com/dotnet/roslyn-api-docs)

可在此处跟踪所有这些存储库的问题和任务。

## <a name="process-for-contributing"></a>参与流程

需要对 [Git 和 GitHub.com](https://guides.github.com/activities/hello-world/) 有基本的理解。

**步骤 1：** 对于小更改，可跳过这一步。 如果有意编写新内容或彻底修改现有内容，请打开[问题](https://github.com/dotnet/docs/issues)，描述要执行的操作。
“文档”文件夹中的内容划分为在目录 (TOC) 中反应的不同部分。 定义主题在 TOC 中的位置。 获取对建议的反馈。

或

还可以从现有问题中进行选择，了解哪些是热门的社区发布内容。 [.NET 社区参与者项目](https://github.com/dotnet/docs/projects/35)列出了许多可用于社区参与者的工作项。 根据你的兴趣和承诺水平，可从以下类别的问题中作出选择：

- **维护**。 此类别包括相当简单的发布内容，如修复损坏或不正确的链接，添加缺少的代码示例，或处理有限内容问题。 在某些情况下，这些问题可能会涉及大量文件。 在此情况下，应让我们知道在开始之前你想要处理的内容。

- **内容更新**。 考虑到文档集比较庞大，内容很容易过时且需要修改。 此外，由于各种原因，会对一些内容进行备份甚至双重备份。 更新内容包括确保单个主题是最新的，或者修改功能区域中的内容以消除重复，并确保所有唯一内容都保存在较小的文档集中。

- **新内容创作**。 如果了解如何创作你自己的主题，这些问题将列出我们知道要添加到文档集的主题。 不过，在你开始研究某个主题之前，请告知我们。 如果你有意编写此处未列出的主题，请提问。 

此外可以查看我们的[待解决问题](https://github.com/dotnet/docs/issues)列表，并自愿参与你感兴趣的工作。 我们使用[空缺](https://github.com/dotnet/docs/labels/up-for-grabs)标签来标记公开供参与的问题。 

**步骤 2：** 根据需要对 `dotnet/docs`、`dotnet/samples` 或 `dotnet/dotnet-api-docs` 存储库进行分支，并为所做更改创建分支。

对于较小的更改，可以使用 GitHub 的 Web 界面。 只需单击要更改的文件上的“编辑此项目分支中的文件”。 在提交所做的更改时，GitHub 会为你创建新分支。

**步骤 3：** 对该新分支进行更改。

如果要新建主题，可以使用此[模板文件](./styleguide/template.md)作为起点。 它包含编写指南，还介绍了每篇文章所需的元数据，例如作者信息。

导航到与步骤 1 中为文章确定的 TOC 位置对应的文件夹。
该文件夹包含该部分中的所有文章的 Markdown 文件。
如有必要，可以创建一个新文件夹来放置内容文件。 该部分的主要文章称为“index.md”。
对于图像和其他静态资源，在包含项目的文件夹内创建名为“媒体”的子文件夹（如果尚不存在）。 在“媒体”文件夹中，使用项目名称创建一个子文件夹（索引文件除外）。
在存储库根目录下的“示例”文件夹中包含更大示例。

请务必遵循正确的 Markdown 语法。 有关详细信息，请参阅[风格指南](./styleguide/template.md)。

### <a name="example-structure"></a>结构示例

    docs
      /about
      /core
        /porting
          porting-overview.md
          /media
            /porting-overview
                portability_report.png

**步骤 4：** 从分支中将拉取请求 (PR) 提交到 `dotnet/docs/master`。

PR 应始终面向主分支。 你应从不打开面向活动分支的 PR。

每个 PR 通常应该一次解决一个问题。 PR 可以修改一个或多个文件。 如果要处理不同文件的多个修补程序，最好是使用单独的 PR。

如果 PR 正在解决现有问题，请将 `Fixes #Issue_Number` 关键字添加到提交消息或 PR 描述中。 以此，在合并 PR 时将自动关闭该问题。 有关详细信息，请参阅[通过提交消息关闭问题](https://help.github.com/articles/closing-issues-via-commit-messages/)。

.NET 团队将审核 PR，并告知是否需要进行任何其他更新/更改才能批准。

**步骤 5：** 与团队讨论后，对分支进行必要的更新。

一旦应用反馈并批准所做的更改，维护人员会将 PR 合并到主分支。

我们会以某种节奏，将所有提交从主分支推送到实时分支，你将能在 https://docs.microsoft.com/dotnet/ 中实时看到你的参与内容。

### <a name="contributing-to-samples"></a>提供示例

我们对存储库中存在的代码做如下区分：

- 示例：读者可以下载并运行示例。 所有示例应都为完整的应用程序或库。 在示例创建库的位置，它应包括单元测试或允许读者运行代码的应用程序。

- 代码段：说明较小的概念或任务。 它们可以编译，但并不是完整的应用程序。

所有代码都位于 [dotnet/samples](https://github.com/dotnet/samples) 存储库中。 我们正在努力建立一个示例文件夹结构与文档文件夹结构匹配的模型。 我们将遵循如下标准：

- 顶级“代码段”文件夹包含小型、集中式示例代码段。
- API 参考示例已置于遵循以下模式的文件夹中：代码段/\<语言>/api/\<命名空间>/\<apiname>。
- 其他顶级文件夹与“文档”存储库中的顶级文件夹匹配。 例如，文档存储库具有“机器学习/教程”文件夹，机器学习教程示例位于“示例/机器学习/教程”文件夹。

此外，“核心”和“标准”文件夹下的所有示例都应在 .NET Core 支持的所有平台上构建和运行。 我们的 CI 生成系统会强制此要求。 顶级“框架”文件夹包含仅在 Windows 上生成和验证的示例。

我们可以在文档存储库添加新内容时扩展这些目录。 例如，我们将添加 Xamarin 目录，如 `xamarin-ios` 和 `xamarin-android` 目录。

创建的每个完整示例都应包含“readme.md”文件。 此文件应包含示例的简短说明（一个或两个段落）。 “readme.md”应告知读者通过研究此示例他们将了解到的内容。 “Readme.md”文件还应包含到 [.NET 文档站点](https://docs.microsoft.com/dotnet/welcome)上实时文档的链接。
要确定存储库中给定文件映射到该站点的位置，请将存储库路径中的 `/docs` 替换为 `https://docs.microsoft.com/dotnet`。

主题还将包含该示例的链接。 直接链接到 GitHub 上的示例文件夹。

有关详细信息，请参阅[示例自述文件](https://github.com/dotnet/samples/blob/master/README.md)。

## <a name="the-c-interactive-experience"></a>C# 交互式体验

C# 中的简短代码示例可以使用 `csharp-interactive` 语言标记来指定浏览器中运行的 C# 示例。 （内联代码示例使用 `csharp-interactive` 标记，对于源代码中包含的代码段，请使用 `code-csharp-interactive` 标记。）这些代码示例在本文中显示一个代码窗口和一个输出窗口。 输出窗口显示用户运行示例后执行交互式代码的任何输出。 

C# 交互式体验改变了我们使用示例的方式。 访问者可以运行该示例以查看结果。 很多因素有助于确定示例或相应的文本是否应包括有关输出的信息。

### <a name="when-to-display-the-expected-output-without-running-the-sample"></a>在不运行示例的情况下何时显示预期输出

- 面向初学者的文章应提供输出，以便读者能够将其工作输出与预期答案进行比较。
- 输出对于主题不可或缺的示例应显示该输出。 例如，关于格式化文本的文章应在不运行示例的情况下显示文本格式。
- 当示例和预期输出都很短时，请考虑显示输出。 它可以节省一些时间。
- 说明当前区域性或固定区域性如何影响输出的文章应解释预期输出。 交互式 REPL（读取评估打印循环）在基于 Linux 的主机上运行。 默认区域性和固定区域性在不同的操作系统和计算机上生成不同输出。 本文应介绍 Windows、Linux 和 Mac 系统中的输出。

### <a name="when-to-exclude-expected-output-from-the-sample"></a>何时不在示例中包含预期输出 

- 示例生成较大输出的文章不应在注释中包含该输出。 运行该示例后，它会遮盖代码。
- 示例演示一个主题但输出并不是理解它的必要条件的文章。 例如，运行 LINQ 查询来解释查询语法，然后显示输出集合中的每个项的代码。

## <a name="dos-and-donts"></a>注意事项

以下列表显示了一些指导规则，当你参与 .NET 文档时应牢记其中的内容：

- 请勿发出大型拉取请求。 可以提出问题并发起讨论，以便我们在你花费大量时间前确定方向。
- 请务必阅读[风格指南](./styleguide/template.md)以及[语气和语调](./styleguide/voice-tone.md)指南。
- 请务必使用[模板](./styleguide/template.md)文件作为工作的起点。
- 请务必在处理文章前，在分叉上创建一个单独的分支。
- 请务必遵循 [GitHub 流工作流](https://guides.github.com/introduction/flow/)。
- 请务必在博客和推文（或任何社交软件上）频繁地发布你的参与内容！

> 注意：你或许会注意到某些主题目前并没有遵循此处指定的所有准则和[风格指南](./styleguide/template.md)。 我们正努力实现整个站点的一致性。 请查看我们当前正在跟踪的有关此特定目标的[未解决问题](https://github.com/dotnet/docs/issues?q=is%3Aissue+is%3Aopen+label%3Aguidelines-adherence)列表。

## <a name="contributor-license-agreement"></a>贡献者许可协议

在合并 PR 前，必须签署 [.NET Foundation 贡献许可协议 (CLA)](https://cla.dotnetfoundation.org)。 对于 .NET Foundation 中的项目，只需签署一次即可。 可在维基百科上详细了解[贡献许可协议 (CLA)](https://en.wikipedia.org/wiki/Contributor_License_Agreement)。

协议：[net-foundation-contribution-license-agreement.pdf](https://github.com/dotnet/home/blob/master/guidance/net-foundation-contribution-license-agreement.pdf)

无需事先签署该协议。 可如常克隆、创建分支并提交 PR。 创建 PR 后，将由 CLA 自动程序对其分类。 如果更改的内容十分琐碎（如修复了拼写错误），则 PR 会被标记为 `cla-not-required`。 其他情况下，会分类为 `cla-required`。 签署 CLA 后，当前和所有未来的拉取请求都会被标记为 `cla-signed`。
