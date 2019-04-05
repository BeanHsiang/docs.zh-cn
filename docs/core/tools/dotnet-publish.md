---
title: dotnet publish 命令
description: dotnet publish 命令可将 .NET Core 项目发布到目录。
ms.date: 05/29/2018
ms.openlocfilehash: 40ce31073ee3f6f94e110f3a4e1eeda0c7b2e48d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54559274"
---
# <a name="dotnet-publish"></a>dotnet 发布

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet publish` - 将应用程序及其依赖项打包到文件夹以部署到托管系统。

## <a name="synopsis"></a>摘要

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)
```
dotnet publish [<PROJECT>] [-c|--configuration] [-f|--framework] [--force] [--manifest] [--no-build] [--no-dependencies]
    [--no-restore] [-o|--output] [-r|--runtime] [--self-contained] [-v|--verbosity] [--version-suffix]
dotnet publish [-h|--help]
```
# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)
```
dotnet publish [<PROJECT>] [-c|--configuration] [-f|--framework] [--force] [--manifest] [--no-dependencies]
    [--no-restore] [-o|--output] [-r|--runtime] [--self-contained] [-v|--verbosity] [--version-suffix]
dotnet publish [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet publish [<PROJECT>] [-c|--configuration] [-f|--framework] [-o|--output] [-r|--runtime] [-v|--verbosity]
    [--version-suffix]
dotnet publish [-h|--help]
```
---

## <a name="description"></a>说明

`dotnet publish` 编译应用程序、读取 project 文件中指定的所有依赖项并将生成的文件集发布到目录。 输出包括以下资产：

* 扩展名为 dll 的程序集中的中间语言 (IL) 代码。
* 包含项目所有依赖项的 .deps.json 文件。
* .runtime.config.json 文件，其中指定了应用程序所需的共享运行时，以及运行时的其他配置选项（例如，垃圾回收类型）。
* 应用程序的依赖项，将这些依赖项从 NuGet 缓存复制到输出文件夹。

`dotnet publish` 命令的输出可供部署至托管系统（例如服务器、电脑、Mac、笔记本电脑）以便执行。 若要准备用于部署的应用程序，这是唯一正式受支持的方法。 根据项目指定的部署的类型，托管系统不一定已在其上安装 .NET Core 共享运行时。 有关详细信息，请参阅 [.NET Core 应用程序部署](../deploying/index.md)。 有关已发布应用程序的目录结构，请参阅[目录结构](/aspnet/core/hosting/directory-structure)。

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="arguments"></a>自变量

`PROJECT`

要发布的项目。 它是 [C#](csproj.md)、F# 或 Visual Basic 项目文件的路径和文件名，或包含 C#、F# 或 Visual Basic 项目文件的目录的路径。 如果未指定，则默认为当前目录。

## <a name="options"></a>选项

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`。

`-f|--framework <FRAMEWORK>`

为指定的[目标框架](../../standard/frameworks.md)发布应用程序。 必须在项目文件中指定目标框架。

`--force`

强制解析所有依赖项，即使上次还原已成功，也不例外。 指定此标记等同于删除 project.assets.json 文件。

`-h|--help`

打印出有关命令的简短帮助。

`--manifest <PATH_TO_MANIFEST_FILE>`

指定一个或多个[目标清单](../deploying/runtime-store.md)，用于剪裁与应用程序一同发布的一组包。 清单文件是 [`dotnet store` 命令](dotnet-store.md)输出的一部分。 若要指定多个清单，请为每个清单添加一个 `--manifest` 选项。 自 .NET Core 2.0 SDK 起，可以使用此选项。

`--no-build`

发布前不生成项目。 还将隐式设置 `--no-restore` 标记。

`--no-dependencies`

忽略项目间引用，仅还原根项目。

`--no-restore`

运行此命令时不执行隐式还原。

`-o|--output <OUTPUT_DIRECTORY>`

指定输出目录的路径。 如未指定，对于依赖于框架的部署，将默认为 ./bin/[configuration]/[framework]/publish/ 或对于独立部署，将默认为 ./bin/[configuration]/[framework]/[runtime]/publish/。
如果路径是相对的，则生成的输出目录与项目文件位置相关，而与当前工作目录不相关。

`--self-contained`

与应用程序一同发布 .NET Core 运行时，因此无需在目标计算机上安装运行时。 如果指定了运行时标识符，默认值为 `true`。 若要详细了解不同的部署类型，请参阅 [.NET Core 应用程序部署](../deploying/index.md)。

`-r|--runtime <RUNTIME_IDENTIFIER>`

发布针对给定运行时的应用程序。 这将在创建[独立部署 (SCD)](../deploying/index.md#self-contained-deployments-scd) 时使用。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。 默认为发布[依赖于框架的部署 (FDD)](../deploying/index.md#framework-dependent-deployments-fdd)。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

`--version-suffix <VERSION_SUFFIX>`

定义版本后缀来替换项目文件的版本字段中的星号 (`*`)。

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`。

`-f|--framework <FRAMEWORK>`

为指定的[目标框架](../../standard/frameworks.md)发布应用程序。 必须在项目文件中指定目标框架。

`--force`

强制解析所有依赖项，即使上次还原已成功，也不例外。 指定此标记等同于删除 project.assets.json 文件。

`-h|--help`

打印出有关命令的简短帮助。

`--manifest <PATH_TO_MANIFEST_FILE>`

指定一个或多个[目标清单](../deploying/runtime-store.md)，用于剪裁与应用程序一同发布的一组包。 清单文件是 [`dotnet store` 命令](dotnet-store.md)输出的一部分。 若要指定多个清单，请为每个清单添加一个 `--manifest` 选项。 自 .NET Core 2.0 SDK 起，可以使用此选项。

`--no-dependencies`

忽略项目间引用，仅还原根项目。

`--no-restore`

运行此命令时不执行隐式还原。

`-o|--output <OUTPUT_DIRECTORY>`

指定输出目录的路径。 如未指定，对于依赖于框架的部署，将默认为 ./bin/[configuration]/[framework]/publish/ 或对于独立部署，将默认为 ./bin/[configuration]/[framework]/[runtime]/publish/。
如果路径是相对的，则生成的输出目录与项目文件位置相关，而与当前工作目录不相关。

`--self-contained`

与应用程序一同发布 .NET Core 运行时，因此无需在目标计算机上安装运行时。 如果指定了运行时标识符，默认值为 `true`。 若要详细了解不同的部署类型，请参阅 [.NET Core 应用程序部署](../deploying/index.md)。

`-r|--runtime <RUNTIME_IDENTIFIER>`

发布针对给定运行时的应用程序。 这将在创建[独立部署 (SCD)](../deploying/index.md#self-contained-deployments-scd) 时使用。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。 默认为发布[依赖于框架的部署 (FDD)](../deploying/index.md#framework-dependent-deployments-fdd)。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

`--version-suffix <VERSION_SUFFIX>`

定义版本后缀来替换项目文件的版本字段中的星号 (`*`)。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`。

`-f|--framework <FRAMEWORK>`

为指定的[目标框架](../../standard/frameworks.md)发布应用程序。 必须在项目文件中指定目标框架。

`-h|--help`

打印出有关命令的简短帮助。

`--manifest <PATH_TO_MANIFEST_FILE>`

指定一个或多个[目标清单](../deploying/runtime-store.md)，用于剪裁与应用程序一同发布的一组包。 清单文件是 [`dotnet store` 命令](dotnet-store.md)输出的一部分。 若要指定多个清单，请为每个清单添加一个 `--manifest` 选项。 自 .NET Core 2.0 SDK 起，可以使用此选项。

`-o|--output <OUTPUT_DIRECTORY>`

指定输出目录的路径。 如未指定，对于依赖于框架的部署，将默认为 ./bin/[configuration]/[framework]/publish/ 或对于独立部署，将默认为 ./bin/[configuration]/[framework]/[runtime]/publish/。
如果路径是相对的，则生成的输出目录与项目文件位置相关，而与当前工作目录不相关。

`-r|--runtime <RUNTIME_IDENTIFIER>`

发布针对给定运行时的应用程序。 这将在创建[独立部署 (SCD)](../deploying/index.md#self-contained-deployments-scd) 时使用。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。 默认为发布[依赖于框架的部署 (FDD)](../deploying/index.md#framework-dependent-deployments-fdd)。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

`--version-suffix <VERSION_SUFFIX>`

定义版本后缀来替换项目文件的版本字段中的星号 (`*`)。

---

## <a name="examples"></a>示例

在当前目录中发布项目：

`dotnet publish`

使用指定的项目文件发布应用程序：

`dotnet publish ~/projects/app1/app1.csproj`

使用 `netcoreapp1.1` 框架发布当前目录中的项目：

`dotnet publish --framework netcoreapp1.1`

使用 `netcoreapp1.1` 框架和 `OS X 10.10` 的运行时发布当前应用程序（必须在项目文件中列出此 RID）。

`dotnet publish --framework netcoreapp1.1 --runtime osx.10.11-x64`

发布当前应用程序，但在还原操作期间不还原项目到项目 (P2P) 引用，只还原根项目（.NET Core SDK 2.0 及更高版本）：

`dotnet publish --no-dependencies`

## <a name="see-also"></a>请参阅

- [目标框架](../../standard/frameworks.md)
- [运行时标识符 (RID) 目录](../rid-catalog.md)
