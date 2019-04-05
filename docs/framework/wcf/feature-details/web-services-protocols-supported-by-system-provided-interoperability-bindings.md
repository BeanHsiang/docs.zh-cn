---
title: 系统提供的互操作性绑定支持的 Web 服务协议
ms.date: 03/30/2017
helpviewer_keywords:
- WS-protocols
- Web services protocols
- Windows Communication Foundation, Web service protocols
ms.assetid: 1f7fc4ff-30fe-4e46-adda-91caad3b06c6
ms.openlocfilehash: 0aa75fe4812553ecbf00542da37f232aca32c1a0
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54606616"
---
# <a name="web-services-protocols-supported-by-system-provided-interoperability-bindings"></a>系统提供的互操作性绑定支持的 Web 服务协议
Windows Communication Foundation (WCF) 构建与支持的一组称为 Web 服务规范的规范的 Web 服务进行互操作。 为了简化互操作性最佳实践的服务配置，WCF，引入了三个可互操作的系统提供绑定： <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType>， <xref:System.ServiceModel.WSHttpBinding?displayProperty=nameWithType>，和<xref:System.ServiceModel.WSDualHttpBinding?displayProperty=nameWithType>。 WCF 的互操作性与组织的进步的结构化信息标准 (OASIS) 标准，包括一个可互操作的系统提供绑定： <xref:System.ServiceModel.WS2007HttpBinding?displayProperty=nameWithType>。 对于元数据发布的 WCF 包含两个可互操作的系统提供绑定： [ \<mexHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpbinding.md)并[ \<mexHttpsBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpsbinding.md)。 本主题列出系统提供的可互操作绑定支持的规范。  
  
## <a name="web-services-protocols-supported-by-basichttpbinding-wshttpbinding-ws2007httpbinding-and-wsdualhttpbinding-bindings"></a>basicHttpBinding、wsHttpBinding、ws2007HttpBinding 和 wsDualHttpBinding 绑定支持的 Web 服务协议  
  
### <a name="all-bindings"></a>所有绑定  
 [ \<BasicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)， [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)，以及[ \<ws2007HttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)绑定支持以下协议。  
  
> [!NOTE]
>  有关用于发布元数据的绑定的信息，请参见本主题后面的“系统提供的元数据绑定”一节。  
  
