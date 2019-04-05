---
title: 使用线程和线程处理
ms.date: 08/08/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], about threading
- managed threading
ms.assetid: 9b5ec2cd-121b-4d49-b075-222cf26f2344
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 15f3aa8d2cd7c21fa2b77660cd668d211f8376a9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54690613"
---
# <a name="using-threads-and-threading"></a>使用线程和线程处理

借助 .NET，可以编写同时执行多个操作的应用程序。 可在单独的线程上执行可能妨碍其他操作的操作，这些线程是称为多线程处理或自由线程处理的进程。  
  
使用多线程处理的应用程序可以更快地响应用户输入，因为在单独的线程上执行处理器密集型任务时，用户界面将保持活动状态。 创建可扩展的应用程序时，多线程编程也很有用，因为可以随着负载的增加添加线程。

> [!NOTE]
> 如果需要更好地控制应用程序线程的行为，可以自己管理线程。 然而，自 .NET Framework 4 起，由于出现了 <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 类、[并行 LINQ (PLINQ)](../parallel-programming/parallel-linq-plinq.md)、<xref:System.Collections.Concurrent?displayProperty=nameWithType> 命名空间中的新并发集合类以及基于任务（而非线程）概念的新编程模型，多线程编程大大得到了简化。 有关详细信息，请参阅[并行编程](../parallel-programming/index.md)和[任务并行库 (TPL)](../parallel-programming/task-parallel-library-tpl.md)。

## <a name="how-to-create-and-start-a-new-thread"></a>如何：创建并启动新线程

可通过创建 <xref:System.Threading.Thread?displayProperty=nameWithType> 类的新实例，并将要在新线程上执行的方法名提供给构造函数来创建新线程。 要启动已创建的线程，请调用 <xref:System.Threading.Thread.Start%2A?displayProperty=nameWithType> 方法。 有关详细信息和示例，请参阅[启动时创建线程并传递数据](creating-threads-and-passing-data-at-start-time.md)一文和 <xref:System.Threading.Thread> API 引用。

## <a name="how-to-stop-a-thread"></a>如何：停止线程

要终止执行线程，请使用 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 方法。 该方法在调用它的线程上引发 <xref:System.Threading.ThreadAbortException>。 有关详细信息，请参阅[销毁线程](destroying-threads.md)。

从 .NET Framework 4 开始，可使用 <xref:System.Threading.CancellationToken?displayProperty=nameWithType> 以协作方式取消线程。 有关详细信息，请参阅[以协作方式取消线程](canceling-threads-cooperatively.md)。

使用 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> 方法使调用线程等待调用该方法的线程终止。

## <a name="how-to-pause-or-interrupt-a-thread"></a>如何：暂停或中断线程

使用 <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> 方法暂停指定时间内的当前线程。 可通过调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 方法来中断受阻止的线程。 有关详细信息，请参阅[暂停并中断线程](pausing-and-resuming-threads.md)。

## <a name="thread-properties"></a>线程属性

下表列出了某些 <xref:System.Threading.Thread> 属性：  
  
|Property|说明|  
|--------------|-----------|  
|<xref:System.Threading.Thread.IsAlive%2A>|如果此线程已启动但尚未正常终止或中止，则返回 `true`。|  
|<xref:System.Threading.Thread.IsBackground%2A>|获取或设置布尔值，该值指示线程是否为后台线程。 后台线程类似前台线程，但后台线程不会阻止进程停止。 属于某个进程的所有前台线程均停止后，公共语言运行时通过对仍处于活动状态的后台进程调用 <xref:System.Threading.Thread.Abort%2A> 方法来结束进程。 有关详细信息，请参阅[前台和后台线程](foreground-and-background-threads.md)。|  
|<xref:System.Threading.Thread.Name%2A>|获取或设置线程的名称。 最常用于在调试时查找各个线程。|  
|<xref:System.Threading.Thread.Priority%2A>|获取或设置由操作系统用来确定线程计划优先顺序的 <xref:System.Threading.ThreadPriority> 值。 有关详细信息，请参阅[计划线程](scheduling-threads.md)和 <xref:System.Threading.ThreadPriority> 引用。|  
|<xref:System.Threading.Thread.ThreadState%2A>|获取 <xref:System.Threading.ThreadState> 值，该值包含线程的当前状态。|  

## <a name="see-also"></a>请参阅

- <xref:System.Threading.Thread?displayProperty=nameWithType>
- [线程与线程处理](threads-and-threading.md)
- [并行编程](../parallel-programming/index.md)
