---
title: Windows Communication Foundation 绑定概述
ms.date: 03/30/2017
helpviewer_keywords:
- bindings [WCF], overview
ms.assetid: cfb5842f-e0f9-4c56-a015-f2b33f258232
ms.openlocfilehash: 7d617400fe5c07e8c9754e322960f31a350f62e5
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54657410"
---
# <a name="windows-communication-foundation-bindings-overview"></a>Windows Communication Foundation 绑定概述
绑定是用来指定所需连接到 Windows Communication Foundation (WCF) 服务的终结点的通信详细信息的对象。 WCF 服务中的每个终结点需要具体指定的绑定。 本主题概述了通信详细信息的绑定所定义的一个绑定，在 WCF 中，包含哪些绑定和如何为终结点指定一个绑定元素的类型。  
  
## <a name="what-a-binding-defines"></a>绑定所定义的内容  
 绑定中的信息可能非常基本，也可能非常复杂。 最基本的绑定仅指定连接终结点所必需的传输协议（如 HTTP）。 一般来说，绑定包含的有关如何连接到终结点的信息属于以下类别中的一种。  
  
 协议  
 确定要使用的安全机制：可靠消息传递功能或事务上下文流设置。  
  
 编码  
 确定消息编码（例如，文本或二进制）。  
  
 传输  
 确定要使用的基础传输协议（例如，TCP 或 HTTP）。  
  
## <a name="the-elements-of-a-binding"></a>绑定的元素  
 绑定基本上由绑定元素的有序堆栈组成，其中每个元素都指定了连接到服务终结点所必需的通信信息的一部分。 该堆栈中最底下的两层都是必需的。 该堆栈的最底层为传输绑定元素，而紧挨着它的上面一层为包含消息编码规范的元素。 用于指定其他通信协议的可选绑定元素位于这两个必需元素的上面。 有关这些绑定元素和及其正确排序的详细信息，请参阅[自定义绑定](../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
## <a name="system-provided-bindings"></a>系统提供的绑定  
 绑定中的信息可能十分复杂，而且某些设置可能与其他设置不兼容。 出于此原因，WCF 包含一组系统提供的绑定。 这些绑定旨在满足大多数应用程序需求。 下面的类表示系统提供的绑定的一些示例：  
  
-   <xref:System.ServiceModel.BasicHttpBinding>：符合 WS 的 HTTP 协议绑定，适用于连接到 Web 服务的基本配置文件规范 (例如，ASP.NET Web 服务基于服务）。  
  
-   <xref:System.ServiceModel.WSHttpBinding>：可互操作绑定，适用于连接到终结点符合 WS-* 协议。  
  
-   <xref:System.ServiceModel.NetNamedPipeBinding>：使用[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]连接到同一台计算机上其他 WCF 终结点。  
  
-   <xref:System.ServiceModel.NetMsmqBinding>：使用[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]来创建与其他 WCF 终结点的已排队的消息连接。  

- <xref:System.ServiceModel.NetTcpBinding>：此绑定提供了更高的性能比 HTTP 绑定，特别适用于本地网络。
  
 有关完整列表，包含的所有提供 WCF 绑定的描述，请参阅[System-Provided Bindings](../../../docs/framework/wcf/system-provided-bindings.md)。  
  
## <a name="using-your-own-bindings"></a>使用自己的绑定  
 如果系统提供的绑定都不具有服务应用程序所需的正确功能组合，则可以创建自己的绑定。 有两种方法可以实现此目的。 你可以使用 <xref:System.ServiceModel.Channels.CustomBinding> 对象从预先存在的绑定元素创建新的绑定，也可以通过从 <xref:System.ServiceModel.Channels.Binding> 绑定派生来创建完全由用户定义的绑定。 有关创建自己的绑定使用这两种方法的详细信息，请参阅[自定义绑定](../../../docs/framework/wcf/extending/custom-bindings.md)并[创建用户定义绑定](../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)。  
  
## <a name="using-bindings"></a>使用绑定  
 使用绑定需要执行两个基本步骤：  
  
1.  选择或定义绑定。 最简单方法是选择 WCF 中包含的系统提供绑定之一并将其用于其默认设置。 您还可以选择一个系统提供的绑定，然后根据您的需求重新设置它的属性值。 或者，您可以创建一个自定义绑定或用户定义的绑定，以实现更高程度的控制和自定义。  
  
2.  创建一个使用所选择或定义的绑定的终结点。  
  
## <a name="code-and-configuration"></a>代码和配置  
 可以通过两种方式来定义绑定：通过代码或通过配置。 这两种方法与您使用的是系统提供的绑定还是自定义绑定无关。 通常，使用代码可以使你在设计时对绑定的定义拥有完全的控制。 但是，使用配置，允许系统管理员或 WCF 服务或客户端能够更改绑定的参数，而无需重新编译服务应用程序的用户。 这种灵活性通常是可取的因为没有方法来预测在其部署 WCF 应用程序的特定计算机需求。 通过将绑定（和寻址）信息保持在代码外部，人们可以更改这些信息，而不必重新编译或重新部署应用程序。 请注意，代码中定义的绑定是在配置中指定的绑定之后创建的，这使得代码定义的绑定可以覆盖配置中定义的任何绑定。  
  
## <a name="see-also"></a>请参阅
- [使用绑定配置服务和客户端](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
