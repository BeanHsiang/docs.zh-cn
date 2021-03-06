---
title: 如何：取消任务及其子级
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to cancel
ms.assetid: 08574301-8331-4719-ad50-9cf7f6ff3048
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ed3129364d73d196b2e25b962b8c42325a144dfd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54642826"
---
# <a name="how-to-cancel-a-task-and-its-children"></a>如何：取消任务及其子级
这些示例展示了如何执行下列任务：  
  
1.  创建并启动可取消任务。  
  
2.  将取消令牌传递给用户委托，并视需要传递给任务实例。  
  
3.  注意并响应用户委托中的取消请求。  
  
4.  （可选）注意已取消任务的调用线程。  
  
 调用线程不会强制结束任务，只会提示取消请求已发出。 如果任务已在运行，至于怎样才能注意请求并适当响应，取决于用户委托的选择。 如果取消请求在任务运行前发出，用户委托绝不会执行，任务对象的状态会转换为“已取消”。  
  
## <a name="example"></a>示例  
 此示例展示了如何终止 <xref:System.Threading.Tasks.Task> 及其子级，以响应取消请求。 还会演示，当用户委托通过引发 <xref:System.Threading.Tasks.TaskCanceledException> 终止时，调用线程可以选择使用 <xref:System.Threading.Tasks.Task.Wait%2A> 方法或 <xref:System.Threading.Tasks.Task.WaitAll%2A> 方法来等待任务完成。 在这种情况下，必须使用 `try/catch` 块来处理调用线程上的异常。  
  
 [!code-csharp[TPL_Cancellation#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cancellation/cs/cancel1.cs#04)]
 [!code-vb[TPL_Cancellation#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cancellation/vb/cancel1.vb#04)]  
  
 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 类与基于 <xref:System.Threading.CancellationTokenSource?displayProperty=nameWithType> 和 <xref:System.Threading.CancellationToken?displayProperty=nameWithType> 类型的取消模型完全集成。 有关详细信息，请参阅[托管线程中的取消](../../../docs/standard/threading/cancellation-in-managed-threads.md)和[任务取消](../../../docs/standard/parallel-programming/task-cancellation.md)。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Threading.CancellationTokenSource?displayProperty=nameWithType>
- <xref:System.Threading.CancellationToken?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>
- [基于任务的异步编程](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)
- [附加和分离的子任务](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)
- [PLINQ 和 TPL 中的 Lambda 表达式](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)
