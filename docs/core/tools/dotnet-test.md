---
title: dotnet test 命令
description: dotnet test 命令可用于在给定项目中执行单元测试。
ms.date: 05/29/2018
ms.openlocfilehash: 1b2a3917a930db0c0a49ebea41f568aaf4a58ee3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54535277"
---
# <a name="dotnet-test"></a>dotnet test

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet test` - 用于执行单元测试的 .NET 测试驱动程序。

## <a name="synopsis"></a>摘要

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```console
dotnet test [<PROJECT>] [-a|--test-adapter-path] [--blame] [-c|--configuration] [--collect] [-d|--diag] [-f|--framework] [--filter]
    [-l|--logger] [--no-build] [--no-restore] [-o|--output] [-r|--results-directory] [-s|--settings] [-t|--list-tests] 
    [-v|--verbosity] [-- <RunSettings arguments>]

dotnet test [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```console
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [--collect] [-d|--diag] [-f|--framework] [--filter]
    [-l|--logger] [--no-build] [--no-restore] [-o|--output] [-r|--results-directory] [-s|--settings] [-t|--list-tests] [-v|--verbosity]

dotnet test [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```console
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [-d|--diag] [-f|--framework] [--filter] [-l|--logger] [--no-build] [-o|--output] [-s|--settings] [-t|--list-tests]  [-v|--verbosity]

dotnet test [-h|--help]
```

---

## <a name="description"></a>说明

`dotnet test` 命令用于执行给定项目中的单元测试。 `dotnet test` 命令启动为项目指定的测试运行程序控制台应用程序。 测试运行程序执行为单元测试框架（例如 MSTest、NUnit 或 xUnit）定义的测试，并报告每个测试是否成功。 如果所有测试均成功，测试运行程序将返回 0 作为退出代码；否则将返回 1。 测试运行程序和单元测试库打包为 NuGet 包并还原为该项目的普通依赖项。

测试项目使用普通 `<PackageReference>` 元素指定测试运行程序，如下方示例项目文件所示：

[!code-xml[XUnit Basic Template](../../../samples/snippets/csharp/xunit-test/xunit-test.csproj)]

## <a name="arguments"></a>自变量

`PROJECT`

指向测试项目的路径。 如未指定，则默认为当前目录。

## <a name="options"></a>选项

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

在测试运行中使用来自指定路径的自定义测试适配器。

`--blame`

在意见模式中运行测试。 此选项有助于隔离导致测试主机出现故障的有问题的测试。 它会在当前目录中创建一个输出文件 (Sequence.xml)，其中捕获了故障前的测试执行顺序。

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`，但项目配置可以替代此默认 SDK 设置。

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

为测试运行启用数据收集器。 有关详细信息，请参阅[监视和分析测试运行](https://aka.ms/vstest-collect)。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

启用测试平台的诊断模式，并将诊断消息写入指定文件。

`-f|--framework <FRAMEWORK>`

查找特定[框架](../../standard/frameworks.md)的测试二进制文件。

`--filter <EXPRESSION>`

使用给定表达式筛选掉当前项目中的测试。 有关详细信息，请参阅[筛选选项详细信息](#filter-option-details)部分。 若要获取使用选择性单元测试筛选的其他信息和示例，请参阅[运行选择性单元测试](../testing/selective-unit-tests.md)。

`-h|--help`

打印出有关命令的简短帮助。

`-l|--logger <LoggerUri/FriendlyName>`

指定测试结果记录器。

`--no-build`

不在运行测试项目之前生成它。 还隐式设置 `--no-restore` 标记。

`--no-restore`

运行此命令时不执行隐式还原。

`-o|--output <OUTPUT_DIRECTORY>`

查找要运行的二进制文件的目录。

`-r|--results-directory <PATH>`

用于放置测试结果的目录。 如果指定的目录不存在，则会创建该目录。

`-s|--settings <SETTINGS_FILE>`

运行测试时要使用的设置。

`-t|--list-tests`

列出当前项目中发现的所有测试。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

`RunSettings arguments`

作为测试的 RunSettings 配置传递的参数。 参数在“-- ”（注意 -- 后的空格）后被指定为 `[name]=[value]` 对。 空格用于分隔多个 `[name]=[value]` 对。

示例：`dotnet test -- MSTest.DeploymentEnabled=false MSTest.MapInconclusiveToFailed=True`

有关 RunSettings 的详细信息，请参阅 [vstest.console.exe：传递 RunSettings 参数](https://github.com/Microsoft/vstest-docs/blob/master/docs/RunSettingsArguments.md)。

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

在测试运行中使用来自指定路径的自定义测试适配器。

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`，但项目配置可以替代此默认 SDK 设置。

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

为测试运行启用数据收集器。 有关详细信息，请参阅[监视和分析测试运行](https://aka.ms/vstest-collect)。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

启用测试平台的诊断模式，并将诊断消息写入指定文件。

`-f|--framework <FRAMEWORK>`

查找特定[框架](../../standard/frameworks.md)的测试二进制文件。

`--filter <EXPRESSION>`

使用给定表达式筛选掉当前项目中的测试。 有关详细信息，请参阅[筛选选项详细信息](#filter-option-details)部分。 若要获取使用选择性单元测试筛选的其他信息和示例，请参阅[运行选择性单元测试](../testing/selective-unit-tests.md)。

`-h|--help`

打印出有关命令的简短帮助。

`-l|--logger <LoggerUri/FriendlyName>`

指定测试结果记录器。

`--no-build`

不在运行测试项目之前生成它。 还隐式设置 `--no-restore` 标记。

`--no-restore`

运行此命令时不执行隐式还原。

`-o|--output <OUTPUT_DIRECTORY>`

查找要运行的二进制文件的目录。

`-r|--results-directory <PATH>`

用于放置测试结果的目录。 如果指定的目录不存在，则会创建该目录。

`-s|--settings <SETTINGS_FILE>`

运行测试时要使用的设置。

`-t|--list-tests`

列出当前项目中发现的所有测试。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

在测试运行中使用来自指定路径的自定义测试适配器。

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`，但项目配置可以替代此默认 SDK 设置。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

启用测试平台的诊断模式，并将诊断消息写入指定文件。

`-f|--framework <FRAMEWORK>`

查找特定[框架](../../standard/frameworks.md)的测试二进制文件。

`--filter <EXPRESSION>`

使用给定表达式筛选掉当前项目中的测试。 有关详细信息，请参阅[筛选选项详细信息](#filter-option-details)部分。 若要获取使用选择性单元测试筛选的其他信息和示例，请参阅[运行选择性单元测试](../testing/selective-unit-tests.md)。

`-h|--help`

打印出有关命令的简短帮助。

`-l|--logger <LoggerUri/FriendlyName>`

指定测试结果记录器。

`--no-build`

不在运行测试项目之前生成它。

`-o|--output <OUTPUT_DIRECTORY>`

查找要运行的二进制文件的目录。

`-s|--settings <SETTINGS_FILE>`

运行测试时要使用的设置。

`-t|--list-tests`

列出当前项目中发现的所有测试。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

---

## <a name="examples"></a>示例

运行当前目录所含项目中的测试：

`dotnet test`

运行 `test1` 项目中的测试：

`dotnet test ~/projects/test1/test1.csproj`

在当前目录运行项目中的测试，并以 trx 格式生成测试结果文件：

`dotnet test --logger:trx`

## <a name="filter-option-details"></a>筛选选项详细信息

`--filter <EXPRESSION>`

`<Expression>` 格式为 `<property><operator><value>[|&<Expression>]`。

`<property>` 是 `Test Case` 的特性。 下面介绍了常用单元测试框架支持的属性：

| 测试框架 | 支持的属性                                                                                      |
| -------------- | --------------------------------------------------------------------------------------------------------- |
| MSTest         | <ul><li>FullyQualifiedName</li><li>name</li><li>ClassName</li><li>Priority</li><li>TestCategory</li></ul> |
| xUnit          | <ul><li>FullyQualifiedName</li><li>DisplayName</li><li>Traits</li></ul>                                   |

`<operator>` 说明了属性和值之间的关系：

| 运算符 | 函数        |
| :------: | --------------- |
| `=`      | 完全匹配     |
| `!=`     | 非完全匹配 |
| `~`      | 包含        |

`<value>` 是字符串。 所有查找都不区分大小写。

不含 `<operator>` 的表达式自动被视为 `FullyQualifiedName` 属性上的 `contains`（例如，`dotnet test --filter xyz` 与 `dotnet test --filter FullyQualifiedName~xyz` 相同）。

表达式可与条件运算符结合使用：

| 运算符            | 函数 |
| ------------------- | -------- |
| <code>&#124;</code> | 或       |
| `&`                 | AND      |

使用条件运算符时，可以用括号将表达式括起来（例如，`(Name~TestMethod1) | (Name~TestMethod2)`）。

若要获取使用选择性单元测试筛选的其他信息和示例，请参阅[运行选择性单元测试](../testing/selective-unit-tests.md)。

## <a name="see-also"></a>请参阅

- [框架和目标](../../standard/frameworks.md)
- [.NET Core 运行时标识符 (RID) 目录](../rid-catalog.md)
