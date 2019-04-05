---
title: 销毁线程
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- destroying threads
- threading [.NET Framework], destroying threads
ms.assetid: df54e648-c5d1-47c9-bd29-8e4438c1db6d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 93832a296f9b80a5374bc729c04e19d1f178e99f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54502541"
---
# <a name="destroying-threads"></a>销毁线程
<xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 方法用于永久停止托管线程。 调用 <xref:System.Threading.Thread.Abort%2A> 时，公共语言运行时在目标线程中抛出目标线程可以捕获的 <xref:System.Threading.ThreadAbortException>。 有关更多信息，请参见<xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>。  
  
> [!NOTE]
>  如果线程在调用 <xref:System.Threading.Thread.Abort%2A> 方法时执行的是非托管代码，运行时将它标记为 <xref:System.Threading.ThreadState.AbortRequested?displayProperty=nameWithType>。 当线程返回到托管代码时，异常就会抛出。  
  
 一旦线程中止，就无法再重启。  
  
 <xref:System.Threading.Thread.Abort%2A> 方法不会导致线程立即中止，因为目标线程可以捕获 <xref:System.Threading.ThreadAbortException>，并在 `finally` 块中执行任意数量的代码。 如果需要等到线程结束，可以调用 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>。 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> 是阻止调用，除非线程实际已停止执行或可选超时间隔已结束，否则不会返回结果。 由于中止的线程可以调用 <xref:System.Threading.Thread.ResetAbort%2A> 方法或在 `finally` 块中执行无限处理，因此如果不指定超时，就无法保证等到线程结束。  
  
 正在等待调用 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> 方法的线程可能会被调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 的其他线程中断。  
  
## <a name="handling-threadabortexception"></a>处理 ThreadAbortException  
 如果应中止线程，无论是由于在自己的代码中调用 <xref:System.Threading.Thread.Abort%2A> 所致，还是由于卸载正在运行线程的应用域（<xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> 使用 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 终止线程）所致，线程都必须处理 <xref:System.Threading.ThreadAbortException>，并在 `finally` 子句中执行任何最终处理，如下面的代码所示。  
  
```vb  
Try  
    ' Code that is executing when the thread is aborted.  
Catch ex As ThreadAbortException  
    ' Clean-up code can go here.  
    ' If there is no Finally clause, ThreadAbortException is  
    ' re-thrown by the system at the end of the Catch clause.   
Finally  
    ' Clean-up code can go here.  
End Try  
' Do not put clean-up code here, because the exception   
' is rethrown at the end of the Finally clause.  
```  
  
```csharp  
try   
{  
    // Code that is executing when the thread is aborted.  
}   
catch (ThreadAbortException ex)   
{  
    // Clean-up code can go here.  
    // If there is no Finally clause, ThreadAbortException is  
    // re-thrown by the system at the end of the Catch clause.   
}  
// Do not put clean-up code here, because the exception   
// is rethrown at the end of the Finally clause.  
```  
  
 清理代码必须位于 `catch` 子句或 `finally` 子句中，因为系统会在 `finally` 子句末尾或 `catch` 子句（如果没有 `finally` 子句的话）末尾重新抛出 <xref:System.Threading.ThreadAbortException>。  
  
 可以调用 <xref:System.Threading.Thread.ResetAbort%2A?displayProperty=nameWithType> 方法，以防系统重新抛出异常。 不过，只有在自己的代码导致 <xref:System.Threading.ThreadAbortException> 抛出时，才应这样做。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Threading.ThreadAbortException>
- <xref:System.Threading.Thread>
- [使用线程和线程处理](../../../docs/standard/threading/using-threads-and-threading.md)
