---
title: 联合与信任
ms.date: 03/30/2017
helpviewer_keywords:
- federation [WCF], and trust
ms.assetid: 4bdec4f2-f8a2-4512-bdcf-14ef54b5877a
ms.openlocfilehash: 1f0872c9aea11a54860fe3075d2756691590e0d4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54532417"
---
# <a name="federation-and-trust"></a>联合与信任
本主题介绍与联合应用程序、 信任边界和配置，并使用已颁发的令牌中 Windows Communication Foundation (WCF) 的各个方面。  
  
## <a name="services-security-token-services-and-trust"></a>服务、安全令牌服务和信任  
 公开联合终结点的服务通常期望客户端使用特定颁发机构提供的令牌进行身份验证。 使用颁发机构的正确凭据来配置服务很重要；否则，将无法通过颁发的令牌来验证签名，客户端也将无法与服务通信。 有关在服务上配置颁发机构凭据的详细信息，请参阅[如何：联合身份验证服务上配置凭据](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)。  
  
 同样，使用对称密钥时，密钥是针对目标服务加密的，因此，必须使用目标服务的正确凭据来配置安全令牌服务；否则，将无法针对目标服务加密密钥，客户端也将无法与服务通信。  
  
 WCF 服务使用的值<xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxClockSkew%2A>上的属性[SecurityBindingElement](../../../../docs/framework/wcf/diagnostics/wmi/securitybindingelement.md)允许的时钟偏差的客户端和服务之间。 在联合中，`MaxClockSkew` 设置应用于客户端与客户端从中获得颁发的令牌的安全令牌服务之间的时钟偏差。 因此，在设置颁发的令牌的有效时间和过期时间时，安全令牌服务不需要进行时钟偏差许可。  
  
> [!NOTE]
>  时钟偏差的重要性随颁发的令牌的生存期的缩短而增加。 在大多数情况下，如果令牌生存期为 30 分钟或更长，则时钟偏差不是一个重要问题。 如果生存期更短或令牌的确切有效时间非常重要，则在设计时应考虑时钟偏差。  
  
## <a name="federated-endpoints-and-time-outs"></a>联合终结点和超时  
 客户端与联合终结点通信时，必须首先从安全令牌服务处获取适当的令牌。 如果安全令牌服务公开一个联合终结点，则客户端必须首先从该终结点的颁发机构处获得令牌。 每次获得令牌都需要时间，而时间取决于向最终终结点发送实际消息的整体超时。  
  
 例如，客户端通道的超时值设置为 30 秒。 在向最终终结点发送消息之前，需要调用两个令牌颁发机构来检索令牌，因此，每个颁发机构有 15 秒钟来颁发令牌。 这种情况下，尝试将失败，并引发 <xref:System.TimeoutException>。 因此，需要将客户端通道的 <xref:System.ServiceModel.IContextChannel.OperationTimeout%2A> 值设置为一个足够大的值，以便有时间检索所有颁发的令牌。 如果没有为 <xref:System.ServiceModel.IContextChannel.OperationTimeout%2A> 属性指定一个值，则需要将 <xref:System.ServiceModel.Channels.Binding.OpenTimeout%2A> 属性和/或 <xref:System.ServiceModel.Channels.Binding.SendTimeout%2A> 属性设置为一个足够大的值，以便有时间检索所有颁发的令牌。  
  
## <a name="token-lifetime-and-renewal"></a>令牌生存期和续订  
 向服务发出初始请求时，WCF 客户端不会检查已颁发的令牌。  相反，WCF 信任安全令牌服务颁发的令牌具有适当有效时间和过期时间。 如果客户端缓存并重用令牌，则会在后续请求时检查令牌生存期，如有必要，客户端会自动续订令牌。 有关令牌缓存的详细信息，请参阅[如何：创建联合客户端](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)。  
  
 对于颁发的令牌或安全上下文令牌的操作，可能会导致协商超时或其他 WCF 客户端请求已颁发的令牌时引发的异常或协商或续订安全时指定短生命周期，约为 30 秒或更少上下文令牌。  
  
## <a name="issued-tokens-and-inclusionmode"></a>颁发的令牌和 InclusionMode  
 在从客户端发送到联合终结点的消息中，是否对颁发的令牌进行序列化，是由 <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.InclusionMode%2A> 类的 <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters> 属性的设置控制的。 此属性可以设置为 <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode> 枚举值之一，但它在大多数联合方案中并无用处。 如果是 `SecurityTokenInclusionMode.Never` 和 `SecurityTokenInclusionMode.AlwaysToInitiator` 值，客户端会向安全令牌服务颁发给依赖方的令牌发送一个引用。 除非依赖方拥有颁发的令牌的副本，否则会因令牌引用不可解析而导致身份验证失败。 WCF 将视为`SecurityTokenInclusionMode.Once`视为等效于`SecurityTokenInclusionMode.AlwaysToRecipient`。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode>
- [如何：创建联合客户端](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)
- [如何：联合身份验证服务上配置凭据](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
- [如何：创建 WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)
