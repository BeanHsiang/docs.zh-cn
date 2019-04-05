---
title: 元数据格式
ms.date: 03/30/2017
ms.assetid: baad1e68-28fc-4a6a-8a43-75e47e7fa871
ms.openlocfilehash: 44ea084287561e13a8db217e49212ee878a26bb7
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54513512"
---
# <a name="metadata-formats"></a>元数据格式
Windows Communication Foundation (WCF) 支持下表中的元数据格式。  
  
## <a name="metadata-specifications-and-usage"></a>元数据的规范和用法  
  
|协议|规范和用法|  
|--------------|-----------------------------|  
|WSDL 1.1|[Web 服务描述语言 (WSDL) 1.1](https://go.microsoft.com/fwlink/?LinkId=94859)<br /><br /> WCF 使用 Web 服务描述语言 (WSDL) 来描述服务。|  
|XML 架构|[XML 架构第 2 部分：数据类型第二版](https://go.microsoft.com/fwlink/?LinkId=94861)和[XML 架构第 1 部分：结构第二版](https://go.microsoft.com/fwlink/?LinkId=94862)<br /><br /> WCF 使用 XML 架构来描述消息中使用的数据类型。|  
|WS Policy|[Web 服务策略 1.2-框架 (Ws-policy)](https://go.microsoft.com/fwlink/?LinkId=94864)<br /><br /> [Web 服务策略 1.5-框架](https://go.microsoft.com/fwlink/?LinkId=94865)<br /><br /> WCF 使用 Ws-policy 1.2 或 1.5 规范与特定于域的断言描述服务要求和功能。|  
|WS Policy 附件|[Web 服务策略 1.2-附件 (Ws-policyattachment)](https://go.microsoft.com/fwlink/?LinkId=94866)<br /><br /> WCF 实现 Ws-policy 附件以附加策略表达式在 WSDL 中的不同范围内。|  
|WS 元数据交换|[Web 服务元数据交换 (Ws-metadataexchange) 1.1 版](https://go.microsoft.com/fwlink/?LinkId=94868)<br /><br /> WCF 实现 Ws-metadataexchange 以检索 XML 架构、 WSDL 和 Ws-policy。|  
|WSDL 的 WS 寻址绑定|[Web 服务寻址 1.0-WSDL 绑定](https://go.microsoft.com/fwlink/?LinkId=94869)<br /><br /> WCF 实现的 Ws-addressing WSDL 附加寻址信息在 WSDL 中的绑定。|  
  
## <a name="see-also"></a>请参阅
- [系统提供的互操作性绑定支持的 Web 服务协议](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)
- [WSDL 和策略](../../../../docs/framework/wcf/feature-details/wsdl-and-policy.md)
