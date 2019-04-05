---
title: <serviceTokenResolver>
ms.date: 03/30/2017
ms.assetid: 6e9001e1-e064-4f47-84b2-46225c177746
author: BrucePerlerMS
ms.openlocfilehash: 1143717882652fc8a03947327b5f1ea89dde7373
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55267425"
---
# <a name="servicetokenresolver"></a>\<serviceTokenResolver>
注册的服务令牌解析程序使用的令牌处理程序集合中的处理程序。 服务标记解析器用于解析传入的令牌和消息中的加密令牌。  
  
 \<system.identityModel>  
\<identityConfiguration>  
\<securityTokenHandlers>  
\<securityTokenHandlerConfiguration>  
\<serviceTokenResolver>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <serviceTokenResolver type=xs:string>  
        </serviceTokenResolver>  
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
|类型|指定的服务令牌解析程序的类型。 任一<xref:System.IdentityModel.Selectors.SecurityTokenResolver>类型或派生类型<xref:System.IdentityModel.Selectors.SecurityTokenResolver>类。 详细了解如何指定`type`属性，请参阅 [自定义类型引用]。 必需。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供配置集合的安全令牌处理程序。|  
  
## <a name="remarks"></a>备注  
 服务标记解析器可用于解析传入的令牌和消息中的加密令牌。 它用于检索应该用于解密传入令牌的密钥。 必须指定`type`属性。 指定的类型可以是<xref:System.IdentityModel.Selectors.SecurityTokenResolver>派生的自定义类型或<xref:System.IdentityModel.Selectors.SecurityTokenResolver>类。  
  
 一些令牌处理程序，可在配置中指定服务令牌解析器设置。 单个标记处理程序上的设置将覆盖指定安全标记处理程序集合。  
  
> [!NOTE]
>  指定`<serviceTokenResolver>`元素的子元素作为[ \<identityConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素已被弃用，但仍然支持向后兼容。 上的设置`<securityTokenHandlerConfiguration>`元素上会覆盖`<identityConfiguration>`元素。  
  
## <a name="example"></a>示例  
  
```xml  
<serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
```
