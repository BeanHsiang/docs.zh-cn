---
title: 开发通道
ms.date: 03/30/2017
ms.assetid: 0513af9f-a0c2-457b-9a50-5b6bfee48513
ms.openlocfilehash: 74a54972ffa7d00d702a2339665d18acdcbf93ef
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54519133"
---
# <a name="developing-channels"></a>开发通道
若要开发使用 Windows Communication Foundation (WCF) 可以使用的协议或传输通道应用程序层需要几个步骤。 本主题介绍这些步骤并为您指出特定主题以了解更多信息。 若要了解通道模型和本主题中提到的各种类型，请参阅[通道模型概述](../../../../docs/framework/wcf/extending/channel-model-overview.md)。 有关完整的传输通道示例，请参阅[传输：UDP](../../../../docs/framework/wcf/samples/transport-udp.md)。  
  
## <a name="the-channel-development-task-list"></a>通道开发任务列表  
 创建用户定义的通道的步骤如下所示： 所有通道必须：  
  
1.  确定您的 <xref:System.ServiceModel.Channels.IOutputChannel> 和 <xref:System.ServiceModel.Channels.IInputChannel> 将支持哪种通道消息交换模式（<xref:System.ServiceModel.Channels.IDuplexChannel>、<xref:System.ServiceModel.Channels.IRequestChannel>、<xref:System.ServiceModel.Channels.IReplyChannel>、<xref:System.ServiceModel.Channels.IChannelFactory> 或 <xref:System.ServiceModel.Channels.IChannelListener>），以及该模式是否支持这些接口的会话变体。 有关详细信息，请参阅[选择消息交换模式](../../../../docs/framework/wcf/extending/choosing-a-message-exchange-pattern.md)。  
  
2.  创建支持您的消息交换模式的通道工厂和侦听器（<xref:System.ServiceModel.Channels.IChannelFactory> 和 <xref:System.ServiceModel.Channels.IChannelListener>）。 有关开发工厂的详细信息，请参阅[客户端：通道工厂和通道](../../../../docs/framework/wcf/extending/client-channel-factories-and-channels.md)。 有关开发侦听器的详细信息，请参阅[服务：通道侦听器和通道](../../../../docs/framework/wcf/extending/service-channel-listeners-and-channels.md)。  
  
3.  确保将任何特定于网络的异常规范化为 <xref:System.TimeoutException?displayProperty=nameWithType> 或 <xref:System.ServiceModel.CommunicationException> 的相应派生类。 有关详细信息，请参阅[处理异常和错误](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md)。  
  
4.  若要从应用程序层使用通道，请添加一个可将自定义通道添加到通道堆栈的 <xref:System.ServiceModel.Channels.BindingElement>。 有关详细信息，请参阅[创建 BindingElement](../../../../docs/framework/wcf/extending/creating-a-bindingelement.md)。  
  
 要在应用程序层启用更完全的支持，需要执行以下附加步骤：  
  
1.  添加一个绑定元素扩展部分，以便将新的绑定元素公开到配置系统。 有关详细信息，请参阅[配置和元数据支持](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)。  
  
2.  添加元数据扩展以将各种功能传递给其他终结点。 有关详细信息，请参阅[配置和元数据支持](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)。  
  
3.  添加一个绑定，该绑定根据定义完善的配置文件来预配置绑定元素堆栈。 有关详细信息，请参阅[创建用户定义绑定](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)。  
  
4.  添加一个绑定部分和绑定配置元素，以便将该绑定公开到配置系统。 有关详细信息，请参阅[配置和元数据支持](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)。  
  
## <a name="see-also"></a>请参阅
- [扩展绑定](../../../../docs/framework/wcf/extending/extending-bindings.md)
