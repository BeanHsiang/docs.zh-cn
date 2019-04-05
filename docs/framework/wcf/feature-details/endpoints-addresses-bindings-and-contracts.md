---
title: 终结点：地址、 绑定和协定
ms.date: 03/30/2017
helpviewer_keywords:
- endpoints [WCF]
- Windows Communication Foundation [WCF], endpoints
- WCF [WCF], endpoints
ms.assetid: 9ddc46ee-1883-4291-9926-28848c57e858
ms.openlocfilehash: a10d9ac5718bf6b88a3a00902f90045c705f8431
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54721784"
---
# <a name="endpoints-addresses-bindings-and-contracts"></a>终结点：地址、 绑定和协定
与 Windows Communication Foundation (WCF) 服务的所有通信都是通过*终结点*的服务。 终结点向客户端访问 WCF 服务提供的功能。  
  
 每个终结点包含四个属性：  
  
-   一个指示可以查找终结点的位置的地址。  
  
-   一个指定客户端如何与终结点进行通信的绑定。  
  
-   一个标识可用操作的协定。  
  
-   一组指定终结点的本地实现细节的行为。  
  
 本主题讨论此终结点结构并说明如何在 WCF 对象模型中表示。  
  
## <a name="the-structure-of-an-endpoint"></a>终结点的结构  
 每个终结点由以下内容组成：  
  
-   地址:地址唯一标识终结点，并告知潜在所在的服务的使用者。 通过在 WCF 对象模型中表示<xref:System.ServiceModel.EndpointAddress>类。 一个 <xref:System.ServiceModel.EndpointAddress> 类包含：  
  
    -   一个表示服务地址的 <xref:System.ServiceModel.EndpointAddress.Uri%2A> 属性。  
  
    -   一个表示服务安全标识和可选消息头集合的 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 属性。 可选消息头用于提供其他更多详细寻址信息来标识终结点或与终结点交互。  
  
     有关详细信息，请参阅[指定一个终结点地址](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)。  
  
-   绑定：绑定指定如何与终结点进行通信。 这包括：  
  
    -   要使用的传输协议（例如，TCP 或 HTTP）。  
  
    -   要用于消息的编码（例如，文本或二进制）。  
  
    -   必需的安全要求（例如，SSL 或 SOAP 消息安全）。  
  
     有关详细信息，请参阅[WCF 绑定概述](../../../../docs/framework/wcf/bindings-overview.md)。 一个绑定由 WCF 对象模型中的抽象基类<xref:System.ServiceModel.Channels.Binding>。 大多数情况下，用户可以使用系统提供的绑定之一。 有关详细信息，请参阅[System-Provided Bindings](../../../../docs/framework/wcf/system-provided-bindings.md)。  
  
-   约定：协定概述了终结点公开给客户端的功能。 协定指定：  
  
    -   客户端可以调用的操作。  
  
    -   消息的窗体。  
  
    -   调用操作所需的输入参数或数据的类型。  
  
    -   客户端可以预期的处理或响应消息的类型。  
  
     有关定义协定的详细信息，请参阅[Designing Service Contracts](../../../../docs/framework/wcf/designing-service-contracts.md)。  
  
-   行为：终结点行为可用于自定义服务终结点的本地行为。 终结点行为通过参与构建 WCFruntime 的过程中实现此目的。 终结点行为的一个示例是 <xref:System.ServiceModel.Description.ServiceEndpoint.ListenUri%2A> 属性，可以利用该属性指定与 SOAP 或 Web 服务描述语言 (WSDL) 地址不同的侦听地址。 有关详细信息，请参阅[ClientViaBehavior](../../../../docs/framework/wcf/diagnostics/wmi/clientviabehavior.md)。  
  
## <a name="defining-endpoints"></a>定义终结点  
 可以通过使用代码以强制方式或通过配置以声明方式指定服务的终结点。 有关详细信息，请参阅[如何：在配置中创建的服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)和[如何：在代码中创建的服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)。  
  
## <a name="in-this-section"></a>本节内容  
 本节说明了绑定、终结点和地址的用途，演示了如何配置绑定和终结点，并演示了如何使用 `ClientVia` 行为和 `ListenUri` 属性。  
  
 [地址](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md)  
 介绍如何在 WCF 中寻址终结点。  
  
 [绑定](../../../../docs/framework/wcf/feature-details/bindings.md)  
 描述如何使用绑定指定客户端与服务相互通信所需的传输、编码和协议详细信息。  
  
 [协定](../../../../docs/framework/wcf/feature-details/contracts.md)  
 描述协定如何定义服务的方法。  
  
 [如何：在配置中创建的服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)  
 描述如何在配置中创建服务终结点。  
  
 [如何：在代码中创建的服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)  
 描述如何在代码中创建服务终结点。  
  
 [如何：使用 Svcutil.exe 验证已编译的服务代码](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-validate-compiled-service-code.md)  
 介绍了如何不承载服务使用情况下检测服务实现和配置中的错误[ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。  
  
## <a name="see-also"></a>请参阅
- [配置服务](../../../../docs/framework/wcf/configuring-services.md)
- [扩展绑定](../../../../docs/framework/wcf/extending/extending-bindings.md)
