---
title: 使用 Parallel.ForEach 编写简单的并行程序
ms.date: 02/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- foreach, parallel version
- parallel programming, foreach
ms.assetid: cb5fab92-1c19-499e-ae91-8b7525dd875f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3bde7ebcc73c5e9e2d87074b78d78bb63cd441ad
ms.sourcegitcommit: 07c4368273b446555cb2c85397ea266b39d5fe50
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2019
ms.locfileid: "56583636"
---
# <a name="how-to-write-a-simple-parallelforeach-loop"></a>如何：编写简单的 Parallel.ForEach 循环

此示例展示了如何使用 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 循环，对任何 <xref:System.Collections.IEnumerable?displayProperty=nameWithType> 或 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 数据源启用数据并行。

> [!NOTE]
> 本文档使用 lambda 表达式在 PLINQ 中定义委托。 如果不熟悉 C# 或 Visual Basic 中的 lambda 表达式，请参阅 [PLINQ 和 TPL 中的 Lambda 表达式](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)。

## <a name="example"></a>示例

此示例假定 C:\Users\Public\Pictures\Sample Pictures 文件夹中有几个 .jpg 文件，并创建名为“Modified”的新子文件夹。 运行该示例时，它会旋转示例图片中的每个 .jpg 图像并将其保存到“Modified”文件夹 可以根据需要修改这两个路径。

[!code-csharp[TPL_Parallel#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleforeach.cs#03)]
[!code-vb[TPL_Parallel#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleforeach.vb#03)]

<xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 循环的工作原理类似 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 循环。 该循环对源集合进行分区，并根据系统环境在多个线程上安排工作。 系统上的处理器越多，并行方法的运行速度就越快。 对于一些源集合，有序循环可能会更快，具体视源大小以及该循环要执行的工作类型而定。 若要详细了解性能，请参阅[数据并行和任务并行的潜在问题](../../../docs/standard/parallel-programming/potential-pitfalls-in-data-and-task-parallelism.md)

若要详细了解并行循环，请参阅[如何：编写简单的 Parallel.For 循环](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md)。

若要将 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 与非泛型集合结合使用，可以使用 <xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType> 扩展方法，将集合转换为泛型集合，如下面的示例所示：

[!code-csharp[TPL_Parallel#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/nongeneric.cs#07)]
[!code-vb[TPL_Parallel#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/nongeneric.vb#07)]

还可以使用并行 LINQ (PLINQ) 并行处理 <xref:System.Collections.Generic.IEnumerable%601> 数据源。 借助 PLINQ，可以使用声明性查询语法来表达循环行为。 有关详细信息，请参阅[并行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)。

## <a name="compile-and-run-the-code"></a>编译并运行代码

可以作为 .NET Framework 的控制台应用程序或 .NET Core 的控制台应用程序编译代码。

Visual Studio 中有适用于 Windows 桌面和 .NET Core 的 Visual Basic 和 C# 控制台应用程序模板。

从命令行，可使用 .NET Core 及其 CLI 工具（例如 `dotnet new console` 或 `dotnet new console -lang vb`），或者可创建文件并使用 .NET Framework 应用程序提供的命令行编译器。

对于.NET Core 项目，必须引用 System.Drawing.Common NuGet 包。 在 Visual Studio 中，使用 NuGet 包管理器安装该包。 或者，可以添加对 .csproj * 或 .vbproj * 文件中的包的引用：
 
```xml
<ItemGroup>
     <PackageReference Include="System.Drawing.Common" Version="4.5.1" />
</ItemGroup>
```

要从命令行运行 .NET Core 控制台应用程序，请使用包含该应用程序的文件夹中的 `dotnet run`。

要从 Visual Studio 中运行控制台应用程序，请按 F5。

## <a name="see-also"></a>请参阅

- [数据并行](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)
- [并行编程](../../../docs/standard/parallel-programming/index.md)
- [并行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