|类别|协议|规范和用法|  
|--------------|--------------|-----------------------------|  
|传输|HTTP 1.1|[HTTP 1.1](https://go.microsoft.com/fwlink/?LinkId=84048)<br /><br /> `BasicHttpBinding`、`WSHttpBinding` 和 `WS2007HttpBinding` 使用 HTTP 和 HTTPS 传输。|  
|消息|MTOM|[MTOM](https://go.microsoft.com/fwlink/?LinkId=95326)<br /><br /> `basicHttpBinding`、`wsHttpBinding` 和 `ws2007HttpBinding` 支持消息传输优化机制 (MTOM)。 默认情况下不使用。 若要使用 MTOM，请将 `messageEncoding` 属性设置为 `"Mtom"`。<br /><br /> 示例:<br /><br /> `<wsHttpBinding> <binding messageEncoding="Mtom"/> </wsHttpBinding>`|  
|元数据|WSDL 1.1|[WSDL 1.1](https://go.microsoft.com/fwlink/?LinkId=94859)<br /><br /> WCF 使用 Web 服务描述语言 (WSDL) 来描述服务。|  
|元数据|WS-Policy|[WS-Policy](https://go.microsoft.com/fwlink/?LinkId=94864)<br /><br /> WCF 使用 WS 策略规范和特定于域的断言描述服务要求和功能。|  
|元数据|WS-Policy 1.5|[WS-Policy 1.5](https://go.microsoft.com/fwlink/?LinkId=95327)<br /><br /> WCF 使用 WS 策略规范和特定于域的断言描述服务要求和功能。|  
|元数据|WS-PolicyAttachment|[WS-PolicyAttachment](https://go.microsoft.com/fwlink/?LinkId=95328)<br /><br /> WCF 实现 Ws-policyattachment 以附加策略表达式在 Web 服务描述语言 (WSDL) 中的不同范围内。|  
|元数据|WS-MetadataExchange|[WS-MetadataExchange](https://go.microsoft.com/fwlink/?LinkId=94868)<br /><br /> WCF 实现 Ws-metadataexchange 以检索 XML 架构、 WSDL 和 Ws-policy。|  
  
### <a name="basichttpbinding"></a>basicHttpBinding  
  
|类别|协议|规范和用法|  
|--------------|--------------|-----------------------------|  
|消息|SOAP 1.1|[SOAP 1.1](https://go.microsoft.com/fwlink/?LinkId=90520)<br /><br /> `basicHttpBinding` 元素根据基本配置文件 1.1 实现 SOAP 1.1 消息协议。|  
|安全性|WSS SOAP Message Security 1.0（WSS SOAP 消息安全 1.0）|[WSS SOAP 消息安全 1.0](https://go.microsoft.com/fwlink/?LinkId=94684)<br /><br /> `basicHttpBinding` 元素根据基本安全配置文件为用户名/密码和基于 X.509 的安全实现 Web 服务安全 (WSS) SOAP 消息安全 1.0 规范。<br /><br /> `<basicHttpBinding> <binding name="Binding1"> <security mode="TransportWithMessageCredential &#124;                     "Message" .../> </binding> </basicHttpBinding>`|  
|安全性|WSS SOAP 消息安全用户名令牌配置文件 1.0|[WSS SOAP 消息安全用户名令牌配置文件 1.0](https://go.microsoft.com/fwlink/?LinkId=95334)<br /><br /> `<basicHttpBinding> <binding name="Binding1"> <security mode="TransportWithMessageCredential"> <transport clientCredentialType="Basic"/> </security> </basicHttpBinding>`|  
|安全性|WSS SOAP 消息安全 X.509 证书令牌配置文件 1.0|[WSS SOAP 消息安全 X.509 证书令牌配置文件 1.0](https://go.microsoft.com/fwlink/?LinkId=95335)<br /><br /> `<basicHttpBinding>   <security mode="Message"> <message clientCredentialType="Certificate"/> </security> </basicHttpBinding>`|  
  
### <a name="wshttpbinding-ws2007httpbinding-and-wsdualhttpbinding"></a>wsHttpBinding、ws2007HttpBinding 和 wsDualHttpBinding  
  
|类别|协议|规范和用法|  
|--------------|--------------|-----------------------------|  
|消息|SOAP 1.2|[入门](https://go.microsoft.com/fwlink/?LinkId=48282)<br /><br /> [消息传递框架](https://go.microsoft.com/fwlink/?LinkId=94664)<br /><br /> [附属 （包括 HTTP 绑定）](https://go.microsoft.com/fwlink/?LinkId=95329)|  
|消息|WS-Addressing 2005/08|[Web 服务寻址 1.0-核心](https://go.microsoft.com/fwlink/?LinkId=90574)<br /><br /> [Web 服务寻址 1.0-SOAP](https://go.microsoft.com/fwlink/?LinkId=95330)<br /><br /> `wsHttpBinding`、`ws2007HttpBinding` 和 `wsDualHttpBinding` 实现万维网联合会 (W3C) WS-Addressing 建议以启用异步消息传送、消息关联和非特定传输寻址机制。<br /><br /> WCF 不支持对 WS-Addressing 标头进行加密，尽管 WS-＊ 规范允许这样做。|  
|消息|WS-Addressing 1.0 - 元数据|[Ws-addressing 1.0 元数据](https://www.w3.org/2007/05/addressing/metadata)policyversion 设置为 1.2 （默认值） 在 ServiceMetadata 行为中设置的策略版本可启用对此协议的支持，wsdl 说明符合 Ws-addressing wsdl，使用policyversion 设置为 1.5，wsdl 说明是符合的 ws-addressing 元数据。<br /><br /> WCF 不支持对 WS-Addressing 标头进行加密，尽管 WS-＊ 规范允许这样做。|  
|安全性|WSS SOAP Message Security 1.0（WSS SOAP 消息安全 1.0）|[WSS SOAP 消息安全 1.0](https://go.microsoft.com/fwlink/?LinkId=94684)<br /><br /> 当 `securityMode` 属性设置为“wsSecurityOverHttp”（默认值）并使用 `wsSecurity` 子元素配置了参数时使用。<br /><br /> `<wsHttpBinding>   <binding name="myBinding">      <security mode="Message" .../>   </binding> </wsHttpBinding>`|  
|安全性|WSS SOAP 消息安全用户名令牌配置文件 1.1|[WSS SOAP 消息安全用户名令牌配置文件 1.0](https://go.microsoft.com/fwlink/?LinkId=95331)<br /><br /> 当 `wsSecurity` 元素的 `authenticationMode` 属性设置为“Username”时使用。<br /><br /> `<wsHttpBinding>   <binding name="MyBinding">     <security mode="Message>       <message           clientCredentialType="UserName        negotiateServiceCredential="false"        establishSecurityContext="false"/>     </security> </binding> </wsHttpBinding>`|  
|安全性|WSS SOAP Message Security X.509 Certificate Token Profile 1.1（WSS SOAP 消息安全 X.509 证书令牌配置文件 1.1）|[WSS SOAP 消息安全 X.509 证书令牌配置文件 1.1](https://go.microsoft.com/fwlink/?LinkId=95332)<br /><br /> 当 `wsSecurity` 元素的 `authenticationMode` 属性设置为“Username”、“Certificate”或“None”时用于消息保护。 另外，当 `wsSecurity` 元素的 `authenticationMode` 属性设置为“Certificate”时用于客户端身份验证。<br /><br /> `<wsHttpBinding>   <binding name="MyBinding">     <security mode="Message>       <message           clientCredentialType="Certificate"        negotiateServiceCredential="false"        establishSecurityContext="false"/>     </security>   </binding> </wsHttpBinding>`|  
|安全性|WSS SOAP 消息安全 Kerberos 令牌配置文件 1.1|[WSS SOAP 消息安全 Kerberos 令牌配置文件 1.1](https://go.microsoft.com/fwlink/?LinkId=95333)<br /><br /> 当 `wsSecurity` 元素的 `authenticationMode` 属性设置为“Windows”时用于身份验证和消息保护。<br /><br /> `<wsHttpBinding>   <binding name="MyBinding">     <security mode="Message>       <message           clientCredentialType="Windows"        negotiateServiceCredential="false"        establishSecurityContext="false"/>     </security>   </binding> </wsHttpBinding>`|  
|安全性|WS-SecureConversation|[WS-SecureConversation](https://go.microsoft.com/fwlink/?LinkId=95317)<br /><br /> 当 `security/@mode` 属性设置为“Message”且 `message/@establishSecurityContext` 属性设置为“true”（默认值）时用于提供安全会话。|  
|安全性|WS-Trust|[WS-Trust](https://go.microsoft.com/fwlink/?LinkId=95318)<br /><br /> 由 WS-SecureConversation 使用（参见上面）。|  
|可靠消息传递|WS-ReliableMessaging|[WS-ReliableMessaging](https://go.microsoft.com/fwlink/?LinkId=95322)<br /><br /> 当绑定配置为使用 `reliableSession` 时使用。<br /><br /> `<wsHttpBinding>  <binding name="myBinding">    <reliableSession/>   </binding> </wsHttpBinding>`|  
|事务|WS-AtomicTransaction|[WS-AtomicTransaction](https://go.microsoft.com/fwlink/?LinkId=95323)<br /><br /> 用于事务管理器之间的通信。 WCF 客户端和服务始终使用本地事务管理器。|  
|事务|WS-Coordination|[WS-Coordination](https://go.microsoft.com/fwlink/?LinkId=95324)<br /><br /> 当 `flowTransactions` 属性设置为“Allowed”或“Required”时用于对事务上下文进行流处理。<br /><br /> `<wsHttpBinding>   <binding transactionFlow="true"/> </wsHttpBinding>`|  
  
## <a name="wsfederationhttpbinding-and-ws2007federationhttpbinding"></a>wsFederationHttpBinding 和 ws2007FederationHttpBinding  
 [ \<WsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)并[ \<ws2007FederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/ws2007federationhttpbinding.md)元素引入为联合方案提供支持，其中第三个参与方颁发用于对客户端进行身份验证令牌。 除了 `wsHttpBinding` 使用的协议以外，`wsFederationHttpBinding` 还使用：  
  
-   用于令牌颁布的 `WS-Trust`。  
  
-   用于已颁发令牌最常见格式的 WSS 安全断言标记语言 (SAML) 令牌配置文件 1.0 和 1.1。  
  
 示例:  
  
```xml  
<wsFederationHttpBinding>  
  <binding name="myBinding">  
     <security mode="Message">  
       <message issuedKeyType="Symmetric"   
                issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1">  
         <issuerMetadata address =   
         'http://localhost/FederationSample/HomeRealmSTS/STS.svc/mex'>  
       </message>  
     </security>  
  </binding>  
</wsFederationHttpBinding>  
```  
  
 有关详细信息，请参阅[联合身份验证](../../../../docs/framework/wcf/feature-details/federation.md)。  
  
## <a name="system-provided-metadata-bindings"></a>系统提供的元数据绑定  
 下表说明系统提供的可互操作元数据绑定（由 <xref:System.ServiceModel.Description.MetadataExchangeBindings?displayProperty=nameWithType> 类公开）支持的协议。  
  
### <a name="mexhttpbinding"></a>mexHttpBinding  
 [ \<MexHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpbinding.md)绑定支持以下协议。 有关使用此绑定的详细信息，请参阅[发布元数据](../../../../docs/framework/wcf/feature-details/publishing-metadata.md)。  
  
|类别|协议|规范和用法|  
|--------------|--------------|-----------------------------|  
|传输|HTTP 1.1|[HTTP 1.1](https://go.microsoft.com/fwlink/?LinkId=84048)|  
|消息|SOAP 1.2|[入门](https://go.microsoft.com/fwlink/?LinkId=48282)<br /><br /> [消息传递框架](https://go.microsoft.com/fwlink/?LinkId=94664)<br /><br /> [附属 （包括 HTTP 绑定）](https://go.microsoft.com/fwlink/?LinkId=95329)|  
|消息|WS-Addressing 2005/08|[Web 服务寻址 1.0-核心](https://go.microsoft.com/fwlink/?LinkId=90574)<br /><br /> [Web 服务寻址 1.0-SOAP](https://go.microsoft.com/fwlink/?LinkId=95330)|  
|元数据|WS-MetadataExchange|[WS-MetadataExchange](https://go.microsoft.com/fwlink/?LinkId=94868)<br /><br /> WCF 实现 Ws-metadataexchange 以检索 XML 架构、 WSDL 和 Ws-policy。|  
  
### <a name="mexhttpsbinding"></a>mexHttpsBinding  
 [\<mexHttpsBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpsbinding.md)支持以下协议。 有关使用此绑定的详细信息，请参阅[发布元数据](../../../../docs/framework/wcf/feature-details/publishing-metadata.md)。  
  
|类别|协议|规范和用法|  
|--------------|--------------|-----------------------------|  
|传输|HTTP 1.1|[HTTP 1.1](https://go.microsoft.com/fwlink/?LinkId=84048)<br /><br /> 启用传输安全。|  
|消息|SOAP 1.2|[入门](https://go.microsoft.com/fwlink/?LinkId=48282)<br /><br /> [消息传递框架](https://go.microsoft.com/fwlink/?LinkId=94664)<br /><br /> [附属 （包括 HTTP 绑定）](https://go.microsoft.com/fwlink/?LinkId=95329)|  
|消息|WS-Addressing 2005/08|[Web 服务寻址 1.0-核心](https://go.microsoft.com/fwlink/?LinkId=90574)<br /><br /> [Web 服务寻址 1.0-SOAP](https://go.microsoft.com/fwlink/?LinkId=95330)|  
|元数据|WS-MetadataExchange|[WS-MetadataExchange](https://go.microsoft.com/fwlink/?LinkId=94868)<br /><br /> WCF 实现 Ws-metadataexchange 以检索 XML 架构、 WSDL 和 Ws-policy。|  
  
## <a name="see-also"></a>请参阅
- [系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)
- [\<basicHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)
- [\<wsHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)
- [\<wsDualHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)
- [\<mexHttpsBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpsbinding.md)
- [\<mexHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpbinding.md)
