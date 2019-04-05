---
title: <securityTokenHandlers>
ms.date: 03/30/2017
ms.assetid: f11a631d-4094-4e11-bb03-4ede74b30281
author: BrucePerlerMS
ms.openlocfilehash: a5af3893ab72d23c2b3814569decfc50431b8e55
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55277519"
---
# <a name="securitytokenhandlers"></a>\<securityTokenHandlers>
指定与该终结点注册的安全令牌处理程序的集合。  
  
 \<system.identityModel>  
\<identityConfiguration>  
\<securityTokenHandlers>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|name|指定的标记处理程序集合的名称。 由框架识别的唯一值是"ActAs"和"OnBehalfOf"。 如果使用这些名称的指定标记处理程序集合，分别处理 ActAs 或 OnBehalfOf 令牌时，将使用集合。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/add.md)|将安全令牌处理程序添加到令牌处理程序集合。|  
|[\<clear>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/clear.md)|清除所有安全令牌处理程序从令牌处理程序集合。|  
|[\<remove>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/remove.md)|令牌处理程序集合中删除的安全令牌处理程序。|  
|[\<securityTokenHandlerConfiguration>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供的令牌处理程序集合的配置。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<identityConfiguration>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|指定服务级别标识设置。|  
  
## <a name="remarks"></a>备注  
 在服务配置，可以指定一个或多个安全令牌处理程序的命名的集合。 可以通过使用指定的名称集合`name`属性。 该框架将处理的唯一名称是"ActAs"和"OnBehalfOf"。 如果这些集合中存在处理程序，它们由安全令牌服务 (STS) 而不是默认处理程序处理时`ActAs`和`OnBehalfOf`令牌。  
  
 默认情况下，该集合填充以下处理程序类型： <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>， <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>， <xref:System.IdentityModel.Tokens.KerberosSecurityTokenHandler>， <xref:System.IdentityModel.Tokens.WindowsUserNameSecurityTokenHandler>， <xref:System.IdentityModel.Tokens.RsaSecurityTokenHandler>， <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>，和<xref:System.IdentityModel.Tokens.EncryptedSecurityTokenHandler>。 可以通过使用修改集合`<add>`， `<remove>`，和`<clear>`元素。 您必须确保仅任何特定类型的单个处理程序集合中存在。 例如，如果派生的处理程序从<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>类，或者您的处理程序或<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>可能在单个集合，但不是能同时配置。  
  
 使用`<securityTokenHandlerConfiguration>`元素集合中指定的处理程序的配置设置。 通过此元素指定的设置将覆盖指定通过在服务上的那些[ \<identityConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素。 一些处理程序 （包括多个内置处理程序类型） 可以支持其他配置的子元素通过`<add>`元素。 上一个处理程序指定设置覆盖指定集合或服务上的等效设置。
