---
title: <audienceUris>
ms.date: 03/30/2017
ms.assetid: 7a3d8515-d756-4afe-a22d-07cbe2217ee3
author: BrucePerlerMS
ms.openlocfilehash: 556c444d5e48e27036c4b49338f6e70de7ef5c5d
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55267269"
---
# <a name="audienceuris"></a>\<audienceUris>
指定 Uri 都是可接受的信赖方 (RP) 标识符的集。 除非某个允许的受众 Uri 作用域内，将不会接受令牌。  
  
 \<system.identityModel>  
\<identityConfiguration>  
\<securityTokenHandlers>  
\<securityTokenHandlerConfiguration>  
\<audienceUris>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <audienceUris mode=xs:string>  
          <add value=xs:string />  
          <clear />  
          <remove value=xs:string />  
        </audienceUris>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|mode|<xref:System.IdentityModel.Selectors.AudienceUriMode>值，该值指定是否应该对传入令牌应用的访问群体限制。 可能的值为"始终"，"从不"，并"BearerKeyOnly"。 默认值为"始终"。 可选。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|`<add value=xs:string>`|添加指定的 URI `value` audienceUris 集合的属性。 需要 `value` 属性。 该 URI 是区分大小写。|  
|`<clear>`|清除 audienceUris 的集合。 从集合中删除所有标识符。|  
|`<remove value=xs:string>`|删除指定的 URI `value` audienceUris 集合中的属性。 需要 `value` 属性。 该 URI 是区分大小写。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供配置集合的安全令牌处理程序。|  
  
## <a name="remarks"></a>备注  
 默认情况下，该集合为空;使用`<add>`， `<clear>`，和`<remove>`要修改集合的元素。 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> 并<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>对象所需配置任何的受众 URI 集合中的值允许的受众 URI 限制中的使用<xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement>对象。  
  
 `<audienceUris>`元素表示由<xref:System.IdentityModel.Configuration.AudienceUriElementCollection>类。 表示添加到集合的单个 URI<xref:System.IdentityModel.Configuration.AudienceUriElement>类。  
  
> [!NOTE]
>  利用`<audienceUris>`元素的子元素作为[ \<identityConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素已被弃用，但仍然支持向后兼容。 上的设置`<securityTokenHandlerConfiguration>`元素上会覆盖`<identityConfiguration>`元素。  
  
## <a name="example"></a>示例  
 下面的 XML 演示如何配置应用程序可接受的受众 Uri。 此示例将配置单个 URI。 将接受令牌作用域为此 URI，所有其他用户将被拒绝。  
  
```xml  
<audienceUris>  
  <add value="http://localhost:19851/"/>  
</audienceUris>  
```
