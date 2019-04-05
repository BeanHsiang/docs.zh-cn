---
title: 分析依赖项将代码移植到 .NET Core
description: 了解如何分析外部依赖项，以便将项目从 .NET Framework 移植到 .NET Core。
author: cartermp
ms.date: 12/07/2018
ms.custom: seodec18
ms.openlocfilehash: 6c0f55150a4a1c4d0fb8b3125565c9ab8ade3117
ms.sourcegitcommit: c6f69b0cf149f6b54483a6d5c2ece222913f43ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55904338"
---
# <a name="analyze-your-dependencies-to-port-code-to-net-core"></a>分析依赖项将代码移植到 .NET Core

若要将代码移植到 .NET Core 或.NET Standard，必须了解依赖项。 外部依赖项是在项目中引用但没有构建的 [NuGet 包](#analyze-referenced-nuget-packages-in-your-projects)或 [Dll](#analyze-dependencies-that-arent-nuget-packages)。 评估每个依赖项并为与 .NET Core 不兼容的依赖项制定应变计划。 下面介绍了如何确定依赖项是否与 .NET Core 兼容。

## <a name="analyze-referenced-nuget-packages-in-your-projects"></a>分析项目中引用的 NuGet 包

如果在项目中引用 NuGet 包，需要验证它们是否与 .NET Core 兼容。
可通过两种方式来实现此目的：

* [使用 NuGet 包资源管理器应用](#analyze-nuget-packages-using-nuget-package-explorer)
* [使用 nuget.org 站点](#analyze-nuget-packages-using-nugetorg)

分析包后，如果它们与 .NET Core 不兼容并且仅面向 .NET Framework，则可检查 [.NET Framework 兼容性模式](#net-framework-compatibility-mode)是否能有助于移植过程。

### <a name="analyze-nuget-packages-using-nuget-package-explorer"></a>使用 NuGet 包资源管理器分析 NuGet 包

NuGet 包本身就是一组包含特定于平台的程序集的文件夹。 所以需要检查包中是否有包含兼容程序集的文件夹。

检查 NuGet 包文件夹最简单方法是使用 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)工具。 安装完成后，使用以下步骤查看文件夹名称：

1. 打开 NuGet 包资源管理器。
2. 单击“从在线源打开包”。
3. 搜索包的名称。
4. 从搜索结果中选择包的名称，然后点击“打开”。
5. 展开右侧的“lib”文件夹并查看文件夹名称。

查找具有以下任意名称的文件夹：

```
netstandard1.0
netstandard1.1
netstandard1.2
netstandard1.3
netstandard1.4
netstandard1.5
netstandard1.6
netstandard2.0
netcoreapp1.0
netcoreapp1.1
netcoreapp2.0
netcoreapp2.1
netcoreapp2.2
portable-net45-win8
portable-win8-wpa8
portable-net451-win81
portable-net45-win8-wpa8-wpa81
```

这些值是映射到 [.NET Standard](../../standard/net-standard.md) 版本的[目标框架名字对象 (TFM)](../../standard/frameworks.md)、.NET Core 以及与 .NET Core 兼容的传统可移植类库 (PCL) 配置文件。

> [!IMPORTANT]
> 查看包支持的 TFM 时，请注意 `netcoreapp*`，它在兼容时，仅适用于 .NET Core 项目，不适用于 .NET Standard 项目。
> 仅面向 `netcoreapp*` 而不是 `netstandard*` 的库只能用于其他 .NET Core 应用。

### <a name="analyze-nuget-packages-using-nugetorg"></a>使用 nuget.org 分析 NuGet 包

或者，可在包页面“依赖项”部分下的 [nuget.org](https://www.nuget.org/) 上查看每个包支持的 TFM。

尽管使用该站点可以比较简单地验证兼容性，但站点上并未提供所有包的“依赖项”信息。

### <a name="net-framework-compatibility-mode"></a>.NET Framework 兼容性模式

在分析完 NuGet 包之后，你可能会发现它们仅面向 .NET Framework，就像大多数 NuGet 包一样。

从 .NET Standard 2.0 开始，引入了 .NET Framework 兼容性模式。 此兼容性模式允许 .NET Standard 和 .NET Core 项目引用 .NET Framework 库。 引用 .NET Framework 库不适用于所有项目（如库使用 Windows Presentation Foundation (WPF) API 时），但它的开启了很多移植方案。

在项目中引用面向 .NET Framework 的 NuGet 包时（如 [Huitian.PowerCollections](https://www.nuget.org/packages/Huitian.PowerCollections)），会收到与以下示例类似的包回退警告 ([NU1701](/nuget/reference/errors-and-warnings/nu1701))：

`NU1701: Package ‘Huitian.PowerCollections 1.0.0’ was restored using ‘.NETFramework,Version=v4.6.1’ instead of the project target framework ‘.NETStandard,Version=v2.0’. This package may not be fully compatible with your project.`

当添加包以及每次生成时都会显示该警告，以确保在项目中测试该包。 如果项目按预期工作，可通过在 Visual Studio 中编辑包属性或在最喜欢的代码编辑器中手动编辑项目文件来取消该警告。

若要通过编辑项目文件来取消警告，请找到要取消警告的包的 `PackageReference` 条目并添加 `NoWarn` 属性。 `NoWarn` 属性接受所有警告 ID 的逗号分隔列表。 以下示例显示如何通过手动编辑项目文件来取消 `Huitian.PowerCollections` 包的 `NU1701` 警告：

```xml
<ItemGroup>
  <PackageReference Include="Huitian.PowerCollections" Version="1.0.0" NoWarn="NU1701" />
</ItemGroup>
```

有关如何在 Visual Studio 中取消编译器警告的详细信息，请参阅[取消 NuGet 包的警告](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages)。

## <a name="port-your-packages-to-packagereference"></a>将包移植到 `PackageReference`

.NET Core 使用 [PackageReference](/nuget/consume-packages/package-references-in-project-files) 来指定包依赖项。 如果使用 [packages.config](/nuget/reference/packages-config) 来指定包，将需要转换为 `PackageReference`。

有关详细信息，请参阅[从 packages.config 迁移到 PackageReference](/nuget/reference/migrate-packages-config-to-package-reference)。

## <a name="what-to-do-when-your-nuget-package-dependency-doesnt-run-on-net-core"></a>NuGet 包依赖项未在.NET Core 上运行时应执行的操作

如果所依赖的 NuGet 包无法在 .NET Core 上运行，可以执行以下几项操作：

1. 如果项目是开放源代码并托管在诸如 GitHub 中，则可以直接与开发人员交流。
2. 可直接在 [nuget.org](https://www.nuget.org/) 上联系作者。搜索包并单击包页面左侧的“联系所有者”。
3. 可以搜索在 .NET Core 上运行的其他包，它与所使用的包进行的是相同的任务。
4. 可以尝试自己编写包所执行的代码。
5. 可以通过更改应用的功能来清除对包的依赖性，至少在该包有可用的兼容性版本之前都能这样做。

请注意，开源项目维护人员和 NuGet 包发布者通常是志愿者。 他们因为关注某个特定领域而免费提供服务，通常从事另外一份职业。 因此，当联系他们请求 .NET Core 支持时请注意这点。

如果采取上述任何操作都无法解决问题，则可能需要移植到最近版本的 .NET Core。

.NET 团队需要了解哪些库最需要使用 .NET Core 支持。 你可以发送电子邮件到 dotnet@microsoft.com，谈谈你想要使用的库。

## <a name="analyze-dependencies-that-arent-nuget-packages"></a>分析不是 NuGet 包的依赖项

用户可能拥有不是 NuGet 包的依赖项，如文件系统中的 DLL。 确定该依赖项是否可移植的唯一方法是运行 [.NET 可移植性分析器](https://github.com/Microsoft/dotnet-apiport)工具。 该工具可以分析面向 .NET Framework 的程序集，并识别不可移植到其他 .NET 平台（如 .NET Core）的 API。 可将该工具作为控制台应用程序或作为 [Visual Studio 扩展](../../standard/analyzers/portability-analyzer.md)来运行。

>[!div class="step-by-step"]
>[下一页](libraries.md)
