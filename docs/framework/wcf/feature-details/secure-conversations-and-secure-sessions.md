---
title: 安全对话和安全会话
ms.date: 03/30/2017
ms.assetid: 48cb104a-532d-40ae-aa57-769dae103fda
ms.openlocfilehash: 6b57f1b9511ef3751fd1f9e5c41d0a0c648972f2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54527895"
---
# <a name="secure-conversations-and-secure-sessions"></a>安全对话和安全会话
Windows Communication Foundation (WCF) 的一项功能是能够建立安全会话之间相互进行身份验证和加密和数字签名过程达成的两个终结点。 例如，服务终结点可能要求客户端终结点发送一个基于 X.509 证书的安全令牌，以便进行身份验证。 在对客户端进行身份验证之后，服务终结点将向客户端返回一个安全上下文令牌 (SCT)，该令牌随后将用于保护该会话中的所有后续消息。 通过建立这一安全会话，可使两个终结点之间交换的一组消息更有效率，因为 SCT 具有对称密钥。 在生成数字签名或加密一组数据时，与对称密钥相比，作为 X.509 证书基础的非对称密钥明显需要更多的计算能力。  
  
 启动策略 (定义中的第 6.2.7 节[Ws-securitypolicy](https://go.microsoft.com/fwlink/?LinkId=99817)标准) 包含用于保护通道，并对 RST/SCT 和 RSTR/SCT 交换之前客户端进行身份验证的消息安全断言。 某些 WCF 标准绑定具有`Security.Message.EstablishSecurityContext`使用哪些控件是否安全对话的属性。 使用自定义绑定时由嵌套安全绑定元素，通过指示 bootstrap [ \<secureConversationBootstrap >](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)配置文件中或通过调用<xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSecureConversationBindingElement%2A>在代码中。  
  
 有关会话的详细信息，请参阅[使用会话的](../../../../docs/framework/wcf/using-sessions.md)。  
  
## <a name="see-also"></a>请参阅
- [会话、实例化和并发](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)
- [如何：创建要求会话的服务](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)
