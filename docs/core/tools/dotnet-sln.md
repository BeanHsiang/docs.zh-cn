---
title: dotnet sln 命令
description: 使用 dotnet-sln 命令，可以便捷地在解决方案文件中添加、删除和列出项目。
ms.date: 06/13/2018
ms.openlocfilehash: a88e22c68f639f2a42e59f9a271e431f04e24a2b
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53169139"
---
# <a name="dotnet-sln"></a>dotnet sln

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet sln` - 修改 .NET Core 解决方案文件。

## <a name="synopsis"></a>摘要

```
dotnet sln [<SOLUTION_NAME>] add <PROJECT> <PROJECT> ...
dotnet sln [<SOLUTION_NAME>] add <GLOBBING_PATTERN>
dotnet sln [<SOLUTION_NAME>] remove <PROJECT> <PROJECT> ...
dotnet sln [<SOLUTION_NAME>] remove <GLOBBING_PATTERN>
dotnet sln [<SOLUTION_NAME>] list
dotnet sln [-h|--help]
```

## <a name="description"></a>说明

使用 `dotnet sln` 命令，可以便捷地在解决方案文件中添加、删除和列出项目。

若要使用 `dotnet sln` 命令，必须存在解决方案文件。 如果需要创建一个解决方案文件，请使用 [dotnet new](dotnet-new.md) 命令，如下例所示：

```
dotnet new sln
```

## <a name="commands"></a>命令

`add <PROJECT> ...`

`add <GLOBBING_PATTERN>`

将一个或多个项目添加到解决方案文件中。 基于 Unix/Linux 的终端支持[通配模式](https://en.wikipedia.org/wiki/Glob_(programming))。

`remove <PROJECT> ...`

`remove <GLOBBING_PATTERN>`

从解决方案文件中删除一个或多个项目。 基于 Unix/Linux 的终端支持[通配模式](https://en.wikipedia.org/wiki/Glob_(programming))。

`list`

列出解决方案文件中的所有项目。

## <a name="arguments"></a>自变量

`SOLUTION_NAME`

要使用的解决方案文件。 如果未指定，此命令会搜索当前目录来获取一个项目文件。 如果目录中有多个解决方案文件，必须指定一个。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

## <a name="examples"></a>示例

将一个 C# 项目添加到解决方案中：

`dotnet sln todo.sln add todo-app/todo-app.csproj`

从解决方案中删除一个 C# 项目：

`dotnet sln todo.sln remove todo-app/todo-app.csproj`

将多个 C# 项目添加到解决方案中：

`dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj`

从解决方案中删除多个 C# 项目：

`dotnet sln todo.sln remove todo-app/todo-app.csproj back-end/back-end.csproj`

使用通配模式将多个 C# 项目添加到解决方案中：

`dotnet sln todo.sln add **/*.csproj`

使用通配模式从解决方案中删除多个 C# 项目：

`dotnet sln todo.sln remove **/*.csproj`

> [!NOTE]
> 通配不是 CLI 功能，而是命令行界面的一个功能。 必须使用支持通配的 shell 才可成功地展开文件。 有关通配的详细信息，请参阅[维基百科](https://en.wikipedia.org/wiki/Glob_(programming))。
