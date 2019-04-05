---
title: 如何：实现动态分区
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to create a dynamic partitioner
ms.assetid: c875ad12-a161-43e6-ad1c-3d6927c536a7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 792488e53ffb7f870e21fdd1ad3ef94bf0303b1a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54720231"
---
# <a name="how-to-implement-dynamic-partitions"></a>如何：实现动态分区
下面的示例展示了如何实现自定义 <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=nameWithType>，以实现动态分区，并可以通过特定重载 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 和 PLINQ 进行使用。  
  
## <a name="example"></a>示例  
 每当分区对枚举器调用 <xref:System.Collections.IEnumerator.MoveNext%2A>，枚举器都会为此分区提供一个列表元素。 如果是 PLINQ 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A>，分区是 <xref:System.Threading.Tasks.Task> 实例。 由于请求在多个线程上并发，因此对当前索引的访问是同步的。  
  
 [!code-csharp[TPL_Partitioners#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#04)]
 [!code-vb[TPL_Partitioners#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/dynamicpartitioner.vb#04)]  
  
 例如，每个区块包含一个元素的区块分区。 通过一次提供更多元素，可以减少对锁的争用，并（从理论上说）实现更快的性能。 不过，在某个时间点，较大的区块可能需要额外的负载均衡逻辑，才能确保所有线程在全部工作完成前一直处于忙碌状态。  
  
## <a name="see-also"></a>请参阅

- [PLINQ 和 TPL 的自定义分区程序](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)
- [如何：实现静态分区程序](../../../docs/standard/parallel-programming/how-to-implement-a-partitioner-for-static-partitioning.md)
