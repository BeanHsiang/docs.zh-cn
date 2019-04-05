---
title: <serviceCertificate> <clientCredentials>元素
ms.date: 03/30/2017
ms.assetid: e50c0ac5-f0df-4c90-b54b-fc602c1f84ea
ms.openlocfilehash: 7134e8b3d253575bf26f26490372aa94549c73b7
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55279677"
---
# <a name="servicecertificate-of-clientcredentials-element"></a>\<serviceCertificate > 的\<clientCredentials > 元素
指定客户端对服务进行身份验证时使用的证书。  
  
 \<system.ServiceModel>  
\<behaviors>  
\<endpointBehaviors>  
\<behavior>  
\<clientCredentials>  
\<serviceCertificate>  
  
## <a name="syntax"></a>语法  
  
```xml  
<serviceCertificate />
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
 无。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<defaultCertificate>](../../../../../docs/framework/configure-apps/file-schema/wcf/defaultcertificate-element.md)|指定在服务或 STS 未通过协商协议提供证书时要使用的 X.509 证书。|  
|[\<scopedCertificates>](../../../../../docs/framework/configure-apps/file-schema/wcf/scopedcertificates-element.md)|表示特定服务为身份验证提供的 X.509（作用域）证书的集合。 此集合通常用于指定联合方案中安全令牌服务的服务证书。|  
|[\<authentication>](../../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)|指定客户端使用的服务证书的身份验证行为。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<clientCredentials>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|指定客户端用于向服务证明自己的身份的凭据。|  
  
## <a name="remarks"></a>备注  
 此配置元素指定客户端在验证使用 SSL 身份验证的服务所出示的证书时使用的设置。 它还包含在客户端上显式配置为对发送给使用消息安全的服务的消息进行加密的服务的所有证书。  
  
 特性`serviceCertificate`元素的特性相等[ \<clientCertificate >](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-clientcredentials-element.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ServiceCertificate%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A>
- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)
- [保护客户端](../../../../../docs/framework/wcf/securing-clients.md)
- [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
