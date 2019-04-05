---
title: System.ServiceModel.Channels.MsmqMessageRejected
ms.date: 03/30/2017
ms.assetid: 9b7c10a7-2af6-44a2-8b1a-90bba0c7cf26
ms.openlocfilehash: 87d6e6fc3205fff9bd977ebe77004dfa489098cb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54681217"
---
# <a name="systemservicemodelchannelsmsmqmessagerejected"></a>System.ServiceModel.Channels.MsmqMessageRejected
MSMQ 已拒绝该消息。  
  
## <a name="description"></a>描述  
 此跟踪指示已拒绝 MSMQ 消息。  
  
 当 Windows Communication Foundation (WCF) （与 NetMsmqBinding 或 MsmqIntegrationBinding 一起使用） 无法处理它们时，可以拒绝 MSMQ 消息。 这些消息称为病毒消息。 当 NetMsmqBinding 或 MsmqIntegrationBinding 上的 `ReceiveErrorHandling` 属性设置为 `Reject` 时，将拒绝病毒消息。 将被拒绝的消息传递回发件人[死信队列](https://go.microsoft.com/fwlink/?LinkID=99544)。  
  
 请参阅[病毒消息处理](https://go.microsoft.com/fwlink/?LinkID=99546)有关消息何时成为病毒和如何将服务配置为适当地处理更多详细信息。  
  
 请参阅[MQMarkMessageRejected](https://go.microsoft.com/fwlink/?LinkID=99548)有关被拒绝的消息在 MSMQ 中的含义的详细信息。  
  
## <a name="see-also"></a>请参阅
- [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)
- [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)
- [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)
- [病毒消息处理](https://go.microsoft.com/fwlink/?LinkID=99546)
- [MQMarkMessageRejected](https://go.microsoft.com/fwlink/?LinkID=99548)
