---
title: .NET Core 3.0 的新增功能
description: 了解 .NET Core 3.0 的新增功能。
dev_langs:
- csharp
- vb
author: thraka
ms.author: adegeo
ms.date: 12/31/2018
ms.openlocfilehash: 89264098ed17b398c83bc2dcddd98d9d8fc958f7
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57679731"
---
# <a name="whats-new-in-net-core-30-preview-2"></a>.NET Core 3.0（预览版 2）的新增功能

本文介绍 .NET Core 3.0（预览版 2）的新增功能。 最大的增强功能之一是对 Windows 桌面应用程序（仅限 Windows）的支持。 通过利用名为“Windows 桌面”的 .NET Core 3.0 SDK 组件，可以移植 Windows 窗体和 Windows Presentation Foundation (WPF) 应用程序。 为清楚起见，Windows 桌面组件仅在 Windows 上受支持，且仅在 Windows 中包含。 有关详细信息，请参阅下面的 [Window 桌面](#windows-desktop)一节。

.NET Core 3.0 添加了对 C#8.0 的支持。

立即在 Windows、Mac 和 Linux 上[下载并开始使用 .NET Core 3.0 预览版 2](https://aka.ms/netcore3download)。 有关版本的完整详细信息，请参阅 [.NET Core 3.0 预览版 2 发行说明](https://aka.ms/netcore3releasenotes)。

要详细了解每个版本的发布内容，请参阅以下文档：

- [.NET Core 3.0 预览版 1 公告](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-preview-1-and-open-sourcing-windows-desktop-frameworks/)
- [.NET Core 3.0 预览版 2 公告](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-preview-2/)

## <a name="c-8"></a>C# 8

.NET Core 3.0 支持 C#8，从 .NET Core 3.0 预览版 2 开始支持这些新功能。 有关 C# 8.0 功能的详细信息，请参阅以下博客文章：

- [使用 C# 8.0 中的模式执行更多操作](https://devblogs.microsoft.com/dotnet/do-more-with-patterns-in-c-8-0/)
- [尝试使用 C# 8.0](https://devblogs.microsoft.com/dotnet/take-c-8-0-for-a-spin/)
- [生成 C# 8.0](https://devblogs.microsoft.com/dotnet/building-c-8-0/)


### <a name="ranges-and-indices"></a>范围和索引

新 `Index` 类型可用于编制索引。 可以从从开头开始计数的 `int` 中创建一个类型，也可以使用从末尾开始计数的前缀 `^` 运算符 (C#) 创建一个：

```csharp
Index i1 = 3;  // number 3 from beginning
Index i2 = ^4; // number 4 from end
int[] a = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
Console.WriteLine($"{a[i1]}, {a[i2]}"); // "3, 6"
```

此外，还有 `Range` 类型，它包含两个 `Index` 值，一个用于开头一个用于结尾，可以使用 `x..y` 范围表达式 (C#) 进行编写。 然后可以使用 `Range` 进行索引以便生成一个切片：

```csharp
var slice = a[i1..i2]; // { 3, 4, 5 }
```

### <a name="async-streams"></a>异步流

`IAsyncEnumerable<T>` 类型是 `IEnumerable<T>` 的新异步版本。 该语言允许通过 `IAsyncEnumerable<T>` 执行 `await foreach` 操作来使用其元素，并对其使用 `yield return` 操作来生成元素。

下面的示例演示如何生成和使用异步流。 `foreach` 语句为异步语句，它本身使用 `yield return` 为调用方生成异步流。 此模式（使用 `yield return`）是生成异步流的建议模型。

```csharp
async IAsyncEnumerable<int> GetBigResultsAsync()
{
    await foreach (var result in GetResultsAsync())
    {
        if (result > 20) yield return result; 
    }
}
```

除了能够 `await foreach`，还可以创建异步迭代器，例如，一个返回 `IAsyncEnumerable/IAsyncEnumerator` 的迭代器，可以在其中进行 `await` 和 `yield` 操作。 对于需要处理的对象，可以使用各种 BCL 类型（如 `Stream` 和 `Timer`）实现的 `IAsyncDisposable`。

>[!NOTE]
>如果要使用 Visual Studio 2019 预览版 2 或[适用于 Visual Studio Code 的 C# 扩展](https://github.com/OmniSharp/omnisharp-vscode/releases/tag/v1.18.0-beta5)的最新预览版进行开发，则需要 .NET Core 3.0 预览版 2，因为要使用异步流。 如果在命令行处使用 .NET Core 3.0 预览版 2，所有内容将按预期工作。

### <a name="using-declarations"></a>Using 声明

Using 声明是确保正确释放对象的新方法。 Using 声明可使对象在作用域内时保持活动状态。 如果对象已不在作用域内，将自动释放对象。 这将减少嵌套的 Using 语句，并使代码更简洁。

```csharp
static void Main(string[] args)
{
    using var options = Parse(args);
    if (options["verbose"]) { WriteLine("Logging..."); }

} // options disposed here
```

### <a name="switch-expressions"></a>Switch 表达式

Switch 表达式是执行 Switch 语句更简洁的方式，但由于它是表达式，因此将返回值。 Switch 表达式还与模式匹配完全集成，并使用放弃模式 `_`，表示 `default` 值。

可在以下示例中查看 Switch 表达式的语法：

```csharp
static string Display(object o) => o switch
{
    Point { X: 0, Y: 0 }         => "origin",
    Point { X: var x, Y: var y } => $"({x}, {y})",
    _                            => "unknown"
};
```

此示例中有两种模式发挥作用。 `o` 首先匹配 `Point` 类型模式，然后匹配{大括号}内部的属性模式。 `_` 描述 `discard pattern`，与 Switch 语句的 `default` 相同。

通过模式，可以编写捕获意图的声明性代码，而不是相关测试的过程化代码。 编译器负责实现这些令人乏味的过程化代码，并保证操作始终正确。

在某些情况下，Switch 语句仍然是比 Switch 表达式更好的选择，并且模式可同时用于这两种语法形式。

有关详细信息，请参阅[使用 C# 8.0 中的模式执行更多操作](https://devblogs.microsoft.com/dotnet/do-more-with-patterns-in-c-8-0/)。

## <a name="ieee-floating-point-improvements"></a>IEEE 浮点改进

正在更新浮点 API，以符合 [IEEE 754-2008 修订](https://en.wikipedia.org/wiki/IEEE_754-2008_revision)。 这些更改旨在公开所有“必需”操作并确保这些操作在行为上符合 IEEE 规范。

分析和格式化修补程序：

* 正确分析并舍入任何输入长度。
* 正确分析并格式化负零。
* 通过执行不区分大小写的检查并允许在前面使用可选的 `+`（如果适用），正确分析无穷大和 NaN。

新的数学 API 有：

* `BitIncrement/BitDecrement`\
相当于 `nextUp` 和 `nextDown` IEEE 运算。 它们将返回最小的浮点数，该数字大于或小于输入值（分别）。 例如，`Math.BitIncrement(0.0)` 将返回 `double.Epsilon`。

* `MaxMagnitude/MinMagnitude`\
相当于 `maxNumMag` 和 `minNumMag` IEEE 运算，它们将（分别）返回大于或小于两个输入的量值的值。 例如，`Math.MaxMagnitude(2.0, -3.0)` 将返回 `-3.0`。

* `ILogB`\
相当于返回整数值的 `logB` IEEE 运算，它将返回输入参数的整数对数（以 2 为底）。 这实际上与 `floor(log2(x))` 相同，但完成后出现最小舍入错误。

* `ScaleB`\
相当于采用整数值的 `scaleB` IEEE 运算，它实际返回 `x * pow(2, n)`，但完成后出现最小舍入错误。

* `Log2`\
相当于返回（以 2 为底）对数的 `log2` IEEE 运算。 它会最小化舍入错误。

* `FusedMultiplyAdd`\
相当于执行乘法加法混合的 `fma` IEEE 运算。 也就是说，它以单个运算的形式执行 `(x * y) + z`，从而最小化舍入错误。 有关示例是返回 `1e308` 的 `FusedMultiplyAdd(1e308, 2.0, -1e308)`。 常规 `(1e308 * 2.0) - 1e308` 返回 `double.PositiveInfinity`。

* `CopySign`\
相当于 `copySign` IEEE 运算，它返回 `x` 的值但带有符号 `y`。

## <a name="net-platform-dependent-intrinsics"></a>.NET 平台依赖内部函数

已添加 API，允许访问某些性能导向的 CPU 指令，例如 SIMD 或位操作指令集。 这些指令有助于在某些情况下实现显著的性能改进，例如高效地并行处理数据。 除公开供程序使用的 API 外，.NET 库已开始使用这些指令改进性能。

以下 CoreCLR PR 通过实现或以下相关应用演示了几个内部函数：

* [实现简单的 SSE2 硬件内部函数](https://github.com/dotnet/coreclr/pull/15585)
* [实现 SSE 硬件内部函数](https://github.com/dotnet/coreclr/pull/15538)
* [Arm64 基 HW 内部函数](https://github.com/dotnet/coreclr/pull/16822)
* [对 Locate{First|Last}Found{Byte|Char} 使用 TZCNT 和 LZCNT](https://github.com/dotnet/coreclr/pull/21073)

有关详细信息，请参阅[依赖 .NET 平台的内部函数](https://github.com/dotnet/designs/blob/master/accepted/platform-intrinsics.md)，它定义了用于定义此硬件基础结构的方法，允许 Microsoft、芯片供应商或其他任何公司或个人定义应向 .NET 代码公开的硬件/芯片 API。

## <a name="default-executables"></a>默认可执行文件

.NET Core 现在将默认生成[依赖于框架的可执行文件](../deploying/index.md#framework-dependent-executables-fde)。 对于使用全局安装的 .NET Core 版本的应用程序而言，这是一项新功能。 到目前为止，仅[自包含部署](../deploying/index.md#self-contained-deployments-scd)会生成可执行文件。

在 `dotnet build` 或 `dotnet publish` 期间，将创建一个假设与你使用的 SDK 的环境和平台相匹配的可执行文件。 和其他本机可执行文件一样，可以使用这些可执行文件执行相同操作，例如：

* 可以双击可执行文件。
* 可以直接从命令提示符启用应用程序，如 Windows 上的 `myapp.exe`，以及 Linux 和 macOS 上的 `./myapp`。

## <a name="build-copies-dependencies"></a>生成副本依赖项

`dotnet build` 现将应用程序的 NuGet 依赖项从 NuGet 缓存复制到生成输出文件夹。 此前，依赖项仅作为 `dotnet publish` 的一部分复制。 

有些操作，比如链接和 razor 页面发布仍需要发布。


## <a name="local-dotnet-tools"></a>本地 dotnet 工具

>[!WARNING]
>.NET Core 3.0 预览版 1 至 .NET Core 3.0 预览版 2 中的 .NET Core 本地工具发生了更改。  如果在预览版 1 中通过运行 `dotnet tool restore` 或 `dotnet tool install` 等命令试用本地工具，则需要删除本地工具缓存文件夹，然后本地工具才能在预览版 2 中正常工作。 此文件夹位于：
>
>在 mac、Linux 上：`rm -r $HOME/.dotnet/toolResolverCache`
>
>在 Windows 上：`rmdir /s %USERPROFILE%\.dotnet\toolResolverCache`
>
>如果不删除此文件夹，将收到错误。

虽然 .NET Core 2.1 支持全局工具，.NET Core 3.0 现在使用本地工具。 本地工具类似于全局工具，但与磁盘上的特定位置相关联。 这支持每个项目和每个存储库工具。 本地安装的任何工具都不可在全局范围使用。 工具是作为 NuGet 包分发的。

本地工具依赖于当前目录中的清单文件名称 `dotnet-tools.json`。 此清单文件定义在该文件夹和以下文件夹中可用的工具。 通过在存储库的根目录中创建此清单文件，可确保克隆代码的任何人都可以恢复和使用所需的工具，以便成功使用代码。

若要创建 `dotnet-tools.json` 清单文件，请使用：

```console
dotnet new tool-manifest
```

使用以下命令向本地清单添加新的工具：

```console
dotnet tool install <packageId>
```

此外，还可以使用以下命令列出本地清单中的工具：

```console
dotnet tool list
```

若要查看全局安装的工具，请使用：

```console
dotnet tool list -g
```

当本地工具清单文件可用，但清单中定义的工具尚未安装时，请使用以下命令自动下载和安装这些工具：

```console
dotnet tool restore
```

使用以下命令运行本地工具：

```console
dotnet tool run <tool-command-name>
```

本地工具运行时，dotnet 将搜索当前目录结构中的清单。 找到工具清单文件时，将在其中搜索请求的工具。 如果在清单中找到工具，但没有缓存，用户将收到一个错误并需要运行 `dotnet tool restore`。

要从本地工具清单文件中删除工具，请运行以下命令：

```console
dotnet tool uninstall <packageId>
```

工具清单文件旨在允许手动编辑，你可能会执行此操作来更新使用存储库所需的版本。 下面是 `dotnet-tools.json` 示例文件：

```json
{
  "version": 1,
  "isRoot": true,
  "tools": {
    "dotnetsay": {
      "version": "2.1.4",
      "commands": [
        "dotnetsay"
      ]
    },
    "t-rex": {
      "version": "1.0.103",
      "commands": [
        "t-rex"
      ]
    }
  }
}
```

对于全局工具和本地工具，需要一个兼容的运行时版本。 目前，NuGet.org 上的许多工具都面向 .NET Core Runtime 2.1。 要在全局范围或本地安装这些工具，仍需要安装 [NET Core 2.1 运行时](https://dotnet.microsoft.com/download/dotnet-core/2.1)。

## <a name="windows-desktop"></a>Windows 桌面

从 .NET Core 3.0 预览版 1 开始，可以使用 WPF 和 Windows 窗体来生成 Windows 桌面应用程序。 这些框架还支持通过 [XAML 岛](/windows/uwp/xaml-platform/xaml-host-controls)从 Windows UI XAML 库 (WinUI) 使用新式控件和 Fluent 样式。

Windows 桌面部件是 Windows .NET Core 3.0 SDK 的一部分。

可以使用以下 `dotnet` 命令创建新的 WPF 或 Windows 窗体应用：

```console
dotnet new wpf
dotnet new winforms
```

Visual Studio 2019 预览版 2 添加了适用于 .NET Core 3.0 Windows 窗体和 WPF 的“新建项目”模板。 设计器仍然不受支持。 可以在 Visual Studio 2019 中打开、启动和调试这些项目。

Visual Studio 2017 15.9 添加了[支持 .NET Core 预览版](https://devblogs.microsoft.com/dotnet/net-core-tooling-update-for-visual-studio-2017-version-15-9/)的功能，但用户需要先启用该功能，而此操作不受支持。

新项目与现有的 .NET Core 项目相同，其中有一些附加内容。 下面是基本 .NET Core 控制台项目与基本 Windows 窗体以及 WPF 项目之间的比较。

在 .NET Core 控制台项目中，该项目使用 `Microsoft.NET.Sdk` SDK 并通过 `netcoreapp3.0` 目标框架在 .NET Core 3.0 上声明依赖项。 要创建 Windows Desktop 应用，请使用 `Microsoft.NET.Sdk.WindowsDesktop` SDK 并选择要使用的 UI 框架：

```diff
-<Project Sdk="Microsoft.NET.Sdk">
+<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
+   <UseWPF>true</UseWPF>
  </PropertyGroup>
</Project>
```

若要选择 Windows 窗体而不是 WPF，请设置 `UseWindowsForms` 而不是 `UseWPF`：

```diff
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
-   <UseWPF>true</UseWPF>
+   <UseWindowsForms>true</UseWindowsForms>
  </PropertyGroup>
</Project>
```

如果应用同时使用这两个框架，则 `UseWPF` 和 `UseWindowsForms` 可以同时设置为 `true`，例如，当 Windows 窗体对话框托管 WPF 控件。

请在 [dotnet/winforms](https://github.com/dotnet/winforms/issues)、[dotnet/wpf](https://github.com/dotnet/wpf/issues) 和 [dotnet/core](https://github.com/dotnet/core/issues) 存储库上共享反馈。

## <a name="msix-deployment-for-windows-desktop"></a>Windows 桌面的 MSIX 部署

[MSIX](https://docs.microsoft.com/windows/msix/) 是新的 Windows 应用包格式。 可以使用它将 .NET Core 3.0 桌面应用程序部署到 Windows 10。

Visual Studio 2019 预览版 2 中提供 [Windows 应用程序打包项目](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-packaging-dot-net)，允许用户使用[独立式](../deploying/index.md#self-contained-deployments-scd) .NET Core 应用程序创建 MSIX 包。

>注意:.NET Core 项目文件必须在 `<RuntimeIdentifiers>` 属性中指定支持的运行时：
```xml
<RuntimeIdentifiers>win-x86;win-x64</RuntimeIdentifiers>
```

## <a name="fast-built-in-json-support"></a>快速内置的 JSON 支持

.NET 生态系统依赖于 [Json.NET](https://www.newtonsoft.com/json) 和其他常用的 JSON 库，它们仍是很好的选择。 Json.NET 使用 .NET 字符串作为其基本数据类型，它实际上是 UTF-16。

新的内置 JSON 支持具有高性能、低分配的特点，并基于 `Span<byte>`。 已向 .NET Core 3.0 `System.Text.Json` 命名空间添加三个新的与 JSON 相关的主类型。

### <a name="utf8jsonreader"></a>Utf8JsonReader

`System.Text.Json.Utf8JsonReader` 是面向 UTF-8 编码 JSON 文本的一个高性能、低分配、只进读取器，从 `ReadOnlySpan<byte>` 读取信息。 `Utf8JsonReader` 是一种基本的低级类型，可用于构建自定义分析器和反序列化程序。 使用新的 `Utf8JsonReader` 读取 JSON 有效负载要比使用 **Json.NET** 的读取器快 2 倍。 在需要将 JSON 令牌实现为 (UTF-16) 字符串之前，它不会进行分配。

此新 API 将包含以下部件：

* 在预览版 1 中：JSON 读取器（顺序访问）
* 接下来推出：JSON 编写器、DOM（随机访问）、poco 序列化程序、poco 反序列化程序

下面是基本的 `Utf8JsonReader` 读取器循环，可以作为起点：

```csharp
using System.Text.Json;

public static void Utf8JsonReaderLoop(ReadOnlySpan<byte> dataUtf8)
{
    var json = new Utf8JsonReader(dataUtf8, isFinalBlock: true, state: default);

    while (json.Read())
    {
        JsonTokenType tokenType = json.TokenType;
        ReadOnlySpan<byte> valueSpan = json.ValueSpan;
        switch (tokenType)
        {
            case JsonTokenType.StartObject:
            case JsonTokenType.EndObject:
                break;
            case JsonTokenType.StartArray:
            case JsonTokenType.EndArray:
                break;
            case JsonTokenType.PropertyName:
                break;
            case JsonTokenType.String:
                string valueString = json.GetStringValue();
                break;
            case JsonTokenType.Number:
                if (!json.TryGetInt32Value(out int valueInteger))
                {
                    throw new FormatException();
                }
                break;
            case JsonTokenType.True:
            case JsonTokenType.False:
                bool valueBool = json.GetBooleanValue();
                break;
            case JsonTokenType.Null:
                break;
            default:
                throw new ArgumentException();
        }
    }

    dataUtf8 = dataUtf8.Slice((int)json.BytesConsumed);
    JsonReaderState state = json.CurrentState;
}
```

### <a name="utf8jsonwriter"></a>Utf8JsonWriter

`System.Text.Json.Utf8JsonWriter` 提供了一种高性能、非缓存的只进方式，通过常见 .NET 类型（例如，`String`、`Int32` 和 `DateTime`）编写 UTF-8 编码的 JSON 文本。 与阅读器一样，编写器是一种基本的低级类型，可用于构建自定义序列化程序。 使用新的 `Utf8JsonWriter` 编写 JSON 有效负载比通过 Json.NET 使用编写器快 30-80%，且无需分配。

下面是可用作起始点的 `Utf8JsonWriter` 的示例用法：

```csharp
static int WriteJson(IBufferWriter<byte> output, long[] extraData)
{
    var json = new Utf8JsonWriter(output, state: default);

    json.WriteStartObject();

    json.WriteNumber("age", 15, escape: false);
    json.WriteString("date", DateTime.Now);
    json.WriteString("first", "John");
    json.WriteString("last", "Smith");

    json.WriteStartArray("phoneNumbers", escape: false);
    json.WriteStringValue("425-000-1212", escape: false);
    json.WriteStringValue("425-000-1213");
    json.WriteEndArray();

    json.WriteStartObject("address");
    json.WriteString("street", "1 Microsoft Way");
    json.WriteString("city", "Redmond");
    json.WriteNumber("zip", 98052);
    json.WriteEndObject();

    json.WriteStartArray("ExtraArray");
    for (var i = 0; i < extraData.Length; i++)
    {
        json.WriteNumberValue(extraData[i]);
    }
    json.WriteEndArray();

    json.WriteEndObject();

    json.Flush(isFinalBlock: true);

    return (int)json.BytesWritten;
}
```

`Utf8JsonWriter` 接受 `IBufferWriter<byte>` 作为输出位置，用于异步写入 json 数据，而作为调用方，你需要提供具体实现。 平台目前不包括此接口的实现。 有关 `IBufferWriter<byte>` 的示例，请参阅[https://gist.github.com/ahsonkhan/c76a1cc4dc7107537c3fdc0079a68b35](https://gist.github.com/ahsonkhan/c76a1cc4dc7107537c3fdc0079a68b35)。

### <a name="jsondocument"></a>JsonDocument

`System.Text.Json.JsonDocument` 是基于 `Utf8JsonReader` 构建的。 `JsonDocument` 可分析 JSON 数据并生成只读文档对象模型 (DOM)，可对模型进行查询，以支持随机访问和枚举。 可以通过 `JsonElement` 类型（由 `JsonDocument` 公开为名为 `RootElement` 的属性）访问构成数据的 JSON 元素。 `JsonElement` 包含 JSON 数组和对象枚举器，以及用于将 JSON 文本转换为常见 .NET 类型的 API。 使用 `JsonDocument` 分析常规 JSON 有效负载并访问其所有成员比使用 Json.NET 快 2-3 倍，且为合理大小（即 < 1 MB）的数据所分配的量非常少。

下面是可用作起始点的 `JsonDocument` 和 `JsonElement` 的示例用法：

```csharp
static double ParseJson()
{
    const string json = " [ { \"name\": \"John\" }, [ \"425-000-1212\", 15 ], { \"grades\": [ 90, 80, 100, 75 ] } ]";

    double average = -1;

    using (JsonDocument doc = JsonDocument.Parse(json))
    {
        JsonElement root = doc.RootElement;
        JsonElement info = root[1];

        string phoneNumber = info[0].GetString();
        int age = info[1].GetInt32();

        JsonElement grades = root[2].GetProperty("grades");

        double sum = 0;
        foreach (JsonElement grade in grades.EnumerateArray())
        {
            sum += grade.GetInt32();
        }

        int numberOfCourses = grades.GetArrayLength();
        average = sum / numberOfCourses;
    }

    return average;
}
```

## <a name="assembly-unloadability"></a>程序集卸载功能

程序集卸载功能是 `AssemblyLoadContext` 的一项新功能。 这项新功能从 API 的角度来看，很大程度上是透明的，公开时只有几个新的 API。 它支持卸载加载程序上下文，为实例化类型、静态字段和程序集本身释放所有内存。 应用程序应该能够永久通过此机制加载和卸载程序集，而不会发生内容泄露。

该新功能可用于类似如下的方案：

* 需要动态插件加载和卸载的插件方案。 
* 动态编译、运行，然后刷新代码。 可用于网站，脚本编写引擎等。
* 加载程序集进行自检（例如，ReflectionOnlyLoad），尽管在很多情况下，[MetadataLoadContext](#type-metadataloadcontext)（发布于预览版 1）是个更好的选择。

有关详细信息，请参阅[使用卸载功能](https://github.com/dotnet/coreclr/pull/22221)文档。

程序集卸载需要非常小心，因为要确保理解对加载程序上下文以外的托管对象的所有引用，并且这些引用均处于管理中。 请求卸载加载程序上下文时，任何外部引用都需要解除引用，以便加载程序上下文其自身实现一致性即可。

.NET Framework 中通过应用程序域 (AppDomain) 提供程序集卸载功能，而 .NET Core 不支持该功能。 相比于这个新模型，AppDomain 既有优势又有局限。 与 AppDomain 相比，这个新的加载程序模型更具灵活性、性能更高。

## <a name="windows-native-interop"></a>Windows 本机互操作

Windows 提供丰富的本机 API，包括平面 C API、COM 和 WinRT 的形式。 从 .NET Core 1.0 开始，一直支持 P/Invoke。 现在，.NET Core 3.0 支持共同创建 COM API 和激活 WinRT API。

可参阅结合使用 COM 和 [Excel 演示源代码](https://github.com/dotnet/samples/tree/master/core/extensions/ExcelDemo)的示例。


## <a name="type-sequencereader"></a>类型：SequenceReader

在 .NET Core 3.0 中，已添加可用作 `ReadOnlySequence<T>` 读取器的 `System.Buffers.SequenceReader`。 这样可以对跨多个支持缓冲区的 `System.IO.Pipelines` 数据进行简单、高性能、低分配分析。 

以下示例将输入 `Sequence` 分解为有效的 `CR/LF` 分隔行：

```csharp
private static ReadOnlySpan<byte> CRLF => new byte[] { (byte)'\r', (byte)'\n' };

public static void ReadLines(ReadOnlySequence<byte> sequence)
{
    SequenceReader<byte> reader = new SequenceReader<byte>(sequence);

    while (!reader.End)
    {
        if (!reader.TryReadToAny(out ReadOnlySpan<byte> line, CRLF, advancePastDelimiter:false))
        {
            // Couldn't find another delimiter
            // ...
        }

        if (!reader.IsNext(CRLF, advancePast: true))
        {
            // Not a good CR/LF pair
            // ...
        }

        // line is valid, process
        ProcessLine(line);
    }
}
```

## <a name="type-metadataloadcontext"></a>类型：MetadataLoadContext

添加了 `MetadataLoadContext` 类型，该类型支持读取程序集元数据，而不会影响调用方的应用程序域。 程序集作为数据读取，包括为与当前运行时环境不同的体系结构和平台构建的程序集。 `MetadataLoadContext` 与 <xref:System.Reflection.Assembly.ReflectionOnlyLoad*> 重叠，后者仅在 .NET Framework 中可用。

[System.Reflection.MetadataLoadContext 包](https://www.nuget.org/packages/System.Reflection.MetadataLoadContext) 现已推出 `MetdataLoadContext`。 它是一个 .NET Standard 2.0 包。

`MetadataLoadContext` 公开的 API 类似于 <xref:System.Runtime.Loader.AssemblyLoadContext> 类型，但不是基于该类型。 与 <xref:System.Runtime.Loader.AssemblyLoadContext> 非常相似，`MetadataLoadContext` 支持在一个独立的程序集加载范围内加载程序集。 `MetdataLoadContext` API 返回 <xref:System.Reflection.Assembly> 对象，支持使用熟悉的反射 API。 不允许以执行为导向的 API，如 [MethodBase.Invoke](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.MetadataLoadContext/src/System/Reflection/TypeLoading/Methods/RoMethod.cs#L127)，并将引发 InvalidOperationException。

下面的示例演示如何在实现给定接口的程序集中找到具体类型：

```csharp
var paths = new string[] {@"C:\myapp\mscorlib.dll", @"C:\myapp\myapp.dll"};
var resolver = new PathAssemblyResolver(paths);
using (var lc = new MetadataLoadContext(resolver))
{
    Assembly a = lc.LoadFromAssemblyName("myapp");
    Type myInterface = a.GetType("MyApp.IPluginInterface");
    foreach (Type t in a.GetTypes())
    {
        if (t.IsClass && myInterface.IsAssignableFrom(t))
            Console.WriteLine($"Class {t.FullName} implements IPluginInterface");
    }
}
```

`MetadataLoadContext` 场景包括设计时功能、生成时工具和运行时启动功能，这些功能需要将一组程序集作为数据进行检查，并在执行检查后释放所有文件锁和内存。

`MetadataLoadContext` 有一个解析程序类传递给其构造函数。 解析程序的工作是在给定 `AssemblyName` 条件下加载 `Assembly`。 解析程序类派生自抽象 `MetadataAssemblyResolver` 类。 `PathAssemblyResolver` 提供了基于路径场景的解析程序的实现。

[MetadataLoadContext 测试](https://github.com/dotnet/corefx/tree/master/src/System.Reflection.MetadataLoadContext/tests/src/Tests)演示了许多用例。 [程序集测试](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.MetadataLoadContext/tests/src/Tests/Assembly/AssemblyTests.cs)是一个很好的起点。

## <a name="tls-13--openssl-111-on-linux"></a>Linux 上的 TLS 1.3 和 OpenSSL 1.1.1

.NET Core 现在可以在给定环境中使用 [OpenSSL 1.1.1 中的 TLS 1.3 支持](https://www.openssl.org/blog/blog/2018/09/11/release111/)。 对于 [OpenSSL 团队](https://www.openssl.org/blog/blog/2018/09/11/release111/)来说，TLS 1.3 有许多好处：

* 由于减少了客户端和服务器之间所需的往返次数，从而提高了连接时间。

* 由于消除了各种过时和不安全的加密算法和加密了更多连接握手，从而提高了安全性。

.NET Core 3.0 预览版 1 能够利用 OpenSSL 1.1.1、OpenSSL 1.1.0 或 OpenSSL 1.0.2（无论在 Linux 系统上找到的最佳版本是什么）。  当 OpenSSL 1.1.1 可用时，SslStream 和 HttpClient 类型将在使用 `SslProtocols.None`（系统默认协议）时使用 TLS 1.3，假定客户端和服务器都支持 TLS 1.3。

下面的示例演示在 Ubuntu 18.10 上 .NET Core 3.0 预览版 1 如何连接到 <https://www.cloudflare.com>：

```csharp
using System;
using System.Net.Security;
using System.Net.Sockets;
using System.Threading.Tasks;

namespace tlstest
{
    class Program
    {
        static async Task Main()
        {
            using (TcpClient tcpClient = new TcpClient())
            {
                string targetHost = "www.cloudflare.com";

                await tcpClient.ConnectAsync(targetHost, 443);

                using (SslStream sslStream = new SslStream(tcpClient.GetStream()))
                {
                    await sslStream.AuthenticateAsClientAsync(targetHost);
                    await Console.Out.WriteLineAsync($"Connected to {targetHost} with {sslStream.SslProtocol}");
                }
            }
        }
    }
}
```

```console
user@comp-ubuntu1810:~/tlstest$ dotnet run
Connected to www.cloudflare.com with Tls13
user@comp-ubuntu1810:~/tlstest$ openssl version
OpenSSL 1.1.1  11 Sep 2018
```

>[!IMPORTANT]
>Windows 和 macOS 尚不支持 TLS 1.3。 当支持可用时，.NET Core 3.0 将在这些操作系统上支持 TLS 1.3。

## <a name="cryptography"></a>密码

添加了对 AES-GCM 和 AES-CCM 密码的支持，通过 `System.Security.Cryptography.AesGcm` 和 `System.Security.Cryptography.AesCcm` 实现。 这些算法都是[使用关联数据的验证加密 (AEAD) 算法](https://en.wikipedia.org/wiki/Authenticated_encryption)，以及第一个添加到 .NET Core 的验证加密 (AE) 算法。

下面的代码演示了如何使用 AesGcm 密码加密和解密随机数据。

AesCcm 代码几乎完全相同（仅类变量名称不同）。

```csharp
// key should be: pre-known, derived, or transported via another channel, such as RSA encryption
byte[] key = new byte[16];
RandomNumberGenerator.Fill(key);

byte[] nonce = new byte[12];
RandomNumberGenerator.Fill(nonce);

// normally this would be your data
byte[] dataToEncrypt = new byte[1234];
byte[] associatedData = new byte[333];
RandomNumberGenerator.Fill(dataToEncrypt);
RandomNumberGenerator.Fill(associatedData);

// these will be filled during the encryption
byte[] tag = new byte[16];
byte[] ciphertext = new byte[dataToEncrypt.Length];

using (AesGcm aesGcm = new AesGcm(key))
{
    aesGcm.Encrypt(nonce, dataToEncrypt, ciphertext, tag, associatedData);
}

// tag, nonce, ciphertext, associatedData should be sent to the other part

byte[] decryptedData = new byte[ciphertext.Length];

using (AesGcm aesGcm = new AesGcm(key))
{
    aesGcm.Decrypt(nonce, ciphertext, tag, decryptedData, associatedData);
}

// do something with the data
// this should always print that data is the same
Console.WriteLine($"AES-GCM: Decrypted data is{(dataToEncrypt.SequenceEqual(decryptedData) ? "the same as" : "different than")} original data.");
```

## <a name="cryptographic-key-importexport"></a>加密密钥导入/导出

.NET Core 3.0 预览版 1 支持从标准格式导入和导出非对称公钥和私钥，而不需要使用 X.509 证书。

所有密钥类型（RSA、DSA、ECDsa、ECDiffieHellman）都支持公钥的 X.509 SubjectPublicKeyInfo 格式，以及私钥的 PKCS#8 PrivateKeyInfo 和 PKCS#8 EncryptedPrivateKeyInfo 格式。 RSA 此外还支持 PKCS#1 RSAPublicKey 和 PKCS#1 RSAPrivateKey。 所有导出方法都生成 DER 编码的二进制数据，导入方法也是如此。 如果密钥以文本友好的 PEM 格式存储，调用方需要在调用导入方法之前对内容进行 base64 解码。

```csharp
using System;
using System.IO;
using System.Security.Cryptography;

namespace rsakeyprint
{
    class Program
    {
        static void Main(string[] args)
        {
            using (RSA rsa = RSA.Create())
            {
                byte[] keyBytes = File.ReadAllBytes(args[0]);
                rsa.ImportRSAPrivateKey(keyBytes, out int bytesRead);
 
                Console.WriteLine($"Read {bytesRead} bytes, {keyBytes.Length-bytesRead} extra byte(s) in file.");
                RSAParameters rsaParameters = rsa.ExportParameters(true);
                Console.WriteLine(BitConverter.ToString(rsaParameters.D));
            }
        }
    }
}
```

```console
user@comp-ubuntu1810:~/rsakeyprint$ echo Making a small key to save on screen space.
Making a small key to save on screen space.
user@comp-ubuntu1810:~/rsakeyprint$ openssl genrsa 768 | openssl rsa -outform der -out rsa.key
Generating RSA private key, 768 bit long modulus (2 primes)
..+++++++
........+++++++
e is 65537 (0x010001)
writing RSA key
user@comp-ubuntu1810:~/rsakeyprint$ dotnet run rsa.key
Read 461 bytes, 0 extra byte(s) in file.
0F-D0-82-34-F8-13-38-4A-7F-C7-52-4A-F6-93-F8-FB-6D-98-7A-6A-04-3B-BC-35-8C-7D-AC-A5-A3-6E-AD-C1-66-30-81-2C-2A-DE-DA-60-03-6A-2C-D9-76-15-7F-61-97-57-
79-E1-6E-45-62-C3-83-04-97-CB-32-EF-C5-17-5F-99-60-92-AE-B6-34-6F-30-06-03-AC-BF-15-24-43-84-EB-83-60-EF-4D-3B-BD-D9-5D-56-26-F0-51-CE-F1
user@comp-ubuntu1810:~/rsakeyprint$ openssl rsa -in rsa.key -inform der -text -noout | grep -A7 private
privateExponent:
    0f:d0:82:34:f8:13:38:4a:7f:c7:52:4a:f6:93:f8:
    fb:6d:98:7a:6a:04:3b:bc:35:8c:7d:ac:a5:a3:6e:
    ad:c1:66:30:81:2c:2a:de:da:60:03:6a:2c:d9:76:
    15:7f:61:97:57:79:e1:6e:45:62:c3:83:04:97:cb:
    32:ef:c5:17:5f:99:60:92:ae:b6:34:6f:30:06:03:
    ac:bf:15:24:43:84:eb:83:60:ef:4d:3b:bd:d9:5d:
    56:26:f0:51:ce:f1
```

可以使用 `System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo` 类检查 PKCS#8 文件。

可以分别使用 `System.Security.Cryptography.Pkcs.Pkcs12Info` 和 `System.Security.Cryptography.Pkcs.Pkcs12Builder` 检查和操作 PFX/PKCS#12 文件。

## <a name="serialport-for-linux"></a>适用于 Linux 的 SerialPort

.NET Core 3.0 现在在 Linux 上支持 <xref:System.IO.Ports.SerialPort?displayProperty=nameWithType>。

以前，.NET Core 只支持在 Windows 上使用 `SerialPort` 类型。

## <a name="more-bcl-improvements"></a>更多的 BCL 改进

.NET Core 2.1 中引入的 `Span<T>`、`Memory<T>` 和相关类型已在 .NET Core 3.0 中优化。 常见操作（例如跨越构造、切片、分析和格式化）现在可以更好地执行。 

此外，像 `String` 这样的类型已经看到了一些潜在的改进，使它们在与 `Dictionary<TKey, TValue>` 和其他集合一起用作键时更有效。 不需要更改代码就可以从这些改进中获益。

以下改进也是 .NET Core 3 预览版 1 中的新增功能：

* 内置于 HttpClient 的 Brotli 支持
* ThreadPool.UnsafeQueueWorkItem(IThreadPoolWorkItem)
* Unsafe.Unbox
* CancellationToken.Unregister
* 复杂算术运算符
* TCP 套接字 API 保持活动状态
* StringBuilder.GetChunks
* IPEndPoint 分析
* RandomNumberGenerator.GetInt32

## <a name="tiered-compilation"></a>分层编译

仅在 .NET Core 3.0 中默认启用[分层编译](https://devblogs.microsoft.com/dotnet/tiered-compilation-preview-in-net-core-2-1/)。 它是一项功能，使运行时能够更适应地使用实时 (JIT) 编译器，从而在启动时获得更好的性能，并最大限度地提高吞吐量。

此功能已作为一项可选功能添加到 [.NET Core 2.1](https://devblogs.microsoft.com/dotnet/announcing-net-core-2-1/)，然后在 [.NET Core 2.2 预览版 2](https://devblogs.microsoft.com/dotnet/announcing-net-core-2-2-preview-2/) 中默认启用。 随后，它在 .NET Core 2.2 版本中还原回可选功能。

## <a name="arm64-linux-support"></a>ARM64 Linux 支持

添加了适用于 Linux 的 ARM64 支持。 ARM64 的主要用例是当前的 IoT 场景。

Alpine、Debian 和 Ubuntu [Docker 映像均适用于 .NET Core for ARM64](https://hub.docker.com/r/microsoft/dotnet/)。

有关详细信息，请查看 [.NET Core ARM64 状态](https://github.com/dotnet/announcements/issues/82)。

>[!NOTE]
> **ARM64** 尚未提供 Windows 支持。

## <a name="install-net-core-30-previews-on-linux-with-snap"></a>通过 Snap 在 Linux 上安装 .NET Core 3.0 预览版

Snap 是在[支持 Snap 的 Linux 分发](https://docs.snapcraft.io/installing-snapd/6735)上安装和试用 .NET Core 预览版的首选方式。

在系统上配置 Snap 后，运行以下命令安装 [.NET Core SDK 3.0 预览版 SDK](https://snapcraft.io/dotnet-sdk)。

```console
sudo snap install dotnet-sdk --beta --classic
```
 
如果使用 Snap 包安装 .NET Core，则默认的 .NET Core 命令为 `dotnet-sdk.dotnet`，而不是直接的 `dotnet`。 命名空间命令的好处是，不会与全局安装的 .NET Core 版本发生冲突。 此命令可以使用以下命令化名为 `dotnet`：

```console
sudo snap alias dotnet-sdk.dotnet dotnet
```

某些发行版需要执行额外步骤来实现对 SSL 证书的访问。 请参阅 [Linux 安装程序](https://github.com/dotnet/core/blob/master/Documentation/linux-setup.md)，了解详细信息。

## <a name="gpio-support-for-raspberry-pi"></a>对 Raspberry Pi 的 GPIO 支持

已向 NuGet 发布了两个新的程序包，可用于 GPIO 编程。

* [System.Device.Gpio](https://www.nuget.org/packages/System.Device.Gpio/0.1.0-prerelease.19078.2)
* [Iot.Device.Bindings](https://www.nuget.org/packages/Iot.Device.Bindings/0.1.0-prerelease.19078.2)

GPIO 包包括用于 GPIO、SPI、I2C 和 PWM 设备的 API。 IoT 绑定包包括针对各种芯片和传感器的[设备绑定](https://github.com/dotnet/iot/blob/master/src/devices/README.md)，与 [dotnet/iot - src/devices](https://github.com/dotnet/iot/tree/master/src/devices) 提供的相同。

这些包中不包含作为 .NET Core 3.0 预览版 1 一部分的已更新的串行端口 API，但这些 API 可作为 .NET Core 平台的一部分提供。


## <a name="platform-support"></a>平台支持

以下操作系统支持 .NET Core 3：

* Windows 客户端：7、8.1、10（1607 及更高版本）
* Windows Server：2012 R2 SP1+
* macOS：10.12+
* RHEL：6+
* Fedora：26+
* Ubuntu：16.04+
* Debian：9+
* SLES：12+
* openSUSE：42.3+
* Alpine：3.8+

芯片支持如下所示：

* Windows、macOS 和 Linux 上的 x64
* Windows 上的 x86
* Windows 和 Linux 上的 ARM32
* Linux 上的 ARM64

对于 Linux，ARM32 在 Debian 9+ 和 Ubuntu 16.04+ 上受支持。 对于 ARM64，它与 ARM32 搭载 Alpine 3.8 等效。 这些版本与支持 X64 的发行版相同。

[Docker 中心的 microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/) 提供适用于 .NET Core 3.0 的 Docker 映像。 Microsoft 目前正在采用 [Microsoft 容器注册表 (MCR)](https://cloudblogs.microsoft.com/opensource/2019/01/17/improved-discovery-experience-microsoft-containers-docker-hub/)，预计最终的 .NET Core 3.0 映像将仅发布到 MCR。
