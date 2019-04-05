---
title: <claimsAuthorizationManager>
ms.date: 03/30/2017
ms.assetid: 9354eee3-f692-4ad6-8427-3169686b8bcc
author: BrucePerlerMS
ms.openlocfilehash: 59d47eda97e97629408ece12a1d1dfbe804feb3e
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55268088"
---
# <a name="claimsauthorizationmanager"></a>\<claimsAuthorizationManager>
注册的传入声明的声明授权管理器。  
  
 \<system.identityModel>  
\<identityConfiguration>  
\<claimsAuthorizationManager>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthorizationManager type = xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthorizationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|类型|派生的自定义类型<xref:System.Security.Claims.ClaimsAuthorizationManager>类。 有关如何指定详细信息`type`属性，请参阅[自定义类型引用](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md)。|  
  
### <a name="child-elements"></a>子元素  
 如果没有任何`type`属性，或者如果`type`属性引用<xref:System.Security.Claims.ClaimsAuthenticationManager>类，`<claimsAuthorizationManager>`元素不接受子元素; 但是，类派生自<xref:System.Security.Claims.ClaimsAuthorizationManager>可以定义子配置元素。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<identityConfiguration>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定服务级别标识设置。|  
  
## <a name="remarks"></a>备注  
 通过提供的默认行为<xref:System.Security.Claims.ClaimsAuthorizationManager>类始终授权的传入声明。 如果没有`type`指定属性或如果`type`特性指定<xref:System.Security.Claims.ClaimsAuthorizationManager>类，`<claimsAuthorizationManager>`元素不接受子元素。 您可以指定`type`属性来注册一个类型派生自<xref:System.Security.Claims.ClaimsAuthorizationManager>类，以实现自定义行为。 派生的类可以支持的子元素通过配置`<claimsAuthorizationManager>`通过重写元素<xref:System.Security.Claims.ClaimsAuthorizationManager.LoadCustomConfiguration%2A>方法来处理这些元素。 为子元素定义的架构由类的设计器。  
  
> [!IMPORTANT]
>  使用时<xref:System.IdentityModel.Services.ClaimsPrincipalPermission>或<xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute>类以提供在代码中，引用的标识配置的基于声明的访问控制`<federationConfiguration>`元素配置的声明授权管理器和用于进行的策略授权决策。 这是为 true，即使在不是被动 Web 方案中，例如 Windows Communication Foundation (WCF) 应用程序或不是基于 Web 的应用程序的方案中。 如果应用程序不是被动的 Web 应用程序，`<claimsAuthorizationManager>`元素 （和其子策略元素，如果存在） 的引用的标识配置是应用的唯一设置。 将忽略所有其他设置。 有关详细信息，请参阅[ \<federationConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)元素。  
  
 此元素设置<xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthorizationManager%2A?displayProperty=nameWithType>属性。  
  
## <a name="example"></a>示例  
 下面的 XML 演示声明授权的配置管理器实现策略组成资源操作对其中每个指定的请求者必须拥有对资源执行操作的声明的布尔组合。 实现声明授权管理器可以使用此策略的代码可在`ClaimsBasedAuthorization`示例。  
  
```xml  
<system.identityModel>  
    <identityConfiguration>  
      <claimsAuthorizationManager type="ClaimsAuthorizationLibrary.MyClaimsAuthorizationManager, ClaimsAuthorizationLibrary">  
        <policy resource="http://localhost:28491/Developers.aspx" action="GET">  
          <or>  
            <claim claimType="http://schemas.microsoft.com/ws/2008/06/identity/claims/role" claimValue="developer" />  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
          </or>  
        </policy>  
        <policy resource="http://localhost:28491/Administrators.aspx" action="GET">  
          <and>  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
            <claim claimType="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country" claimValue="USA" />  
          </and>  
        </policy>  
        <policy resource="http://localhost:28491/Default.aspx" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/Claims.aspx" action="GET">  
        </policy>  
      </claimsAuthorizationManager>  
    <identityConfiguration>  
<system.identityModel>  
```
