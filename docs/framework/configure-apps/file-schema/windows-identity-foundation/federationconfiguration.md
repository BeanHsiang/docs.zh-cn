---
title: <federationConfiguration>
ms.date: 03/30/2017
ms.assetid: 8b14054c-6d07-46ab-ab58-03f14beac0f2
author: BrucePerlerMS
ms.openlocfilehash: befa74f02ccb0dde4448f36c0698feebaf6201ce
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55286398"
---
# <a name="federationconfiguration"></a>\<federationConfiguration>
配置<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>(WSFAM) 和<xref:System.IdentityModel.Services.SessionAuthenticationModule>(SAM) 时使用联合身份验证通过 WS 联合身份验证协议。 配置<xref:System.Security.Claims.ClaimsAuthorizationManager>使用时<xref:System.IdentityModel.Services.ClaimsPrincipalPermission>或<xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute>类以提供基于声明的访问控制。  
  
 \<system.identityModel.services>  
\<federationConfiguration>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration name=xs:string identityConfigurationName=xs:string>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|name|此联合身份验证配置元素的名称。 此属性主要用于将来的协议提供一个扩展点。 可选。|  
|identityConfigurationName|中指定的标识配置节的名称[ \<identityConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素使用。 如果未指定此属性，则使用默认标识配置节。 可选。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<cookieHandler>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|配置由 SAM 使用的 cookie 处理程序。 可选。|  
|[\<serviceCertificate>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/servicecertificate.md)|配置用于加密和解密令牌的证书。 可选。|  
|[\<wsFederation>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/wsfederation.md)|配置 WS 联合身份验证模块 (WSFAM)。 可选。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<system.identityModel.services>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md)|使用 WS 联合身份验证协议进行身份验证的配置节。|  
  
## <a name="remarks"></a>备注  
 \<FederationConfiguration > 元素提供了两种不同方案中的设置：  
  
-   元素时使用 WS 联合被动 Web 应用程序中，包含配置设置<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>(WSFAM) 和<xref:System.IdentityModel.Services.SessionAuthenticationModule>(SAM)。 它还引用了要用来配置安全令牌处理程序和证书，以及声明授权管理器和声明身份验证管理器等组件的标识配置。  
  
-   使用时<xref:System.IdentityModel.Services.ClaimsPrincipalPermission>或<xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute>类来提供基于声明的访问控制在代码中，元素引用配置的声明授权管理器和使用进行授权策略的标识配置决策。 这是为 true，即使在不是被动 Web 方案; 的方案中例如，Windows Communication Foundation (WCF) 应用程序或不是基于 Web 的应用程序。 如果应用程序不是被动的 Web 应用程序， [ \<claimsAuthorizationManager >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/claimsauthorizationmanager.md)元素 （和其子策略元素，如果存在） 的引用的标识配置`<federationConfiguration>`元素应用的唯一设置。 将忽略所有其他成员。  
  
 无论何种方案，在运行时加载默认联合身份验证配置。 行为定义，如下所示：  
  
1.  如果没有任何`<federationConfiguration>`元素不存在，运行时创建的联合身份验证配置，并使用默认值填充它。 这种默认联合身份验证配置将引用的默认标识配置。  
  
2.  如果某个`<federationConfiguration>`元素存在，它是无论它是名为还是未命名的默认联合身份验证配置。 如果其`identityConfiguration`指定属性，引用名为的标识配置; 否则，引用默认标识配置。  
  
3.  如果未命名`<federationConfiguration>`元素存在，它是默认的联合身份验证配置。 如果其`identityConfiguration`指定属性，引用名为的标识配置; 否则，引用默认标识配置。  
  
4.  如果多个名为`<federationConfiguration>`元素是否存在以及是否未命名`<federationConfiguration>`元素存在，将引发异常。  
  
 通常情况下，只有一个`<federationConfiguration>`定义部分。 本部分是默认联合身份验证配置。 你可以指定多个唯一命名`<federationConfiguration>`元素; 但是，在这种情况下，如果你想要加载而未命名的联合身份验证配置，则必须提供的处理程序。 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfigurationCreated> 事件并设置<xref:System.IdentityModel.Services.Configuration.FederationConfigurationCreatedEventArgs.FederationConfiguration%2A?displayProperty=nameWithType>属性的处理程序内<xref:System.IdentityModel.Services.Configuration.FederationConfiguration>对象从相应的值初始化`<federationConfiguration>`配置文件中的元素。  
  
 `<federationConfiguration>`元素表示由<xref:System.IdentityModel.Services.Configuration.FederationConfigurationElement>类。 表示配置对象本身<xref:System.IdentityModel.Services.Configuration.FederationConfiguration>类。 将单个<xref:System.IdentityModel.Services.Configuration.FederationConfiguration>上设置实例<xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType>属性，并提供应用程序的联合的配置。  
  
## <a name="example"></a>示例  
 下面的 XML 演示`<federationConfiguration>`元素指定 WSFAM 设置，并指定默认 cookie 处理程序 (实例<xref:System.IdentityModel.Services.ChunkedCookieHandler>类) 由 SAM 使用。  
  
> [!WARNING]
>  在此示例中，cookie 处理程序和 WSFAM 都不需要使用 HTTPS。 这是因为`requireHttps`特性，可以在`<wsFederation>`元素并`requireSsl`特性，可以在`<cookieHandlerElement>`是`false`。 因为它们可能会存在安全风险，这些设置不会建议用于大多数生产环境。  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <wsFederation passiveRedirectEnabled="true"   
      issuer="http://localhost:15839/wsFederationSTS/Issue"   
      realm="http://localhost:50969/" reply="http://localhost:50969/"   
      requireHttps="false"   
      signOutReply="http://localhost:50969/SignedOutPage.html"   
      signOutQueryString="Param1=value2&Param2=value2"   
      persistentCookiesOnPassiveRedirects="true" />  
    <cookieHandler requireSsl="false" />  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>
- <xref:System.IdentityModel.Services.SessionAuthenticationModule>
- <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType>
- [\<identityConfiguration>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)
