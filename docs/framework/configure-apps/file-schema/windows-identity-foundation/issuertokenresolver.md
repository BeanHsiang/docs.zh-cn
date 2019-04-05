---
title: <issuerTokenResolver>
ms.date: 03/30/2017
ms.assetid: f74392f6-3f5b-4880-bd8a-3a9130d31e65
author: BrucePerlerMS
ms.openlocfilehash: a37935fa9302493c0ecaab0f56e1414d44637af6
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55269219"
---
# <a name="issuertokenresolver"></a>\<issuerTokenResolver>
注册令牌处理程序集合中的处理程序使用的颁发者令牌解析程序。 颁发者令牌解析程序用于解决签名令牌对传入令牌和消息。  
  
 \<system.identityModel>  
\<identityConfiguration>  
\<securityTokenHandlers>  
\<securityTokenHandlerConfiguration>  
\<issuerTokenResolver>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerTokenResolver type=xs:string>  
        </issuerTokenResolver>  
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
|类型|指定颁发者令牌解析器的类型。 必须是<xref:System.IdentityModel.Tokens.IssuerTokenResolver>类或派生类型<xref:System.IdentityModel.Tokens.IssuerTokenResolver>类。 必需。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供配置集合的安全令牌处理程序。|  
  
## <a name="remarks"></a>备注  
 颁发者令牌解析程序用于解决签名令牌对传入令牌和消息。 它用于检索用来检查签名的加密材料。 必须指定`type`属性。 指定的类型可以是<xref:System.IdentityModel.Tokens.IssuerTokenResolver>派生的自定义类型或<xref:System.IdentityModel.Tokens.IssuerTokenResolver>类。  
  
 一些令牌处理程序，可在配置中指定颁发者令牌解析器设置。 单个标记处理程序上的设置将覆盖指定安全标记处理程序集合。  
  
> [!NOTE]
>  指定`<issuerTokenResolver>`元素的子元素作为[ \<identityConfiguration >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素已被弃用，但仍然支持向后兼容。 上的设置`<securityTokenHandlerConfiguration>`元素上会覆盖`<identityConfiguration>`元素。  
  
## <a name="example"></a>示例  
 以下 XML 显示了配置为颁发者令牌解析程序基于派生的自定义类<xref:System.IdentityModel.Tokens.IssuerTokenResolver>。 令牌解析器维护自定义配置元素中初始化受众密钥对的字典 (`<AddAudienceKeyPair>`) 为类定义。 此类替代<xref:System.IdentityModel.Selectors.SecurityTokenResolver.LoadCustomConfiguration%2A>方法来处理此元素。 在下面的示例; 显示重写但是，它将调用的方法不会显示为简洁起见。 有关完整示例，请参阅`CustomToken`示例。  
  
```xml  
<issuerTokenResolver type="SimpleWebToken.CustomIssuerTokenResolver, SimpleWebToken">  
  <AddAudienceKeyPair  symmetricKey="wAVkldQiFypTQ+kdNdGWCYCHRcee8XmXxOvgmak8vSY=" audience="http://localhost:19851/" />  
</issuerTokenResolver>  
```  
  
## <a name="example"></a>示例  
  
```  
public override void LoadCustomConfiguration(System.Xml.XmlNodeList nodelist)  
{  
    foreach (XmlNode node in nodelist)  
    {  
        XmlDictionaryReader rdr = XmlDictionaryReader.CreateDictionaryReader(new XmlTextReader(new StringReader(node.OuterXml)));  
        rdr.MoveToContent();  
  
        string symmetricKey = rdr.GetAttribute("symmetricKey");  
        string audience = rdr.GetAttribute("audience");  
  
        this.AddAudienceKeyPair(audience, symmetricKey);  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.IdentityModel.Tokens.IssuerTokenResolver>
