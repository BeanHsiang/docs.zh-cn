---
title: 单并发模式中的有序消息处理
ms.date: 03/30/2017
ms.assetid: a90f5662-a796-46cd-ae33-30a4072838af
ms.openlocfilehash: c9f2460a1def19212d3ba866b0b443830e9b69bb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54745840"
---
# <a name="ordered-processing-of-messages-in-single-concurrency-mode"></a>单并发模式中的有序消息处理
WCF 使消息被处理的顺序提供任何保证，除非基础通道是会话。  例如，使用 MsmqInputChannel 不是会话通道的 WCF 服务将无法按顺序处理消息。 有某些情况下，其中一名开发人员可能希望在订单处理行为，但不是希望使用会话。 本主题介绍在单一并发模式中运行服务时，如何配置这种行为。  
  
## <a name="in-order-message-processing"></a>有序消息处理  
 名为 <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A> 的新特性已添加到 <xref:System.ServiceModel.ServiceBehaviorAttribute>。 当 <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A> 设置为 true 并且<xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> 设置为 <xref:System.ServiceModel.ConcurrencyMode.Single> 时，将按顺序处理发送到服务的消息。 下面的代码段演示如何设置这些特性。  
  
```  
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single, EnsureOrderedDispatch = true )]  
    class Service : IService  
    {  
         // ...  
    }  
```  
  
 如果 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> 设置为任何其他值，则引发 <xref:System.InvalidOperationException>。  
  
## <a name="see-also"></a>请参阅
- [会话、实例化和并发](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)
- [并发](../../../../docs/framework/wcf/samples/concurrency.md)
