---
title: 将代码从 .NET Framework 移植到 .NET Core
description: 了解移植过程以及发现在将 .NET Framework 项目移植到 .NET Core 时可能有用的工具。
author: cartermp
ms.date: 12/07/2018
ms.custom: seodec18
ms.openlocfilehash: 870320c8467237e87a2675ec5cfb57647026d8ec
ms.sourcegitcommit: c6f69b0cf149f6b54483a6d5c2ece222913f43ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55903567"
---
# <a name="port-your-code-from-net-framework-to-net-core"></a>将代码从 .NET Framework 移植到 .NET Core

如果有在 .NET Framework 上运行的代码，用户也可能会对在 .NET Core 上运行代码感兴趣。 下面提供了移植过程的概述以及在将代码移植到 .NET Core 时可能非常有用的工具列表。

## <a name="overview-of-the-porting-process"></a>移植过程概述

这是我们建议在将项目移植到.NET Core 时采取的过程。 该过程的每个步骤将在以后的文章中详细介绍。

1. 标识并记录第三方依赖项。

   此步骤包含了解什么是第三方依赖项，如何依赖于它们，如何查看它们是否也在 .NET Core 上运行，以及如果没有在其上运行可以采取的步骤。 它还介绍了如何将依赖项迁移到 .NET Core 中使用的 [PackageReference](/nuget/consume-packages/package-references-in-project-files) 格式。

2. 将希望移植的所有项目重定向到目标 .NET Framework 4.7.2 或更高版本。

   此步骤可确保在 .NET Core 不支持特殊 API 的情况下，可以为特定于 .NET Framework 的目标使用备用 API。

3. 使用 [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) 来分析程序集并基于结果制定移植计划。

   API Portability Analyzer 工具分析已编译的程序集并生成报表，该报表将显示高级可移植性摘要和不可用于 .NET Core 上的正在使用的每个 API 的细目。 可以使用此报表和代码库的分析结果一起制定移植代码的计划。

4. 移植测试代码。

   由于移植到 .NET Core 对代码库来说是很大的更改，因此强烈建议移植测试代码，以便在移植代码时可以进行测试。 MSTest、xUnit 和 NUnit 都支持 .NET Core。

5. 执行移植计划！

以下列表显示了在移植过程中使用可能有所帮助的工具：

* .NET Portability Analyzer - [命令行工具](https://github.com/Microsoft/dotnet-apiport/releases)或 [Visual Studio 扩展](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)，可生成有关 .NET Framework 和 .NET Core 之间代码移植性的报表的工具链，并且带有程序集到程序集的问题细目。 有关详细信息，请参阅 [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md)。
* .NET API 分析器 - 一个 Roslyn 分析器，可用于发现不同平台上的潜在 C# API 兼容性风险，并检测是否调用了弃用的 API。 有关详细信息，请参阅 [.NET API 分析器](../../standard/analyzers/api-analyzer.md)。
* Reverse Package Search - 一个[有用的 Web 服务](https://packagesearch.azurewebsites.net)，能够实现搜索某一类型并找到包含该类型的包。

此外，可以尝试使用 [CsprojToVs2017](https://github.com/hvanbakel/CsprojToVs2017) 工具将较小的解决方案或单个项目移植到 .NET Core 项目文件格式。

> [!WARNING] 
> CsprojToVs2017 是第三方工具。 不能保证它适用于所有项目，而且它可能会导致所依赖的行为发生细微变化。 CsprojToVs2017 应作为一个起点，以自动化可自动执行的基本操作。 它不是迁移项目文件格式的有保证的解决方案。

>[!div class="step-by-step"]
>[下一页](net-framework-tech-unavailable.md)
