---
title: Web 服务协议互操作性指南
ms.date: 03/30/2017
ms.assetid: f2981678-ebdb-433d-899b-467f7df95fb2
ms.openlocfilehash: 96fdf00b5d64f1ed588907fc2717388b30ae1d92
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54521382"
---
# <a name="web-services-protocols-interoperability-guide"></a>Web 服务协议互操作性指南
Windows Communication Foundation (WCF) 实现多个 Web 服务协议。 这些协议中有许多都包含大量留给实施者来决定的选项和扩展点。 本主题提供了一系列 WCF 实现的 Web 服务协议。 本节中的其他主题介绍每个受支持的协议的实现详细信息。  
  
## <a name="web-services-protocols-implemented-by-wcf"></a>由 WCF 实现的 Web 服务协议  
 Web 服务通过协定功能的应用程序协议和 WCF 的 Web 服务 (WS) 基础结构协议，通过通道提供支持。 通过 XML 架构描述语言 1.0 (XSD) 和 Web 服务描述语言 (WSDL) 1.1 完成应用程序协议的互操作性。  
  
 基础结构协议互操作性由 WS-* 规范提供。 WCF 通道提供支持多个 WS-\*基础结构协议。 WCF 通道使用绑定元素进行配置。 下表包含的完整列表的 WS-\*由各种 WCF 绑定元素实现的基础结构协议。  
  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 支持下表中的规范。  
  
