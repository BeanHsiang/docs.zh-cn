---
title: 使映像更易于在.NET 中进行调试
description: 了解如何使用 IDE 简化调试切换配置的可执行映像和命令行选项。
ms.date: 08/30/2018
helpviewer_keywords:
- images [.NET Framework], debugging
- executable image for debugging
- debugging [.NET Framework], executable images for
ms.assetid: 7d90ea7a-150f-4f97-98a7-f9c26541b9a3
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5bab707afb059d4fcbd46a9ee54edead991be523
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57362003"
---
# <a name="making-an-image-easier-to-debug-in-net"></a>使映像更易于在.NET 中进行调试

编译非托管代码时，可以通过设置 IDE 开关或命令线选项来配置可执行映像进行调试。 例如，可以使用 Visual C++ 中的 /Zi 命令行选项，使其发出调试符号文件（文件扩展名为 .pdb）。 同样，/Od 命令行选项告知编译器禁用优化。 生成的代码运行得更慢，但它是更轻松地调试，这很必要。

编译.NET Framework 托管代码时，Visual c + +、 Visual Basic 和 C# 等编译器会将它们的源程序编译为 Microsoft 中间语言 (MSIL)。 MSIL 然后进行 JIT 编译的之前执行，为本机代码。 与非托管代码一样，可以通过设置 IDE 开关或命令行选项来配置可执行映像进行调试。 此外可以配置用于大致相同的方式在调试 JIT 编译。

这种 JIT 配置具有两个方面：

- 可以请求 JIT 编译器以生成跟踪信息。 这使调试程序能将 MSIL 链与其机器码对应项相匹配，并跟踪存储本地变量和函数参数的位置。 从.NET Framework 2.0 版开始，JIT 编译器始终生成跟踪信息，因此无需进行请求它。

- 可以请求 JIT 编译器不优化生成的计算机代码。

通常情况下，生成 MSIL 的编译器设置这些 JIT 编译器选项，相应地基于 IDE 开关或命令行选项指定，例如，/**Od**。

某些情况下，可能需要更改 JIT 编译器的行为，使其生成的机器码更易于调试。 例如，可能希望为零售版本或控制优化生成实时跟踪信息。 可以使用初始化 (.ini) 文件来执行此操作。

例如，如果你想要调试该程序集名为*MyApp.exe*，则可以创建一个名为文本文件*MyApp.ini*，在相同的文件夹*MyApp.exe*，其中包含以下三行：

```ini
[.NET Framework Debugging Control]
GenerateTrackingInfo=1
AllowOptimize=0
```

可将每个选项的值设置为 0 或 1，任何不存在选项默认为 0。 将 `GenerateTrackingInfo` 设为 1、`AllowOptimize` 设为 0，这可提供最简单的调试。

从.NET Framework 2.0 版开始，JIT 编译器始终生成跟踪信息而不考虑为值`GenerateTrackingInfo`; 但是，`AllowOptimize`值仍产生影响。 如果使用 [Ngen.exe（本机映像生成器）](../../../docs/framework/tools/ngen-exe-native-image-generator.md)预编译本机映像而不进行优化，Ngen.exe 执行时 .ini 文件必须存在于 `AllowOptimize=0` 的目标文件夹。 如果已经预编译程序集而不进行优化，则必须删除预编译的代码使用 NGen.exe **/uninstall**选项才能重新运行 Ngen.exe 将代码预编译为优化。 如果.ini 文件不存在的文件夹中，默认情况下 Ngen.exe 将代码预编译为优化。

<xref:System.Diagnostics.DebuggableAttribute?displayProperty=nameWithType> 控制程序集的设置。 **DebuggableAttribute**是否 JIT 编译器应优化和/或生成跟踪信息包括两个字段的控件。 从.NET Framework 2.0 版开始，JIT 编译器始终生成跟踪信息。

对于零售版本中，编译器不设置任何**DebuggableAttribute**。 默认情况下，JIT 编译器生成最高的性能，最难调试的机器码。 启用实时跟踪会稍微降低性能，禁用优化会极大降低性能。

DebuggableAttribute 一次应用于整个程序集，而不是应用于程序集中的单个模块。 因此，开发工具必须将自定义属性附加到程序集元数据令牌，如果已经创建程序集，则附加到名为 System.Runtime.CompilerServices.AssemblyAttributesGoHere 的类。 然后，ALink 工具升级这些**DebuggableAttribute**它们的一部分可以从每个模块的程序集的属性。 如果没有冲突，ALink 操作失败。

> [!NOTE]
> 在 .NET Framework 1.0 版本中，当指定 /clr 和 /Zi 编译器选项时，Microsoft Visual C++ 编译器将添加 DebuggableAttribute。 在.NET framework 版本 1.1 中，您必须添加**DebuggableAttribute**手动在代码或使用 **/ASSEMBLYDEBUG**链接器选项。

## <a name="see-also"></a>请参阅

- [调试、跟踪和分析](../../../docs/framework/debug-trace-profile/index.md)
- [启用 JIT 附加调试](../../../docs/framework/debug-trace-profile/enabling-jit-attach-debugging.md)
- [启用分析](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/s5ec0es1(v=vs.100))
