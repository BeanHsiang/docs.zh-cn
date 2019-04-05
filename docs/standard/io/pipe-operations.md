---
title: .NET Framework 中的管道操作
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- pipes [.NET Framework]
- pipe operations [.NET Framework]
- interprocess communication [.NET Framework], pipes
- I/O [.NET Framework], pipes
ms.assetid: 7b964ebd-7a4f-4d28-8194-7841f9e4c702
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 919d4606e4ba72f07ba382244f8508975beffec9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54741228"
---
# <a name="pipe-operations-in-the-net-framework"></a>.NET Framework 中的管道操作
管道为进程间通信提供了平台。 管道分为两种类型：  
  
-   匿名管道。  
  
     匿名管道在本地计算机上提供进程间通信。 与命名管道相比，虽然匿名管道需要的开销更少，但提供的服务有限。 匿名管道是单向的，不能通过网络使用。 仅支持一个服务器实例。 匿名管道可用于线程间通信，也可用于父进程和子进程之间的通信，因为管道句柄可以轻松传递给所创建的子进程。  
  
     在 .NET Framework 中，可通过使用 <xref:System.IO.Pipes.AnonymousPipeServerStream> 和 <xref:System.IO.Pipes.AnonymousPipeClientStream> 类来实现匿名管道。  
  
     请参阅[如何：使用匿名管道进行本地进程间通信](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)。  
  
-   命名管道。  
  
     命名管道在管道服务器和一个或多个管道客户端之间提供进程间通信。 命名管道可以是单向的，也可以是双向的。 它们支持基于消息的通信，并允许多个客户端使用相同的管道名称同时连接到服务器进程。 命名管道还支持模拟，这样连接进程就可以在远程服务器上使用自己的权限。  
  
     在 .NET Framework 中，可通过使用 <xref:System.IO.Pipes.NamedPipeServerStream> 和 <xref:System.IO.Pipes.NamedPipeClientStream> 类来实现命名管道。  
  
     请参阅[如何：使用命名管道进行网络进程间通信](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)。  
  
## <a name="see-also"></a>请参阅

- [文件和流 I/O](../../../docs/standard/io/index.md)
- [如何：使用匿名管道进行本地进程间通信](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)
- [如何：使用命名管道进行网络进程间通信](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)
