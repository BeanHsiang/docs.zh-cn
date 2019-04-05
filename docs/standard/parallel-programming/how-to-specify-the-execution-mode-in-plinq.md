---
title: 如何：在 PLINQ 中指定执行模式
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to use execution mode
ms.assetid: e52ff26c-c5d3-4fab-9fec-c937fb387963
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c67b23da6742af3cb65da6da49dbab982a0248bb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54694615"
---
# <a name="how-to-specify-the-execution-mode-in-plinq"></a>如何：在 PLINQ 中指定执行模式
此示例展示了如何强制 PLINQ 规避默认启发，同时并行执行查询，无论查询的形状如何。  
  
> [!WARNING]
>  本示例旨在演示用法，运行速度可能不如等效的顺序 LINQ to Objects 查询快。 若要详细了解加速，请参阅[了解 PLINQ 中的加速](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
## <a name="example"></a>示例  
 [!code-csharp[PLINQ#22](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#22)]
 [!code-vb[PLINQ#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#22)]  
  
 PLINQ 旨在利用机会并行执行查询。 不过，并非所有查询都受益于并行执行。 例如，如果查询包含一个工作量极小的用户委托，顺序运行查询的速度通常更快。 这是因为相较所实现的加速，启用并行执行所涉及的开销更加昂贵。 因此，PLINQ 并不自动并行执行每个查询。 它先检查查询的形状和所包含的各种运算符。 根据此分析，默认执行模式下的 PLINQ 可能会决定顺序执行部分或全部查询。 不过，在某些情况下，你对查询更加了解，所做决定可能优于 PLINQ 根据分析所做的决定。 例如，你可能知道委托非常昂贵，且查询一定会受益于并行执行。 在这种情况下，可以使用 <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> 方法并指定 <xref:System.Linq.ParallelExecutionMode.ForceParallelism> 值，以指示 PLINQ 始终并行运行查询。  
  
## <a name="compiling-the-code"></a>编译代码  
 将此代码剪切并粘贴到 [PLINQ 数据样本](../../../docs/standard/parallel-programming/plinq-data-sample.md)中，并通过 `Main` 调用方法。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Linq.ParallelEnumerable.AsSequential%2A>
- [并行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
