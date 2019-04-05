---
title: 托管线程处理基本知识
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- multiple threads
- threading [.NET Framework], multiple threads
- threading [.NET Framework], about threading
- managed threading
ms.assetid: b2944911-0e8f-427d-a8bb-077550618935
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e053a04ba0587a4eca166fa710bc465094feca80
ms.sourcegitcommit: dcc8feeff4718664087747529638ec9b47e65234
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "55479563"
---
# <a name="managed-threading-basics"></a>托管线程处理基本知识

本节的前五个主题有助于确定何时使用托管线程处理，并介绍一些基本功能。 若要了解提供附加功能的类，请参阅[线程处理对象和功能](../../../docs/standard/threading/threading-objects-and-features.md)和[同步基元概述](../../../docs/standard/threading/overview-of-synchronization-primitives.md)。  
  
 本节中的剩余主题涵盖了高级主题，其中包括托管线程与 Windows 操作系统的交互。  
  
> [!NOTE]
>  在 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中，任务并行库和 PLINQ 提供了多线程程序中的任务并行和数据并行 API。 有关详细信息，请参阅[并行编程](../../../docs/standard/parallel-programming/index.md)。  
  
## <a name="in-this-section"></a>本节内容

 [线程与线程处理](../../../docs/standard/threading/threads-and-threading.md)  
 介绍了多个线程的优缺点，并概述了可能创建线程或使用线程池线程的方案。  
  
 [托管线程中的异常](../../../docs/standard/threading/exceptions-in-managed-threads.md)  
 介绍了对于不同版本的 .NET Framework，线程中未经处理的异常行为，特别是导致应用终止的情况。  
  
 [为多线程处理同步数据](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)  
 介绍了在用于多个线程的类中同步数据的策略。  
  
 [前台和后台线程](../../../docs/standard/threading/foreground-and-background-threads.md)  
 介绍了前台和后台线程的区别。  
  
 [Windows 中的托管和非托管线程](../../../docs/standard/threading/managed-and-unmanaged-threading-in-windows.md)  
 介绍了托管和非托管线程的关系，列出了 Windows 线程 API 的相当托管版本，并讨论了 COM 单元和托管线程的交互。  
  
 [Thread.Suspend、垃圾回收和安全点](../../../docs/standard/threading/thread-suspend-garbage-collection-and-safe-points.md)  
 介绍了线程暂停和垃圾回收。  
  
 [线程本地存储：线程相关的静态字段和数据槽](../../../docs/standard/threading/thread-local-storage-thread-relative-static-fields-and-data-slots.md)  
 介绍了线程相对存储机制。  
  
 [托管线程中的取消](../../../docs/standard/threading/cancellation-in-managed-threads.md)  
 介绍了如何使用取消令牌取消异步操作或长时间运行的同步操作。  
  
## <a name="reference"></a>参考

 <xref:System.Threading.Thread>  
 提供**线程**类的参考文档，无论该类是来自托管代码还是在托管应用程序中创建的，它都表示一个托管线程。  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 提供了一种安全实现多线程处理与用户界面对象的方式。  
  
## <a name="related-sections"></a>相关章节

 [同步基元概述](../../../docs/standard/threading/overview-of-synchronization-primitives.md)  
 介绍了用于同步多个线程活动的托管类。  
  
 [托管线程处理的最佳做法](../../../docs/standard/threading/managed-threading-best-practices.md)  
 介绍了常见的多线程处理问题，以及避免这些问题发生的策略。  
  
 [并行编程](../../../docs/standard/parallel-programming/index.md)  
 介绍了任务并行库和 PLINQ，它们极大地简化了创建异步和多线程 .NET Framework 应用的工作。
