---
title: dotnet tool update 命令
description: dotnet tool update 命令在你计算机上更新指定的 .NET Core 全局工具。
ms.date: 05/29/2018
ms.openlocfilehash: bc7edada013c118564d44cbe4542dacb76925692
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54516637"
---
# <a name="dotnet-tool-update"></a>dotnet tool update

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a>name

`dotnet tool update` - 在你的计算机上更新指定的 [.NET Core 全局工具](global-tools.md)。

## <a name="synopsis"></a>摘要

```console
dotnet tool update <PACKAGE_NAME> <-g|--global> [--configfile] [--framework] [-v|--verbosity]
dotnet tool update <PACKAGE_NAME> <--tool-path> [--configfile] [--framework] [-v|--verbosity]
dotnet tool update <-h|--help>
```

## <a name="description"></a>说明

`dotnet tool update` 命令让你可以将计算机上的 .NET Core 全局工具更新为包的最新稳定版。 此命令卸载并重新安装工具，有效地对工具进行更新。 若要使用此命令，需要使用 `--global` 选项指定从用户范围的安装中更新工具或使用 `--tool-path` 选项指定安装工具的路径。

## <a name="arguments"></a>自变量

`PACKAGE_NAME`

包含要更新的 .NET Core 全局工具的 NuGet 包的名称/ID。 你可以使用 [dotnet tool list](dotnet-tool-list.md) 命令查找包名称。

## <a name="options"></a>选项

`--add-source <SOURCE>`

添加安装过程中要使用的其他 NuGet 包源。

`--configfile <FILE>`

要使用的 NuGet 配置 (nuget.config) 文件。

`--framework <FRAMEWORK>`

指定要更新工具的[目标框架](../../standard/frameworks.md)。

`-g|--global`

指定此更新用于用户范围的工具。 不能与 `--tool-path` 选项一起使用。 如果不指定此选项，则必须指定 `--tool-path` 选项。

`-h|--help`

打印出有关命令的简短帮助。

`--tool-path <PATH>`

指定全局工具的安装位置。 路径可以是绝对的，也可以是相对的。 不能与 `--global` 选项一起使用。 如果不指定此选项，则必须指定 `--global` 选项。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="examples"></a>示例

更新 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool update -g dotnetsay`

更新位于特定 Windows 文件夹的 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool update dotnetsay --tool-path c:\global-tools`

更新位于特定 Linux/macOS 文件夹的 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool update dotnetsay --tool-path ~/bin`

## <a name="see-also"></a>请参阅

- [.NET Core 全局工具](global-tools.md)
