---
title: <generatePublisherEvidence> 元素
ms.date: 03/30/2017
helpviewer_keywords:
- generatePublisherEvidence element
- <generatePublisherEvidence> element
ms.assetid: 7d208f50-e8d5-4a42-bc1a-1cf3590706a8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9f029131f5b10cc487021ee15e72552a26c0b04e
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55275842"
---
# <a name="generatepublisherevidence-element"></a>\<generatePublisherEvidence > 元素
指定是否在运行时创建<xref:System.Security.Policy.Publisher>代码访问安全性 (CAS) 的证据。  
  
 \<configuration>  
\<运行时 >  
\<generatePublisherEvidence>  
  
## <a name="syntax"></a>语法  
  
```xml  
<generatePublisherEvidence    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定是否在运行时创建<xref:System.Security.Policy.Publisher>证据。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|不会创建<xref:System.Security.Policy.Publisher>证据。|  
|`true`|创建<xref:System.Security.Policy.Publisher>证据。 这是默认设置。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## <a name="remarks"></a>备注  
  
> [!NOTE]
>  在[!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)]和更高版本，此元素具有对程序集加载时间没有影响。 有关详细信息，请参阅中的"安全策略简化"一节[安全更改](../../../../../docs/framework/security/security-changes.md)。  
  
 公共语言运行时 (CLR) 尝试在加载时，若要创建验证 Authenticode 签名<xref:System.Security.Policy.Publisher>程序集证据。 但是，默认情况下，大多数应用程序不需要<xref:System.Security.Policy.Publisher>证据。 标准 CAS 策略不依赖于<xref:System.Security.Policy.PublisherMembershipCondition>。 应避免与验证发布者签名，除非你的应用程序使用的自定义 CA 策略的计算机上执行，或要满足的需求关联的不必要的启动成本<xref:System.Security.Permissions.PublisherIdentityPermission>在部分信任环境中。 （标识权限的要求总是在完全信任环境中成功。）  
  
> [!NOTE]
>  我们建议服务使用`<generatePublisherEvidence>`元素以提高启动性能。  使用此元素还有助于避免可能导致超时和取消的服务启动的延迟。  
  
## <a name="configuration-file"></a>配置文件  
 仅在应用程序配置文件中，可以使用此元素。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用`<generatePublisherEvidence>`要禁用检查应用程序的 CA 发布服务器策略元素。  
  
```xml  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [运行时设置架构](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)