|规范/文档|Link|  
|-----------------------------|----------|  
|HTTP 1.1|[RFC 2616](https://go.microsoft.com/fwlink/?LinkId=90372)|  
|SOAP 1.1 HTTP 绑定|[简单对象访问协议 (SOAP) 1.1](https://go.microsoft.com/fwlink/?LinkId=90520)，第 7 节|  
|SOAP 1.2 HTTP 绑定|[SOAP 版本 1.2 第 2 部分：附属内容 （第二版）](https://go.microsoft.com/fwlink/?LinkId=95329)，第 7 节|  
  
 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 和 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> 支持下表中的规范。  
  
|规范/文档|Link|  
|-----------------------------|----------|  
|XML|[可扩展标记语言 (XML) 1.0 （第四版）](https://go.microsoft.com/fwlink/?LinkId=15139)|  
|SOAP 1.1|[简单对象访问协议 (SOAP) 1.1)](https://go.microsoft.com/fwlink/?LinkId=96687)|  
|SOAP 1.2 核心|[SOAP 版本 1.2 第 1 部分：消息传递框架 （第二版）](https://go.microsoft.com/fwlink/?LinkId=94664)|  
|WS-Addressing 2004/08|[Web 服务寻址 (Ws-addressing)](https://go.microsoft.com/fwlink/?LinkId=81239)|  
|W3C Web 服务寻址 1.0 - 核心|[Web 服务寻址 1.0-核心](https://go.microsoft.com/fwlink/?LinkId=96688)|  
|W3C Web 服务寻址 1.0 - SOAP 绑定|[Web 服务寻址 1.0-SOAP 绑定](https://go.microsoft.com/fwlink/?LinkId=96689)|  
|W3C Web 服务寻址 1.0 - WSDL 绑定*|[Web 服务寻址 1.0-WSDL 绑定](https://go.microsoft.com/fwlink/?LinkId=96690)|  
|W3C Web 服务寻址 1.0 元数据|[Web 服务寻址 1.0-元数据](https://www.w3.org/TR/ws-addr-metadata/)|  
|WSDL SOAP1.1 绑定|[Web 服务描述语言 (WSDL) 1.1](https://go.microsoft.com/fwlink/?LinkId=96160)|  
|WSDL SOAP1.2 绑定|[用于 SOAP 1.2 的 WSDL 1.1 绑定扩展](https://go.microsoft.com/fwlink/?LinkId=96691)|  
  
 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> 支持下表中的规范。  
  
|规范/文档|Link|  
|-----------------------------|----------|  
|XOP|[XML 二进制优化打包](https://go.microsoft.com/fwlink/?LinkId=96714)|  
|MTOM + SOAP1.2 绑定|[SOAP 消息传输优化机制](https://go.microsoft.com/fwlink/?LinkId=96713)|  
|MTOM SOAP 1.1 绑定|[用于 MTOM 1.0 SOAP 1.1 绑定](https://go.microsoft.com/fwlink/?LinkId=96712)|  
|MTOM WS-PolicyAssertions|即将发布。|  
  
 <xref:System.ServiceModel.Channels.SecurityBindingElement> 支持下表中的规范。  
  
|规范/文档|链接|  
|-----------------------------|----------|  
|WSS:SOAP 消息安全 1.0|[Web 服务安全：SOAP 消息安全 1.0](https://go.microsoft.com/fwlink/?LinkId=94684)|  
|WSS:用户名令牌配置文件 1.0|[Web 服务安全用户名令牌配置文件 1.0](https://go.microsoft.com/fwlink/?LinkId=95334)<br /><br /> 需要Password/@Type= PasswordText （默认值）|  
|WSS:X.509 令牌配置文件 1.0|[Web 服务安全 X.509 证书令牌配置文件](https://go.microsoft.com/fwlink/?LinkId=95335)|  
|WSS:SAML 1.1 令牌配置文件 1.0|[Web 服务安全：SAML 令牌配置文件](https://go.microsoft.com/fwlink/?LinkId=96693)|  
|WSS:SOAP 消息安全 1.1|[Web 服务安全：SOAP 消息安全 1.1](https://go.microsoft.com/fwlink/?LinkId=91240)|  
|WSS 用户名令牌配置文件 1.1|[Web 服务安全用户名令牌配置文件 1.1](https://go.microsoft.com/fwlink/?LinkId=95331)<br /><br /> 不实现基于密码的密钥派生；<br /><br /> 需要Password/@Type= PasswordText （默认值）|  
|WSS:X509 令牌配置文件 1.1|[Web 服务安全 X.509 证书令牌配置文件 1.1](https://go.microsoft.com/fwlink/?LinkId=95332)|  
|WSS:Kerberos 令牌配置文件 1.1|[Web 服务安全 Kerberos 令牌配置文件 1.1](https://go.microsoft.com/fwlink/?LinkId=95333)|  
|WSS:SAML 1.1 令牌配置文件 1.1|[Web 服务安全 SAML 令牌配置文件 1.1](https://go.microsoft.com/fwlink/?LinkId=96694)|  
|WS-Secure 对话|[Web 服务安全对话语言](https://go.microsoft.com/fwlink/?LinkId=95317)|  
|WS-Trust 1.4|[Web 服务信任语言](https://go.microsoft.com/fwlink/?LinkId=169514)|  
|WS-SecurityPolicy 2005/07|[Web 服务安全对话语言](https://go.microsoft.com/fwlink/?LinkId=95317)<br /><br /> 已根据提交到 OASIS WS-SX 技术委员会的勘误表进行了修正。<br /><br /> [ws-sx 消息](https://go.microsoft.com/fwlink/?LinkId=96700)|  
|WS-ReliableMessaging 1.1|[可靠消息传送协议版本 1.1](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-1.md)|  
  
 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> 支持下表中的规范。  
  
|规范/文档|Link|  
|-----------------------------|----------|  
|WS-Coordination|[Web 服务协调](https://go.microsoft.com/fwlink/?LinkId=95324)|  
|WS-AtomicTransaction|[Web 服务原子事务](https://go.microsoft.com/fwlink/?LinkId=95323)|  
  
 <xref:System.ServiceModel.Description.MetadataExporter>、<xref:System.ServiceModel.Description.MetadataImporter>、<xref:System.ServiceModel.Description.WsdlExporter>、<xref:System.ServiceModel.Description.WsdlImporter> 和 <xref:System.ServiceModel.Description.MetadataResolver> 类支持以下元数据规范：  
  
-   [XML 架构第 1 部分：结构第二版](https://go.microsoft.com/fwlink/?LinkId=3536)  
  
-   [XML 架构第 2 部分：数据类型第二版](https://go.microsoft.com/fwlink/?LinkId=40138)  
  
-   [WSDL 1.1](https://go.microsoft.com/fwlink/?LinkId=96160)  
  
-   [WS-Policy 1.2](https://go.microsoft.com/fwlink/?LinkId=96705)  
  
-   [WS-Policy 1.5](https://go.microsoft.com/fwlink/?LinkId=96706)  
  
-   [WS-PolicyAttachment 1.2](https://go.microsoft.com/fwlink/?LinkId=96707)  
  
-   [WS-MetadataExchange 1.1](https://go.microsoft.com/fwlink/?LinkId=94868)  
  
-   [Ws-transfer Get 进行元数据检索](https://go.microsoft.com/fwlink/?LinkId=96708)  
  
 此外，跨 WCF 实现以下互操作性配置文件：  
  
-   [基本配置文件 1.1](https://go.microsoft.com/fwlink/?LinkId=69313)  
  
-   [简单 SOAP 绑定 1.0](https://go.microsoft.com/fwlink/?LinkId=96710)  
  
-   [基本安全配置文件 1.0 工作草案](https://go.microsoft.com/fwlink/?LinkId=96711)  
  
## <a name="see-also"></a>请参阅
- [系统提供的互操作性绑定支持的 Web 服务协议](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)
- [消息协议](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)
- [数据协定架构引用](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)
- [WSDL 和策略](../../../../docs/framework/wcf/feature-details/wsdl-and-policy.md)
- [安全协议](../../../../docs/framework/wcf/feature-details/security-protocols.md)
- [可靠消息传送协议版本 1.0](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-0.md)
- [可靠消息传送协议版本 1.1](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-1.md)
- [事务协议](../../../../docs/framework/wcf/feature-details/transaction-protocols.md)
- [上下文交换协议](../../../../docs/framework/wcf/feature-details/context-exchange-protocol.md)
