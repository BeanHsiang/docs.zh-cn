---
title: 源链接和 .NET 库
description: 有关使用源链接改进 .NET 库调试的最佳做法建议。
author: jamesnk
ms.author: mairaw
ms.date: 01/15/2019
ms.openlocfilehash: 10596f589af7abee6ff7833ef25c606294337196
ms.sourcegitcommit: e39d93d358974b9ed4541cedf4e25c0101015c3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2019
ms.locfileid: "55204751"
---
# <a name="source-link"></a>源链接

源链接是一种使开发人员可以从 NuGet 对 .NET 程序集进行源代码调试的技术。 源链接在创建 NuGet 包时执行，然后将源代码管理元数据嵌入在程序集和包中。 下载包并且在 Visual Studio 中启用了源链接的开发人员可以单步执行其源代码。 源链接提供源代码管理元数据来创造出色的调试体验。

## <a name="source-link-demo"></a>源链接演示

> [!VIDEO https://www.youtube.com/embed/gyRGhCQPkB4?start=61]

## <a name="using-source-link"></a>使用源链接

可以在 [dotnet/sourceLink](https://github.com/dotnet/sourcelink/blob/master/README.md) GitHub 存储库上找到有关使用源链接的说明。

可以使用 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)以确认源链接元数据是否已成功嵌入在包中。 检查 `Repository` 元数据是否存在并具有注释标识符，以及 .pdb 文件是否与每个目标的 .dll 放置在一起。

![NuGet 包资源管理器中的 SourceLink](./media/sourcelink/nuget-package-explorer-sourcelink.png "NuGet 包资源管理器中的源链接")

**✔️ 请考虑**使用源链接将源代码管理元数据添加到程序集和 NuGet 包。

> [!TIP]
> 可以通过将调试器特性添加到类型来进一步增强开发人员的调试体验。
> * <xref:System.Diagnostics.DebuggerDisplayAttribute> 可以自定义类或字段在调试器变量窗口中的显示方式。
> * <xref:System.Diagnostics.DebuggerStepThroughAttribute> 指示调试器逐行执行代码，而不是单步执行代码。
> * <xref:System.Diagnostics.DebuggerBrowsableAttribute> 控制成员是否会显示在调试器变量窗口中以及其显示方式。

✔️ 请考虑发布符号文件 (`*.pdb`)。

> 为获得最佳调试体验，库应发布符号文件并使用源链接。 有关符号文件和符号包的详细信息，请参阅[符号包](./nuget.md#symbol-packages)。

>[!div class="step-by-step"]
>[上一页](dependencies.md)
>[下一页](publish-nuget-package.md)
