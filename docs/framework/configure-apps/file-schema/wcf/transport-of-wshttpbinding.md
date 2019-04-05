---
title: <transport> 的 <wsHttpBinding>
ms.date: 03/30/2017
ms.assetid: 21e38acf-450a-4bda-82b6-de305e1f7cd8
ms.openlocfilehash: ea025751020d6d98292f6bc3ecfe9421af0cb793
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372316"
---
# <a name="transport-of-wshttpbinding"></a>\<transport> of \<wsHttpBinding>

定义 HTTP 传输的身份验证设置。

\<system.serviceModel>\
\<bindings>\
\<wsHttpBinding>\
\<binding>\
\<安全 > \
\<transport>

## <a name="syntax"></a>语法

```xml
<wsHttpBinding>
  <binding>
    <security mode="None|Transport|TransportWithMessageCredential|TransportCredentialOnly">
      <transport clientCredentialType="Basic|Certificate|Digest|None|Ntlm|Windows"
                 proxyCredentialType="Basic|Digest|None|Ntlm|Windows"
                 realm="string" />
        <extendedProtectionPolicy policyEnforcement="Never|WhenSupported|Always"
                                  protectionScenario="TransportSelected|TrustedProxy">
          <customServiceNames>
          </customServiceNames>
        </extendedProtectionPolicy>
      </transport>
    </security>
  </binding>
</wsHttpBinding>
```

## <a name="type"></a>类型

<xref:System.ServiceModel.HttpTransportSecurity>

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`clientCredentialType`|指定用于向服务证明客户端身份的凭据。 此属性的类型为 <xref:System.ServiceModel.HttpClientCredentialType>。|
|`proxyCredentialType`|指定用于向域代理证明客户端身份的凭据。 此属性的类型为 <xref:System.ServiceModel.HttpProxyCredentialType>。|
|`realm`|一个字符串，指定摘要式或基本身份验证的身份验证领域。 默认值为一个空字符串。<br /><br /> 身份验证领域至少指定执行身份验证的主机的名称。 它还可以指定具有访问权限的用户的集合。 用户可以查询身份验证领域，以确定多个可能的用户名和密码中哪一个可以使用。|
|`policyEnforcement`|此枚举指定应何时强制实施 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>。<br /><br /> 1.Never – 绝不强制实施此策略（禁用扩展保护）。<br />2.WhenSupported – 仅在客户端支持扩展保护时才强制实施此策略。<br />3.Always – 总是强制实施此策略。 不支持扩展保护的客户端将无法进行身份验证。|

## <a name="clientcredentialtype-attribute"></a>clientCredentialType 属性

|值|描述|
|-----------|-----------------|
|`None`|禁用安全性。|
|`Basic`|使用基本身份验证。|
|`Digest`|使用摘要式身份验证。|
|`Ntlm`|对 Windows 域使用 NTLM 身份验证作为回退。|
|`Windows`|使用集成 Windows 身份验证。|
|`Certificate`|使用 X.509 证书对客户端进行身份验证。|

## <a name="proxycredentialtype-attribute"></a>proxyCredentialType 属性

|值|描述|
|-----------|-----------------|
|`None`|禁用安全性。|
|`Basic`|使用基本身份验证。|
|`Digest`|使用摘要式身份验证。|
|`Ntlm`|对 Windows 域使用 NTLM 作为回退。|
|`Windows`|使用集成 Windows 身份验证。|
|`Certificate`|使用 X.509 证书对客户端进行身份验证。|

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[\<security>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)|表示的安全功能[ \<wsHttpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)。|

## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.HttpTransportSecurity>
- <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.WSHttpSecurityElement.Transport%2A>
- <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>
- [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
- [绑定](../../../../../docs/framework/wcf/bindings.md)
- [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)
- [使用绑定配置服务和客户端](../../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../../../docs/framework/misc/binding.md)
