---
title: 路由协定
ms.date: 03/30/2017
ms.assetid: 9ceea7ae-ea19-4cf9-ba4f-d071e236546d
ms.openlocfilehash: 593c7a328aba82c35f5876e6e325844c829c08c7
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54707708"
---
# <a name="routing-contracts"></a>路由协定
路由协定定义路由服务可处理的消息模式。  每个协定都是无类型协定，允许服务在不了解消息架构或操作的情况下接收消息。 这样，路由服务就可以按照通常方式来路由消息，而不必对路由的基础消息的细节进行额外配置。  
  
## <a name="routing-contracts"></a>路由协定  
 由于路由服务接受泛型 WCF 消息对象，因此，在选择协定时，首先需要考虑与客户端和服务通信时将采用的通道的形状。 路由服务在处理消息时使用对称消息泵，因此，入站协定的形状通常必须与出站协定的形状匹配。 但是，一些情况下，服务模型调度程序可以修改形状，例如当调度程序的双工通道转换为请求-答复通道，或当它不是必需的和未使用 （也就是说，从通道删除会话支持当**SessionMode.Allowed**转换**IInputSessionChannel**到**IInputChannel**)。  
  
 为了支持这些消息泵，路由服务在 <xref:System.ServiceModel.Routing> 命名空间中提供了一些协定，当定义路由服务使用的服务终结点时，必须使用这些协定。 这些协定都是无类型协定，允许接收任何消息类型或操作，并允许路由服务在不了解特定消息架构的情况下处理消息。 有关路由服务使用的约定的详细信息，请参阅[路由协定](../../../../docs/framework/wcf/feature-details/routing-contracts.md)。  
  
 路由服务提供的协定位于 <xref:System.ServiceModel.Routing> 命名空间中，下表对这些协定进行了说明。  
  
|协定|形状|通道形状|  
|--------------|-----------|-------------------|  
|<xref:System.ServiceModel.Routing.ISimplexDatagramRouter>|SessionMode = SessionMode.Allowed<br /><br /> AsyncPattern = true<br /><br /> IsOneWay = true|IInputChannel -> IOutputChannel|  
|<xref:System.ServiceModel.Routing.ISimplexSessionRouter>|SessionMode = SessionMode.Required<br /><br /> AsyncPattern = true<br /><br /> IsOneWay = true|IInputSessionChannel -> IOutputSessionChannel|  
|<xref:System.ServiceModel.Routing.IRequestReplyRouter>|SessionMode = SessionMode.Allowed<br /><br /> AsyncPattern = true|IReplyChannel -> IRequestChannel|  
|<xref:System.ServiceModel.Routing.IDuplexSessionRouter>|SessionMode=SessionMode.Required<br /><br /> CallbackContract=typeof(ISimplexSession)<br /><br /> AsyncPattern = true<br /><br /> IsOneWay = true<br /><br /> TransactionFlow(TransactionFlowOption.Allowed)|IDuplexSessionChannel -> IDuplexSessionChannel|  
  
## <a name="see-also"></a>请参阅
- [路由服务](../../../../docs/framework/wcf/feature-details/routing-service.md)
- [路由简介](../../../../docs/framework/wcf/feature-details/routing-introduction.md)
