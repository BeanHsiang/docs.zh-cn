---
title: dotnet tool uninstall 命令
description: dotnet tool uninstall 命令从你计算机上卸载指定的 .NET Core 全局工具。
ms.date: 05/29/2018
ms.openlocfilehash: 4d53d305131e3399ab5d9c19f9319f3ba3544c19
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54680918"
---
# <a name="dotnet-tool-uninstall"></a>dotnet tool uninstall

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a>name

`dotnet tool uninstall` - 从你的计算机上卸载指定的 [.NET Core 全局工具](global-tools.md)。

## <a name="synopsis"></a>摘要

```console
dotnet tool uninstall <PACKAGE_NAME> <-g|--global>
dotnet tool uninstall <PACKAGE_NAME> <--tool-path>
dotnet tool uninstall <-h|--help>
```

## <a name="description"></a>说明

`dotnet tool uninstall` 为你提供一种从计算机上卸载 .NET Core 全局工具的方法。 若要使用此命令，需要使用 `--global` 选项指定要删除用户范围的工具或使用 `--tool-path` 选项指定安装工具的路径。

## <a name="arguments"></a>自变量

`PACKAGE_NAME`

包含要卸载的 .NET Core 全局工具的 NuGet 包的名称/ID。 你可以使用 [dotnet tool list](dotnet-tool-list.md) 命令查找包名称。

## <a name="options"></a>选项

`-g|--global`

指定要从用户范围的安装中删除工具。 不能与 `--tool-path` 选项一起使用。 如果不指定此选项，则必须指定 `--tool-path` 选项。

`-h|--help`

打印出有关命令的简短帮助。

`--tool-path <PATH>`

指定卸载全局工具的位置。 路径可以是绝对的，也可以是相对的。 不能与 `--global` 选项一起使用。 如果不指定此选项，则必须指定 `--global` 选项。

## <a name="examples"></a>示例

卸载 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool uninstall -g dotnetsay`

从特定 Windows 文件夹卸载 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool uninstall dotnetsay --tool-path c:\global-tools`

从特定 Linux/macOS 文件夹卸载 [dotnetsay](https://www.nuget.org/packages/dotnetsay/) 全局工具：

`dotnet tool uninstall dotnetsay --tool-path ~/bin`

## <a name="see-also"></a>请参阅

- [.NET Core 全局工具](global-tools.md)
