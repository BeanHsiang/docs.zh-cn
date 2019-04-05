---
title: 自定义消息格式化程序
ms.date: 03/30/2017
ms.assetid: c07435f3-5214-4791-8961-2c2b61306d71
ms.openlocfilehash: e1633bdd3959ba812251ef1b78bcd0e83b2060c6
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54612758"
---
# <a name="custom-message-formatters"></a>自定义消息格式化程序
消息内容通常为 XML 格式，该格式通常不便于在应用程序中使用。 应用程序操作对象，并且获取和设置其属性。 Windows Communication Foundation (WCF) 使用*数据协定*转换<xref:System.ServiceModel.Channels.Message>轻松地处理应用程序的对象的对象。 我们将这些过程称为序列化和反序列化。 请注意，这些词同样用于描述传输层对消息连网格式所进行的序列化和反序列化，这是一个不相关的过程。  
  
 如果需要实现通过数据协定无法完成的消息和对象之间的专用转换，则可以使用自定义消息格式化程序。 方法是修改或扩展客户端或服务上的特定协定操作的执行行为。  
  
## <a name="custom-message-formatters-on-the-client"></a>自定义客户端上的消息格式化程序  
 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 接口定义用于控制客户端应用程序的消息与对象之间的转换方法。  
  
 您必须实现此接口。 首先重写 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%2A> 方法以反序列化消息。 在接收传入消息后，将消息调度到客户端操作之前调用此方法。  
  
 然后，重写 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%2A> 方法以序列化对象。 在发送传出消息前调用此方法。  
  
 若要将自定义格式化程序插入服务应用程序，请使用操作行为将 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 对象分配给 <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> 属性。 有关行为的信息，请参阅[配置和扩展的运行时行为带有](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## <a name="custom-message-formatters-on-the-service"></a>自定义服务上的消息格式化程序  
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> 接口定义将服务应用程序中的 <xref:System.ServiceModel.Channels.Message> 对象转换为操作参数并将参数转换为 <xref:System.ServiceModel.Channels.Message> 对象的方法。  
  
 您必须实现此接口。 首先重写 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%2A> 方法以反序列化消息。 在接收传入消息后，将消息调度到客户端操作之前调用此方法。  
  
 然后，重写 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%2A> 方法以序列化对象。 在发送传出消息前调用此方法。  
  
 若要将自定义格式化程序插入服务应用程序，请使用操作行为将 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> 对象分配给 <xref:System.ServiceModel.Dispatcher.DispatchOperation.Formatter%2A> 属性。 有关行为的信息，请参阅[配置和扩展的运行时行为带有](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>
- <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>
- [使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)
