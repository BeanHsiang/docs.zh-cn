---
title: 中间层客户端应用程序
ms.date: 03/30/2017
ms.assetid: f9714a64-d0ae-4a98-bca0-5d370fdbd631
ms.openlocfilehash: 457a215274c4804ac38958d8f840e8f4100a7be0
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54718892"
---
# <a name="middle-tier-client-applications"></a>中间层客户端应用程序
本主题讨论特定于使用 Windows Communication Foundation (WCF) 的中间层客户端应用程序的各种问题。  
  
## <a name="increasing-middle-tier-client-performance"></a>提高中间层客户端应用程序的性能  
 与以前的通信技术，例如使用 Web 服务相比[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]，WCF 客户端实例的创建可能会由于 WCF 的丰富功能集更复杂。 例如，打开 <xref:System.ServiceModel.ChannelFactory%601> 对象时，该对象会与服务建立一个安全会话，该过程将增加客户端实例的启动时间。 通常情况下，这些附加功能不会影响客户端应用程序极大地因为 WCF 客户端进行多次调用，然后关闭。  
  
 中间层客户端应用程序，但是，可以快速创建多个 WCF 客户端对象并，因此，实现提高的初始化需求。 调用服务时，有两种主要的方法可以提高中间层应用程序的性能：  
  
-   缓存的 WCF 客户端对象并将其重复用于后续调用在可能的情况。  
  
-   创建<xref:System.ServiceModel.ChannelFactory%601>对象，然后使用该对象来创建新的 WCF 客户端通道对象为每个调用。  
  
 使用这些方法时要考虑的问题包括：  
  
-   如果服务通过使用会话维护特定于客户端的状态，则不能因为服务的状态与中间层客户端的重用中间层 WCF 客户端具有多个客户端层的请求。  
  
-   如果该服务必须在每个客户端的基础上进行身份验证，则必须创建每个传入请求的新客户端而不是重用中间层 WCF 客户端 （或 WCF 客户端通道对象），因为在中间层上的中间层客户端凭据不能修改在 WCF 客户端后 (或<xref:System.ServiceModel.ChannelFactory%601>) 已创建。  
  
-   由于通道及其创建的客户端是线程安全的，因此它们可能不支持同时向网络中写入多条消息。 如果要发送较大的消息，特别是消息流，则发送操作可能会阻塞，因为它要等待另一个发送操作完成。 这会导致两种问题：缺少并发性；当控制流返回到重用信道的服务（即，共享的客户端调用了一种服务，该服务的代码路径会导致对共享的客户端进行回调）时，存在死锁的可能性。 这是你重复使用的 WCF 客户端的类型无关，则返回 true。  
  
-   无论您是否共享出错的通道，您都必须处理它。 然而，重用通道时，出错通道可以关闭多个挂起的请求或发送。  
  
 有关演示如何重用多个请求的客户端的最佳实践示例，请参阅[ASP.NET 客户端中的数据绑定](../../../../docs/framework/wcf/samples/data-binding-in-an-aspnet-client.md)。  
  
 此外，如果客户端使用可用 <xref:System.Xml.Serialization.XmlSerializer> 进行序列化的数据类型，则会在运行时生成并编译这些数据类型的序列化代码，从而导致启动性能降低；但你可以提高那些客户端的启动性能。 [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)可以通过从应用程序的已编译程序集生成必要的序列化代码提高这些应用程序的启动性能。 有关详细信息，请参阅[如何：改善启动时间的 WCF 客户端应用程序的使用 XmlSerializer](../../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)。  
  
## <a name="see-also"></a>请参阅
- [使用 WCF 客户端访问服务](../../../../docs/framework/wcf/feature-details/accessing-services-using-a-client.md)
