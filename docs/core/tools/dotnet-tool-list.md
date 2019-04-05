---
title: dotnet tool list 命令
description: dotnet tool list 命令从计算机中列出指定的 .NET Core 全局工具。
ms.date: 05/29/2018
ms.openlocfilehash: d3ff7fc90faf6ede3f7de0d5af5112c77ca140db
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54712905"
---
# <a name="dotnet-tool-list"></a>dotnet tool list

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a>name

`dotnet tool list` - 列出当前安装在计算机上的默认目录中或指定路径中的所有 [.NET Core 全局工具](global-tools.md)。

## <a name="synopsis"></a>摘要

```console
dotnet tool list <-g|--global>
dotnet tool list <--tool-path>
dotnet tool list <-h|--help>
```

## <a name="description"></a>说明

`dotnet tool list` 命令让你可以列出计算机上（当前用户配置文件）或特定路径中安装的所有用户范围的 .NET Core 全局工具。 此命令列出包名称、安装的版本以及全局工具命令。 若要使用此 list 命令，需要使用 `--global` 选项指定要查看所有用户范围的工具或者使用 `--tool-path` 选项指定自定义路径。

## <a name="options"></a>选项

`-g|--global`

列出用户范围的全局工具。 不能与 `--tool-path` 选项一起使用。 如果不指定此选项，则必须指定 `--tool-path` 选项。

`-h|--help`

打印出有关命令的简短帮助。

`--tool-path <PATH>`

指定用于查找全局工具的自定义位置。 路径可以是绝对的，也可以是相对的。 不能与 `--global` 选项一起使用。 如果不指定此选项，则必须指定 `--global` 选项。

## <a name="examples"></a>示例

列出计算机上安装的所有用户范围的全局工具（当前用户配置文件）：

`dotnet tool list -g`

列出特定 Windows 文件夹中的全局工具：

`dotnet tool list --tool-path c:\global-tools`

列出特定 Linux/macOS 文件夹中的全局工具：

`dotnet tool list --tool-path ~/bin`

## <a name="see-also"></a>请参阅

- [.NET Core 全局工具](global-tools.md)
