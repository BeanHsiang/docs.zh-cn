---
title: 开始创建高质量的 .NET 库
description: 开始构建 .NET 库。
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: e26c6632252257ab8cb5598f1b201559b760dc6b
ms.sourcegitcommit: e39d93d358974b9ed4541cedf4e25c0101015c3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2019
ms.locfileid: "55204635"
---
# <a name="get-started"></a>入门

## <a name="cross-platform-targetingcross-platform-targetingmd"></a>[跨平台定位](./cross-platform-targeting.md)

如何使用 .NET Standard 和多目标来创建跨平台库。 .NET 可以在许多平台上运行，优秀的 .NET 库应能尽量为尽可能多的平台和开发人员提供支持。

## <a name="strong-namingstrong-namingmd"></a>[强命名](./strong-naming.md)

了解强命名及其优点和缺点。 对 .NET 库进行强命名可以让大多数开发者使用它，这是推荐的最佳做法。

## <a name="nuget-and-open-source-librariesnugetmd"></a>[NuGet 和开放源代码库](./nuget.md)

为开放源代码 .NET 库创建 NuGet 包的最佳方法，包括在 NuGet.org 上公开发布的所有包的推荐元数据。

### <a name="dependenciesdependenciesmd"></a>[依赖项](./dependencies.md)

NuGet 使构建 .NET 库时可以轻松地使用现有包。 了解 NuGet 依赖项的常见冲突来源以及如何避免冲突。

### <a name="source-linksourcelinkmd"></a>[源链接](./sourcelink.md)

源链接是一个很棒的工具，.NET 库的用户在调试时可以使用它进入其源代码。 本文概述了源链接是什么以及为什么要使用它。

### <a name="publishingpublish-nuget-packagemd"></a>[发布](./publish-nuget-package.md)

虽然 NuGet.org 是最广为人知和使用范围最广的存储库，但有很多平台可以发布 NuGet 包。 了解可用的不同 NuGet 包存储库以及发布 .NET 库的安全性最佳做法。

## <a name="versioningversioningmd"></a>[版本控制](./versioning.md)

优秀的 .NET 库可以随着时间的推移不断发展：增加功能、修复 bug 并提高后续版本的性能。 了解各种版本号以及如何向开发人员传达重大更改。

### <a name="breaking-changesbreaking-changesmd"></a>[中断性变更](./breaking-changes.md)

对于 .NET 库而言，在现有用户的稳定性与未来的创新之间找到平衡点非常重要。 了解不同类型的重大更改和添加新功能的策略，同时保持向后兼容性。

>[!div class="step-by-step"]
>[上一页](index.md)
>[下一页](cross-platform-targeting.md)