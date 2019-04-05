---
title: Internet Explorer 完成的与 WCF 完成的服务证书验证之间的差异
ms.date: 03/30/2017
helpviewer_keywords:
- service certificate validation [WCF]
- certificates [WCF], service certificate validation
ms.assetid: 9dffcab2-70a9-40f0-99fd-d3a0b296028f
ms.openlocfilehash: 08a790dbbc8bc51a1e47bbcbcf90ec7c035bf3df
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54549780"
---
# <a name="differences-between-service-certificate-validation-done-by-internet-explorer-and-wcf"></a>Internet Explorer 完成的与 WCF 完成的服务证书验证之间的差异
由于 Internet Explorer 和 Windows Communication Foundation (WCF) 验证服务证书时使用 HTTPS 的方式不同，很可能 Internet Explorer 将无法再访问帮助页或 Web 服务描述语言(WSDL) 服务的即使 WCF 客户端仍能够成功将消息发送到服务终结点。 这是因为 Internet Explorer 会检查是否有服务证书`ServerAuthentication`中的增强的使用标志，对象标识符 (OID)，而 WCF 不强制实施此类约束。 如果 Internet Explorer 无法访问服务帮助页或服务的 WSDL，请使用[ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)访问服务元数据。  
  
## <a name="see-also"></a>请参阅
- [HTTPS、通过 TCP 的 SSL 与 SOAP 安全之间的证书验证差异](../../../../docs/framework/wcf/feature-details/cert-val-diff-https-ssl-over-tcp-and-soap.md)
- [如何：检索元数据并实现兼容服务](../../../../docs/framework/wcf/feature-details/how-to-retrieve-metadata-and-implement-a-compliant-service.md)
