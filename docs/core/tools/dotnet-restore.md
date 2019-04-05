---
title: dotnet restore 命令
description: 了解如何使用 dotnet-restore 命令还原依赖项和特定于项目的工具。
ms.date: 05/29/2018
ms.openlocfilehash: 6f54671fcd1c17d2466d5a38027e02da5e7494e9
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53170777"
---
# <a name="dotnet-restore"></a>dotnet restore

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet restore` - 恢复项目的依赖项和工具。

## <a name="synopsis"></a>摘要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet restore [<ROOT>] [--configfile] [--disable-parallel] [--force] [--ignore-failed-sources] [--no-cache]
    [--no-dependencies] [--packages] [-r|--runtime] [-s|--source] [-v|--verbosity] [--interactive]
dotnet restore [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet restore [<ROOT>] [--configfile] [--disable-parallel] [--ignore-failed-sources] [--no-cache]
    [--no-dependencies] [--packages] [-r|--runtime] [-s|--source] [-v|--verbosity]
dotnet restore [-h|--help]
```
---

## <a name="description"></a>说明

`dotnet restore` 命令使用 NuGet 还原依赖项以及在 project 文件中指定的特定于项目的工具。 默认情况下会并行执行对依赖项和工具的还原。

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

为了还原依赖项，NuGet 需要包所在的源。 通常通过 *NuGet.config* 配置文件提供源。 安装 CLI 工具时提供一个默认的配置文件。 可以通过在项目目录中创建自己的 *NuGet.config* 文件来指定其他源。 也可以在命令提示符处指定每次调用的其他源。

对于依赖项，使用 `--packages` 参数指定还原操作期间放置还原包的位置。 如未指定，将使用默认的 NuGet 包缓存，可在所有操作系统上的用户主目录中的 `.nuget/packages` 目录找到它。 例如 Linux 上的 /home/user1 或 Windows 上的 C:\Users\user1。

对于特定于项目的工具，`dotnet restore` 首先还原打包工具所在的包，然后继续还原 project 文件中指定的工具依赖项。

`dotnet restore` 命令的行为会受 Nuget.Config 文件（如果有）中某些设置的影响。 例如，在 NuGet.Config 中设置 `globalPackagesFolder` 会将还原的 NuGet 包置于指定的文件夹中。 这是在 `dotnet restore` 命令中指定 `--packages` 选项的替代方法。 有关详细信息，请参阅 [NuGet.Config reference](/nuget/schema/nuget-config-file)（NuGet.Config 引用）。

## <a name="implicit-dotnet-restore"></a>隐式 `dotnet restore`

从 .Net Core 2.0 开始，当发出下列命令时，如有必要，将隐式运行 `dotnet restore`。

- [`dotnet new`](dotnet-new.md)
- [`dotnet build`](dotnet-build.md)
- [`dotnet build-server`](dotnet-build-server.md)
- [`dotnet run`](dotnet-run.md)
- [`dotnet test`](dotnet-test.md)
- [`dotnet publish`](dotnet-publish.md)
- [`dotnet pack`](dotnet-pack.md)

在大多数情况下，不再需要显式使用 `dotnet restore` 命令。

有时，隐式运行 `dotnet restore` 可能不方便。 例如，某些自动化系统（如生成系统）需要显式调用 `dotnet restore`，以控制还原发生的时间，以便可以控制网络使用量。 要防止隐式运行 `dotnet restore`，可以通过上述任意命令使用 `--no-restore` 标记以禁用隐式还原。

## <a name="arguments"></a>自变量

`ROOT`

要还原的项目文件的可选路径。

## <a name="options"></a>选项

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--configfile <FILE>`

供还原操作使用的 NuGet 配置文件 (*NuGet.config*)。

`--disable-parallel`

禁用并行还原多个项目。

`--force`

强制解析所有依赖项，即使上次还原已成功，也不例外。 指定此标记等同于删除 project.assets.json 文件。

`-h|--help`

打印出有关命令的简短帮助。

`--ignore-failed-sources`

如果存在符合版本要求的包，则源失败时警告。

`--no-cache`

指定不缓存包和 HTTP 请求。

`--no-dependencies`

当使用项目到项目 (P2P) 引用还原项目时，还原根项目，不还原引用。

`--packages <PACKAGES_DIRECTORY>`

指定还原包的目录。

`-r|--runtime <RUNTIME_IDENTIFIER>`

指定程序包还原的运行时。 这用于还原 *.csproj* 文件中的 `<RuntimeIdentifiers>` 标记中未显式列出的运行时的程序包。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。 通过多次指定此选项提供多个 RID。

`-s|--source <SOURCE>`

指定要在还原操作期间使用的 NuGet 包源。 此设置会替代 NuGet.config 文件中指定的所有源。 多次指定此选项可以提供多个源。

`--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

`--interactive`

允许命令停止并等待用户输入或操作（例如，完成身份验证）。 从 .NET Core 2.1.400 开始。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--configfile <FILE>`

供还原操作使用的 NuGet 配置文件 (*NuGet.config*)。

`--disable-parallel`

禁用并行还原多个项目。

`-h|--help`

打印出有关命令的简短帮助。

`--ignore-failed-sources`

如果存在符合版本要求的包，则源失败时警告。

`--no-cache`

指定不缓存包和 HTTP 请求。

`--no-dependencies`

当使用项目到项目 (P2P) 引用还原项目时，还原根项目，不还原引用。

`--packages <PACKAGES_DIRECTORY>`

指定还原包的目录。

`-r|--runtime <RUNTIME_IDENTIFIER>`

指定程序包还原的运行时。 这用于还原 *.csproj* 文件中的 `<RuntimeIdentifiers>` 标记中未显式列出的运行时的程序包。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。 通过多次指定此选项提供多个 RID。

`-s|--source <SOURCE>`

指定要在还原操作期间使用的 NuGet 包源。 这会替代 NuGet.config 文件中指定的所有源。 多次指定此选项可以提供多个源。

`--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

---

## <a name="examples"></a>示例

还原当前目录中项目的依赖项和工具：

`dotnet restore`

还原在给定路径中找到的 `app1` 项目的依赖项和工具：

`dotnet restore ~/projects/app1/app1.csproj`

通过将提供的文件路径用作源，在当前目录中还原项目的依赖项和工具：

`dotnet restore -s c:\packages\mypackages`

通过将提供的两个文件路径用作源，在当前目录中还原项目的依赖项和工具：

`dotnet restore -s c:\packages\mypackages -s c:\packages\myotherpackages`

还原当前目录中项目的依赖项和工具，并仅显示最少的输出：

`dotnet restore --verbosity minimal`
