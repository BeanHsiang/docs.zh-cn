---
title: 基于目标和使用的标准比较 ASP.NET Web 服务与 WCF
ms.date: 03/30/2017
ms.assetid: d3890278-fa9b-4902-91ea-8da73b7143cc
ms.openlocfilehash: 74ef2f3f3505125f8720695e218617817fcae82d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54548373"
---
# <a name="comparing-aspnet-web-services-to-wcf-based-on-purpose-and-standards-used"></a>基于目标和使用的标准比较 ASP.NET Web 服务与 WCF
开发 ASP.NET Web 服务的目标是生成通过使用 Simple Object Access Protocol (SOAP) over HTTP 来发送和接收消息的应用程序。 消息的结构可使用 XML 架构来定义，并且提供了一种工具，以便将消息序列化为 .NET Framework 对象以及将这种对象反序列化为消息。 该技术可以自动生成元数据，以便用 Web 服务描述语言 (WSDL) 描述 Web 服务，并且提供了另一个工具，用来从 WSDL 生成 Web 服务的客户端。  
  
 WCF 是用于启用.NET Framework 应用程序与其他软件实体交换消息。 默认情况下使用 SOAP，但消息可采用任何格式，并可以使用任何传输协议传递。 消息的结构可使用 XML 架构来定义，并且提供多种选项以便将消息序列化为 .NET Framework 对象以及将这种对象反序列化为消息。 WCF 可以自动生成元数据来描述使用 WSDL 中的技术构建的应用程序，而且它还提供了一种工具从 WSDL 生成这些应用程序的客户端。  
  
 中介绍了 ASP.NET Web 服务支持的标准[XML Web 服务使用 ASP.NET 创建](https://go.microsoft.com/fwlink/?LinkId=94872)。 在列出了更广泛的标准 WCF 支持列表[Web 服务协议支持的系统提供的互操作性绑定](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)。  
  
## <a name="see-also"></a>请参阅
- [从开发的角度比较 ASP.NET Web 服务与 WCF](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-development.md)
