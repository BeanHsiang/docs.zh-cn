---
title: WPF 社区反馈
ms.date: 03/01/2018
helpviewer_keywords:
- community resources [WPF]
- forums [WPF]
- bug descriptions [WPF]
ms.assetid: 468b060a-d54b-4900-a74a-9faccb554045
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f77058ac0cb87d0316395bce1dfb11401a2ce806
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54585336"
---
# <a name="wpf-community-feedback"></a>WPF 社区反馈

Microsoft 公开各种社区资源以便于你了解、 讨论并提供在 Windows Presentation Foundation (WPF) 的反馈。 这些资源包括论坛并[Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)站点。 每种社区资源的优点各不相同。 是一组使用每个特别大型社区和 Microsoft 确保最佳的响应的最佳实践是在这里，介绍这些优点。

> [!NOTE]
> 不要使用位于每个页面底部的反馈部分来发送产品反馈。 这些链接仅用于发送文档反馈。

## <a name="forums"></a>论坛

[WPF 论坛](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=wpf)是用于讨论和解决问题的主要社区资源。 论坛通过提供一整套支持功能来便于讨论和解决问题，其中包括：

- 搜索。
- 讨论跟踪。
- 丰富的文本和代码格式。
- Visual Studio 集成。
- 最具价值专家 (MVP) 和社区参与。
- 确保以最快速度响应文章的监视功能。

为您提出有关 WPF 社区的问题的另一个选项是[Stack Overflow](https://stackoverflow.com/questions/tagged/wpf)。

### <a name="forum-best-practices"></a>论坛最佳做法

使用以下最佳做法可帮助以解决问题中尽可能快速地发布到 WPF 论坛。 这些做法适用于所有论坛。

#### <a name="search-existing-posts"></a>搜索现有文章

某些问题普遍存在，在你之前，其他人已经遇到过这些问题。 因此，你可以快速解决问题，也可以在现有讨论中添加意见。

#### <a name="use-meaningful-titles"></a>使用有意义的标题

简明而有意义的标题来提高您的发布的可发现性。 它们也便于其他 WPF 论坛的社区成员以确定是否能够解决您的问题。

#### <a name="include-appropriate-content"></a>包含相应的内容

描述问题和如何尝试完成本指南。 如有可能，请包含支持的代码段或可能的最简单示例以演示问题。 所有这些详细信息都将有助于增加快速解答问题的机会。

## <a name="visual-studio-developer-community"></a>Visual Studio 开发者社区

有时，问题可能会难以解决或无法解决。 出现这些情况是因为技术中有 Bug、将技术应用到特定方案存在困难或缺少对特定方案的支持。 此信息很重要给 Microsoft，并可以通过提供[Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)站点。

在 WPF 产品反馈中心上发布的项将被路由到 WPF 团队的内部 bug 数据库。 因此，它是最可靠的方式向 WPF 功能所有者获取你的反馈。 此外，你可以验证和跟踪建议与 bug 以及对它们投票，从而可帮助 WPF 团队确定问题优先级。

### <a name="developer-community-best-practices"></a>开发人员社区最佳做法

在发布到 Visual Studio 开发人员社区，搜索现有发布的文章，提供有意义的标题和适当的内容是重要的最佳实践，就像它们是在 WPF 论坛发布帖子。 下面列出了一些还应使用的其他最佳做法。

#### <a name="search-existing-posts"></a>搜索现有文章

某些问题普遍存在，在你之前，其他人已经遇到过这些问题。 因此，你可以快速解决问题，或者可以添加您的输入现有问题。

#### <a name="use-meaningful-titles"></a>使用有意义的标题

简明而有意义的标题可增加你的问题在最短时间内定向到最合适的 WPF 团队的机会。 这是对于 WPF，其中包含许多相关的功能等技术尤其重要。

#### <a name="describe-how-to-reproduce-your-bug"></a>说明如何重现 bug

发布有关 Bug 的文章时，包含以下相关内容很重要：

- 提供清晰的 Bug 说明。
- 使用代码段支持 Bug 说明。
- 提供用于演示如何重现 Bug 的步骤列表。
- 包含有可能是用于重现 Bug 的最小代码示例。
- 指明 Bug 是否可以一成不变地重现。
- 包含相关的异常信息。

 如果 Bug 与安装或设置有关，请附加相关的安装日志和快照（位于 %temp% 文件夹中带有“dd_”前缀的文件）。

 对于编译或生成问题，请附加生成日志。 通过使用 /v： 开关从命令行或通过配置相应级别从集成开发环境 (IDE) 与 Visual Studio 一样，的 MSBuild 系统可以配置为支持具有多种详细级别的日志记录。

#### <a name="provide-environment-information"></a>提供环境信息

背景信息通常可用于向文章添加上下文。 具体而言，提到的操作系统平台、 处理器系列和体系结构，如"Windows 10 版本 1709，intel （） 至强®，x64。"

如果所发布的问题与呈现相关，还应包含图形卡和驱动程序详细信息（如有可能）。 此信息很重要，因为 WPF 是一个演示框架。

#### <a name="provide-solution-or-project-information"></a>提供的解决方案或项目信息

Bug 可能与用于开发和生成应用程序的工具以及生成的应用程序的类型有关。 因此，可以用于指定以下信息：

- 生成的应用程序的类型，如：
  - 应用程序 (*.exe*) 或库 (*.dll*)
  - Extensible Application Markup Language (XAML) 浏览器应用程序 (XBAP)
  - 松散 XAML 应用程序
  - 独立安装应用程序
  - ClickOnce 部署的独立应用程序
- 开发工具，如：
  - MSBuild
  - Expression Graphic Designer
  - Expression Interactive Designer
  - Visual Studio
- 解决方案配置，如：
  - 一种解决方案
  - 单个项目
  - 具有多个依赖项目的解决方案
- 应用程序是否具有特定于语言或非特定于语言的资源。 例如，是否为 `Application`、`Page` 和 `Resource` 类型指定了 `UICulture` 项目属性或可本地化的元数据？
- 是否在 AssemblyInfo.cs 或 AssemblyInfo.vb 文件中使用了非特定于语言的设置。

#### <a name="provide-scenario-and-impact-information"></a>提供方案和影响信息

提供有关显示 bug 及其影响的情况的信息。 它确定是否、 何时以及如何修复问题或是否可以改用可接受的解决方法时，此信息是对 WPF 团队非常重要。

通常，故障和数据丢失方案具有重大影响，因此也最容易确定优先级。 但是，某些 Bug 仅显示在不常见的方案中，在有些情况下这些方案也可能是主线方案。 提供有关方案和影响上下文帮助 WPF 团队做出正确的决策。

## <a name="see-also"></a>请参阅

- [如何报告 Visual Studio 2017 的问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)
