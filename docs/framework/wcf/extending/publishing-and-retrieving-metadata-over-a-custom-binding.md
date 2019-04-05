---
title: 通过自定义绑定发布和检索元数据
ms.date: 03/30/2017
ms.assetid: 904e11b4-d90e-45c6-9ee5-c3472c90008c
ms.openlocfilehash: 850f341e933e44d92f130dae90aff5b5c1a882b5
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54639544"
---
# <a name="publishing-and-retrieving-metadata-over-a-custom-binding"></a>通过自定义绑定发布和检索元数据
<xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> 提供对向服务添加元数据终结点的支持。 这些元数据终结点可以响应在具有的 URL 的 HTTP GET 请求`?wsdl`查询字符串和 Ws-transfer GET 请求的 Ws-metadataexchange (MEX) 规范中定义。 MEX 终结点可实现 <xref:System.ServiceModel.Description.IMetadataExchange?displayProperty=nameWithType> 协定。  
  
## <a name="publishing-metadata-over-a-custom-binding"></a>通过自定义绑定发布元数据  
 通过将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A?displayProperty=nameWithType> 或 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A?displayProperty=nameWithType> 属性设置为 `true`，可以启用 HTTP GET 元数据终结点和 HTTPS GET 元数据终结点。 无法配置这些终结点的绑定。  
  
 <xref:System.ServiceModel.Description.IMetadataExchange>协定，但是，可与任何终结点，包括那些使用自定义绑定，因为<xref:System.ServiceModel.Description.IMetadataExchange>终结点都与任何其他 Windows Communication Foundation (WCF) 服务终结点相同。 如果你了解如何修改系统提供的绑定的配置，或者了解如何配置 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>，则可以将绑定配置为与 <xref:System.ServiceModel.Description.IMetadataExchange> 终结点一起使用。  
  
## <a name="retrieving-metadata-over-a-custom-binding"></a>通过自定义绑定检索元数据  
 可以从 HTTP Get 和 HTTPS Get 元数据终结点使用标准 HTTP 或 HTTPS GET 请求检索元数据。  
  
 若要从 MEX 元数据终结点检索元数据可以通常使用 WCF 支持的标准 MEX 绑定之一。 有关详细信息，请参阅 <xref:System.ServiceModel.Description.MetadataExchangeBindings?displayProperty=nameWithType>。 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> 类型和 Svcutil.exe 工具将根据指定元数据终结点的地址自动选择这些标准 MEX 绑定之一。  
  
 如果 MEX 元数据终结点使用与标准 MEX 绑定之一不同的其他绑定，则你可以使用代码或通过提供 <xref:System.ServiceModel.Description.MetadataExchangeClient> 客户端终结点配置来配置由 <xref:System.ServiceModel.Description.IMetadataExchange> 所使用的绑定。 Svcutil.exe 工具可自动从其配置文件中加载一个 <xref:System.ServiceModel.Description.IMetadataExchange> 客户端终结点配置，该配置具有与元数据终结点地址的 URI 方案相同的名称。  
  
## <a name="security"></a>安全性  
 通过自定义绑定发布元数据时，请确保该绑定提供您的元数据所要求的安全支持。 例如，若要防止信息泄漏，并确保客户端具有获取元数据的权限，您可以通过将 <xref:System.ServiceModel.Description.IMetadataExchange> 终结点配置为要求身份验证和加密的方式使元数据和应用程序更加安全。 该示例[自定义安全元数据终结点](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)演示此方案。  
  
## <a name="see-also"></a>请参阅
- [保护服务](../../../../docs/framework/wcf/securing-services.md)
- [WS-MetadataExchange 绑定](../../../../docs/framework/wcf/extending/ws-metadataexchange-bindings.md)
- [如何：配置自定义 Ws-metadata Exchange 绑定](../../../../docs/framework/wcf/extending/how-to-configure-a-custom-ws-metadata-exchange-binding.md)
- [如何：检索元数据通过非 MEX 绑定](../../../../docs/framework/wcf/extending/how-to-retrieve-metadata-over-a-non-mex-binding.md)
