---
title: <parameter>
ms.date: 03/30/2017
ms.assetid: 0fb41e2d-64f7-44ab-993e-05892eac6d82
ms.openlocfilehash: 8b14dc1908ef3a06549154f70efb2d4e5cb10076
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55289417"
---
# <a name="parameter"></a>\<parameter>
指定当声明类型是泛型类型时的泛型参数。  
  
 \<system.runtime.serialization>  
\<dataContractSerializer>  
\<declaredTypes > 元素  
\<添加 > 元素\<declaredTypes >  
\<knownType > 元素  
\<参数 > 元素  
  
## <a name="syntax"></a>语法  
  
```xml  
<parameter index="Integer"
           type="String" />
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|索引|当声明类型是泛型类型时，指定将返回已知类型的泛型参数。|  
|类型|一个字符串，描述用于序列化和反序列化的已知类型。|  
  
## <a name="index-attribute"></a>index 特性  
  
|值|描述|  
|-----------|-----------------|  
|“0”|泛型类型中的第一个参数。 例如，一个 <xref:System.Collections.Generic.List%601> 仅有一个参数。 如果此参数用作声明类型，则将 index 特性设置为“0”。|  
|"1"|泛型类型中的第二个参数。 例如，一个 <xref:System.Collections.Generic.Dictionary%602> 有两个参数。 如果通过第二个参数返回已知类型，则将 index 特性设置为“1”。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<knownType>](../../../../../docs/framework/configure-apps/file-schema/wcf/knowntype.md)|指定一个可由声明类型的字段或属性返回的已知类型。|  
  
## <a name="remarks"></a>备注  
 有关已知类型的详细信息，请参阅[Data Contract Known Types](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)和<xref:System.Runtime.Serialization.DataContractSerializer>。  
  
 请参阅[ \<dataContractSerializer >](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)有关使用此元素的示例。  
  
 此配置元素不能同时具有两个属性。 如果设置两个属性，则发生 <xref:System.Configuration.ConfigurationErrorsException>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Runtime.Serialization.DataContractSerializer>
- [数据协定已知类型](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)
- [\<dataContractSerializer>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)
- [\<add>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)
