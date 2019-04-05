---
title: .NET Core 全局工具
description: 概述：介绍 .NET Core 全局工具及其适用的 .NET Core CLI 命令。
author: KathleenDollard
ms.date: 05/29/2018
ms.custom: seodec18
ms.openlocfilehash: 3bbf1e7953482dc07f05570443cf640a9fab6258
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53170831"
---
# <a name="net-core-global-tools-overview"></a>.NET Core 全局工具概述

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

.NET Core 全局工具是一种特殊的 NuGet 包，其中包含控制台应用程序。 全局工具可安装在计算机上的默认位置（包含在 PATH 环境变量中）或自定义位置。

若要使用 .NET Core 全局工具，请执行以下操作：

* 查找该工具的相关信息（通常是一个网站或 GitHub 页面）。
* 在源的主页（通常为 NuGet.org）查看作者和统计信息。
* 安装该工具。
* 调用该工具。
* 更新该工具。
* 卸载该工具。

> [!IMPORTANT]
> .NET Core 全局工具在路径中显示，且以完全信任的方式运行。 除非你信任工具作者，否则请勿安装 .NET Core 全局工具。

## <a name="find-a-net-core-global-tool"></a>查找 .NET Core 全局工具

目前，.NET Core 命令行接口 (CLI) 中没有全局工具搜索功能。

可在 [NuGet](https://www.nuget.org) 上查找 .NET Core 全局工具。 但是 NuGet 尚不能专门针对 .NET Core 全局工具进行搜索。

还可在博客文章或 [natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) GitHub 存储库中找到工具建议。

也可以在 [aspnet/DotNetTools](https://github.com/aspnet/DotNetTools/) GitHub 存储库查看 ASP.NET 团队创建的全局工具的源代码。

## <a name="check-the-author-and-statistics"></a>查看作者和统计信息

由于 .NET Core 全局工具以完全信任的方式运行且通常安装在你的路径中，所以它们的作用会很强大。 请勿下载不信任的人提供的工具。

如果该工具在 NuGet 中托管，可以通过搜索该工具来查看作者和统计信息。

## <a name="install-a-global-tool"></a>安装全局工具

若要安装全局工具，请使用 [dotnet tool install](dotnet-tool-install.md) .NET Core CLI 命令。 下面的示例演示如何在默认位置安装全局工具：

```console
dotnet tool install -g dotnetsay
```

如果无法安装该工具，则会显示错误消息。 检查所需源是否正在被检查。

如果想安装工具的预发布版本或特定版本，可以采用以下格式指定版本号：

```console
dotnet tool install -g <package-name> --version <version-number>
```

如果安装成功，会出现一条消息，显示用于调用工具的命令以及所安装的版本，类似于以下示例：

```
You can invoke the tool using the following command: dotnetsay
Tool 'dotnetsay' (version '2.0.0') was successfully installed.
```

全局工具可安装在默认目录或特定位置中。 默认目录为：

| (OS)          | 路径                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

这些位置在首次运行 SDK 时添加到用户的路径，所以可以直接调用安装在这里的全局工具。

请注意，全局工具是特定于用户的，而不是针对计算机全局的。 特定于用户的意思是无法在一台计算机上安装所有用户都可用的全局工具。 只有安装了该工具的用户配置文件才能使用它。

也可在特定目录安装全局工具。 如果在特定目录安装全局工具，用户必须确保命令是可用的，方法是将该目录添加至路径、使用指定目录调用命令或从特定目录调用该工具。
在这种情况下，.NET Core CLI 不将此地址自动添加至 PATH 环境变量。

## <a name="use-the-tool"></a>使用该工具

安装工具后，可以使用它的命令来调用它。 注意，该命令可能和包名称不同。

如果该命令为 `dotnetsay`，可以使用以下内容调用它：

```console
dotnetsay
```

如果工具作者希望工具出现在 `dotnet` 提示符的上下文中，他们可能采用称为 `dotnet <command>` 的方式进行编写，例如：

```console
dotnet doc
```

若要查找安装的全局工具包中包含哪些工具，可以使用 [dotnet tool list](dotnet-tool-list.md) 命令列出安装的包。

若要查看使用说明，可以访问工具的网站或键入下列命令之一：

```console
<command> --help
dotnet <command> --help
```

### <a name="what-could-go-wrong"></a>可能出现的问题

全局工具是[依赖框架的应用程序](../deploying/index.md#framework-dependent-deployments-fdd)，也就是说它们依赖于计算机上安装的 .NET Core 运行时。 如果没有找到所需的运行时，则遵循常规的 .NET Core 运行时前滚规则，例如：

* 应用程序前滚至指定的主要版本和次要版本的最高修补程序版本。
* 如果主要版本号和次要版本号没有匹配的运行时，则使用下一个较高的次要版本。
* 前滚不会发生在运行时的预览版之间，也不会发生在预览版和发行版之间。 因此，使用预览版创建的全局工具必须由作者重新生成和重新发布，再重新安装。
* 在 .NET Core 2.1 Preview 1 中创建的全局工具可能会出现其他问题。 有关详细信息，请参阅 [.NET Core 2.1 Preview 2 已知的问题](https://github.com/dotnet/core/blob/master/release-notes/2.1/Preview/2.1.0-preview2-known-issues.md)。

如果应用程序无法找到合适的运行时，它就无法运行并报告错误。

另一个可能出现的问题是，在较早预览版中创建的全局工具不能在当前安装的 .NET Core 运行时中运行。 若要查看计算机上安装了哪些运行时，可以使用以下命令：

```console
dotnet --list-runtimes
```

与全局工具的作者联系，看看他们是否能重新编译工具包，并将更新了版本号的工具包重新发布至 NuGet。 如果作者更新了 NuGet 上的包，用户便可更新副本。

.NET Core CLI 在首次使用时尝试将默认位置添加到 PATH 环境变量。 但是，在某些情况下，位置不会自动添加至 PATH，例如：

* 如果已设置 `DOTNET_SKIP_FIRST_TIME_EXPERIENCE` 环境变量。
* 如果已在 macOS 上使用 .tar.gz 文件（而不是 .pkg）安装了 .NET Core SDK。
* 在 Linux 上，需要编辑 shell 环境文件来配置 PATH。

## <a name="other-cli-commands"></a>其他 CLI 命令

.NET Core SDK 包含支持 .NET Core 全局工具的其他命令。 将 `dotnet tool` 命令用于以下选项之一：

* `--global` 或 `-g` 指定命令用于用户范围的全局工具。
* `--tool-path` 指定全局工具的自定义位置。

若要了解哪些命令可用于全局工具：

```console
dotnet tool --help
```

更新全局工具涉及卸载该工具并重新安装它的最新稳定版。 若要更新全局工具，请使用 [dotnet tool update](dotnet-tool-update.md) 命令：

```console
dotnet tool update -g <packagename>
```

使用 [dotnet tool uninstall](dotnet-tool-uninstall.md) 命令删除全局工具：

```console
dotnet tool uninstall -g <packagename>
```

若要显示计算机上目前安装的所有全局工具及其版本和命令，请使用 [dotnet tool list](dotnet-tool-list.md) 命令：

```console
dotnet tool list -g
```