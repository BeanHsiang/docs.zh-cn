---
title: global.json 概述
description: 了解如何在运行 .NET Core CLI 命令时使用 global.json 文件设置 .NET Core SDK 版本。
ms.date: 12/03/2018
ms.custom: updateeachrelease, seodec18
ms.openlocfilehash: e0f929a049812cac6f62e5218629c9b0add83de8
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53170764"
---
# <a name="globaljson-overview"></a>global.json 概述

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

通过 global.json 文件，可定义在运行 .NET Core CLI 命令时使用的 .NET Core SDK 版本。 选择 .NET Core SDK 与指定项目所面向的运行时无关。 .NET Core SDK 版本指示使用哪个版本的 .NET Core CLI 工具。 通常会使用最新版本的工具，因此不需要 global.json 文件。

有关指定运行时的详细信息，请参阅[目标框架](../../standard/frameworks.md)。

.NET Core SDK 在当前工作目录（不必与项目目录相同）或其某个父目录中查找 global.json 文件。

## <a name="globaljson-schema"></a>global.json 架构

### <a name="sdk"></a>SDK

类型：对象

指定要选择的 .NET Core SDK 的相关信息。

#### <a name="version"></a>version

类型：String

要使用的 .NET Core SDK 版本。

请注意，此字段：

- 不具备通配支持，也就是说，必须指定完整版本号。
- 不支持版本范围。

下面的示例展示 global.json 文件的内容：

```json
{
  "sdk": {
    "version": "2.2.100"
  }
}
```

## <a name="globaljson-and-the-net-core-cli"></a>global.json 和 .NET Core CLI

最好能知道哪些版本可用，以便在 global.json 文件中设置相应版本。 可在 [.NET 下载](https://www.microsoft.com/net/download/all)站点中找到支持的可用 SDK 的完整列表。 从 .NET Core 2.1 SDK 开始，可运行以下命令来验证计算机上已安装的 SDK 版本：

```console
dotnet --list-sdks
```

若要在计算机上安装其他 .NET Core SDK 版本，请访问 [.NET 下载](https://www.microsoft.com/net/download/all)站点。

可执行 [dotnet new](dotnet-new.md) 命令在当前目录中创建一个新的 global.json 文件，类似于以下示例：

```console
dotnet new globaljson --sdk-version 2.2.100
```

## <a name="matching-rules"></a>匹配规则

> [!NOTE]
> 匹配规则由 apphost 掌管，apphost 是.NET Core 运行时的一部分。
> 如果并行安装了多个运行时，则使用最新版本的主机。

从 .NET Core 2.0 开始，在确定要使用的 SDK 版本时，适用以下规则：

- 如果未找到 global.json 文件或 global.json 未指定 SDK 版本，则使用最新安装的 SDK 版本。 最新 SDK 版本可能是发布版本或预发布版本 - 以版本号更高的为准。
- 如果 global.json 指定了 SDK 版本：
  - 如果计算机上安装了该指定的 SDK 版本，则使用该版本。
  - 如果计算机上未安装指定的 SDK 版本，则使用最新安装的该版本的 SDK 修补程序版本。 最新安装的 SDK 修补程序版本可能是发布版本或预发布版本 - 以版本号更高的为准。 在 .NET Core 2.1 及更高版本中，在选择 SDK 版本时将忽略低于指定修补程序版本的修补程序版本。
  - 如果找不到指定的 SDK 版本和相应的 SDK 修补程序版本，会引发错误。

SDK 版本目前由以下部分组成：

`[.NET Core major version].[.NET Core minor version].[xyz][-optional preview name]`

.NET Core SDK 的功能版本由 SDK 版本 2.1.100 及更高版本所采用的版本号的最后一部分 (`xyz`) 的第一个数字 (`x`) 表示。 通常，.NET Core SDK 的发布周期比 .NET Core 快。

修补程序版本由 SDK 版本 2.1.100 及更高版本所采用的版本号的最后一部分 (`xyz`) 的后两位数字 (`yz`) 表示。 例如，如果将 `2.1.300` 指定为 SDK 版本，则可选的 SDK 版本号最多到 `2.1.399`，但 `2.1.400` 不视为 `2.1.300` 的一个修补程序版本。

版本号架构过渡期间发布了 .NET Core SDK 版本 `2.1.100` 到 `2.1.201`，但未正确使用 `xyz` 表示法。 强烈建议如果在 global.json 文件中指定了这些版本，请确保目标计算机上安装了指定版本。

如果使用 .NET Core SDK 1.x，在指定了版本但未找到完全匹配项的情况下，则使用最新安装的 SDK 版本。 最新 SDK 版本可能是发布版本或预发布版本 - 以版本号更高的为准。

## <a name="troubleshooting-build-warnings"></a>针对生成警告的疑难解答

> [!WARNING]
> 使用的是 .NET Core SDK 的预览版本， 可通过当前项目中的 global.json 文件定义 SDK 版本。 有关详细信息，请访问 <https://go.microsoft.com/fwlink/?linkid=869452>

此警告指示正在使用 .NET Core SDK 预览版本编译项目，如[匹配规则](#matching-rules)部分所述。 .NET Core SDK 的各种版本均品质优良稳定，在业内口碑良好。 但如果不想使用预览版本，可将 global.json 文件添加到项目层次结构中以指定要使用的 SDK 版本，并使用 `dotnet --list-sdks` 来确认计算机上已安装该版本。 发布新版本时，若要使用新版本，可删除 global.json 文件或将其更新以使用较新版本。

> [!WARNING]
> 启动项目 '{startupProject}' 面向框架 '.NETCoreApp' 的版本 '{targetFrameworkVersion}'。 此版本的 Entity Framework Core .NET 命令行工具仅支持 2.0 或更高版本。 有关使用旧版工具的信息，请参阅 <https://go.microsoft.com/fwlink/?linkid=871254>

从 .NET Core 2.1 SDK（版本 2.1.300）开始，SDK 中包含 `dotnet ef` 命令。 此警告指示项目面向 EF Core 1.0 或 1.1，后者与 .NET Core 2.1 SDK 及更高版本不兼容。 若要编译项目，请在计算机上安装 .NET Core 2.0 SDK（版本 2.1.201）及更早版本，并使用 global.json 文件定义所需 SDK 版本。 有关 `dotnet ef` 命令的详细信息，请参阅 [EF Core .NET 命令行工具](/ef/core/miscellaneous/cli/dotnet)。

## <a name="see-also"></a>请参阅

- [如何解析 SDK 项目](/visualstudio/msbuild/how-to-use-project-sdk#how-project-sdks-are-resolved)