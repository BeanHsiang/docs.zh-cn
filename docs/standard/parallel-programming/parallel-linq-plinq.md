---
title: 并行 LINQ (PLINQ)
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- PLINQ, overview
ms.assetid: 3d4d0cd3-bde4-490b-99e7-f4e41be96455
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2c438170ec48f40e59f8710d4e3820d6e915bed5
ms.sourcegitcommit: c6f69b0cf149f6b54483a6d5c2ece222913f43ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55903821"
---
# <a name="parallel-linq-plinq"></a>并行 LINQ (PLINQ)
并行 LINQ (PLINQ) 是 LINQ to Objects 的并行实现。 PLINQ 将整套 LINQ 标准查询运算符实现为 <xref:System.Linq> 命名空间的扩展方法，并提供适用于并行操作的其他运算符。 PLINQ 将 LINQ 语法的简洁和可靠性与并行编程的强大功能结合在一起。 就像面向任务并行库的代码一样，PLINQ 查询会根据主计算机的能力按比例调整并发程度。  
  
 在许多情况下，PLINQ 可通过更有效地使用主计算机上的所有可用内核来显著提高 LINQ to Objects 查询的速度。 这一性能提升使桌面具备高性能计算能力。  
  
## <a name="in-this-section"></a>本节内容  
 [PLINQ 介绍](../../../docs/standard/parallel-programming/introduction-to-plinq.md)  
  
 [了解 PLINQ 中的加速](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)  
  
 [PLINQ 中的顺序保留](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)  
  
 [PLINQ 中的合并选项](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)  
  
 [如何：创建并执行简单的 PLINQ 查询](../../../docs/standard/parallel-programming/how-to-create-and-execute-a-simple-plinq-query.md)  
  
 [如何：在 PLINQ 查询中控制排序](../../../docs/standard/parallel-programming/how-to-control-ordering-in-a-plinq-query.md)  
  
 [如何：合并并行和顺序 LINQ 查询](../../../docs/standard/parallel-programming/how-to-combine-parallel-and-sequential-linq-queries.md)  
  
 [如何：处理 PLINQ 查询中的异常](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md)  
  
 [如何：取消 PLINQ 查询](../../../docs/standard/parallel-programming/how-to-cancel-a-plinq-query.md)  
  
 [如何：编写自定义 PLINQ 聚合函数](../../../docs/standard/parallel-programming/how-to-write-a-custom-plinq-aggregate-function.md)  
  
 [如何：在 PLINQ 中指定执行模式](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md)  
  
 [如何：在 PLINQ 中指定合并选项](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)  
  
 [如何：使用 PLINQ 循环访问文件目录](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md)  
  
 [如何：衡量 PLINQ 查询性能](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md)  
  
 [PLINQ 数据示例](../../../docs/standard/parallel-programming/plinq-data-sample.md)  
  
## <a name="see-also"></a>请参阅

- <xref:System.Linq.ParallelEnumerable>
- [并行编程](../../../docs/standard/parallel-programming/index.md)
- [语言集成查询 (LINQ) - C#](../../csharp/programming-guide/concepts/linq/index.md)  
- [语言集成查询 (LINQ) - Visual Basic](../../visual-basic/programming-guide/concepts/linq/index.md)  
