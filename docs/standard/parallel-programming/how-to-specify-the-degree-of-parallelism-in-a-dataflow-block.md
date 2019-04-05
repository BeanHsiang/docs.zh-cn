---
title: 如何：指定数据流块中的并行度
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dataflow block, specifying parallelism in TPL
- Task Parallel Library, dataflows
- TPL dataflow library, specifying parallelism
ms.assetid: e4088541-ee05-40db-95f5-147cfe62fde7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 78459e6cc2b40c9f3b821e4c4b53aec0c2f543db
ms.sourcegitcommit: a36cfc9dbbfc04bd88971f96e8a3f8e283c15d42
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54222750"
---
# <a name="how-to-specify-the-degree-of-parallelism-in-a-dataflow-block"></a>如何：指定数据流块中的并行度
本文档介绍如何设置 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A?displayProperty=nameWithType> 属性使执行数据流块一次处理多条消息。 当数据流块需要执行长时间运行的计算并且可从并行处理消息中获益时，这种做法很有用。 此示例使用 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601?displayProperty=nameWithType> 类并发执行多个数据流操作；但是，您可以对 TPL 数据流库提供的任何预定义的执行块类型（<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>、<xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=nameWithType>）指定最大并行度。

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="example"></a>示例  
 下面的示例执行两个数据流计算并输出每个计算所需的运行时间。 第一个计算指定最大并行度为 1，这是默认值。 最大并行度 1 会使数据流块按顺序处理消息。 第二个计算与第一个类似，但指定的最大并行度与可用处理器的数量相等。 这使数据流块能够并行执行多个操作。  
  
 [!code-csharp[TPLDataflow_DegreeOfParallelism#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_degreeofparallelism/cs/dataflowdegreeofparallelism.cs#1)]
 [!code-vb[TPLDataflow_DegreeOfParallelism#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_degreeofparallelism/vb/dataflowdegreeofparallelism.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
 复制示例代码，并将它粘贴到 Visual Studio 项目中，或粘贴到 `DataflowDegreeOfParallelism.cs`（对于 Visual Basic，则为 `DataflowDegreeOfParallelism.vb`）文件中，再在 Visual Studio 开发人员命令提示窗口中运行以下命令。  
  
 Visual C#  
  
 **csc.exe /r:System.Threading.Tasks.Dataflow.dll DataflowDegreeOfParallelism.cs**  
  
 Visual Basic  
  
 **vbc.exe /r:System.Threading.Tasks.Dataflow.dll DataflowDegreeOfParallelism.vb**  
  
## <a name="robust-programming"></a>可靠编程  
 默认情况下，每个预定义的数据流块会按照接收消息的顺序将消息传播出去。  虽然在指定的最大并行度大于 1 时会同时处理多条消息，但这些消息仍然按被接收的顺序进行传播。  
  
 由于 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A> 属性表示最大并行度，因此数据流块执行时的并行度可能小于指定的值。 为了满足功能需求或需要考虑可用系统资源不足的问题时，数据流块可以使用较小的并行度。 数据流块选择的并行度从不会大于您指定的值。  
  
## <a name="see-also"></a>请参阅

- [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
