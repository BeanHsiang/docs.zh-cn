---
title: <routing> 的 <serviceBehavior>
ms.date: 03/30/2017
ms.assetid: d8f9c844-4629-4a45-9599-856dc8f01794
ms.openlocfilehash: 3f23cbb45aa72b1aae18c845e68b426a4214d499
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354215"
---
# <a name="routing-of-servicebehavior"></a>\<路由 > 的\<serviceBehavior >
提供对路由服务的运行时访问以允许对路由配置进行动态修改。  
  
 \<system.ServiceModel>  
\<behaviors>  
\<serviceBehaviors>  
\<behavior>  
\<路由 >  
  
## <a name="syntax"></a>语法  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <routing filterTable="String"
               routeOnHeadersOnly="Boolean"
               SoapProcessingEnabled="Boolean" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|filterTable|一个字符串，指定路由服务要计算的筛选器所在的路由表的名称。 此值必须匹配`name`的属性[ \<filterTable >](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertable.md)中的元素[ \<filterTables >](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertables.md)部分。|  
|routeOnHeaderOnly|一个布尔值，指定筛选器将同时检查消息正文和标头，还是仅检查标头。 默认值为 `true`。|  
|soapProcessingEnabled|一个布尔值，指定是否应进行 SOAP 处理。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<behavior>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|指定行为元素。|  
  
## <a name="remarks"></a>备注  
 将此配置元素添加到服务的行为配置中后，此配置元素将对该服务启用路由。 您可以在此元素中指定服务要使用的实际路由表。  
  
 通过使用此配置节，您可以在部署模式发生更改时动态更改路由设置。 在运行时，您可以使用新的路由设置注册自己的路由扩展，路由服务将开始对新消息和会话使用更新后的配置信息，而使正在实施的消息/会话使用启动时的任何现有规则。  这样，您可以在运行时对路由服务进行会话安全的无回收重新配置。  
  
