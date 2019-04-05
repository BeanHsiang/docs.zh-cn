---
title: <clientCertificate> <clientCredentials>元素
ms.date: 03/30/2017
ms.assetid: 3b3fa000-3434-4142-a178-11903bdd2c5d
ms.openlocfilehash: 1ca2973b4c0e745f13c1364b2284909d07da738c
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55273120"
---
# <a name="clientcertificate-of-clientcredentials-element"></a>\<clientCertificate > 的\<clientCredentials > 元素
定义用于针对服务进行客户端身份验证的 X.509 证书。  
  
 \<system.ServiceModel>  
\<behaviors>  
\<endpointBehaviors>  
\<behavior>  
\<clientCredentials>  
\<clientCertificate>  
  
## <a name="syntax"></a>语法  
  
```xml  
<clientCertificate findValue="String"
                   storeLocation="LocalMachine/CurrentUser"
                   storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                   X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`findValue`|一个字符串，包含要在 X.509 证书存储中搜索的值。 此属性中包含的类型必须满足 `X509FindType` 属性值的要求。 默认值为一个空字符串。|  
|`storeLocation`|指定客户端用于向服务验证自身身份的 X.509 证书的位置。 包括以下有效值：<br /><br /> -LocalMachine： 分配给本地计算机的证书存储。<br />-CurrentUser： 分配给当前用户的证书存储。<br /><br /> 默认值为 LocalMachine。 此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.StoreLocation>。|  
|`storeName`|指定要搜索的 X.509 证书存储的名称。 包括以下有效值：<br /><br /> -通讯簿：其他用户的证书存储区。<br />-   AuthRoot:第三方证书颁发机构 (Ca) 证书存储区。<br />-CertificateAuthority:中间证书颁发机构 (Ca) 证书存储区。<br />-不允许：已吊销证书的证书存储区。<br />-我：个人证书的证书存储区。<br />根：受信任的根证书颁发机构 (Ca) 证书存储区。<br />-TrustedPeople:直接受信任的人和资源的证书存储区。<br />-TrustedPublisher:直接受信任的发行者的证书存储区。<br /><br /> 默认值为 My。 此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.StoreName>。|  
|X509FindType|定义要执行的 X.509 搜索的类型。 `findValue` 属性中包含的类型必须满足此属性的要求。 包括以下有效值：<br /><br /> -FindByThumbPrint<br />-   FindBySubjectName<br />-   FindBySubjectDistinguishedName<br />-FindByIssuerName<br />-FindByIssuerDistinguishedName<br />-   FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />-FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />-FindByExtension<br />-FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> 默认值为 FindBySubjectDistinguishedName。 此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.X509FindType>。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<clientCredentials>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|指定用于向服务验证客户端身份的凭据。|  
  
## <a name="remarks"></a>备注  
 此配置元素指定用于对具有此元素的客户端进行身份验证的证书。 有关详细信息，请参阅[如何：指定客户端凭据值](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ClientCertificate%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>
- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>
- [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)
- [如何：指定客户端凭据值](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)
- [保护客户端](../../../../../docs/framework/wcf/securing-clients.md)
- [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
