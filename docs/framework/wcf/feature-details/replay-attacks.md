---
title: 重播攻击
ms.date: 03/30/2017
ms.assetid: 7a17e040-93cd-4432-81b9-9f62fec78c8f
ms.openlocfilehash: bceaa1bb723144ee4e3b534aa1537acdc7f65fc3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54712072"
---
# <a name="replay-attacks"></a>重播攻击
一个*重播攻击*攻击者复制双方之间的消息流，并重播到一个或多个参与方的流时，会发生。 除非攻击得到缓解，否则，受到攻击的计算机会将该消息流作为合法消息进行处理，从而导致一系列不良后果，例如重复订购某种产品。  
  
## <a name="bindings-may-be-subject-to-reflection-attacks"></a>绑定可能会遭受反射攻击  
 *反射攻击*像它们来自接收方的答复一样进行重播回发送方的消息。 标准*重播检测*中 Windows Communication Foundation (WCF) 机制不会自动处理这。  
  
 因为 WCF 服务模型将已签名的消息 ID 添加到请求消息，并期望有符号的反射攻击会得到缓解默认情况下`relates-to`对响应消息的标头。 因此，请求消息无法作为响应进行重播。 在安全的可靠消息 (RM) 方案中，反射攻击会由于以下原因而得到缓解：  
  
-   创建序列架构和创建序列响应消息架构是不同的。  
  
-   对于单工序列，无法将客户端发送的序列消息重播回客户端，因为客户端无法理解这样的消息。  
  
-   对于双工序列，这两个序列 ID 必须是唯一的。 因此，无法将传出序列消息作为传入序列消息重播回发送方（所有序列标头和正文也都进行了签名）。  
  
 唯一容易遭受反射攻击的绑定是那些不使用 WS-Addressing 的绑定，即那些禁用了 WS-Addressing 的自定义绑定以及那些使用基于对称密钥的安全的绑定。 默认情况下，<xref:System.ServiceModel.BasicHttpBinding> 不使用 WS-Addressing，但是它不会以使其容易遭受反射攻击的方式使用基于对称密钥的安全。  
  
 自定义绑定的缓解是不建立安全上下文或要求使用 WS-Addressing 标头。  
  
## <a name="web-farm-attacker-replays-request-to-multiple-nodes"></a>Web 场：攻击者到多个节点重播请求  
 客户端使用在网络场中实现的服务。 攻击者将发送到网络场中某个节点的请求重播到该网络场中的其他节点。 另外，如果重新启动服务，则会刷新重播缓存，从而使攻击者可以重播请求。 （该缓存包含已使用过的、先前已见到的消息签名值并可以防止重播，因此这些签名只能使用一次。 重播缓存不在整个网络场中共享。）  
  
 缓解措施包括：  
  
-   将消息模式安全与有状态安全上下文令牌结合使用（启用或不启用安全对话）。 有关详细信息，请参阅[如何：创建安全上下文令牌的安全会话](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)。  
  
-   将服务配置为使用传输级安全。  
  
## <a name="see-also"></a>请参阅
- [安全注意事项](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)
- [信息泄漏](../../../../docs/framework/wcf/feature-details/information-disclosure.md)
- [特权提升](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)
- [拒绝服务](../../../../docs/framework/wcf/feature-details/denial-of-service.md)
- [篡改](../../../../docs/framework/wcf/feature-details/tampering.md)
- [不支持的方案](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
