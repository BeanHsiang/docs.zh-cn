---
title: 计划线程
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], scheduling
- scheduling threads
ms.assetid: 67e4a0eb-3095-4ea7-b20f-908faa476277
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 502e118a67e157ce7756efdece866564fddc6ab7
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54611483"
---
# <a name="scheduling-threads"></a>计划线程

每个线程都会分配有线程优先级。 在公共语言运行时内创建的线程初始分配有 <xref:System.Threading.ThreadPriority.Normal?displayProperty=nameWithType> 的优先级。 在运行时外部创建的线程保留有在进入托管环境前的优先级。 若要获取或设置任意线程的优先级，可以使用 <xref:System.Threading.Thread.Priority?displayProperty=nameWithType> 属性。  
  
 线程根据优先级被排入执行计划。 即使线程是在运行时内执行，操作系统也会为所有线程分配处理器时间片。 用于确定线程执行顺序的计划算法详细信息因各个操作系统而异。 在一些操作系统下，（在可以执行的线程中）优先级最高的线程始终都被计划为第一个运行。 如果有多个线程的优先级相同，计划程序会遍历具有此优先级的全部线程，为每个线程分配固定的执行时间片。 只要有更高优先级的线程可供运行，就不会执行优先级较低的线程。 如果在给定优先级没有其他任何可运行的线程，计划程序会转到下一个较低优先级，并计划执行具有此优先级的线程。 如果较高优先级的线程变得可运行，就会强占优先级较低的线程，并获准重新执行。 除此之外，如果应用的用户界面在前台和后台之间转换，操作系统还可以动态调整线程优先级。 其他操作系统可能会选择使用不同的计划算法。  
  
## <a name="see-also"></a>请参阅

- [使用线程和线程处理](../../../docs/standard/threading/using-threads-and-threading.md)
- [Windows 中的托管和非托管线程](../../../docs/standard/threading/managed-and-unmanaged-threading-in-windows.md)
