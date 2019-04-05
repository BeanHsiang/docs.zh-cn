---
title: dotnet tool install 命令
description: dotnet tool install 命令在计算机上安装指定的 .NET Core 全局工具。
ms.date: 05/29/2018
ms.openlocfilehash: 1348eb1165c77376a885fdcbf094bd17b2aa3514
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54563699"
---
# <a name="dotnet-tool-install"></a>dotnet tool install

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a>name

`dotnet tool install` - 在计算机上安装指定的 [.NET Core 全局工具](global-tools.md)。

## <a name="synopsis"></a>摘要

```console
dotnet tool install <PACKAGE_NAME> <-g|--global> [--add-source] [--configfile] [--framework] [-v|--verbosity] [--version]
dotnet tool install <PACKAGE_NAME> <--tool-path> [--add-source] [--configfile] [--framework] [-v|--verbosity] [--version]
dotnet tool install <-h|--help>
```

## <a name="description"></a>说明

`dotnet tool install` 为用户提供一种在计算机上安装 .NET Core 全局工具的方法。 若要使用此命令，需要使用 `--global` 选项指定用户范围的安装或者使用 `--tool-path` 选项指定安装路径。

指定 `-g`（或 `--global`）选项时，全局工具默认安装在以下目录中：

| (OS)          | 路径                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

## <a name="arguments"></a>自变量

`PACKAGE_NAME`

包含要安装的 .NET Core 全局工具的 NuGet 包的名称/ID。

## <a name="options"></a>选项

`--add-source <SOURCE>`

添加安装过程中要使用的其他 NuGet 包源。

`--configfile <FILE>`

要使用的 NuGet 配置 (nuget.config) 文件。

`--framework <FRAMEWORK>`

指定要安装工具的[目标框架](../../standard/frameworks.md)。 默认情况下，.NET Core SDK 尝试选择最合适的目标框架。

`-g|--global`

指定安装是用户范围的。 不能与 `--tool-path` 选项一起使用。 如果不指定此选项，则必须指定 `--tool-path` 选项。

`-h|--help`

打印出有关命令的简短帮助。

`--tool-path <PATH>`

指定全局工具的安装位置。 路径可以是绝对的，也可以是相对的。 如果路径不存在，命令会尝试创建它。 不能与 `--global` 选项一起使用。 如果不指定此选项，则必须指定 `--global` 选项。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

`--version <VERSION_NUMBER>`

要安装的工具版本。 默认情况下，安装最新的稳定包版本。 使用此选项安装工具的预览版或较旧版本。

## <a name="examples"></a>示例

在默认位置安装 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool install -g dotnetsay`

在特定 Windows 文件夹安装 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool install dotnetsay --tool-path c:\global-tools`

在特定 Linux/macOS 文件夹安装 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool install dotnetsay --tool-path ~/bin`

安装 2.0.0 版的 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool install -g dotnetsay --version 2.0.0`

## <a name="see-also"></a>请参阅

- [.NET Core 全局工具](global-tools.md)
